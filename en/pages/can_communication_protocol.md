# CAN Communication Protocol

## 1 Products Information

### 1.1 CAN Protocol Overview

*     CAN is an abbreviation of Controller Area Network (hereafter referred to as CAN) and is an ISO international standardized serial communication protocol.

*     INNFOS product design is subject to the CAN2.0A protocol standard. This article details the CAN communication protocol format of the company's products and the CAN communication structure of the product.

### 1.2 Comprehensive performance parameters

<table style="width:400px"><thead><COL WIDTH=50%><COL WIDTH=50%><tr><th colspan="2"style=background:PaleTurquoise>Table 1-1 Description of the comprehensive performance parameters</th></tr></thead><tbody><tr><td>project</td><td>Description</td></tr><tr><td>Link layer protocol</td><td>CAN bus</td></tr><tr><td>CAN-ID type</td><td>11bit-CAN2.0A</td></tr><tr><td>Baud rate</td><td>1Mbit/s</td></tr><tr><td>Maximum number of sites</td><td>63</td></tr><tr><td>CAN frame length</td><td>0~8 bytes</td></tr><tr><td>Application layer CAN frame type</td><td>Data frame, remote frame</td></tr><tr><td>Terminal matching resistor</td><td>120Ω</td></tr></tbody></table>

The baud rate of this communication protocol is 1Mbit/s. For CAN communication, the cable types have little effect on the transmission distance, but the wire diameter is as thick as possible. The maximum number of nodes is 64. The company's products use 0.205mm2 wire diameter, the largest. The transmission distance is 25m.

## 2 Wiring

* The INNFOS actuator's patch cord interface is a CAN communication interface, as shown in the figure below. The internal pins of the same name are connected together, and their interface definitions are shown in Figure 2-1. The CAN interface connector is equipped with at least CANH, CANL, and CGND pins.


<table><thead><tr><th colspan="4" style=background:PaleTurquoise>Table 2-1 Communication Signal Connector Pin Definitions</th></tr></thead><tbody><tr><td style="width:80px">Pin number</td><td>definition</td><td>description</td><td>	Terminal pin distribution</td></tr><tr><td>1</td><td>PVDD</td><td>功率电源</td><td rowspan="9"><img src="../img/peixian2-2.png" style="width:550px"></td></tr><tr><td>3</td><td>PVDD</td><td>Power supply</td></tr><tr><td>5</td><td>PVDD</td><td>Power supply</td></tr><tr><td>2</td><td>GND</td><td>Power Ground</td></tr><tr><td>4</td><td>GND</td><td>Power Ground</td></tr><tr><td>6</td><td>CGND</td><td>CAN Ground</td></tr><tr><td>7</td><td>CANL</td><td>CAN communication interface</td></tr><tr><td>8</td><td>CANH</td><td>CAN communication interface</td></tr></tbody></table>

**Table 2-1 Communication Signal Connector Pin Definitions**

The connection of CAN_GND greatly improves the anti-interference performance of the CAN interface.


### 2.1 CAN communication bus and multi-node connection

<img src="../img/wiring2-3.png" style="width:600px">

**图2-1 CAN通信网络的连接方式为总线连接方式**

Each CAN transceiver device is attached to the bus, and each branch length is less than 0.3m, otherwise it will cause reflection and cause communication problems. 


*  It is recommended to use shielded twisted pair connection,two 120Ω termination matching resistors should be connected at both ends of the bus in order to prevent signal reflection. The shielding layer shall be reliably generally grounded at a single point.

*   Use a multimeter to measure the resistance between CANH and CANL to confirm that the resistance at both ends of the field is correctly connected. The normal resistance value should be at about 60Ω (the parallel value of the two resistors).

*   The maximum number of attached devices is 64.

*   For long-distance communication of CAN equipment, CAN_GND of different CAN circuits must be connected to each other to ensure that the reference potentials between different communication devices are equal.

*   CGND refers to CAN_GND, which can be used as a signal level reference and improve the anti-interference ability; GND is the common ground in the three-phase power supply of the actuator, and collects the large current of the three-phase power supply to the negative pole.


### 2.2 Twisted pairs are recommended to use as CAN communication cables

Twisted pairs are recommended to use as CAN communication cables because of its good resistance to high-frequency magnetic field noise interference and abilities to reduce the external radiation of the cables, as shown in Figure 2-5.

<img src="../img/wiring2-5.png" style="width:600px">

**Fig 2-2：Schematic diagram of twisted pair**


*   The torque D of the twisted pair should be less than 2cm. The smaller the torque, the better the interference resistance will be.

*   For short-distance low-speed communication, twisted-pair shielded wires can be used to increase the anti-interference ability, STP is connected to PE.

*   Shielded wires are not recommended for long distance high speed communication. The large distributed capacitance between the shield and the signal line could cause transmission delay of signal.

### 2.3 Descriptions for other devices without external CAN_GND port wiring

#### The device is non-isolated CAN, sharing GND or COM port with other signals

<img src="../img/wiring2-11.png" style="width:600px">

**Fig 2-3：Connections shared with other circuits**

## 3 communication protocol

### 3.1 communication protocol format

<img src="../img/wiring2-13.png" style="width:600px">

**图3-1**

Figure 3-1: Device address corresponding identifier bit, CAN bus standard data frame identifier bit is 11 bits, this protocol uses only 8 of them, just occupies one byte, data length corresponds to DLC, occupies a half byte. The contents of the instruction parameter are also located in data field. The content of the instruction located at front followed by the parameter, the high byte located at front followed by the low byte.The data length is equal to the instruction character plus the parameter content

**Device Address** 
A byte of data，identifies the address of the device to communicate with, 0x01 to 0xff are available. 0x00 is the broadcast address. 

**The length of data** 
Half a byte of data, identifies the number of specific data to be communicated. The range is 0x00 to 0x0F. The data out of range will not be processed. 

**Instruction byte** 
A byte of data，identifies the specific operation performed by the master and the slave. The value ranges from 0x00 to 0xff. 

**Parameter content** 
The specific parameter content of an instruction whose length is equal to the data length minus one. Some instructions do not contain specific data and should have a data digit of 1.


#### IQmath Instruction

<img src="../img/3-1communicationprotocol.png" style="width:600px">

**Fig3-2**

<table style="width:650px"><thead><tr><th rowspan="2" style=background:PaleTurquoise>Data Type</th><th colspan="2" style=background:PaleTurquoise>Range</th><th rowspan="2"style=background:PaleTurquoise>Resolution/Precision</th></tr><tr> <td>Min</td> <td>Max</td> </tr></thead><tbody><tr><td>_iq30</td><td>-2</td><td>1.999 999 999</td><td>0.000 000 001</td></tr><tr><td>_iq29</td><td>-4</td><td>3.999 999 998</td><td>0.000 000 002</td></tr><tr><td>_iq28</td><td>-8</td><td>7.999 999 996</td><td>0.000 000 004</td></tr><tr><td>_iq27</td><td>-16</td><td>15.999 999 993</td><td>0.000 000 007</td></tr><tr><td>_iq26</td><td>-32</td><td>31.999 999 985</td><td>0.000 000 015</td></tr><tr><td>_iq25</td><td>-64</td><td>63.999 999 970</td><td>0.000 000 030</td></tr><tr><td>`_iq24`</td><td>`-128`</td><td>`127.999 999 940`</td><td>`0.000 000 060`</td></tr><tr><td>_iq23</td><td>-256</td><td>255.999 999 981</td><td>0.000 000 119</td></tr><tr><td>_iq22</td><td>-512</td><td>511.999 999 762</td><td>0.000 000 238</td></tr><tr><td>_iq21</td><td>-1024</td><td>1023.999 999 523</td><td>0.000 000 477</td></tr><tr><td>_iq20</td><td>-2048</td><td>2047.999 999 046</td><td>0.000 000 954</td></tr><tr><td>_iq19</td><td>-4096</td><td>4095.999 998 093</td><td>0.000 001 907</td></tr><tr><td>_iq18</td><td>-8192</td><td>8191.999 996 185</td><td>0.000 003 815</td></tr><tr><td>_iq17</td><td>-16384</td><td>16383.999 992 371</td><td>0.000 007 629</td></tr><tr><td>_iq16</td><td>-32768</td><td>32767.999 984 741</td><td>0.000 015 259</td></tr><tr><td>_iq15</td><td>-65536</td><td>65535.999 969 482</td><td>0.000 030 518</td></tr><tr><td>_iq14</td><td>-131072</td><td>131071.999 938 965</td><td>0.000 061 035</td></tr><tr><td>_iq13</td><td>-262144</td><td>262143.999 877 930</td><td>0.000 122 070</td></tr><tr><td>_iq12</td><td>-524288</td><td>524287.999 755 859</td><td>0.000 244 141</td></tr><tr><td>_iq11</td><td>-1048576</td><td>1048575.999 511 719</td><td>0.000 488 281</td></tr><tr><td>_iq10</td><td>-2097152</td><td>2097151.999 023 437</td><td>0.000 976 563</td></tr><tr><td>_iq9</td><td>-4194304</td><td>4194303.998 046 875</td><td>0.001 953 125</td></tr><tr><td>_iq8</td><td>-8388608</td><td>8388607.996 093 750</td><td>0.003 906 250</td></tr><tr><td>_iq7</td><td>-16777216</td><td>16777215.992 187 500</td><td>0.007 812 500</td></tr><tr><td>_iq6</td><td>-33554432</td><td>33554431.984 375 000</td><td>0.015 625 000</td></tr><tr><td>_iq5</td><td>-67108864</td><td>67108863.968 750 000</td><td>0.031 250 000</td></tr><tr><td>_iq4</td><td>-134217728</td><td>134217727.937 500 000</td><td>0.062 500 000</td></tr><tr><td>_iq3</td><td>-268435456</td><td>268435455.875 000 000</td><td>0.125 000 000</td></tr><tr><td>_iq2</td><td>-536870912</td><td>536870911.750 000 000</td><td>0.250 000 000</td></tr><tr><td>_iq1</td><td>-1073741824</td><td>1 073741823.500 000 000</td><td>0.500 000 000</td></tr></tbody></table>

Note:_iq24 is INNFOS main application.

*  In general ，The processor we used only supports hardware floating-point arithmetic directly, such as some devices with FPU, or just supports fixed-point arithmetic. In this case, the processing of floating-point numbers needs to be done by the compiler. On devices that support hardware floating-point processing, the quickest way to program floating-point operations is to use floating-point types directly, such as single-precision floats. However, in many cases, limited to cost, material and other factors, when we use only one fixed-point processor, if directly using the float type for floating-point type operations,even a simple floating-point arithmetic will make the compiler to generate a lot of code. It will cause a significantly increase of the program excution time, and the resources occupied will mutiply. This involves the problem of how to efficiently handle floating-point operations on fixed-point processors.

*  Since it is a fixed-point processor, it is much more efficient at processing fixed-point numbers, or literal “integers” than it is dealing with floating-point types. So on fixed-point processors, we use fixed-point integers to represent a floating-point number, and specify integer digits and scales to easily convert fixed-point and floating-point numbers. Taking a 32-bit fixed-point number as an example, suppose the conversion factor is Q, that is, the number of decimal places in 32 bits is Q, and the number of integer digits is 31-Q (in the case of signed numbers). The conversion relationship of fixed-point numbers and floating-point numbers is:


references:

[C28x_IQmath_Library.pdf](../img/C28x_IQmath_Library.pdf)

[IQ-MATH_Library.pdf](../img/IQ-MATH_Library.pdf)


Fixed point number = floating point number × 2^Q 

For example, when the floating point number -2.0 is converted to a fixed point number with Q of 24, the result is: fixed point number = -2 × 2^24 = -33554432. 

The range of representation of the 32-bit signed number is: -2147483648 to 2147483647. If we convert the maximum value of 2147483647 of the signed fixed point number to a floating point number corresponding to Q, the result is: floating point number 2147483647/2^24=127.999999940.

* See Appendix D for specific methods of IQ value conversion.

### 3.2 CAN communication protocol command application example

**Example 1. Write command**

<table style="width:400px"><thead><tr><th colspan="4"style=background:PaleTurquoise>Read the current speed value of the actuator motor ID 0x01</th></tr></thead><tbody><tr><td>Device address</td><td>Data length</td><td>CMD</td><td>parameter</td></tr><tr><td>0x01</td><td>0x01</td><td>0x05</td><td>NO</td></tr></tbody></table>

Device address: 0x01 = Object ID 

Data length: 0x1 = Data length 

Instruction character: 0x05 = Current speed command read 

Parameter content: None = Parameter content sent 

Content: 0x05


<table style="width:400px"><thead><tr><th colspan="4"style=background:PaleTurquoise>Answer command</th></tr></thead><tbody><tr><td>Device address</td><td>Data length</td><td>Command Key</td><td>CMD</td></tr><tr><td>0x01</td><td>0x05</td><td>0x05</td><td>data[3~0]</td></tr></tbody></table>


Return device address: 0x01 = Response object ID 

Data length: 0x5 = Data length of the response 5 bits 

Instruction character: 0x05 = Acknowledge the current speed command (same as the send command) 

Parameter content: 0xXX 0xXX 0xXX 0xXX = Parameter content of the response

Response content :0x05 0xXX 0xXX 0xXX 0xXX 


Description: The parameter content data[3~0] is in the high position and the low bit is in the back. For the _IQ24 format. _IQ(-1.0)~_IQ(1.0) represents the reverse speed full scale and forward speed full scale. The full scale is 6000 RPM. If data = _IQ (0.5). 
Then it is 0.5*6000=3000RPM.


**Example 2. Write command**

<table style="width:400px"><thead><tr><th colspan="4"style=background:PaleTurquoise>Set the current position value of the actuator motor ID to 0x01 </th></tr></thead><tbody><tr><td>Device address</td><td>Data length</td><td>CMD</td><td>parameter</td></tr><tr><td>0x01</td><td>0x5</td><td>0x0A</td><td>0x05 0x00 0x00 0x00</td></tr></tbody></table>


Device address: 0x01 = Set object ID 
Data length: 0x5 = Data length 
Instruction character: 0x0A = Set position 
Parameter: 0x05 0x00 0x00 0x00 = Parameter content sent 
Send content: 0x0A 0x05 0x00 0x00 0x00 

Description: Parameter content data[3 ~0] The high position is in the front and the low position is in the back. For the _IQ24 format. _IQ(-128.0)~_IQ(127.999999940) represents the reverse position value full scale and forward position value full scale. If data=_IQ(5.0), set the current position to 5.


*    应答内容：无应答（特殊协议）


* * *

* General steps for using the command mode:

(1) SCA enable, command: 0x2A 01;

(2) Select the usage mode, command: current loop 0x07 01, speed loop 0x07 02, position loop 0X07 03, S-position mode 0X07 06, S-speed mode 0X07 07, HOMING mode 0X07 08;

(3) Set the relevant parameters, the instruction refers to the appendix of the manual. For the current value, speed value, position parameter, it is not 0, then it starts, and if it is 0, it stops;

(4) End of use, SCA disable, command: 0X2A 00. The disable command must be sent before the power is turned off, otherwise the zero position may be lost.


* * *

<img src="../img/position.jpg" style="width:600px">

**图3-3**

Note:

*  The maximum amplitude (Maximum) set by the host computer is _IQ (1.0), and the minimum amplitude (Minimal) is _IQ (-1.0), which acts as a limiting function (the schematic diagram is shown in Figure 3-2). Example: (Figure: 3-2 uses the output of the position loop through the limiter module as the input of the speed loop. Assuming _IQ(0.5), _IQ(-0.5), the maximum speed of the position loop output should be ±0.5x6000=±3000RPM )

*  The upper limit of the proportional integral setting is _IQ (127.999999940), and the lower limit of the set value is _IQ (-128.0), but the set value is adjusted according to the actual operation (schematic diagram: 3-2)

*  The current loop sets the current value range from _IQ(-1.0)~_IQ(1.0). The actual current value is the IQ value multiplied by the full scale. Example: (QDD-6010 model actuator full-scale current value is 33A, _IQ (0.5) The actual current value is 0.5x33A=16.5A, See the SCAs parameter list)

*  The speed loop sets the speed value range from _IQ(-1.0)~_IQ(1.0), and the actual speed value is the IQ value multiplied by the full scale (see ). Example: (_IQ (0.5) the actual speed is 0.5 * 6000 = 3000RPM)

*  Since the position loop is in _IQ24 format, the forward full scale is _IQ (127.999999940), the reverse full scale is _IQ (-128.0), and the IQ value is the actual value. For example: （_IQ(60.0) is the actual position. 60R, that is, the position where the zero position is rotated forward by 60 turns.)

*  Speed loop curve mode and position loop curve mode, you can set the acceleration, deceleration, and relatively smooth to reach your preset speed value and position, which can avoid excessive current during operation, trigger actuator over-current protection or Power supply overcurrent protection.


### 3.3 CAN communication protocol command reference

#### Receive command

<table style="width:600px"><thead><tr><th colspan="3"style=background:PaleTurquoise>3.3.1.1 Send data 1 byte, return data 2 bytes</th></tr><tr><td style="width:150px">Command name</td><td colspan="2">Receive command</td></tr></thead><tbody><tr><td>Description</td><td colspan="2">This command type sends a data length of 1, and returns a data length of 2</td></tr><tr><td>command key</td><td colspan="2">See instruction 1</td></tr><tr><td>Data length</td><td colspan="2">1</td></tr><tr><td>Data content</td><td colspan="2">NO</td></tr><tr><td>Command character (return value)</td><td colspan="2">See read instruction 1</td></tr><tr><td>Data length (return value)</td><td colspan="2">2</td></tr><tr><td rowspan="2">slave computer returns data</td><td>0x01：Success / enable /  normal</td><td rowspan="2">See the pattern table for the query return data.</td><tr><td>0x00：Failed / disabled /  abnormal</td></tr></tbody></table>

<table style="width:600px"><thead><tr><th colspan="3"style=background:PaleTurquoise>3.3.1.2 Send data 1 byte, return data 3 bytes</th></tr></thead><tbody><tr><td style="width:150px">Command name</td><td colspan="2">Receive command</td></tr><tr><td>Description</td><td colspan="2">This command class sends a data length of 1, returns a data length of 3, reads the actuator parameter value, and the high order first. The value is 2^8 times the true value.`（Special instructions are specified in the instruction list）`</td></tr><tr><td>command key</td><td colspan="2">See read instruction2</td></tr><tr><td>Data length</td><td colspan="2">1</td></tr><tr><td>Data content</td><td colspan="2">NO</td></tr><tr><td>Command character (return value)</td><td colspan="2">See read instruction2</td></tr><tr><td>Data length (return value)</td><td colspan="2">3</td></tr><tr><td>slave computer returns data</td><td>The data is in IQ8 format</td><td>See also the alarm instruction list</td></tr></tbody></table>

<table style="width:600px"><thead><tr><th colspan="3"style=background:PaleTurquoise>3.3.1.3 Send data 1 byte, return data 5 bytes</th></tr></thead><tbody><tr><td style="width:150px">Command name</td><td>Receive command</td></tr><tr><td>Description</td><td>This command class sends a data length of 1, returns a data length of 5, the high actuator parameter value will be read first. <br>The value is 2^24 times the true value.`（Special instructions are specified in the instruction list）`</td></tr><tr><td>command key</td><td>See read instruction3</td></tr><tr><td>Data length</td><td>1</td></tr><tr><td>Data content</td><td>NO</td></tr><tr><td>Command character (return value)</td><td>See read instruction3</td></tr><tr><td>Data length (return value)</td><td>5</td></tr><tr><td>slave computer returns data</td><td>	The data is in IQ24 format.`(Special instructions are specified in the instruction list)`</td></tr></tbody></table>

#### Write commands

<table style="width:600px"><thead><tr><th colspan="3"style=background:PaleTurquoise>3.3.2.1Send data 2 bytes, return data 2 bytes</th></tr></thead><tbody><tr><td style="width:150px">Command name</td><td colspan="2">write command</td></tr><tr><td>Description</td><td colspan="2">This command will send a data length of 2, the return data length is 2, and a byte after the data is sent indicates that the parameter content is to be written. </td></tr><tr><td>command key</td><td colspan="2">write command 1</td></tr><tr><td>Data length</td><td colspan="2">2</td></tr><tr><td rowspan="2">Data content</td><td>0x01 Enable</td><td rowspan="2">See mode table for mode settings.</td></tr> <tr><td>0x00 Disable</td></tr><tr><td>Command character (return value)</td><td colspan="2">write command 1</td></tr><tr><td>Data length (return value)</td><td colspan="2">2</td></tr><tr><td rowspan="2">slave computer returns data</td><td colspan="2">0x01 success</td></tr><tr><td colspan="2">0x00 fail</td></tr></tbody></table>

Note:( After power-on, send the power-on command to use. 
The shutdown command must be send before power-off, otherwise the zero position may be lost.)

<table style="width:600px"><thead><tr><th colspan="2"style=background:PaleTurquoise>3.3.2.2Send data 3 bytes, return data 2 bytes</th></tr></thead><tbody><tr ><td style="width:150px">Command name</td><td colspan="2">write command</td></tr><tr><td>Description</td><td>The data length of this command class is 3 bytes, the return data length is 2 bytes, and the 2 bytes after the data is sent indicate that higher parameter content is to be written first. The value is 2^8 times the true value.</td></tr><tr><td>command key</td><td>write command 2</td></tr><tr><td>Data length</td><td colspan="2">3</td></tr><tr><td rowspan="2">Data content</td><td>value in IQ8 format</td></tr><tr><td>0x00：Disable</td></tr><tr><td>Command character (return value)</td><td>write command 2</td></tr><tr><td>Data length (return value)</td><td>2</td></tr><tr><td rowspan="2">slave computer returns data</td><td>0x01：success</td></tr><tr><td>0x00：fail</td></tr></tbody></table>


<table style="width:600px"><thead><tr><th colspan="3"style=background:PaleTurquoise >3.3.2.3Send data 5 bytes, return data 2 bytes or less</th></tr></thead><tbody><tr><td style="width:150px">Command name</td><td colspan="2">Receive command</td></tr><tr><td>Description</td><td colspan="2">The data length of this command class is 5 bytes, the return data length is 2 bytes, and the 4 bytes after the data is sent indicate that higher parameter content is to be written first. The value is 2^24 times the true value.`(Special instructions are specified in the instruction list)`</td></tr><tr><td>command key</td><td colspan="2">write command 3</td></tr><tr><td>Data length</td><td colspan="2">5</td></tr><tr><td>Data content</td><td colspan="2">value in IQ24 format。`(Special instructions are specified in the instruction list)`</td></tr><tr><td>Command character (return value)</td><td colspan="2">write command 3</td></tr><tr><td>Data length (return value)</td><td colspan="2">2 or 0</td></tr><tr><td rowspan="2">slave computer returns data</td><td>0x01：success</td><td rowspan="2">`((Three special instructions have no return data, which has been marked in the instruction list)。`</td></tr><tr><td>0x00：fail</td></tr></tbody></table>

<table style="width:600px"><thead><tr><th colspan="2" style=background:PaleTurquoise>3.3.2.4 Send data 1 bytes, return data 2 bytes</th></tr></thead><tbody><tr><td style="width:150px">Command name</td><td>write command</td></tr><tr><td>Description</td><td>The data length of this command class is 1 bytes, the return data length is 2 bytes</td></tr><tr><td>command key</td><td>write command 4</td></tr><tr><td>Data length</td><td>1</td></tr><tr><td>Data content</td><td>No</td></tr><tr><td>Command character (return value)</td><td>write command 4</td></tr><tr><td>Data length (return value)</td><td>2</td></tr><tr><td rowspan="2">slave computer returns data</td><td>0x01：sucess</td></tr><tr><td>0x00：fail</td></tr></tbody></table>


## 4 Appendix A

### A.1 Write command code value definition table

<table style="width:700px"><thead><tr><th colspan="3" style=background:PaleTurquoise>A.1.1 read instruction1</th></tr></thead><tbody><tr><td style="width:100px">Command key</td><td style="width:200px">Definition</td><td>Description</td></tr><tr><td>0x00</td><td>shake hands</td><td>The PC sends command, and the slave computer responds to it, indicating that the slave computer is ready to communicate with the host computer. It can also be used as a heartbeat protocol to query the status of the slave in real time.</td></tr> <tr><td>0x55</td><td>inquiry actuator current mode</td><td>Read the current mode of the actuator managed by the lower computer.</td></tr><tr><td>0xB0</td><td>Query the last shutdown state of the actuator</td><td>Read the last shutdown state of the actuator, normal / abnormal</td></tr><tr><td>0x71</td><td>Current loop filter status</td><td>Read current loop filter enable/disable for the specified ID actuator.</td></tr><tr><td>0x75</td><td>Speed loop filter status</td><td>Read speed loop filter enable/disable for the specified ID actuator</td></tr><tr><td>0x79</td><td>Position loop filter status</td><td>Read Position loop filter enable/disable for the specified ID actuator</td></tr><tr><td>0x2B</td><td>Actuator enable/disable</td><td>Read enable/disable status for the specified ID actuator</td></tr></tbody></table>

<table style="width:700px"><thead><tr><th colspan="3" style=background:PaleTurquoise>A.1.2 read instruction2</th></tr></thead><tbody><tr><td style="width:100px">Command key</td><td style="width:200px">Definition</td><td>Description</td></tr><tr><td>0x73</td><td>Current loop filter bandwidth</td><td>Read the bandwidth (Hz) of the specified ID actuator current loop filter</td></tr><tr><td>0x77</td><td>Speed loop filter bandwidth</td><td>Read the bandwidth (Hz) of the specified ID actuator speed loop filter</td></tr><tr><td>0x7B</td><td>Position loop filter bandwidth</td><td>Read the bandwidth (Hz) of the specified ID actuator Position loop filter</td></tr><tr><td>0x6C</td><td>Actuator motor protection temperature</td><td>Read motor protection temperature of actuator with the specified ID</td></tr><tr><td>0x6E</td><td>Actuator motor recovery temperature</td><td>Read motor recovery temperature of actuator with the specified ID</td></tr><tr><td>0x62</td><td>Actuator inverter protection temperature</td><td>Read inverter protection temperature of actuator with the specified ID</td></tr><tr><td>0x64</td><td>Actuator inverter recovery temperature</td><td>Read inverter recovery temperature of actuator with the specified ID</td>></tr><tr><td>0xFF</td><td>Alarm command (special command)</td><td>Lower machine alarm information</td></tr></tbody></table>

<table style="width:700px"><thead><tr><th colspan="3" style=background:PaleTurquoise>A.1.3 Read command 3</th></tr></thead><tbody><tr><td style="width:100px">Command key</td><td style="width:200px">Definition</td><td style="width:400px">Description</td></tr><tr><td>0x04</td><td>current value</td><td>Read the current current value of the specified ID actuator. The current value needs to be multiplied by the current full scale (See the SCAs parameter list). The unit is A.</td></tr><tr><td>0x05</td><td>Current speed value</td><td>Read the current speed value of the specified ID actuator. The true speed value needs to be multiplied by the speed full scale (see Appendix D) in RPM.</td></tr><tr><td>0x06</td><td>	Current position value</td><td>Reads the current position value of the specified ID executor in R</td></tr><tr><td>0x15</td><td>Current loop P</td><td>Read P of the current loop of the specified ID actuator</td></tr><tr><td>0x16</td><td>Current loop I</td><td>Read I of the current loop of the specified ID actuator</td></tr><tr><td>0x17</td><td>Speed loop P</td><td>Read the current speed loop P of the specified ID actuator</td></tr><tr><td>0x18</td><td>Speed loop I</td><td>Read the current speed loop I of the specified ID actuator</td></tr><tr><td>0x19</td><td>position loop P</td><td>Read the current position loop P of the specified ID executor</td></tr><tr><td>0x1A</td><td>position loop I</td><td>Read the current position loop I of the specified ID executor</td></tr><tr><td>0x1C</td><td>Max speed of position trapezoidal curve</td><td>Reads the maximum speed of the trapezoidal curve of the current position of the specified ID actuator</td></tr><tr><td>0x1D</td><td>Acceleration of position trapezoidal curve</td><td>Reads the maximum acceleration of the trapezoidal curve at the current position of the specified ID actuator</td></tr><tr><td>0x1E</td><td>Deceleration of position trapezoidal curve</td><td>Read the maximum deceleration of the trapezoidal curve of the current position of the specified ID actuator</td></tr><tr><td>0x22</td><td>Max speed of the speed trapezoidal curve</td><td>Reads the maximum speed of the current speed trapezoidal curve of the specified ID actuator</td></tr><tr><td>0x23</td><td>Acceleration of velocity trapezoidal curve</td><td>Reads the maximum acceleration of the current speed trapezoidal curve of the specified ID actuator</td></tr><tr><td>0x24</td><td>Deceleration of the speed trapezoidal curve</td><td>Reads the maximum deceleration of the current speed trapezoidal curve of the specified ID actuator</td></tr><tr><td>0x34</td><td>Lower limit of current loop output</td><td>Read the lower limit of the current current loop output of the specified ID actuator</td></tr><tr><td>0x35</td><td>Upper limit of current loop output</td><td>Read the upper limit of the current current loop output of the specified ID actuator</td></tr><tr><td>0x36</td><td>Lower limit of the speed loop output</td><td>Read the lower limit of the current speed loop output of the specified ID actuator</td></tr><tr><td>0x37</td><td>Upper limit of speed loop output</td><td>Read the upper limit of the current speed loop output of the specified ID actuator</td></tr><tr><td>0x38</td><td>Lower limit of position loop output</td><td>Read the lower limit of the current position loop output of the specified ID actuator</td></tr><tr><td>0x39</td><td>Upper limit of position loop output</td><td>Read the upper limit of the current position loop output of the specified ID actuator</td></tr><tr><td>0x85</td><td>Upper limit of actuator position</td><td>read upper limit of actuator position</td></tr><tr><td>0x86</td><td>Lower limit of actuator position</td><td>Read the lower limit of the position of the execution ID actuator</td></tr><tr><td>0x8A</td><td>	Actuator position offset</td><td>Read the position offset value of the specified ID actuator</td></tr><tr><td>0x92</td><td>The lower limit of the current when the actuator is automatically reset to zero</td><td>Read the lower limit of the current when the specified ID actuator is automatically reset to zero</td></tr><tr><td>0x93</td><td>	The upper limit of the current when the actuator is automatically reset to zero</td><td>Read the upper limit of the current when the specified ID actuator is automatically reset to zero</td></tr><tr><td>0x7F</td><td>Stall energy</td><td>Reads the stall energy of the specified ID actuator. （The value is 75.225 times the true value）The heating energy after blocking, the unit is J.</td></tr></tbody></table>

### A.2 Write command code value definition table

<table style="width:700px"><thead><tr><th colspan="3" style=background:PaleTurquoise>A.2.1 Write command 1</th></tr></thead><tbody><tr><td style="width:100px">Command key</td><td style="width:200px">Definition</td><td>Description</td></tr><tr><td>0x07：</td><td>Set the mode of the specified ID executor</td><td>Set the current mode of the specified ID executor</td></tr><tr><td>0x70：</td><td>Current loop filter status</td><td>Set the current loop filter enable/disable for the specified ID actuator</td></tr><tr><td>0x74：</td><td>Speed loop filter status</td><td>Set the speed loop filter enable/disable for the specified ID actuator</td></tr><tr><td>0x78：</td><td>Position loop filter status</td><td>Set position loop filter enable/disable for the specified ID actuator</td></tr><tr><td>0x2A：</td><td>Actuator on/off status</td><td>Set the specified ID actuator to power on/off</td></tr>
</tbody></table>


<table style="width:700px"><thead><tr><th colspan="3" style=background:PaleTurquoise>A.2.2 Write command 2</th></tr></thead><tbody><tr><td>Command key</td><td>Definition</td><td>Description</td></tr><tr><td>0x72：</td><td>Current loop filter bandwidth</td><td>Set the bandwidth (Hz) of the specified ID actuator current loop filter</td></tr><tr><td>0x76：</td><td>Speed loop filter bandwidth</td><td>Set the bandwidth (Hz) of the specified ID actuator speed loop filter</td></tr><tr><td>0x7A：</td><td>Position loop filter bandwidth</td><td>Set the bandwidth (Hz) of the specified ID actuator position loop filter</td></tr><tr><td>0x61：</td><td>Actuator protection temperature</td><td>Set the protection temperature of the specified ID actuator °C</td></tr><tr><td>0x63：</td><td>Actuator recovery temperature</td><td>Set the recovery temperature of the specified ID actuator °C</td></tr>
</tbody></table>


<table style="width:700px"><thead><tr><th colspan="3" style=background:PaleTurquoise>A.2.3 Write command 3</th></tr></thead><tbody><tr><td>Command key</td><td>Definition</td><td>Description</td></tr><tr><td>0x08：</td><td>Current value</td><td>Set the current current value of the specified ID actuator (Note: no return data)</td></tr><tr><td>0x09：</td><td>Current speed</td><td>Sets the current speed value for the specified ID executor. (Note: no return data)</td></tr><tr><td>0x0A：</td><td>Current value</td><td>Sets the current speed value for the specified ID executor. (Note: no return data)</td></tr><tr><td>0x0E：</td><td>Current loop P</td><td>Change the P value of the specified ID actuator current loop</td></tr><tr><td>0x0F：</td><td>Current loop I</td><td>Set the I value of the specified ID actuator current loop</td></tr><tr><td>0x10：</td><td>Speed loop P</td><td>Set the P value of the specified ID actuator speed loop</td></tr><tr><td>0x11：</td><td>Speed loop I</td><td>Set the I value of the specified ID actuator speed loop</td></tr><tr><td>0x12：</td><td>Position loop P</td><td>Set the P value of the specified ID actuator position loop</td></tr><tr><td>0x13：</td><td>Position loop I</td><td>Set the I value of the specified ID actuator position loop</td></tr><tr><td>0x1F：</td><td>Maximum speed of position trapezoidal curve</td><td>Change the maximum speed of the trapezoidal curve of the specified ID actuator position</td></tr><tr><td>0x20：</td><td>Acceleration of position trapezoidal curve</td><td>Change the maximum acceleration of the trapezoidal curve of the specified ID actuator position</td></tr><tr><td>0x21：</td><td>Deceleration speed of position trapezoidal curve</td><td>Change the maximum deceleration of the trapezoidal curve of the specified ID actuator position</td></tr><tr><td>0x25：</td><td>Maximum speed of the speed trapezoidal curve</td><td>Change the maximum speed of the specified ID actuator speed trapezoid</td></tr><tr><td>0x26：</td><td>Acceleration of velocity trapezoidal curve</td><td>Change the acceleration of the specified ID actuator speed trapezoidal curve</td></tr><tr><td>0x27：</td><td>Deceleration of the speed trapezoidal curve</td><td>Change the deceleration of the specified ID actuator speed trapezoid</td></tr><tr><td>0x2E：</td><td>Lower limit of current loop output</td><td>Change the lower limit of the specified ID actuator current loop output</td></tr><tr><td>0x2F：</td><td>Upper limit of current loop output</td><td>Change the upper limit of the specified ID actuator current loop output</td></tr><tr><td>0x30：</td><td>Lower limit of the speed loop output</td><td>Change the lower limit of the specified ID actuator speed loop output</td></tr><tr><td>0x31：</td><td>Upper limit of speed loop output</td><td>Change the upper limit of the specified ID actuator speed loop output</td></tr><tr><td>0x32：</td><td>Lower limit of position loop output</td><td>Change the lower limit of the specified ID actuator position loop output</td></tr><tr><td>0x33：</td><td>Upper limit of position loop output</td><td>Change the upper limit of the specified ID actuator position loop output</td></tr><tr><td>0x83：</td><td>Upper limit of actuator position</td><td>Change the upper limit of the position of the specified ID actuator</td></tr><tr><td>0x84：</td><td>Lower limit of actuator position</td><td>Lower limit of actuator position</td></tr><tr><td>0x87：</td><td>Lower limit of actuator position</td><td>Set the Home value of the specified ID executor</td></tr><tr><td>0x89：</td><td>Actuator position offset</td><td>Set the position offset value of the specified ID actuator</td></tr><tr><td>0x90：</td><td>Current lower limit of SCA while automatically zeroed</td><td>Set the lower limit of the current when the specified ID actuator is automatically reset to zero.</td></tr><tr><td>0x91：</td><td>Current upper limit of SCA while automatically zeroed</td><td>Set the upper limit of the current when the specified ID actuator is automatically reset to zero.</td></tr><tr><td>0x7E：</td><td>Stall energy</td><td>Set the stall energy of the specified ID actuator. (The value is 75.225 times the true value)The heating energy after blocking, the unit is J</td></tr></tbody></table>


<table style="width:700px"><thead><tr><th colspan="3" style=background:PaleTurquoise>A.2.4 Write command 4</th></tr></thead><tbody><tr><td>Command key</td><td>Definition</td><td>Description</td></tr><tr><td>0xFE：</td><td>Eliminate the alarm of the lower computer</td><td>Eliminate the alarm action of the lower position machine. After receiving the command, the lower position machine stops the alarm, otherwise the lower position machine is inoperable.</td></tr><tr><td>0x88</td><td>Clear Homing data</td><td>Clear Homing data</td></tr><tr><td>0x0D</td><td>Storage parameter</td><td>Storage parameter</td></tr></tbody></table>

## 5 Appendix B :Mode table

<table style="width:400px"><thead><tr style=background:PaleTurquoise><th>Command key</th><th>Command key</th></tr></thead><tbody><tr><td>0x01</td><td>Current mode</td></tr><tr><td>0x02</td><td>Speed mode</td></tr><tr><td>0x03</td><td>Position mode</td></tr><tr><td>0x06</td><td>Position trapezoidal mode (S curve)</td></tr><tr><td>0x07</td><td>Speed trapezoidal mode (S curve)</td></tr><tr><td>0x08</td><td>Homing mode</td></tr></tbody></table>

## 6 AppendixC：Alarm instruction list

<table style="width:600px"><thead><tr style=background:PaleTurquoise><th>Command character</th><th>Command character</th></tr></thead><tbody><tr><td>0x0001</td><td>Overvoltage abnormality</td></tr><tr><td>0x0002</td><td>Undervoltage abnormality</td></tr><tr><td>0x0004</td><td>Abnormal blocking</td></tr><tr><td>0x0008</td><td>Overheating abnormality</td></tr><tr><td>0x0010</td><td>Abnormal read and write parameters</td></tr><tr><td>0x0020</td><td>Multi-turn count abnormality</td></tr><tr><td>0x0040</td><td>Inverter temperature sensor is abnormal</td></tr><tr><td>0x0080</td><td>communication is abnormal</td></tr><tr><td>0x0100</td><td>communication is abnormal</td></tr><tr><td>0x0200</td><td>Position mode step greater than 1</td></tr><tr><td>0x0400</td><td>DRV protection</td></tr><tr><td>other</td><td>Device exception</td></tr><tr><td>explaination</td><td>Multiple errors can be alarmed at the same time. If the return data is 0X05, the error is 0X01 overvoltage abnormality and 0004 blocked abnormality.</td></tr></tbody></table>


## 7 Appendix D: Command Sending and IQ Value Conversion Method
* The comment section of the manual indicates that the IQ value in the position mode is the actual value, ranging from -128 to 127. 999999940. At this time, only the corresponding position value needs to be converted into an IQ value to be input into the parameter content. In the speed and current mode, the corresponding parameter value needs to be converted before converting the IQ value. If the current speed value is set to 100 RPM, the current value of the setting needs to be divided by the maximum value, ie 100/6000=0.01666666, and then Then, the IQ conversion is performed by 0.016666666, and the obtained value is the parameter value.

* For example, we need to set the current position to 60R (note the limit of the step response in the position mode. If the difference between the set position and the current position exceeds 1R, it will not respond), first find the corresponding command. The third type of write command (write command 3) in Appendix A indicates that the instruction to set the current position value is 0x0A. After finding the instruction, look for the corresponding transmission format of the instruction. In the "CAN Communication Protocol Command Reference", the 3.3.2.3 subsection corresponds to the third type of write instruction, and the transmission data length is 5, that is, one byte instruction + 4 bytes parameter. content. When the data content is applied to the IQ24 format, the IQ conversion is performed directly on 60, that is, 60*2^24=1006632960, and then unified into hexadecimal (according to the test software), 3C 00 00 00. According to the data frame format description of CAN bus, the instruction parameter should be at the highest position, and the content of the parameter is after, the content of the instruction we send is 0x 0A 3C 00 00 00, which also corresponds to the length of the data in the description is 5 (bytes). The instruction is sent to this point.

* Correspondingly, if the current or speed mode settings commands need to be sent,the parameter values need to be convert firstly (divided by the corresponding maximum value), to get a number in the range of -1 to 1, and then perform IQ conversion. The steps and methods for sending commands are the same as the position mode. Note that the data format used by each command, if it's in IQ8 format, convert the 2^24 in the formula to 2^8 and then convert it.

## Appendix F: Version Change Record

**The following table briefly describes the version change record.**

<table style="width:800px"><thead><tr style="background:PaleTurquoise"><th style="width:80px">Version number</th><th style="width:100px">Update time</th><th style="width:100px">Change type</th><th style="width:80px">Position</th><th>Update content</th></tr></thead><tbody><tr><td rowspan="4">V1.0.5</td><td rowspan="4">19.05.14</td><td>add</td><td>Appendix A</td><td>Temperature sensor and inverter temperature sensor read and write commands</td></tr><tr><td>modify</td><td>Chapter II Wiring</td><td>Modify Chapter 2 Wiring Modify Figure 2-3</td></tr><tr><td>modify</td><td>Chapter II Wiring</td><td>Modify Chapter 2 Wiring Modify Figure 2-3</td></tr><tr><td>Delete</td><td>Appendix D</td><td>Delete Appendix D"Model Table"</td></tr><tr><th>V1.0.4</th><th>18.12.14</th><th>add</th><th>Appendix E</th><th>Command transmission and IQ value conversion method</th></tr><tr><td rowspan=4>V1.0.3</td><td rowspan=4>18.03.19</td><td>add</td><td>Chapter III Communication Protocol</td><td>More actuator parameter information instructions, actuator temperature information commands, query last shutdown status command, Homing command than the previous version.</td></tr><tr><td>add</td><td>Chapter III Communication Protocol</td><td>Added storage parameter instruction</td></tr><tr><td>modify</td><td>Chapter III Communication Protocol</td><td>Revised the layout of the third chapter</td></tr><tr><td>add</td><td>Chapter III Communication Protocol</td><td>Added storage parameter instruction</td></tr><tr><td rowspan=2>V1.0.2</td><td  rowspan=2>18.01.30</td><td>modify</td><td>all content</td><td>Micro servo changed its name to INNFOS actuator</td></tr><tr><td>add</td><td>Chapter III Communication Protocol</td><td>More alarm commands than the previous version</td></tr><tr><td>V1.0.1</td><td>17.12.29</td><td>modify</td><td>Chapter III Communication Protocol</td><td>More alarm commands than the previous version</td></tr><tr><td  rowspan=2>V1.0.0</td><td  rowspan=2>17.12.15</td><td>modify</td><td>Chapter II wiring</td><td>Updated CAN interface definition</td></tr><tr><td>add</td><td>Chapter III Communication Protocol</td><td>Added switch command</td></tr></tbody></table>

