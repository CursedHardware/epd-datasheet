# EPD PINOUT (30x2 PIN)

- GDEW1248C63
- GDEW1248T3
- GDEW1248Z95

## Reference design

- <https://v4.cecdn.yun300.cn/100001_1909185148/DESPI-C1248_SCH%20V1.0.pdf>

## Connector

- FH12-30S-0.5SH

## Definition

|   # | Type |                           Name | Side  | Description                               | Note                     |
| --: | ---: | -----------------------------: | ----- | :---------------------------------------- | :----------------------- |
|   1 |    I |                            CS# | M1/M2 | (SPI SS) Chip select                      |                          |
|   2 |    O |                            GDR | M1/M2 | N-Channel MOS-FET gate drive control      |                          |
|   3 |    P |                           RESE | M1/M2 | Current sense input for control loop      | [RESE][rese]             |
|   4 |    P |                V<sub>SH</sub>R | M1/M2 | Positive source driving voltage for _RED_ | Driving voltage          |
|   5 |    O |                T<sub>SCL</sub> |       | (I2C) Sensor Clock                        |                          |
|   6 |  I/O |                T<sub>SDA</sub> |       | (I2C) Sensor Data                         |                          |
|   7 |    I |                 BS<sub>1</sub> |       | Bus selection                             | [BS1][bs1]               |
|   8 |    O |                          BUSY# | M1/M2 | Busy state output                         | [BUSY][busy]             |
|   9 |    I |                           RST# |       | Global reset pin                          | [SPI][spi], [RES#][resn] |
|  10 |    I |                           D/C# |       | (SPI) Data/Command control                | [SPI][spi], [D/C#][dcn]  |
|  11 |    I |                            CS# | S1/S2 | (SPI SS) Chip select                      | [SPI][spi]               |
|  12 |    I |                            SCL |       | (SPI SCLK) Serial clock                   | [SPI][spi]               |
|  13 |  I/O |                            SDA |       | (SPI MOSI) Serial data in                 | [SPI][spi]               |
|  14 |  I/O |             L/R<sup>SYNC</sup> | M1/M2 | 2 + 2 Cascade Sync Signal                 |                          |
|  15 |  I/O |           M1/M2<sup>SYNC</sup> | M1/M2 | 2 + 2 Cascade Sync Signal                 |                          |
|  16 |  I/O |           M2/M1<sup>SYNC</sup> | M1/M2 | 2 + 2 Cascade Sync Signal                 |                          |
|  17 |  PWR |               V<sub>DD</sub>IO | M1/M2 | (SPI VCC) IO voltage supply               |                          |
|  18 |  PWR |                 V<sub>DD</sub> | M1/M2 | Corelogic power                           |                          |
|  19 |  PWR |                 V<sub>SS</sub> | M1/M2 | (GND) Digital ground                      |                          |
|  20 |  PWR |  V<sub>DD</sub><sup>1.8V</sup> | M1/M2 | (1.8V) Voltage input & output             |                          |
|  21 |  PWR | V<sub>OTP</sub><sup>7.5V</sup> | M1/M2 | (7.5V) OTP program power                  |                          |
|  22 |  PWR |                 V<sub>SH</sub> | M1/M2 | Positive source driving voltage           | Driving voltage          |
|  23 |  PWR |                 V<sub>GH</sub> | M1/M2 | Positive gate driving voltage             | Driving voltage          |
|  24 |  PWR |                 V<sub>SL</sub> | M1/M2 | Negative source driving voltage           | Driving voltage          |
|  25 |  PWR |                 V<sub>GL</sub> | M1/M2 | Negative gate driving voltage             | Driving voltage          |
|  26 |    O |                V<sub>COM</sub> | M1/M2 | `VCOM` output                             |                          |
|  27 |    O |                          BUSY# | S1/S2 | Busy state output                         |                          |
|  28 |  PWR |                V<sub>SH</sub>R | S1/S2 | Positive source driving voltage for _RED_ | Driving voltage          |
|  29 |  PWR |                 V<sub>SH</sub> | S1/S2 | Positive source driving voltage           | Driving voltage          |
|  30 |  PWR |                 V<sub>SL</sub> | S1/S2 | Positive gate driving voltage             | Driving voltage          |

[bs1]: SPI-24PIN.md#bs1
[busy]: SPI-24PIN.md#busy
[csn]: SPI-24PIN.md#csn
[dcn]: SPI-24PIN.md#dcn
[rese]: SPI-24PIN.md#rese
[resn]: SPI-24PIN.md#resn
[spi]: SPI-24PIN.md#spi

## Cascade

|                   M1 | PIN# | PIN# | M2                   |
| -------------------: | ---: | :--- | :------------------- |
|                  SCL |   12 | 12   | SCL                  |
|                  SDA |   13 | 13   | SDA                  |
|     L<sup>SYNC</sup> |   14 | 16   | M2/M1<sup>SYNC</sup> |
| M1/M2<sup>SYNC</sup> |   15 | 15   | M2/M1<sup>SYNC</sup> |
| M2/M1<sup>SYNC</sup> |   16 | 14   | R<sup>SYNC</sup>     |
|      V<sub>COM</sub> |   26 | 26   | V<sub>COM</sub>      |
