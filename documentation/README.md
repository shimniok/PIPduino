# PIPduino User Guide

PIPduino is a 'duino is easier and cheaper to permanently Put In a Project than the standard Arduino. [For sale on Tindie](https://www.tindie.com/products/bot_thoughts/pipduino).

## Overview

 * Use standalone boards from [Sparkfun](https://www.sparkfun.com/), [Pololu](http://www.pololu.com/), [Adafruit](https://www.adafruit.com/), etc.
 * ```I2C``` port with 4 connections for interfacing all those sensors
 * ```SPI/ISP``` port can be used for AVR In-System Programming or SPI port
 * All Digital and Analog pins exposed.
 * Servo-style ```signal```, ```VCC```, ```GND``` pins on *DIGITAL* and *ANALOG* ports
 * Select from a wide variety of power supply options
 * Programming and/or serial on ```FTDI``` port
 * ATmega328P at 16MHz, Arduino Optiboot, looks like an Uno board
 * Optional 3mm indicator LEDs (leave them off to reduce power consumption)
 * And more...

## Pinout
The PIPduino breaks out dedicated digital and analog pins as well as pins for Serial, SPI, and I2C. The tables below list all the Arduino Pins, and the PIPduino *Port* they are found on, and alternate functions.

### Digital

The primary function of the pins below is Arduino digital input and output.
Pins D10-D13 are also used for SPI (See *SPI/ISP* below).

| Arduino Pin | Alternate | Port |
|:---:|---|---|
| D0 | Serial RX (FTDI TXO) | FTDI |
| D1 | Serial TX (FTDI RXI) | FTDI |
| D2 | - | DIGITAL |
| D3 | PWM | DIGITAL |
| D4 | - | DIGITAL |
| D5 | PWM | DIGITAL |
| D6 | PWM | DIGITAL |
| D7 | - | DIGITAL |
| D8 | - | DIGITAL |
| D9 | PWM | DIGITAL |
| D10 | PWM | DIGITAL |
| D11 | PWM | SPI/ISP |
| D12 | - | SPI/ISP |
| D13 | LED | SPI/ISP |

### Analog

Arduino analog pins can also be used for digital input/output. Pins A4-A5 are
used for I2C (See *I2C* below). Pins A6-A7 are analog input, only.

| Arduino Pin | Alternate | Port |
|:---:|---|---|
| A0 | Digital | ANALOG |
| A1 | Digital | ANALOG |
| A2 | Digital | ANALOG |
| A3 | Digital | ANALOG |
| A4 | Digital, SDA | I2C |
| A5 | Digital, SCL | I2C |
| A6 | - | ANALOG |
| A7 | - | ANALOG |

### SPI/ISP
The SPI port doubles as the In-System Programming port (AVRISP). Use the SS
solder jumper under the board to select SPI:D10 to use the SPI port with D10
as the active-low Slave Select pin.

| Arduino Pin | Function | Port |
|:---:|---|---|
| D10 | SS | SPI/ISP |
| D11 | MOSI | SPI/ISP |
| D12 | MISO | SPI/ISP |
| D13 | SCK | SPI/ISP |

NOTE: there is a silkscreen error on R0.2: the SS solder jumper silkscreen
identifies the wrong digital pin for SPI operation. In fact, D10 is used for
Slave Select.

### I2C
The A4 and A5 pins are dedicated to I2C SDA and SCL use, respectively, since so
many sensors speak I2C. SMT pull-up resistors are installed on the board for
these pins. The board has connections for four I2C devices but you can also
daisy chain I2C devices, too.

| Arduino Pin | Function | Port |
|:---:|---|---|
| A4 | SDA | I2C |
| A5 | SCL | I2C |

### Serial / FTDI
The D0 and D1 pins are broken out to the FTDI/Serial port for TX (FTDI RXI) and RX (FTDI TXO) pins, respectively. The FTDI pins can be used for Arduino program downloading, or can be used for serial I/O. Because there's no pull-up they can also be used for GPIO pins D0 and D1.

| Arduino Pin | Function | FTDI | Port |
|:---:|---|:---:|---|
| D0 | Serial TX | RXI | FTDI |
| D1 | Serial RX | TXO | FTDI |


## Programming
### Arduino
PIPduino is Arduino compatible, so use the good ol' Arduino IDE.

### FTDI
Program with a standard FTDI cable or Sparkfun FTDI basic breakout or equivalent. Within the Arduino IDE, select the appropriate serial device, and choose "Arduino Uno" as the board.

### ISP
You can also program with ISP. On the bottom of the board, use the SS solder jumper to select ISP:RES for ISP programming.

## Power
Several options are available for powering your PIPduino and sensors/devices.

### Powering the Board
* Use the onboard regulator. Connect the VIN/GND port to a supply of anywhere from Vcc+0.23V to 16V.
* Bypass the regulator and supply 3.3V or 5V directly to any VCC/GND pin pair.
* FTDI can supply voltage through the VCC pin if the board is not powered. A diode allows you to plug in FTDI whether the board is already powered or not. It drops 0.2-0.5V depending on current draw.

CAUTION: in any case above, your FTDI adapter's output voltage must be LESS THAN the voltage on the VCC pins of the POWER, ANALOG, DIGITAL, and I2C ports.

### Powering Devices
A VCC and GND pin are provided for every port with a servo-style pinout (Signal, VCC, GND), plus there is a power distribution port, POWER, with 4 additional VCC/GND pairs. In most cases, the easiest option is to simply build a 0.1" pitch header/cable (or use a pre-built servo connector) to connect your device.

If your device requires a 3.3V supply, you can either use a separate regulator board to power 3.3V devices or use a 3.3V PIPduino.

### Onboard Regulator
The onboard regulator features reverse bias protection and thermal shutdown protection. Because of the DPAK package for the regulator IC and due to robust thermal design of the board, it has been tested to supply a full 500mA continuous without going into thermal shutdown.

In fact, I torture-tested the board, powering it with a 3S LiPo (~12V), dumping out over 520mA (above the rated spec for the regulator) for a good five minutes. The hottest spot I measured was a stable 140°C on the tab. Ambient temperature was 22°C. The regulator never went into thermal shutdown. When tested at approximately 250mA, the hottest temperature I found after several minutes was a stable 93°C.

Note that a lower input voltage won't make so much heat. And drawing less current means less heat. A higher ambient temperature will reduce heat dissipation, so keep that in mind.

CAUTION: when supplying maximum current, the board gets REALLY HOT!!

## Mounting

* Mounting holes for M3 (#4) size screws on a 40mm square
* Board size is 46mm (13/16") square
