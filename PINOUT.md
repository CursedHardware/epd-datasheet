# EPD General PINOUT

## Reference design

- <http://pmoc98298.pic37.websiteonline.cn/upload/DESPI-C01-sch-V11.pdf>
- <https://www.waveshare.com/w/upload/5/5b/1.54inch_e-Paper_Schematic.pdf>
- <https://www.waveshare.com/w/upload/5/57/2.13inch_e-Paper_HAT_Schematic.pdf>
- <https://oshwhub.com/ludas/mo-shui-ping-qu-dong>

## Connector

| PIN# | Connector      | Interface |
| ---- | -------------- | --------- |
| 24   | FH12-24S-0.5SH | SPI       |
| 34   | FH12-34S-0.5SH | SPI       |

## 24PIN Definition

|   # | Type |               Name | Description                                | Note                       |
| --: | ---: | -----------------: | :----------------------------------------- | :------------------------- |
|  01 |   NC |                 NC | Keep Open                                  |                            |
|  02 |    O |                GDR | N-Channel MOSFET gate drive control        |                            |
|  03 |    O |               RESE | Current sense input for the control loop   | [RESE](#rese)              |
|  04 |    C |     V<sub>GL</sub> | Negative gate driving voltage              |                            |
|  05 |    C |     V<sub>GH</sub> | Positive gate driving voltage              |                            |
|  06 |    O |    T<sub>SCL</sub> | (I2C) Sensor Clock                         | [Digital Temperature][dt]  |
|  07 |  I/O |    T<sub>SDA</sub> | (I2C) Sensor Data                          | [Digital Temperature][dt]  |
|  08 |    I |     BS<sub>1</sub> | Bus selection                              | [BS1](#bs1)                |
|  09 |    O |               BUSY | Busy state output                          | [BUSY](#busy)              |
|  10 |    I |               RES# | Reset                                      | [SPI](#spi), [RES#](#resn) |
|  11 |    I |               D/C# | (SPI) Data/Command control                 | [SPI](#spi), [D/C#](#dcn)  |
|  12 |    I |                CS# | (SPI SS) Chip select input                 | [SPI](#spi), [CS#](#csn)   |
|  13 |  I/O |      D<sub>0</sub> | (SPI SCLK) Serial clock                    | [SPI](#spi)                |
|  14 |  I/O |      D<sub>1</sub> | (SPI MOSI) Serial data in                  | [SPI](#spi)                |
|  15 |    I |   V<sub>DD</sub>IO | (SPI VCC) Power Supply for interface logic |                            |
|  16 |    I |     V<sub>DI</sub> | Power Supply for the chip                  |                            |
|  17 |      |     V<sub>SS</sub> | (GND) Ground                               |                            |
|  18 |    C |     V<sub>DD</sub> | Corelogic power                            |                            |
|  19 |    C |     V<sub>PP</sub> | Power Supply for OTP programming           |                            |
|  20 |    C |     V<sub>SH</sub> | Positive source driving voltage            |                            |
|  21 |    C | PRE V<sub>GH</sub> | Power Supply for `VGH` and `VSH`           |                            |
|  22 |    C |     V<sub>SL</sub> | Negative source driving voltage            |                            |
|  23 |    C | PRE V<sub>GL</sub> | Power Supply for `VCOM`, `VGL` and `VSL`   |                            |
|  24 |    C |    V<sub>COM</sub> | `VCOM` driving voltage                     |                            |

```plain
I: Input
O: Output
C: PWR
NC: No Connection
```

[dt]: sensors/lm75.md

## Note

### CSn

This pin (`CS#`) is the chip select input connecting to the MCU.
<br>The chip is enabled for MCU communication only when `CS#` is pulled _LOW_.

### D/Cn

| `D/C#` | Think of the data as |
| ------ | -------------------- |
| _LOW_  | Command              |
| _HIGH_ | Data                 |

### RESn

This pin (`RES#`) is reset signal input.
<br>The Reset is active _LOW_.

### BUSY

This pin (`BUSY`) is Busy state output pin.
<br>When Busy is _HIGH_, the operation of chip should not be interrupted and any commands should not be issued to the module.
<br>The driver IC will put Busy pin _HIGH_ when the driver IC is working such as:

- Outputting display waveform
- Programming with OTP
- Communicating with digital temperature sensor

### Panel break detection

The panel break detection function is used to detect the breakage at panel edge.
<br>When the panel break detection command is issued, the panel break detection will be executed.
<br>During the detection period, `BUSY` output is at _HIGH_ level.
<br>`BUSY` output is at _LOW_ level when the detection is completed.
<br>Then, user can issue the Status Bit Read command to check the status bit for the result of panel break.

### `BS1`

| SPI Mode | `BS1`              | `RES#`   | `CS#`    | `D/C#`           |
| -------: | ------------------ | -------- | -------- | ---------------- |
|   4-wire | Connect to `VSS`   | Required | Required | Required         |
|   3-wire | Connect to `VDDIO` | Required | Required | Connect to `VSS` |

\* 3-wire: 9 bits SPI, first bit is `D/C#`

### `RESE`

While shorting `RESE` and resistor, this model is suitable for the following E-Paper displays:

| Resistor     | Driver IC Provided |
| ------------ | ------------------ |
| 0.47 &Omega; | Solomon Systech    |
| 3.00 &Omega; | Ultra Chip         |

References:

- <https://forum.arduino.cc/index.php?topic=436411.msg3326970#msg3326970>
- <https://www.crystalfontz.com/blog/why-does-my-epaper-display-not-work-with-my-epaper-adapter-board/>

### SPI

3-wire SPI caveats:
<br>The operation is similar to 4-wire SPI while `D/C#` pin is not used and it must be tied to _LOW_.
<br>In the write operation, a 9-bit data will be shifted into the shift register on every clock rising edge.
<br>The bit shifting sequence is `D/C#` bit, `D7` bit, `D6` bit to `D0` bit.
<br>The first bit is `D/C#` bit which determines the following byte is **command** or **data**.
<br>When `D/C#` bit is **0**, the following byte is **command**.
<br>When `D/C#` bit is **1**, the following byte is **data**.

| SPI Mode | Function      | D0 (`SCLK`) PIN | D1 (`MOSI`) PIN | `D/C#` PIN | `CS#` PIN |
| -------: | ------------- | :-------------: | --------------: | ---------- | --------- |
|   4-wire | Write Command |     &#8593;     |     Command bit | _LOW_      | _LOW_     |
|   4-wire | Write Data    |     &#8593;     |        Data bit | _HIGH_     | _LOW_     |
|   3-wire | Write Command |     &#8593;     |     Command bit | Tie _LOW_  | _LOW_     |
|   3-wire | Write Data    |     &#8593;     |        Data bit | Tie _LOW_  | _LOW_     |

- _LOW_ is connected to V<sub>SS</sub> and _HIGH_ is connected to V<sub>DD</sub>IO
- &#8593; stands for rising edge of signal
- `MOSI` is shifted into an 8-bit shift register on every rising edge of `SCLK` in the order of `D7`, `D6`, ... `D0`.
  <br>The level of `D/C#` should be kept over the whole byte.
  <br>The data byte in the shift register is written to the Graphic Display Data RAM (RAM)
  <br>or Data Byte register or command Byte register according to `D/C#` pin.
