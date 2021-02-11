# EPD PINOUT (30 PIN)

- GDEW0102I3F
- GDEW0102I4FC
- GDEW0102T4

## Reference design

- <https://cetest02.cn-bj.ufileos.com/100001_1909185148/DESPI-C102_SCH%20V1.0.pdf>

## Connector

- FH12-30S-0.5SH

## Definition

|   # | Type |             Name | Description                     | Note                      |
| --: | ---: | ---------------: | :------------------------------ | :------------------------ |
|   1 |  PWR |   V<sub>PP</sub> | OTP program power               |                           |
|   2 |  PWR |              GND | (GND) Digital ground            |                           |
|   3 |  PWR |   V<sub>DD</sub> | Digital power                   |                           |
|   4 |  I/O |              SDA | (SPI MOSI) Serial data in       | [SPI][spi]                |
|   5 |    I |              SCL | (SPI SCLK) Serial clock         | [SPI][spi]                |
|   6 |    I |              CS# | (SPI SS) Chip select            | [SPI][spi], [CS#][csn]    |
|   7 |    I |             D/C# | (SPI) Data/Command control      | [SPI][spi], [D/C#][dcn]   |
|   8 |    I |             RES# | Global reset pin                | [SPI][spi], [RES#][resn]  |
|   9 |    O |             BUSY | Busy state output               | [BUSY][busy]              |
|  10 |    I |   BS<sub>1</sub> | Bus selection                   | [BS1][bs1]                |
|  11 |  PWR |   V<sub>DD</sub> | (SPI VDD) Digital power input   |                           |
|  12 |  PWR |   V<sub>DL</sub> | Negative source driving voltage | Driving voltage           |
|  13 |  PWR |   V<sub>DH</sub> | Positive source driving voltage | Driving voltage           |
|  14 |  PWR |   V<sub>GH</sub> | Positive gate driving voltage   | Driving voltage           |
|  15 |  PWR |   V<sub>GL</sub> | Negative gate driving voltage   | Driving voltage           |
|  16 |  PWR |              C6N | Negative side                   | Capacitor connecting pins |
|  17 |  PWR |              C6P | Pegative side                   | Capacitor connecting pins |
|  18 |  PWR |              C5N | Negative side                   | Capacitor connecting pins |
|  19 |  PWR |              C5P | Pegative side                   | Capacitor connecting pins |
|  20 |  PWR |              C4N | Negative side                   | Capacitor connecting pins |
|  21 |  PWR |              C4P | Pegative side                   | Capacitor connecting pins |
|  22 |  PWR |              C3N | Negative side                   | Capacitor connecting pins |
|  23 |  PWR |              C3P | Pegative side                   | Capacitor connecting pins |
|  24 |  PWR |              C2N | Negative side                   | Capacitor connecting pins |
|  25 |  PWR |              C2P | Pegative side                   | Capacitor connecting pins |
|  26 |  PWR |              C1N | Negative side                   | Capacitor connecting pins |
|  27 |  PWR |              C1P | Pegative side                   | Capacitor connecting pins |
|  28 |  PWR | V<sub>COM</sub>L | Negative pumping voltage        | Internal use              |
|  29 |  PWR | V<sub>COM</sub>H | Positive pumping voltage        | Internal use              |
|  30 |    O |  V<sub>COM</sub> | `VCOM` output                   |                           |

[spi]: SPI-24PIN.md#spi
[csn]: SPI-24PIN.md#csn
[dcn]: SPI-24PIN.md#dcn
[resn]: SPI-24PIN.md#resn
[busy]: SPI-24PIN.md#busy
[bs1]: SPI-24PIN.md#bs1
