# Introduction

PIPduino is a 'duino that has a host of features making it easy for you to Put In a Project. [For sale on Tindie](https://www.tindie.com/products/bot_thoughts/pipduino).

## Features

 * Each digital and analog pin has a corresponding 5V and GND pin.
 * Flexible power: voltage regulator takes 6.1-15V, power from any 5V/GND pin
 * FTDI / Serial port can power the board
 * SPI port doubles as ISP port, user selectable
 * I2C port for interfacing all those sensors 
 * ATmega328P at 16MHz, Arduino Optiboot, looks like an Uno board
 * Optional 3mm indicator LEDs (leave them off to reduce power consumption)

# Pinout
The PIPduino breaks out dedicated digital and analog pins as well as pins for Serial, SPI, and I2C.

## Digital
 * D0: used for TXO on FTDI port
 * D1: used for RXI on FTDI port
 * D2: DIGITAL Port
 * D3: DIGITAL Port (PWM)
 * D4: DIGITAL Port
 * D5: DIGITAL Port (PWM)
 * D6: DIGITAL Port (PWM)
 * D7: DIGITAL Port
 * D8: DIGITAL Port
 * D9: DIGITAL Port (PWM)
 * D10: DIGITAL Port (PWM), also ~SS on SPI port (see SPI/ISP)

## Analog
 * A0: ANALOG Port
 * A1: ANALOG Port
 * A2: ANALOG Port
 * A3: ANALOG Port
 * A4: used for SDA on I2C PORT
 * A5: used for SCL on I2C PORT
 * A6: ANALOG Port
 * A7: ANALOG Port

## SPI/ISP
The SPI port doubles as the In-System Programming port (AVRISP). Use the SS solder jumper under the board to select SPI:D10 to use the SPI port with D10 as the slave select pin.

NOTE: there is a silkscreen error on R0.2 -- the ~SS solder jumper silkscreen identifies the wrong digital pin for SPI operation. In fact, D10 is used for ~SS.

## I2C
The A4 and A5 pins are dedicated to I2C SDA and SCL use, respectively, since so many sensors speak I2C. Pull-up resistors are included. The board has connections for four I2C devices but you can also daisy chain them, too.

## Serial / FTDI
The D0 and D1 pins are broken out to the FTDI/Serial port for RXI and TXO pins, respectively. The FTDI pins can be used for Arduino program downloading, or can be used for serial I/O. Because there's no pull-up they can also be used for GPIO pins D0 and D1.

# Programming
## Arduino
PIPduino is Arduino compatible, so use the good ol' Arduino IDE.

## FTDI
Program with a standard FTDI cable or Sparkfun FTDI basic breakout or equivalent. Within the Arduino IDE, select the appropriate serial device, and choose "Arduino Uno" as the board.

## ISP
You can also program with ISP. On the bottom of the board, use the SS solder jumper to select ISP:RES for ISP programming.

# Power
Several options are available for powering your PIPduino and sensors/devices.

## Powering the Board
* Use the onboard regulator. Connect the VIN/GND port to a supply of anywhere from Vcc+0.23V to 16V.
* Bypass the regulator and supply 3.3V or 5V directly to any VCC/GND pin pair.
* FTDI can supply voltage through the VCC pin if the board is not powered. A diode allows you to plug in FTDI whether the board is already powered or not. It drops 0.2-0.5V depending on current draw. 

CAUTION: in any case above, your FTDI adapter's output voltage must be LESS THAN the voltage on the VCC pins of the POWER, ANALOG, DIGITAL, and I2C ports.

## Powering Devices
A VCC and GND pin are provided for every port with a servo-style pinout (Signal, VCC, GND), plus there is a power distribution port, POWER, with 4 additional VCC/GND pairs. In most cases, the easiest option is to simply build a 0.1" pitch header/cable (or use a pre-built servo connector) to connect your device.

If your device requires a 3.3V supply, you can either use a separate regulator board to power 3.3V devices or use a 3.3V PIPduino.

## Onboard Regulator
The onboard regulator features reverse bias protection and thermal shutdown protection. Because of the DPAK package for the regulator IC and due to robust thermal design of the board, it has been tested to supply a full 500mA continuous without going into thermal shutdown.

In fact, I torture-tested the board, powering it with a 3S LiPo (~12V), dumping out over 520mA (above the rated spec for the regulator) for a good five minutes. The hottest spot I measured was a stable 140°C on the tab. Ambient temperature was 22°C. The regulator never went into thermal shutdown. When tested at approximately 250mA, the hottest temperature I found after several minutes was a stable 93°C.

Note that a lower input voltage won't make so much heat. And drawing less current means less heat. A higher ambient temperature will reduce heat dissipation, so keep that in mind.

CAUTION: when supplying maximum current, the board gets REALLY HOT!!

# Mounting

* Mounting holes for M3 (#4) size screws on a 40mm square
* Board size is 46mm (13/16") square