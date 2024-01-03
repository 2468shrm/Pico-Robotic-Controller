# Pico-Robotic-Controller

A carrier board for a Raspberry Pi Pico (W) for use in FRC robotics. Similar
to the XRP board.

## Disclaimer / Warning

This is an experimental device. Not all interfaces have been fully validated
for proper function. Use at your own risk.

## Introduction (Motivation)

You may assume that this board is indended to compete with the XRP product
from WPI, other developers, and SparkFun. __It is not__. The XRP board is
awesome and I'll likely end up acquiring one (or two) for myself. I have
been working on lo w-cost, roboRIO-like carrier boards for FRC for a couple
of years.

Why create a carrier board like the roboRIO? To enable a lower-cost
prototyping solution. This solution makes it less risky to a costly
than using a roboRIO solution. Breaking a roboRIO means costly replacement
that is sometimes hard to replace. One goal was to provide as many
similar interfaces as possible but cost 25% the budget.

Things I didn't need to do with my use model: support LabVIEW despite being
a team who lives and breaths LabVIEW. I did want to support rapid prototyping
and so exploring circuitpython was a goal; particularly because of the
library support for the STEMMA QT/Qwiic based sensors available from
Adafruit.

## Board Images

![Top View](https://github.com/2468shrm/Pico-Robotic-Controller/blob/main/Images/Top.png?raw=true)

![Isometric View from the I2C connector corner](https://github.com/2468shrm/Pico-Robotic-Controller/blob/main/Images/Iso%20STEMMA%20QT.png?raw=true)

![Isometric View from the digital I/O connector corner](https://github.com/2468shrm/Pico-Robotic-Controller/blob/main/Images/Iso%20DIO.png?raw=true)

## Board Features

The carrier board has the following interfaces and features.

- RaspberryPi Pico W board
  - Does the thinking
  - Provides WiFi and/or Bluetooth
  - Socketed for replacemnt if needed
- Adafruit Picobell CAN board (optional)
  - Provides CAN connectivity for integration into FRC robots allowing CAN-connected applications (e.g. smart sensors)
- Adafruit Ethernet Featherwing board (optional)
  - Provides Ethernet connectivity for integration into FRC robots allowing Ethernet connected applications (e.g. smart sensors)
- Power
  - 12V Battery input provides main board supply
    - 5V regulator module, OR
    - A connection to external 5V regulator (using WAGO 250-202) connector if the 5V supply current requirements are higher than the module can provide
  - Servo/PWM interface independently powered by an external source
    - Due to the potential need for different voltage and higher current
    - Not needed if connecting to external motor controllers (REV, CTRE, etc.)
- Four (4) STEMMA QT/Qwiic connections provided through a 4-port I2C switch run off the Pico W I2C 1 interface
- Eight (8) Servo PWM interfaces and an additional 8 PWM signals generated by a 16-channel generator connected to the Pico W I2C 0 interface
 - The Servo PWM interace has its own power input; for increased voltage or current for high-torque servo motors
- Two (2) analog input (ADC) ports, 3V maximum
- Eight (8) digital I/O ports, divided into 2 4-pin groups
  - Uses the roboRIO DIO 3-pin interface
  - Each group provides jumper-selectable power (5V or 3.3V)
  - Pico inputs are 3.3V only (maximum) input, with level shifting based on the group's selected power
  - All DIOs have LEDs to indicate logic level (Dark is LOW, Illuminated is HIGH)
- One NEOPIXEL interface for providing visual sensor status or communication
- One on-board single-pixel NEOPIXEL for board status

## Comparison to XRP Board

The XRP board has some significant philospohical and design choices and features.

- XRP was designed with the intent of learning robotics on a small platform, using the WPILib framework
- Includes four motor controllers (1.5A each) integrated on the PCB
- Has a gyro and accelerometer integrated on the PCB
- The connectors are six-position JST (vertical) that integrates digital I/Os for encoders in addition to the M+ and M- motor signals (i.e. not a sensor standard like Qwiic or STEMMA QT)

The PRC does not include any motor controllers on the board. However, it
does provide a 2x5 pin connector and a dedicated PWM generator (I2C bus 0,
address 0x41). The intent is to provide a board with 4 12V, 3.3 A motor
controllers using a separate/dedicated battery input. Providing the capability
to drive four H-Bridges allows for demonstration chassis (skid steer or
Meccanum). This allows replaceable solutions as well as future upgrades for
higher current. Moreover, the PWM / Servo connections allow for use of
a conventional FRC PWM-controlled motor controller.

The PRC provides four STEMMA QT / Qwiic connectors in lieu of a specific set
of sensors (IMU). This allows out use of different sensors dependent on
the application.

The PRC also has CAN and Ethernet connectivity in addition to the WiFi and
BlueTooth provided by the Pice W board.

Differences between the roboRIO, XPR, and PRC boards.
<table>
  <tr style="background-color:#404040">
    <th>Interface / Feature</th>
    <th>RoboRIO</th>
    <th>XRP</th>
    <th>SHRH's Board</th>
  </tr>
  <tr>
    <td>Processing</td>
    <td>Zinq</td>
    <td>RPi Pico W</td>
    <td>RPi Pico W</td>
  </tr>
  <tr>
    <td>Ethernet</td>
    <td>1 Gb</td>
    <td><code>&#8212;</code></td>
    <td>Via 10/100 Mb FeatherWing</td>
  </tr>
  <tr>
    <td>WiFi</td>
    <td>Via OpenMesh</td>
    <td>Y</td>
    <td>Y</td>
  </tr>
  <tr>
    <td>USB Host</td>
    <td>Y</td>
    <td><code>&#8212;</code></td>
    <td><code>&#8212;</code></td>
  </tr>
  <tr>
    <td>CAN</td>
    <td>Y</td>
    <td><code>&#8212;</code></td>
    <td>Via Picobell CAN board</td>
  </tr>
  <tr>
    <td>Relay</td>
    <td>Y</td>
    <td><code>&#8212;</code></td>
    <td><code>&#8212;</code></td>
  </tr>
  <tr>
    <td>Digital I/O</td>
    <td>10 + MXP</td>
    <td><code>&#8212;</code></td>
    <td>8</td>
  </tr>
  <tr>
    <td>ADC</td>
    <td>4</td>
    <td><code>&#8212;</code></td>
    <td>2</td>
  </tr>
  <tr>
    <td>I2C</td>
    <td>2</td>
    <td><code>&#8212;</code></td>
    <td><code>&#8212;</code></td>
  </tr>
  <tr>
    <td>STEMMA QT / Qwiic</td>
    <td><code>&#8212;</code></td>
    <td>4</td>
    <td>4</td>
  </tr>
  <tr>
    <td>SPI</td>
    <td>2</td>
    <td><code>&#8212;</code></td>
    <td><code>&#8212;</code></td>
  </tr>
  <tr>
    <td>RS-232</td>
    <td>1</td>
    <td><code>&#8212;</code></td>
    <td><code>&#8212;</code></td>
  </tr>
  <tr>
    <td>Gyro</td>
    <td>Y</td>
    <td>6 DOF IMU (LSM6DSO)</td>
    <td><code>&#8212;</code></td>
  </tr>
  <tr>
    <td>Status LEDs</td>
    <td>Y</td>
    <td>Pico W LED</td>
    <td>Y (NEOPIXEL) + Pico W LED</td>
  </tr>
  <tr>
    <td>NEOPIXEL String</td>
    <td>2 via PWM outputs</td>
    <td><code>&#8212;</code></td>
    <td>Y</td>
  </tr>
  <tr>
    <td>Low-Current Motor Control</td>
    <td><code>&#8212;</code></td>
    <td>4</td>
    <td>4 on sidecar board</td>
  </tr>
  <tr>
    <td>Per H-Bridge Max Current</td>
    <td><code>&#8212;</code></td>
    <td>1.5 A</td>
    <td>3.3 A</td>
  </tr>
  <tr>
    <td>I/Os Per Motor Interface</td>
    <td><code>&#8212;</code></td>
    <td>2 (equivalent of STEMMA per motor)</td>
    <td><code>&#8212;</code></td>
  </tr>
  <tr>
    <td>Reset Button</td>
    <td>Y</td>
    <td>Y</td>
    <td>Y</td>
  </tr>
  <tr>
    <td>Power In</td>
    <td>12 V</td>
    <td>5-11 V</td>
    <td>12 V</td>
  </tr>
  <tr>
    <td>Power Conntector</td>
    <td>Sauro</td>
    <td>Barrel</td>
    <td>Wago 250-202</td>
  </tr>
  <tr>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
</table>

Differences between the XRP and PRC pin usage and functions.

<table>
  <tr style="background-color:#404040">
    <th>Pin</th>
    <th>Pico W Alternatives</th>
    <th>XRP Interface</th>
    <th>XRP Function</th>
    <th>PRC Board</th>
  </tr>
  <tr>
    <td>GPIO 0</td>
    <td>U0 TX / SDA0 / MISO0</td>
    <td rowspan="4">Motor 3</td>
    <td>Encoder A</td>
    <td>DIO 0</td>
  </tr>

  <tr>
    <td>GPIO 1 </td>
    <td>U0 RX / SCL0 / CS0</td>
    <td>Encoder B</td>
    <td>DIO 1</td>
  </tr>
  <tr>
    <td>GPIO 2</td>
    <td>SDA1 / SCK0</td>
    <td>Phase</td>
    <td>PWM Gen SDA</td>
  </tr>
  <tr>
    <td>GPIO 3 </td>
    <td>SCL1 / MOSI0</td>
    <td>Enable</td>
    <td>PWM Gen SCL</td>
  </tr>
  <tr>
    <td>GPIO 4 </td>
    <td>U1 TX / SDA0 / MISO0</td>
    <td rowspan="4">Left Motor</td>
    <td>Encoder A</td>
    <td>I2C Switch SDA</td>
  </tr>
  <tr>
    <td>GPIO 5</td>
    <td>U1 RX / SCL0 / CS0</td>
    <td>Encoder B</td>
    <td>I2C Switch SCL</td>
  </tr>
  <tr>
    <td>GPIO 6</td>
    <td>SDA1 / SCK0</td>
    <td>Phase</td>
    <td>DIO 2</td>
  </tr>
  <tr>
    <td>GPIO 7</td>
	<td>SCL1 / MOSI0</td>
    <td>Enable</td>
    <td>DIO 3</td>
  </tr>
  <tr>
    <td>GPIO 8</td>
    <td>U1 TX / SDA0 / MISO1</td>
    <td rowspan="4">Motor 4</td>
    <td>Encoder A</td>
    <td>DIO 4</td>
  </tr>
  <tr>
    <td>GPIO 9</td>
    <td>U1 RX / SCL0 / CS1</td>
    <td>Encoder B</td>
    <td>DIO 5</td>
  </tr>
  <tr>
    <td>GPIO 10</td>
    <td>SDA1 / SCK1</td>
    <td>Phase</td>
    <td>DIO 6</td>
  </tr>
  <tr>
    <td>GPIO 11</td>
 	<td>SCL1 / MOSI1</td>
    <td>Enable</td>
    <td>DIO 7</td>
  </tr>
  <tr>
    <td>GPIO 12</td>
	<td>U0 TX / SDA0 / MISO1</td>
    <td rowspan="4">Right Motor</td>
    <td>Encoder A</td>
    <td>PWM Gen Enable</td>
  </tr>
  <tr>
    <td>GPIO 13</td>
	<td>U0 RX / SCL0 / CS1</td>
    <td>Encoder B</td>
    <td>Reset Switch</td>
  </tr>
  <tr>
    <td>GPIO 14</td>
 	<td>SDA1 / SCK1</td>
    <td>Phase</td>
    <td>not connected</td>
  </tr>
  <tr>
    <td>GPIO 15</td>
    <td>SCL1 / MOSI1</td>
    <td>Enable</td>
    <td>SPI CS (Ethernet)</td>
  </tr>
  <tr>
    <td>GPIO 16</td>
    <td>U0 TX / SDA0 / MISO0</td>
    <td>Servo 1</td>
    <td>Signal</td>
    <td>SPI MISO</td>
  </tr>
  <tr>
    <td>GPIO 17</td>
    <td>U0 RX / SCL0 / CS0</td>
    <td>Servo 2</td>
    <td>Signal</td>
    <td>NEOPIXEL (board)</td>
  </tr>
  <tr>
    <td>GPIO 18</td>
    <td>SDA1 / SCK0</td>
    <td rowspan="2">IMU / Qwiic</td>
    <td>SDA</td>
    <td>SPI SCK</td>
  </tr>
  <tr>
    <td>GPIO 19</td>
    <td>SCL1 / MOSI0</td>
    <td>SCL</td>
    <td>SPI MOSI</td>
  </tr>
  <tr>
    <td>GPIO 20</td>
    <td>SDA0</td>
    <td rowspan="2">Range</td>
    <td>Trigger</td>
    <td>SPI CS (CAN)</td>
  </tr>
  <tr>
    <td>GPIO 21</td>
    <td>SCL0</td>
    <td>Echo</td>
    <td>SPI INT (CAN)</td>
  </tr>
  <tr>
    <td>GPIO 22</td>
    <td></td>
    <td></td>
    <td>User button / extra</td>
    <td>NEOPIXEL (String)</td>
  </tr>
  <tr>
    <td>GPIO 26</td>
    <td>SDA1 / ADC0</td>
    <td rowspan="2">Line Follower</td>
    <td>Left</td>
    <td>ADC 0</td>
  </tr>
  <tr>
    <td>GPIO 27</td>
    <td>SCL1 / ADC1</td>
    <td>Right</td>
    <td>ADC 1</td>
  </tr>
  <tr>
    <td>GPIO 28</td>
    <td></td>
    <td></td>
    <td>VIN_meas / extra</td>
    <td>not connected</td>
  </tr>
</table>

## PRC Board Detail / Theory of Operation

The following describes the PRC board components, features, and 

When exploring the board's detail and function, it may be helpful to refer to
the board's schematic ([Link](https://github.com/2468shrm/Pico-Robotic-Controller/blob/main/Images/Pico%20Robotic%20Controller%20Schematic.pdf)).

### Main Power / Battery Input

The power system has the following components:
- +BATT - The main power supply (+BATT) is connected to J1, a 2-position WAGO 250 series connector. The typical use is a 12V battery or power supply.
- +12V - Connected to +BATT through a diode-capacitor filter. The intent of the filter is to avoid brownouts on the robot from affecting board performance.
- +5V - The Pico W uses a 5V source normally supplied by USB's VBUS. However, the board provides a 5V source. This is done via either installing a 5V 3A regulator module ([Amazon Link](https://www.amazon.com/gp/product/B08JZ5FVLC)), or by installing a 2-position WAGO 250-series connector (J11) and providing an external 5V supply.  The external solution would be used only in situations where 3A is insufficient (e.g. a very long NEOPIXEL strip).
- SERVO_VDD - A dedicated power input is provided for use cases involving servo motors. This is required since the +5V supply is limited to 3A which may not be sufficient for servo motors in stall. Moreover, while servo motors may operate at 5V, they're better at operating at higher voltages (6V).
- VSYS - VSYS is a pin on the Pico W board that is sourced from VBUS through a Schottky diode, but this is only functional when the VBUS is connected.  VSYS is also soured by a PFET (Q1, a DMG2305UX-13) as recommended by the Pico W datasheet ([Raspberry Pi Pico W Datasheet](https://datasheets.raspberrypi.com/picow/pico-w-datasheet.pdf#page=15)). Refer to sections 3.4 and 3.5 of the datasheet for details. This allows a computer connected via VBUS at the same time the board is powred by +BATT (or the J11 external source).
- VBUS - The USB OTG's power pin. Note that J6 is provided (and needs to have a jumper installed)  in order to source VBUS from the board's +5V supply when the USB OTG interface is being used in HOST mode.

### Processing and Communications
The PRC is intended to serve as a low-cost roboRIO.  To that end it includes
computation and communication at the heart of the system.

#### Pi Pico W
The PRC includes a socket to install a Raspberry Pi Pico W board. This
is in component designator U2.

#### CAN  
The PRC includes a socket to install an Adafruit Picowbell board
([link](https://www.adafruit.com/product/5728)). This board uses a Microchip
MCP2515 SPI to CAN device. This is an optional device; the PRC can opeate with
CAN, Ethernet, Both, or none.

The CAN and Ethernet boards share the same SPI MOSI, MISO, and SCK signals, but
have independent chips selects (and in the case of CAN a separate interrupt
signal).

#### Ethernet
The PRC includes a socket to install an Adafruit Ethernet Featherwing
([link](https://www.adafruit.com/product/3201)).This is an optional device;
the PRC can opeate with CAN, Ethernet, Both, or none.

The CAN and Ethernet boards share the same SPI MOSI, MISO, and SCK signals, but
have independent chips selects.

### Sensors
There are multiple digital and analog sensor connection methods used with the PRC
board. These include a number of I2C interfaces that use the Qwiic/STEMMA QT format,
analog inputs, and digital I/Os.

#### Qwiic / STEMMA QT
There are four (4) Qwiic/STEMMA QT connectors. These connectors (X1-X4) connect
to the Pico W I2C bus 1 via an TCA9546 4-port I2C switch/mux (I2C bus 1
address 0x70).

The Qwiic/STEMMA QT connector provide the two I2C signals (each connector coming
from one dedicated output of the I2C mux/switch), 3.3V, and GND. This format
connector assumes the attached device provides the SDA/SCL pull ups and any local
level shifting to the sensor. It also assumes the board provides 3.3V conversion
to the sensor used. Each Qwiic/STEMMA QT connection may chain multiple sensors
provided their I2C addresses do not collide and the signal integrity of the I2C
signals is maintained.

The Qwiic/STEMMA QT to mux/switch channel is provided in the following table.
<table>
  <tr style="background-color:#404040">
    <th>Channel</th>
    <th>Interface</th>
    <th>Function / # </th>
  </tr>
  <tr>
    <td>0</td>
    <td rowspan="2">X1</td>
    <td>SDA0</td>
  </tr>
  <tr>
    <td>1</td>
    <td>SCL0</td>
  </tr>
  <tr>
    <td>2</td>
    <td rowspan="2">X2</td>
    <td>SDA1</td>
  </tr>
  <tr>
    <td>3</td>
    <td>SCL1</td>
  </tr>
  <tr>
    <td>4</td>
    <td rowspan="2">X3</td>
    <td>SDA3</td>
  </tr>
  <tr>
    <td>5</td>
    <td>SCL3</td>
  </tr>
  <tr>
    <td>6</td>
    <td rowspan="2">X4</td>
    <td>SDA2</td>
  </tr>
  <tr>
    <td>7</td>
    <td>SCL2</td>
  </tr>
</table>

#### ADC / Analog Input
There are two (2) analog input pins that connect to the Pico W ADC0 and ADC1
pins. The board buffers the input signals between pin and Pico W ADC inputs with
a unity gain opamp.  This is done to provide the highest accuracy while allowing
the use of sensors with larger output impedances.

The ADCs use a 3x2 pin header, and uses the same pin layout as the roboRIO's AIN
connections; signal, power, and ground. Ground is closest to the board edge and
power in the middle. The power pin voltage is 3.3V since the Pico W ADC range is
0 to 3.3 V.

#### Digital Input/Output (DIO)
There are eight (8) DIOs arranged in two groups of four, DIO0-3 and DIO4-7.
Each group has an independent level shifter (TXS0104E). The level shifter
includes 10 kΩ pull ups. Since the Pico W has 3.3V (only) I/Os, the VCCA of both
level shifters use 3.3 V. However the VCCB of the external side of each level
shifter is set by an external jumper (J5 for DIO0-3 and J9 for DIO4-7) and
can be set to either 3.3 V or 5 V.

Each DIO group uses a 3x4 pin header, and uses the same pin layout as the roboRIO's
DIO connections; signal, power, and ground. Ground is closest to the board edge
and power in the middle. The power pin voltage is the same voltage pdovided
to the VCCB of the level shifter.

### Motor Control
There are two main interfaces for controlling motors and servos.
1. PWM/Servo interface. Eight (8) conventional PWM/Servo connections.
1. There is also a dedicated motor control interface to connect to a custom, 4 channel, low-current, motor driver board.

#### PWM/Servo

The PWM/Servo interface uses the first 8 channels of a PCA9685 PWM generator
(I2C bus 0, I2C address 0x40).

If using the PWM/Servo interface for servo control, connect the J12 connector
(supplying SERVO_VDD) to an external power supply. This is not needed if the
PWM/Servo interface is being used to connect to external motor controllers
from REV, CTRE, etc.

<table>
  <tr style="background-color:#404040">
    <th>Channel</th>
    <th>Interface</th>
    <th>Function / # </th>
  </tr>
  <tr>
    <td>0</td>
    <td rowspan="8">PWM Block</td>
    <td>PWM 0</td>
  </tr>
  <tr>
    <td>1</td>
    <td>PWM 1</td>
  </tr>
  <tr>
    <td>2</td>
    <td>PWM 2</td>
  </tr>
  <tr>
    <td>3</td>
    <td>PWM 3</td>
  </tr>
  <tr>
    <td>4</td>
    <td>PWM 4</td>
  </tr>
  <tr>
    <td>5</td>
    <td>PWM 5</td>
  </tr>
  <tr>
    <td>6</td>
    <td>PWM 6</td>
  </tr>
  <tr>
    <td>7</td>
    <td>PWM 7</td>
  </tr>
  <tr>
    <td>8-15</td>
    <td colspan="2">Unused</td>
  </tr>
</table>

#### Motor Control

The motor control interface uses the first 8 channels of a dedicated PCA9685 PWM
generator (I2C bus 0, I2C address 0x41).

These connect to the motor controller board and drive four (4) instances of a TI
DRV8870 3.5 A motor controller. This board is intended to be used in FTC-class
robots or for classroom and learning (not competition) use. 

The DRV8870 has 2 signal inputs per IC (IN1, IN2).  The motor controller
operates as follows:

<table>
  <tr style="background-color:#404040">
    <th>IN1</th>
    <th>IN2</th>
    <th>OUT 1</th>
    <th>OUT 2</th>
    <th>Motor Action </th>
  </tr>
  <tr>
    <td>0</td>
    <td>0</td>
    <td>High-Z</td>
    <td>High-Z</td>
    <td><u>Coast</u><br />Current direction remains and flows through reverse body diodes of H-bridge. </td>
  </tr>
  <tr>
    <td>0</td>
    <td>1</td>
    <td>GND</td>
    <td>VDD</td>
    <td><u>Reverse</u><br />Current flows from OUT 2 to OUT 1.</td>
  </tr>
  <tr>
    <td>1</td>
    <td>0</td>
    <td>VDD</td>
    <td>GND</td>
    <td><u>Forward</u><br /> Current flows from OUT 1 to OUT 2.</td>
  </tr>
  <tr>
    <td>1</td>
    <td>1</td>
    <td>GND</td>
    <td>GND</td>
    <td><u>Brake</u><br />Current recirculates between low-side H-bridge.</td>
  </tr>
</table>

Note: When pulse width modulating the IN1 & IN2 to provide speed control
of the attached motors, it is important to realize that operating in coast
or brake modes is important to consider.

In coast mode, the motor coasts when both IN1 and IN2 are 0. This matches
the normal signal polarity of a PWM signal (high represents active).

<table>
  <tr style="background-color:#404040">
    <th>Mode</th>
    <th>Direction</th>
    <th>IN1</th>
    <th>IN2</th>
  </tr>
  <tr>
    <td rowspan="2">Coast</td>
    <td>Forward</td>
    <td>PWM'd</td>
    <td>0</td>
  </tr>
  <tr>
    <td>Reverse</td>
    <td>0</td>
    <td>PWM'd</td>
  </tr>
</table>

The PWM will drive the motor fur the duration of the high time of the duty
cycle and coast through the low time.

In brake mode, the motor breaks when both IN1 and IN2 are 1. This is opposite
the normal signal polarity of a PWM signal, so the signal generation needs
to be inverted and the low-time needs to represent the desired fraction of
the output. Also, the PWM'd input signal must be swapped so that the
correct direction is maintained.

<table>
  <tr style="background-color:#404040">
    <th>Mode</th>
    <th>Direction</th>
    <th>IN1</th>
    <th>IN2</th>
  </tr>
  <tr>
    <td rowspan="2">Coast</td>
    <td>Forward</td>
    <td>1</td>
    <td>inverse PWM'd</td>
  </tr>
  <tr>
    <td>Reverse</td>
    <td>Inverse PWM'd</td>
    <td>1</td>
  </tr>
</table>

Also note this is a not the PWM encoding used for servo controls. The PWM
modulation applied to IN1 and IN2 is full duty cycle of the signal's period
(not the first 2 ms of 20 ms signal).

I2C bus 0, address 0x41
<table>
  <tr style="background-color:#404040">
    <th>Channel</th>
    <th>Interface</th>
    <th>Function / # </th>
  </tr>
  <tr>
    <td>0</td>
    <td rowspan="2">M0</td>
    <td>IN1</td>
  </tr>
  <tr>
    <td>1</td>
    <td>IN2</td>
  </tr>
  <tr>
    <td>2</td>
    <td rowspan="2">M1</td>
    <td>IN1</td>
  </tr>
  <tr>
    <td>3</td>
    <td>IN2</td>
  </tr>
  <tr>
    <td>4</td>
    <td rowspan="2">M2</td>
    <td>IN1</td>
  </tr>
  <tr>
    <td>5</td>
    <td>IN2</td>
  </tr>
  <tr>
    <td>6</td>
    <td rowspan="2">M3</td>
    <td>IN1</td>
  </tr>
  <tr>
    <td>7</td>
    <td>IN2</td>
  </tr>
  <tr>
    <td>8-15</td>
    <td colspan="2">Unused</td>
  </tr>
</table>

### Status

The PRC provides simple interfaces for visual status.

#### NEOPIXEL on PCB

A single NEOPIXEL device is mounted on the board. This is intended to provide
visual status while developing code or tuning algodrithms and mechanisms.

#### NEOPIXEL Strip

A 3-position 250-series WAGo connector is provided to connect a NEOPIXEL strip
to the board. This is intended to provide visual status for distant observation.
The most common use case being robot to driver status across the FRC field.

### PCB Layer Usage

The PRC PCB uses four layers primarily to keep power distribution as clean
as possible. The layers are used as described in the following table. Each
layer label includes a link to the layer's image.

<table>
  <tr style="background-color:#404040">
    <th>Layer</th>
    <th>Use</th>
  </tr>
  <tr>
    <td rowspan="3"><a href="https://github.com/2468shrm/Pico-Robotic-Controller/blob/main/Images/F.Cu.png">F.Cu</a></td>
    <td>+3V3 fill (main +3.3V plane)</td>
  </tr>
  <tr>
    <td>Signal routing</td>
  </tr>
  <tr>
    <td>Component placement (SMT)</td>
  </tr>
  <tr>
    <td rowspan="2"><a href="https://github.com/2468shrm/Pico-Robotic-Controller/blob/main/Images/In1.Cu.png">In1.Cu</a></td>
    <td>+BATT fill (main battery plane)</td>
  </tr>
  <tr>
    <td>Signal routing</td>
  </tr>
  <tr>
    <td rowspan="3"><a href="https://github.com/2468shrm/Pico-Robotic-Controller/blob/main/Images/In2.Cu.png">In2.Cu</a></td>
    <td>+5V fill (main +5V plane)</td>
  </tr>
  <tr>
    <td>VIOA and VIOB (DIO power)</td>
  </tr>
  <tr>
    <td>Signal routing (across CPU, CAN, Eth modules)</td>
  </tr>
  <tr>
    <td rowspan="2"><a href="https://github.com/2468shrm/Pico-Robotic-Controller/blob/main/Images/B.Cu.png">B.Cu</a></td>
    <td>Ground fill (main ground plane)</td>
  </tr>
  <tr>
    <td>+5V fill (small fills and 5V traces)</td>
  </tr>
</table>
