Ethernet Communication Protocol
=======


## Introduction

*   Ethernet is currently the most widely used LAN technology because of its simplicity, low cost, strong scalability and good integration with IP networks.
*   INNFOS products are designed on the basis of UDP protocol. This article details the Ethernet communication protocol format and the product Ethernet communication structure.


## Actuator connection

![connect.png](../img/connect2.png "连接拓扑图")

Connect the device as shown above and turn it on again.

Warning: Do not plug or unplug cables with electrified operation, otherwise the device may be damaged.


## Communication

This protocol is divided into physical layer, data link layer and user layer.

*   physical layer

The electrical interface standard is Ethernet, IEEE 802.3-2002 standard, 100M full duplex communication.

*   Data link layer

The data link layer specifies the specific format of the data frame. The upper and lower computer use the same data format in which the data is represented by a 16-bit number.


*   User layer

The user layer defines the command interface for the slave to communicate with the host.

## Communication protocol

### Communication protocol format

<table class="tableizer-table">
<thead><tr class="tableizer-firstrow"><th>Frame header</th><th>Device address</th><th>command byte</th><th>Number of data bits</th><th>Data content</th><th>CRC codecheck</th><th>End of frame</th></tr></thead><tbody>
 <tr><td>1 byte</td><td>1 byte</td><td>1 byte</td><td>2 byte</td><td>N byte</td><td>2 byte</td><td>1 byte</td></tr></tbody></table>

**Frame header**

* Fixed byte `0xEE`, which identifies the beginning of a transmission frame.

**Device address**

* One byte identifies the address of the device to communicate with, `0x01` to 0xff are available. `0x00` is the broadcast address.

**command byte**

* One byte identifies the address of the device to communicate with, `0x01` to `0xFF` are available. `0x00` is the broadcast address.

**Number of data bits**

* Two bytes identify the number of specific data to be communicated, ranging from `0x0000` to `0xFFFF`, and the out of range is not processed.

**Data content**

* The specific data content of an instruction is the same length as the previous data digits. Some instructions do not contain specific data and should have a data digit of zero.

**CRC codecheck**

* Two bytes identify the CRC16 check result of the data content in the communication. If there is no data in the command, there is no CRC check digit. For the CRC calculation method, please refer to the CRC check code calculation method.

**End of frame**

* Fixed byte `0XED`, identifying the end of a transmission frame.

### **Ethernet communication protocol command application examples**

#### Protocol example

**Example 1. Read command**

<table><tr><th colspan="6">Read the current speed value with actuator ID 1</th></tr><tr><td >Frame header</td><td >Device address</td><td >command byte</td><td >Data length (2 bytes）</td><td >Parameter </td><td >End of frame</td></tr><tr><td >0xEE</td><td >0x01</td><td >0x5</td><td >0x00 0x00</td><td >none</td><td >0xED</td></tr></table>

Frame header: `0xEE` = Protocol header

Device address: `0x01` = Read ID 

Command character: `0x05` = Read current speed command 

Data length: `0x00 0x00` = Data length 

Parameter content: None = Sent parameter

End of frame: `0xED` = Protocol Tail 

Send content: `0x05`


<table class="tableizer-table">
<tbody><tr><td  colspan="7"style=background:PaleTurquoise>Answer command</td></tr><tr><td>Frame header</td><td>Device address</td><td>command byte</td><td>Data length (2 bytes)</td><td>Parameter</td><td>CRC codecheck</td><td>End of frame</td></tr><tr><td>0xEE</td><td>0x01</td><td>0x5</td><td>0x00 0x04</td><td>Data length (4 bytes)</td><td>Data length (2 bytes)</td><td>0xED</td></tr></tbody></table>

Frame header: `0xEE` = Protocol header 

Device address: `0x01` = Read object ID 

Command character: `0x05` = Current speed command read

Data length: `0x04` = Data length 

Parameter content: Four-byte speed data = Transmitted parameter 

Check Bit: Two bytes of data = check digit 

End of frame: `0xED` = Protocol tail

Response content: `0x05 0xXX 0xXX 0xXX 0xXX` 

Description: The high parameter data [0~3] is put in front followed by lower data in _IQ24 format. _IQ(-1.0)~_IQ(1.0) represents the reverse speed full scale and forward speed full scale. The full scale is 6000RPM. If data = _IQ (0.5),then it is 0.5*6000=3000RPM.

**Example 2. Write command**

<table class="tableizer-table">
<thead ><tr class="tableizer-firstrow"><th  colspan="7" style=background:PaleTurquoise>Set the ratio P of the current loop with actuator ID 1 (set value is 5）</th></tr></thead><tbody><tr><th>Frame header</th><th>Device address</th><th>command byte</th><th>Data length</th><th>parameter</th><th>CRC codecheck</th><th>End of frame</th></tr><tr><td>0xEE</td><td>0x01</td><td>0x0E</td><td>0x4</td><td>0x05 0x00 0x00 0x00</td><td>2 bytes</td><td>0xED</td></tr></tbody></table>

Frame header: `0xEE` = Protocol header 

Device address: `0x01` = Set object ID 

Data length: `0x04` = Data length

Command character: `0x0E` = Position set 

Parameter content: `0x05 0x00 0x00 0x00` = Sent parameter 

Check bit: Two bytes of data = Check digit

End of frame: `0xED` = End of protocol

Send content: `0x0E 0x05 0x00 0x00 0x00 `

Description: The high parameter data [0~3] is put in front followed by lower data in _IQ24 format. For the _IQ24 format. _IQ(-128.0)~_IQ(127.999999940) represents the reverse position value full scale and forward position value full scale. If data=_IQ(5.0), the ratio is 5.

<table class="tableizer-table">
<thead><tr class="tableizer-firstrow"><th colspan="7" style=background:PaleTurquoise>Answer command</th></tr></thead><tbody><tr><th>Frame header</th><th>Device address</th><th>command byte</th><th>Data length</th><th>parameter</th><th>End of frame</th></tr><tr><td>0xEE</td><td>0x01</td><td>0x0E</td><td>0x1</td><td>0x01</td><td>0xED</td></tr></tbody></table>

Frame header: `0xEE` = Protocol header 

Return device address: `0x01` = Response object ID 

Data length: `0x01` = Data length of the response 

Command character: `0x0E` = Acknowledgement setting 

Current position instruction (corresponding to transmission) 

Parameter content: `0x01` = Parameter response (0x01 indicates successful write) 

End of frame: `0xED` = end of protocol

Response content: `0x0E 0x01`

## Transmission process

### Communication Configuration

The Ethernet communication uses udp, and the ECB fixes the ip address to 192.168.1.30 (default), which can be modified by the relevant protocol. The PC needs to modify the network configuration. The IP address is changed to 192.168.1.xxx, and the xxx is greater than 100 to avoid conflict with the ECB address. The subnet mask is 255.255.255.0, and the default gateway is 192.168.1.1. After configuration set successfully and the connection is successfully powered, the ECB's ip address can be pinged, which means successful connection. The communication port is 2000 to communicate with the actuator through this port.

### Handshake with ECB

First handshake with the ECB to use Ethernet communication, after the ECB successfully responds, send the query actuator address instruction and return to the actuator address command to start sending command control and adjust the actuator.

Send command: 

`0xEE 0x00 0x44 0x00 0x00 0xED` to ECB

A return command will be received after successful communication: 

`0xEE 0x00 0x44 0x00 0x01 0x01 0xED` 

Send the protocol by broadcast (ie send the protocol to 192.168.1.255) to get ECB IP address and send other commands through the ip address.

### Query actuator

Send command: 
`0xEE 0x00 0x02 0x00 0x00 0xED` 
The ID and mac address information will be sent after successful communication. Since it is necessary to poll and find the actuator, this instruction takes about 0.5s to return the actuator id. If it is not received actuator address information for a long time, it can be considered that no actuator is successfully connected. Return instruction example: 
`0xEE 0x06 0x02 0x00 0x04 0x01 0x64 0x5A 0xDF 0x3B 0x3F 0xED `
`0x06` is actually the actuator ID, `0x01 0x64 0x5A 0xDF` is the actuator mac address. (When multiple actuators are successfully connected, this command will be returned multiple for many times)


### Communicating with the actuator


After successfully querying the actuator, the actuator can communicate with the actuator according to the actuator ID, for example, the command to start the actuator with ID 6 is: `0xEE 0x06 0x2A 0x00 0x01 0x01 0x7E 0x80 0xED`
`0x060x` is the actuator ID and `0x2A` is the command to turn on or turn off the actuator, `0x00 0x01` is the data length, `0x01` is the boot (`0x00` is the shutdown), `0x7E 0x80 `is the CRC check code.

### Control actuator

##### Position control

Send command to activate Ladder Position Mode:
`0xEE 0x06 0x07 0x00 0x01 0x06 0x3F 0x42 0xED`
Data `0x06` is in trapezoidal position mode [see mode table](#!pages/Ethernet_Communication_Protocol.md#Appendix_B:mode_commands "wikilink")，`0x3F 0x42` is [CRC Check code](#!pages/Ethernet_Communication_Protocol.md#CRC_check_code_calculation_method "wikilink")  that will receive a return after successful activation:
`0xEE 0x06 0x07 0x00 0x01 0x01 0xED`
At this point a speed command can be sent:
`0xEE 0x06 0x0A 0x00 0x04 0x00 0x01 0x00 0x00 0x01 0xD8 0xED`
The `0x0A` bit sets the speed value command and the `0x00 0x01 0x00 0x00` bit sets the position value. The value is the set target position 1R. Calculate the IQ24 value obtained by the formula: target position /128*(2^24), IQ24 Please refer to the introduction of [ IQmath for an introduction](#!pages/Ethernet_Communication_Protocol.md#IQmath_Introduction "wikilink")。


Note: the commands for setting the speed current position value are not returned, and other commands are returned. For more communication instructions, please refer to [Ethernet communication protocol command reference](#!pages/Ethernet_Communication_Protocol.md#Ethernet_Communication_Protocol_Command_Reference "wikilink")。

## Ethernet Communication Protocol Command Reference

### Read command
<table class="tableizer-table"><thead><tr class="tableizer-firstrow"></tr></thead><tbody><tr><td  colspan="3" style=background:PaleTurquoise>2.3.1.1 Send data 0 byte, return data 1 byte</td></tr><tr><td style="width:250px">Command Name</td><td colspan="2">Read Command</td></tr><tr><td>description</td><td colspan="2">This command sends a data length of 1, and its return data with the length of 2</td></tr><tr><td>Command byte</td><td colspan="2">See <a href="#!pages/Ethernet_Communication_Protocol.md#Read_instruction_1">read instruction 1</a></td></tr><tr><td>Data length</td><td colspan="2">0</td></tr><tr><td>Data content/td><td colspan="2">No</td></tr><tr><td>Command byte（return value）</td><td colspan="2">See <a href="#!pages/Ethernet_Communication_Protocol.md#Read_instruction_1">read instruction 1</a></td></tr><tr><td>Data length （return value）</td><td colspan="2">1</td></tr><tr><td rowspan="2">Lower machine returns data</td><td>0x01：Success / enable / boot / normal</td><td rowspan="2">Pattern query return data see <a href="#!pages/Ethernet_Communication_Protocol.md#Appendix_B:mode_table">mode table</a></td></tr><tr><td>0x00：Failed / disabled / shut down / abnormal</td></tr></tbody></table>

<table class="tableizer-table">
<thead><tr class="tableizer-firstrow"></tr></thead><tbody><tr><td colspan="3" style=background:PaleTurquoise>2.3.1.2 Send data 0 byte, return data 2 bytes</td></tr><tr><td style="width:250px">Command name</td><td colspan="2">Read command</td></tr><tr><td>Description</td><td  colspan="2">This command sends a data length of 1, and its return data with the length of 3. the parameter in high position shows first. The value is 2^8 times the true value（special instructions are specified in the instruction list）</td></tr><tr><td>Command character</td><td  colspan="2">See <a href="#!pages/Ethernet_Communication_Protocol.md#Read_instruction_2">read instruction 2</a></td></tr><tr><td>Data length</td><td  colspan="2">0</td></tr> <tr><td>Data content</td><td  colspan="2">None</td></tr><tr><td>Command character (return value)</td><td  colspan="2"><a href="#!pages/Ethernet_Communication_Protocol.md#Read_instruction_2">read instruction 2</a></td></tr><tr><td>Data length (return value)</td><td  colspan="2">2</td></tr><tr><td>Lower machine returns data</td><td>The data is in iq8 format</td><td>Or see<a href="#!pages/Ethernet_Communication_Protocol.md#Appendix_C:the_error_warning_instruction_list"> the error warning instruction list</a></td></tr></tbody></table>

<table class="tableizer-table">
<thead><tr class="tableizer-firstrow"></tr></thead><tbody><tr><td  colspan="2" style=background:PaleTurquoise>2.3.1.3 Send data 0 byte, return data 4 bytes</td></tr><tr><td style="width:250px">Command name</td><td>Read command</td></tr><tr><td>Description</td><td>This command sends a data length of 1, and its return data with the length of 5. the parameter in high position shows first. The value is 2^24 times the true value（special instructions are specified in the instruction list）</td></tr><tr><td>Command character</td><td>See <a href="#!pages/Ethernet_Communication_Protocol.md#Read_instruction_3">read instruction 3</a></td></tr><tr><td>data length</td><td>0</td></tr><tr><td>Data content</td><td>none</td></tr><tr><td>Command character (return value)</td><td>See <a href="#!pages/Ethernet_Communication_Protocol.md#Read_instruction_3">read instruction 3</a></td></tr><tr><td>Data length (return value)</td><td>4</td></tr> <tr><td>Lower machine returns data</td><td>Data is formed as iq24(special instructions are specified in the instruction list）</td></tr></tbody></table>

### Write command

<table class="tableizer-table">
<thead><tr class="tableizer-firstrow"></tr></thead><tbody><tr><td colspan="3"style=background:PaleTurquoise>2.3.2.1 Send data 1 byte, return data 1 byte</td></tr><tr><td style="width:250px">Command name</td><td colspan="2">Write command</td></tr><tr><td>Description</td><td colspan="2">This command class sends a data length of 2, a return data length is 2, and a byte after the data is sent indicates that the parameter content is to be written. (note: a power-on command should be sent to use and a power-off command should be sent before powering off, otherwise the zero position may be lost.)</td></tr><tr><td>Command character</td><td colspan="2">See <a href="#!pages/Ethernet_Communication_Protocol.md#Write_instruction_1">write instruction 1</a></td></tr><tr><td>Data length</td><td colspan="2">1</td></tr><tr><td rowspan="2">Data content</td><td>0x01：enable/ power on</td><td rowspan="2">The mode setting is <a href="#!pages/Ethernet_Communication_Protocol.md#Appendix_B:mode_table">mode table</a></td></tr><tr><td>0x00：disable/power off</td></tr><tr><td>Data length (return value)</td><td colspan="2"><a href="#!pages/Ethernet_Communication_Protocol.md#Write_instruction_1">write instruction 1</a></td></tr><tr><td>Data length (return value)</td><td colspan="2">1</td></tr><tr><td rowspan="2">Lower machine returns data</td><td colspan="2">0x01：Success</td></tr><tr><td colspan="2">0x00：Failed</td></tr></tbody></table>

<table class="tableizer-table">
<thead><tr class="tableizer-firstrow"></tr></thead><tbody><tr><td colspan="2"style=background:PaleTurquoise>Send data 2 byte, return data 1 byte</td></tr><tr><td style="width:250px">Command name</td><td>Write command</td></tr><tr><td>Description</td><td>The data length of this command is 3 bytes, the return data length is 2 bytes, and the sent data 2 bytes at last indicate that the parameter content is to be written, and the high parameter shows in front. The value is 2^8 times the true value.</td></tr><tr><td>Command character</td><td>See <a href="#!pages/Ethernet_Communication_Protocol.md#Instruction_2">instruction 2</a></td></tr><tr><td>Data length</td><td>2</td></tr><tr><td rowspan="2">Data content</td><td>The value is formed IQ8</td></tr><tr><td>0x00：Disable/power off</td></tr><tr><td>Instruction (return value)</td><td>See <a href="#!pages/Ethernet_Communication_Protocol.md#Write_command_2">write command 2</a></td></tr><tr><td>Data length (return value)</td><td>1</td></tr><tr><td rowspan="2">IAS return data</td><td>0x01：Success</td></tr><tr><td>0x00：Fail</td></tr></tbody></table>

<table class="tableizer-table">
<thead><tr class="tableizer-firstrow"><th  colspan="3"style=background:PaleTurquoise>2.3.2.3 Send data 4 byte, return data is 1 byte or less</th></tr></thead><tbody> <tr><td style="width:250px">Command name</td><td colspan="2">Write command</td></tr><tr><td>Description</td><td  colspan="2">The data length of this command is 5 bytes, the return data length is 2 2 bytes, and the sent data 4 bytes at last indicate that the parameter content is to be written. The value is 2^24 times the true value. (Special instructions are specified in the instruction list)</td></tr><tr><td>Command byte</td><td  colspan="2">See <a href="#!pages/Ethernet_Communication_Protocol.md#Write_command_3">write command 3</a></td></tr><tr><td>Data content</td><td  colspan="2">4</td></tr><tr><td>Data content</td><td  colspan="2">The value is formed IQ24 (Special instructions are specified in the instruction list)</td></tr><tr><td>Instruction (return value)</td><td  colspan="2">See <a href="#!pages/Ethernet_Communication_Protocol.md#Write_command_3">write command 3</a></td></tr><tr><td>Data length (return value)</td><td  colspan="2">1Or0</td></tr><tr><td  rowspan="2">Lower machine returns data</td><td>0x01：Success</td><td  rowspan="2">(There are no return data for the three special instructions, which are marked in the instruction list)</td></tr><tr><td  colspan="1">0x00：Fail</td></tr></tbody></table>

<table class="tableizer-table">
<thead><tr class="tableizer-firstrow"><th colspan="2"style=background:PaleTurquoise>2.3.2.4 Send data 0 byte, return data is 1 byte</th></tr></thead><tbody><tr><td style="width:250px">Command name</td><td>Write command</td></tr><tr><td>Description</td><td>This command class sends a data length of 1, and returns a data length of 2</td></tr><tr><td>Command byte</td><td>See <a href="#!pages/Ethernet_Communication_Protocol.md#Write_command_4">write command 4</a></td></tr><tr><td>Data length</td><td>0</td></tr><tr><td>Data content</td><td>None</td></tr><tr><td>Command (return value)</td><td>See <a href="#!pages/Ethernet_Communication_Protocol.md#Write_command_4">write command 4</a></td></tr><tr><td>Data length(return value)</td><td>1</td></tr><tr><td rowspan="2">Lower machine returns data</td><td>0x01：success</td></tr><tr><td>0x00：fail</td></tr></tbody></table>

## Appendix A

#### </span>IQmath Introduction

*   The processor we use generally supports hardware floating-point operations directly, such as some devices with FPU, or only supports fixed-point operations. In this case, the processing of floating-point numbers needs to be done by the compiler. On devices that support hardware floating-point processing, the quickest way to program floating-point operations is to use floating-point types directly, such as single-precision floats. However, in many cases we can only use one fixed-point processor because the limitation of cost, material and other factors. That directly using the float type for floating-point operations will make the compiler generate a lot of code to complete the operation that looks very simple, which causes longer execution time, and occupies multiplied resources. This involves the problem of how to efficiently handle floating-point operations on fixed-point processors.


*   Since it is a fixed-point processor, its efficiency in processing fixed-point numbers, or literally "integers", is much higher than it is in dealing with floating-point types. On fixed-point processors, we use fixed-point integers to represent a floating-point number, and specify integer digits and scales to easily convert fixed-point and floating-point numbers. Taking a 32-bit fixed-point number as an example, suppose the conversion factor is Q, that is, the number of decimal places in 32 bits is Q, and the number of integer digits is 31-Q (in the case of signed numbers), then fixed-point numbers and floating-point numbers Conversion relationship is


![see IQ-MATH Library file](../img/3-1通信协议.png "详见 IQ-MATH Library文档") 


[IQ-MATH Library file](../img/C28x_IQmath_Library.pdf "详见 IQ-MATH Library文档") 

*    Fixed point number = floating point number × 2^Q

*   For example, when floating point number -2.0 is converted to a fixed point with Q of 24, the result is: fixed point number = -2 × 2^24 = -33554432

*   The range of 32-bit signed numbers is: -2147483648 to 2147483647. If we convert the maximum value of signed fixed-point numbers 2147483647 to a floating-point number of Q24, the result is: floating point number 2147483647/2^24=127.999999940

<table class="tableizer-table">
<thead><tr class="tableizer-firstrow"></tr></thead><tbody>
 <tr><td rowspan="2"style=background:PaleTurquoise>Data Type</td><td colspan="2"style=background:PaleTurquoise>Range</td><td  rowspan="2"style=background:PaleTurquoise>Resolution/Precision</td></tr> <tr><td>Min</td><td>Max</td></tr><tr><td>_iq30</td><td>-2</td><td>1.999 999 999</td><td>0.000 000 001</td></tr><tr><td>_iq29</td><td>-4</td><td>3.999 999 998</td><td>0.000 000 002</td></tr><tr><td>_iq28</td><td>-8</td><td>7.999 999 996</td><td>0.000 000 004</td></tr><tr><td>_iq27</td><td>-16</td><td>15.999 999 993</td><td>0.000 000 007</td></tr><tr><td>_iq26</td><td>-32</td><td>31.999 999 985</td><td>0.000 000 015</td></tr><tr><td>_iq25</td><td>-64</td><td>63.999 999 970</td><td>0.000 000 030</td></tr> <tr><td>_iq24</td><td>-128</td><td>127.999 999 940</td><td>0.000 000 060</td></tr><tr><td>_iq23</td><td>-256</td><td>255.999 999 981</td><td>0.000 000 119</td></tr><tr><td>_iq22</td><td>-512</td><td>511.999 999 762</td><td>0.000 000 238</td></tr> <tr><td>_iq21</td><td>-1024</td><td>1023.999 999 523</td><td>0.000 000 477</td></tr> <tr><td>_iq20</td><td>-2048</td><td>2047.999 999 046</td><td>0.000 000 954</td></tr> <tr><td>_iq19</td><td>-4096</td><td>4095.999 998 093</td><td>0.000 001 907</td></tr> <tr><td>_iq18</td><td>-8192</td><td>8191.999 996 185</td><td>0.000 003 815</td></tr> <tr><td>_iq17</td><td>-16384</td><td>16383.999 992 371</td><td>0.000 007 629</td></tr> <tr><td>_iq16</td><td>-32768</td><td>32767.999 984 741</td><td>0.000 015 259</td></tr> <tr><td>_iq15</td><td>-65536</td><td>65535.999 969 482</td><td>0.000 030 518</td></tr> <tr><td>_iq14</td><td>-131072</td><td>131071.999 938 965</td><td>0.000 061 035</td></tr> <tr><td>_iq13</td><td>-262144</td><td>262143.999 877 930</td><td>0.000 122 070</td></tr> <tr><td>_iq12</td><td>-524288</td><td>524287.999 755 859</td><td>0.000 244 141</td></tr> <tr><td>_iq11</td><td>-1048576</td><td>1048575.999 511 719</td><td>0.000 488 281</td></tr> <tr><td>_iq10</td><td>-2097152</td><td>2097151.999 023 437</td><td>0.000 976 563</td></tr> <tr><td>_iq9</td><td>-4194304</td><td>4194303.998 046 875</td><td>0.001 953 125</td></tr> <tr><td>_iq8</td><td>-8388608</td><td>8388607.996 093 750</td><td>0.003 906 250</td></tr> <tr><td>_iq7</td><td>-16777216</td><td>16777215.992 187 500</td><td>0.007 812 500</td></tr> <tr><td>_iq6</td><td>-33554432</td><td>33554431.984 375 000</td><td>0.015 625 000</td></tr> <tr><td>_iq5</td><td>-67108864</td><td>67108863.968 750 000</td><td>0.031 250 000</td></tr> <tr><td>_iq4</td><td>-134217728</td><td>134217727.937 500 000</td><td>0.062 500 000</td></tr> <tr><td>_iq3</td><td>-268435456</td><td>268435455.875 000 000</td><td>0.125 000 000</td></tr> <tr><td>_iq2</td><td>-536870912</td><td>536870911.750 000 000</td><td>0.250 000 000</td></tr> <tr><td>_iq1</td><td>-1073741824</td><td>1 073741823.500 000 000</td><td>0.500 000 000</td></tr></tbody></table>


![3-2通信协议-1.png](../img/3-2通信协议-1.png "3-2通信协议-1.png")

*   Notes:
*   The maximum amplitude (Maximum) set by PC is _IQ (1.0), and the minimum amplitude (Minimal) is _IQ (-1.0), which acts as a limiting function (the schematic diagram is shown in Figure 3-2). Example: (Figure: 3-2 uses the output of position loop through the limiter module as the input of the speed loop. Assuming _IQ(0.5), _IQ(-0.5), the maximum speed of the position loop output should be ±0.5x6000=±3000RPM )

*   The upper limit of the proportional integral setting is _IQ (128.0), and the lower limit is _IQ (-128.0), but the set value is adjusted according to the actual operation (schematic diagram: 3-2)
*   The current loop sets the current value range from _IQ(-1.0)~_IQ(1.0). The actual current value is the IQ value multiplied by the full scale. Example: (QDD-6010 model actuator full-scale current value is 33A, _IQ (0.5) The actual current value is 0.5x33a=16.5A, see Appendix D: Model Table)
*   The speed loop sets the speed value range from _IQ(-1.0)~_IQ(1.0), and the actual speed value is the IQ value multiplied by the full scale (see ). Example: (_IQ (0.5) the actual speed is 0.5 * 6000 = 3000RPM)
*   Since the position loop is in _IQ24 format, the forward full scale is _IQ (127.999999940), the reverse full scale is _IQ (-128.0), and the IQ value is the actual value. For example: (_IQ(60.0) is the actual position. 60R, that is, the position where the zero position is rotated forward by 60 turns.)
*   Acceleration, deceleration can be set in the speed loop curve mode and position loop curve mode and relatively smoothly reach the preset speed value and position, which can avoid trigger actuator over-current protection or power supply overcurrent protection while meeting the excessive current during operation.

### CRC check code calculation method

The CRC check only calculates the data content, all the contents between the data byte and CRC check. The calculation method is as following.

CRC check code calculation method (c++):


    const uint8_t chCRCHTalbe[] =                                 // CRC High byte value table
    {
        0x00, 0xC1, 0x81, 0x40, 0x01, 0xC0, 0x80, 0x41, 0x01, 0xC0, 0x80, 0x41,
        0x00, 0xC1, 0x81, 0x40, 0x01, 0xC0, 0x80, 0x41, 0x00, 0xC1, 0x81, 0x40,
        0x00, 0xC1, 0x81, 0x40, 0x01, 0xC0, 0x80, 0x41, 0x01, 0xC0, 0x80, 0x41,
        0x00, 0xC1, 0x81, 0x40, 0x00, 0xC1, 0x81, 0x40, 0x01, 0xC0, 0x80, 0x41,
        0x00, 0xC1, 0x81, 0x40, 0x01, 0xC0, 0x80, 0x41, 0x01, 0xC0, 0x80, 0x41,
        0x00, 0xC1, 0x81, 0x40, 0x01, 0xC0, 0x80, 0x41, 0x00, 0xC1, 0x81, 0x40,
        0x00, 0xC1, 0x81, 0x40, 0x01, 0xC0, 0x80, 0x41, 0x00, 0xC1, 0x81, 0x40,
        0x01, 0xC0, 0x80, 0x41, 0x01, 0xC0, 0x80, 0x41, 0x00, 0xC1, 0x81, 0x40,
        0x00, 0xC1, 0x81, 0x40, 0x01, 0xC0, 0x80, 0x41, 0x01, 0xC0, 0x80, 0x41,
        0x00, 0xC1, 0x81, 0x40, 0x01, 0xC0, 0x80, 0x41, 0x00, 0xC1, 0x81, 0x40,
        0x00, 0xC1, 0x81, 0x40, 0x01, 0xC0, 0x80, 0x41, 0x01, 0xC0, 0x80, 0x41,
        0x00, 0xC1, 0x81, 0x40, 0x00, 0xC1, 0x81, 0x40, 0x01, 0xC0, 0x80, 0x41,
        0x00, 0xC1, 0x81, 0x40, 0x01, 0xC0, 0x80, 0x41, 0x01, 0xC0, 0x80, 0x41,
        0x00, 0xC1, 0x81, 0x40, 0x00, 0xC1, 0x81, 0x40, 0x01, 0xC0, 0x80, 0x41,
        0x01, 0xC0, 0x80, 0x41, 0x00, 0xC1, 0x81, 0x40, 0x01, 0xC0, 0x80, 0x41,
        0x00, 0xC1, 0x81, 0x40, 0x00, 0xC1, 0x81, 0x40, 0x01, 0xC0, 0x80, 0x41,
        0x00, 0xC1, 0x81, 0x40, 0x01, 0xC0, 0x80, 0x41, 0x01, 0xC0, 0x80, 0x41,
        0x00, 0xC1, 0x81, 0x40, 0x01, 0xC0, 0x80, 0x41, 0x00, 0xC1, 0x81, 0x40,
        0x00, 0xC1, 0x81, 0x40, 0x01, 0xC0, 0x80, 0x41, 0x01, 0xC0, 0x80, 0x41,
        0x00, 0xC1, 0x81, 0x40, 0x00, 0xC1, 0x81, 0x40, 0x01, 0xC0, 0x80, 0x41,
        0x00, 0xC1, 0x81, 0x40, 0x01, 0xC0, 0x80, 0x41, 0x01, 0xC0, 0x80, 0x41,
        0x00, 0xC1, 0x81, 0x40
    };
    const uint8_t chCRCLTalbe[] =                                 // CRC low byte value table
    {
        0x00, 0xC0, 0xC1, 0x01, 0xC3, 0x03, 0x02, 0xC2, 0xC6, 0x06, 0x07, 0xC7,
        0x05, 0xC5, 0xC4, 0x04, 0xCC, 0x0C, 0x0D, 0xCD, 0x0F, 0xCF, 0xCE, 0x0E,
        0x0A, 0xCA, 0xCB, 0x0B, 0xC9, 0x09, 0x08, 0xC8, 0xD8, 0x18, 0x19, 0xD9,
        0x1B, 0xDB, 0xDA, 0x1A, 0x1E, 0xDE, 0xDF, 0x1F, 0xDD, 0x1D, 0x1C, 0xDC,
        0x14, 0xD4, 0xD5, 0x15, 0xD7, 0x17, 0x16, 0xD6, 0xD2, 0x12, 0x13, 0xD3,
        0x11, 0xD1, 0xD0, 0x10, 0xF0, 0x30, 0x31, 0xF1, 0x33, 0xF3, 0xF2, 0x32,
        0x36, 0xF6, 0xF7, 0x37, 0xF5, 0x35, 0x34, 0xF4, 0x3C, 0xFC, 0xFD, 0x3D,
        0xFF, 0x3F, 0x3E, 0xFE, 0xFA, 0x3A, 0x3B, 0xFB, 0x39, 0xF9, 0xF8, 0x38,
        0x28, 0xE8, 0xE9, 0x29, 0xEB, 0x2B, 0x2A, 0xEA, 0xEE, 0x2E, 0x2F, 0xEF,
        0x2D, 0xED, 0xEC, 0x2C, 0xE4, 0x24, 0x25, 0xE5, 0x27, 0xE7, 0xE6, 0x26,
        0x22, 0xE2, 0xE3, 0x23, 0xE1, 0x21, 0x20, 0xE0, 0xA0, 0x60, 0x61, 0xA1,
        0x63, 0xA3, 0xA2, 0x62, 0x66, 0xA6, 0xA7, 0x67, 0xA5, 0x65, 0x64, 0xA4,
        0x6C, 0xAC, 0xAD, 0x6D, 0xAF, 0x6F, 0x6E, 0xAE, 0xAA, 0x6A, 0x6B, 0xAB,
        0x69, 0xA9, 0xA8, 0x68, 0x78, 0xB8, 0xB9, 0x79, 0xBB, 0x7B, 0x7A, 0xBA,
        0xBE, 0x7E, 0x7F, 0xBF, 0x7D, 0xBD, 0xBC, 0x7C, 0xB4, 0x74, 0x75, 0xB5,
        0x77, 0xB7, 0xB6, 0x76, 0x72, 0xB2, 0xB3, 0x73, 0xB1, 0x71, 0x70, 0xB0,
        0x50, 0x90, 0x91, 0x51, 0x93, 0x53, 0x52, 0x92, 0x96, 0x56, 0x57, 0x97,
        0x55, 0x95, 0x94, 0x54, 0x9C, 0x5C, 0x5D, 0x9D, 0x5F, 0x9F, 0x9E, 0x5E,
        0x5A, 0x9A, 0x9B, 0x5B, 0x99, 0x59, 0x58, 0x98, 0x88, 0x48, 0x49, 0x89,
        0x4B, 0x8B, 0x8A, 0x4A, 0x4E, 0x8E, 0x8F, 0x4F, 0x8D, 0x4D, 0x4C, 0x8C,
        0x44, 0x84, 0x85, 0x45, 0x87, 0x47, 0x46, 0x86, 0x82, 0x42, 0x43, 0x83,
        0x41, 0x81, 0x80, 0x40
    };
    
    static uint16_t CRC16_1(uint8_t* pchMsg, int16_t wDataLen)
    {
        uint8_t chCRCHi = 0xFF; // High CRC byte initialization
        uint8_t chCRCLo = 0xFF; // Low CRC byte initialization
        int16_t wIndex;            // Index in the CRC loop
        while (wDataLen--)
        {
            // Calculate CRC
            wIndex = chCRCHi ^ *pchMsg++;
            chCRCHi = chCRCLo ^ chCRCHTalbe[wIndex];
            chCRCLo = chCRCLTalbe[wIndex];
        }
        return ((chCRCHi << 8) | chCRCLo);
    }

In the CRC16_1 method, pchmsg points to the address and wdatalen is the byte length of the content to be verified. This method returns a two-byte crc check code to add to the corresponding position in the sent command. After receiving the instruction with the crc check code, the check code can also be calculated by the method and compared with the check code in the return command to verify the validity of the data.

**Example**

?	Actuator boot command:

`0xEE 0x06 0x2A 0x00 0x01 0x01 0x7E 0x80 0xED`

`0xEE` is the frame header, `0x06` is the actuator ID, `0x2A` is the power-on command character, `0x00 0x01` is the data length, `0x01` is the data content, and `0xED` is the frame tail. The data content `0x01` calculated by the above method is `0x7E 0x80`.

### **A.1 Read instruction code definition table**


#### Read command 1
<table class="tableizer-table">
<thead><tr class="tableizer-firstrow"></tr></thead><tbody>
 <tr><td colspan="3"style=background:PaleTurquoise>A.1.1 Read command 1</td></tr> <tr><td>Command byt</td><td>Definition</td><td>Description</td></tr> <tr><td>0x00 ：</td><td>Handshake</td><td>The upper computer sends this command, and the lower computer responds with a return, indicating that the lower computer is ready to communicate with the upper computer. It can also be used as a heartbeat protocol to query the status.</td></tr> <tr><td>0x55：</td><td>Query actuator current mode</td><td>Read the current mode of the actuator managed by the lower computer.</td></tr> <tr><td>0xB0</td><td>Query the last shutdown state of the actuator</td><td>Read the last shutdown state of the actuator, normal / abnormal</td></tr> <tr><td>0x71：</td><td>Current loop filter status</td><td>Read current loop filter enable/disable for the specified ID actuator</td></tr> <tr><td>0x75：</td><td>Speed loop filter status</td><td>Read current loop filter enable/disable for the specified ID actuator</td></tr> <tr><td>0x79：</td><td>Position loop filter status</td><td>Read current loop filter enable/disable for the specified ID actuator</td></tr> <tr><td>0x2B</td><td>Current loop filter status</td><td>Reads the specified ID actuator power on/off status.</td></tr></tbody></table>

#### Read command 2
<table class="tableizer-table">
<thead><tr class="tableizer-firstrow"></tr></thead><tbody>
 <tr><td  colspan="3"style=background:PaleTurquoise>A.1.2 Read command 2</td></tr> <tr><td>Command byte</td><td>Definition</td><td>description</td></tr> <tr><td>0x73：</td><td>Current loop filter bandwidth</td><td>Read current loop filter bandwidth(Hz) of specified ID actuator</td></tr> <tr><td>0x77：</td><td>Speed loop filter bandwidth</td><td>Read Position speed filter bandwidth (Hz) of specified ID actuator</td></tr> <tr><td>0x7B：</td><td>Position loop filter bandwidth</td><td>Read Position loop filter bandwidth of specified ID actuator</td></tr> <tr><td>0x5F</td><td>Read the temperature of specified ID actuator</td><td>Read the temperature℃ of specified ID actuator</td></tr> <tr><td>0x60</td><td>Read inverter temperature</td><td>Read inverter temperature ℃</td></tr> <tr><td>0x62</td><td>Read actuator protection temperature</td><td>Read actuator protection temperature℃ of specified ID actuator</td></tr> <tr><td>0x64</td><td>Read actuator recovery temperature</td><td>Read actuator recovery temperature ℃ of specified ID actuator</td></tr> <tr><td>0xFF</td><td>Alarm command (special command)</td><td>Lower machine alarm information</td></tr></tbody></table>

#### Read command 3
<table class="tableizer-table">
<thead><tr class="tableizer-firstrow"></tr></thead><tbody>
 <tr><td  colspan="3"style=background:PaleTurquoise>A.1.3 Read command 3</td></tr> <tr><td>Command byte</td><td>Definition?
</td><td>Description</td></tr> <tr><td>0x04：</td><td>Current current value</td><td>Read the current value of the specified ID actuator. The current value needs to be multiplied by the current full scale (see Appendix D) with A as the unit.</td></tr> <tr><td>0x05：</td><td>Current speed value</td><td>Read the current speed value of the specified ID actuator. The true speed value needs to be multiplied by the speed full scale (see Appendix D) in RPM.</td></tr> <tr><td>0x06：</td><td>Current position value</td><td>Read the current position value of the specified ID executor in R</td></tr> <tr><td>0x15：</td><td>Current loop P</td><td>Read Current loop P of the specified ID actuator</td></tr> <tr><td>0x16：</td><td> Current loop I</td><td>Read Current loop I of the specified ID actuator</td></tr> <tr><td>0x17：</td><td>Speed loop P</td><td>Read Speed loop P of the specified ID actuator</td></tr> <tr><td>0x18：</td><td>Speed loop I</td><td>Read Speed loop I of the specified ID actuator</td></tr> <tr><td>0x19：</td><td>Position loop P</td><td>Read Speed loop I of the specified ID actuator</td></tr> <tr><td>0x1A：</td><td>Position loop I</td><td>Read Position loop I of the specified ID actuator</td></tr> <tr><td>0x1C：</td><td>Maximum speed of position trapezoidal curve</td><td>Read the maximum speed of position trapezoidal curve of the specified ID actuator</td></tr> <tr><td>0x1D：</td><td>Acceleration of position trapezoidal curve</td><td>Read the  max acceleration of position trapezoidal curve of the specified ID actuator</td></tr> <tr><td>0x1E：</td><td>Deceleration of position trapezoidal curve</td><td>Read the max deceleration of position trapezoidal curve of the specified ID actuator</td></tr> <tr><td>0x22：</td><td>Maximum speed of the speed trapezoidal curve</td><td>Read the maximum speed of the speed trapezoidal curve of the specified ID actuator</td></tr> <tr><td>0x23：</td><td>Acceleration of speed trapezoidal curve</td><td>Read acceleration of speed trapezoidal curve Of the specified ID actuator</td></tr> <tr><td>0x24：</td><td>Deceleration of speed trapezoidal curve</td><td>Read deceleration of speed trapezoidal curve of the specified ID actuator</td></tr> <tr><td>0x34：</td><td>Lower limit of current loop output</td><td>Read lower limit of current loop output of the specified ID actuator</td></tr> <tr><td>0x35：</td><td>Upper limit of current loop output</td><td>Read upper limit of current loop output of the specified ID actuator</td></tr> <tr><td>0x36：</td><td>Lower limit of speed loop output</td><td>Read lower limit of speed loop output of the specified ID actuator</td></tr> <tr><td>0x37：</td><td>Upper limit of speed loop output</td><td>Read upper limit of speed loop output of the specified ID actuator</td></tr> <tr><td>0x38：</td><td>Lower limit of position loop output</td><td>Read lower limit of position loop output of the specified ID actuator</td></tr> <tr><td>0x39：</td><td>Upper limit of position loop output</td><td>Read upper limit of position loop output of the specified ID actuator</td></tr> <tr><td>0x7D：</td><td>Inertia</td><td>Read inertia of the specified ID actuator</td></tr> <tr><td>0x85：</td><td>Upper limit of actuator position</td><td>Read upper limit of actuator position of the specified ID actuator</td></tr> <tr><td>0x86：</td><td>Lower limit of actuator position</td><td>Read lower limit of actuator position of the specified ID actuator</td></tr> <tr><td>0x8A：</td><td>Actuator position offset position</td><td>Read actuator position offset position of the specified ID actuator</td></tr> <tr><td>0x92：</td><td>The lower limit of the current when the actuator is automatically reset to zero</td><td>Read the lower limit of the current when the actuator is automatically reset to zero of the specified ID actuator</td></tr> <tr><td>0x93：</td><td>The upper limit of the current when the actuator is automatically reset to zero</td><td>Read the upper limit of the current when the actuator is automatically reset to zero of the specified ID actuator</td></tr> <tr><td>0x7F：</td><td>Stall energy</td><td>Reads the stall energy of the specified ID actuator. (The value is 75.225 times of the true value) The heating energy after blocking, the unit is J.</td></tr></tbody></table>

### **A.2 Write command code value definition table**

#### Write command 1
<table class="tableizer-table">
<thead><tr class="tableizer-firstrow"><th colspan="3"style=background:PaleTurquoise>A.2.1 Command byte</th></tr></thead><tbody>
 <tr><td>Command byte</td><td>Definition?</td><td>Description</td></tr> <tr><td>0x07：</td><td>Set the mode of the specified ID executor</td><td>Set the current mode of the specified ID actuator</td></tr> <tr><td>0x70：</td><td>Current loop filter status</td><td>Set the current loop filter enable/disable for the specified ID actuator</td></tr> <tr><td>0x74：</td><td>Speed loop filter status
</td><td>Set the speed loop filter enable/disable for the specified ID actuator</td></tr> <tr><td>0x78：</td><td>Position loop filter status</td><td>Set the position loop filter enable/disable for the specified ID actuator</td></tr> <tr><td>0x2A：</td><td>Actuator on/off status</td><td>Set the specified ID actuator to power on/off</td></tr></tbody></table>

#### Write command 2
<table class="tableizer-table">
<thead><tr class="tableizer-firstrow"><th colspan="3"style=background:PaleTurquoise>A.2.2 Write command 2</th></tr></thead><tbody>
 <tr><td>Command byte</td><td>Definition?</td><td>Description</td></tr> <tr><td>0x72：</td><td>Current loop filter bandwidth</td><td>Set the bandwidth (Hz) of the specified ID actuator current loop filter</td></tr> <tr><td>0x76：</td><td>Speed? loop filter bandwidth</td><td>Set the bandwidth (Hz) of the specified ID actuator speed? loop filter</td></tr> <tr><td>0x7A：</td><td>Position loop filter bandwidth</td><td>Set the bandwidth (Hz) of the specified ID actuator position loop filter</td></tr> <tr><td>0x61：</td><td>Current loop filter bandwidth</td><td>Set the bandwidth (Hz) of the specified ID actuator current loop filter</td></tr> <tr><td>0x63：</td><td>Actuator recovery temperature</td><td>Set the recovery temperature of the specified ID actuator °C</td></tr></tbody></table>

#### Write command 3
<table class="tableizer-table">
<thead><tr class="tableizer-firstrow"><th colspan="3"style=background:PaleTurquoise>A.2.3 Write command 3</th></tr></thead><tbody>
 <tr><td>Command byte</td><td>Definition</td><td>Description?</td></tr> <tr><td>0x08：</td><td>Current value</td><td>Sets the current value of the specified ID actuator. (Note: no return data)</td></tr> <tr><td>0x09：</td><td>Current speed value</td><td>Sets the current speed value of the specified ID actuator. (Note: no return data）</td></tr> <tr><td>0x0A：</td><td>Current position value</td><td>Sets the current position value of the specified ID actuator. (Note: no return data)</td></tr> <tr><td>0x0E：</td><td>Current loop P?
</td><td>Change current loop P of the specified ID actuator</td></tr> <tr><td>0x0F：</td><td>Current loop I?</td><td>Change current loop I of the specified ID actuator</td></tr> <tr><td>0x10：</td><td>Speed loop P</td><td>Change speed loop P of the specified ID actuator</td></tr> <tr><td>0x11：</td><td>Speed loop I</td><td>Change speed loop I of the specified ID actuator</td></tr> <tr><td>0x12：</td><td>Position loop P</td><td>Change position loop P of the specified ID actuator</td></tr> <tr><td>0x13：</td><td>Position loop I</td><td>Change position loop I of the specified ID actuator</td></tr> <tr><td>0x1F：</td><td>Maximum speed of position trapezoidal curve</td><td>Change maximum speed of position trapezoidal curve of the specified ID actuator</td></tr> <tr><td>0x20：</td><td>Acceleration of position trapezoidal curve</td><td>Change acceleration of position trapezoidal curve of the specified ID actuator</td></tr> <tr><td>0x21：</td><td>Deceleration speed of position trapezoidal curve</td><td>Change deceleration of position trapezoidal curve of the specified ID actuator</td></tr> <tr><td>0x25：</td><td>Maximum speed of the speed trapezoidal curve</td><td>Change maximum speed of the speed trapezoidal curve of the specified ID actuator</td></tr> <tr><td>0x26：</td><td>Acceleration of velocity trapezoidal curve</td><td>Change acceleration of velocity trapezoidal curve of the specified ID actuator</td></tr> <tr><td>0x27：</td><td>Deceleration of the speed trapezoidal curve</td><td>Change deceleration of velocity trapezoidal curve of the specified ID actuator</td></tr> <tr><td>0x2E：</td><td>Lower limit of current loop output</td><td>Change the lower limit of the specified ID actuator current loop output</td></tr> <tr><td>0x2F：</td><td>Upper limit of current loop output</td><td>Change the upper limit of the specified ID actuator current loop output</td></tr> <tr><td>0x30：</td><td>Lower limit of speed loop output</td><td>Change the lower limit of the specified ID actuator speed loop output</td></tr> <tr><td>0x31：</td><td>Upper limit of speed loop output
</td><td>Change the upper limit of the specified ID actuator speed loop output</td></tr> <tr><td>0x32：</td><td>Lower limit of position loop output</td><td>Change the lower limit of the specified ID actuator position loop output</td></tr> <tr><td>0x33：</td><td>Upper limit of position loop output</td><td>Change the upper limit of the specified ID actuator position loop output</td></tr> <tr><td>0x83：</td><td>Upper limit of actuator position</td><td>Change the upper limit of the position of the specified ID actuator</td></tr> <tr><td>0x84：</td><td>Lower limit of actuator position</td><td>Change the position lower limit of the specified ID actuator</td></tr> <tr><td>0x87：</td><td>Actuator's Home value</td><td>Set the Home value of the specified ID executor</td></tr> <tr><td>0x89：</td><td>Actuator position offset</td><td>Set the position offset value of the specified ID actuator</td></tr> <tr><td>0x90：</td><td>The upper current when the actuator is automatically zeroed</td><td>Set the lower limit of the current when the specified ID actuator is automatically reset to zero.</td></tr> <tr><td>0x91：</td><td>The lower current when the actuator is automatically zeroed</td><td>Set the upper limit of the current when the specified ID actuator is automatically reset to zero.</td></tr> <tr><td>0x7E：</td><td>Stall energy</td><td>Set the stall energy of the specified ID actuator. (The value is 75.225 times the true value) The heating energy after blocking, the unit is J</td></tr></tbody></table>

#### Write command 4
<table class="tableizer-table">
<thead><tr class="tableizer-firstrow"><th   colspan="3"style=background:PaleTurquoise>A.2.4 Write command 4</th></tr></thead><tbody>
 <tr><td>Command byte</td><td>Definition?</td><td>Description</td></tr> <tr><td>0xFE：</td><td>Eliminate the alarm of the lower computer</td><td>Eliminate the alarm action of the lower position machine. After receiving the command, the lower position machine stops the alarm, otherwise the lower position machine is inoperable.</td></tr> <tr><td>0x88</td><td>Clear Homing data</td><td>Clear Homing data</td></tr> <tr><td>0x0D</td><td>Storage parameter</td><td>Store parameters to EEPROM</td></tr></tbody></table>

## Appendix B:mode commands

<table class="tableizer-table">
<thead><tr class="tableizer-firstrow"><th style=background:PaleTurquoise>Command byte</th><th style=background:PaleTurquoise>Command byte</th></tr></thead><tbody>
 <tr><td>01</td><td>Current mode</td></tr> <tr><td>02</td><td>Speed mode</td></tr> <tr><td>03</td><td>Position mode</td></tr> <tr><td>04</td><td>Teaching mode</td></tr> <tr><td>05</td><td>Playback mode</td></tr> <tr><td>06</td><td>Trapezoidal position mode</td></tr> <tr><td>07</td><td>Trapezoidal speed mode</td></tr> <tr><td>08</td><td>Homing mode</td></tr></tbody></table>

## Appendix C: error warning commands


<table class="tableizer-table">
<thead><tr class="tableizer-firstrow"><th style=background:PaleTurquoise>command</th><th style=background:PaleTurquoise>Command</th></tr></thead><tbody>
 <tr><td>0x0001</td><td>Over voltage error</td></tr> <tr><td>0x0002</td><td>Under-voltage error</td></tr> <tr><td>0x0004</td><td>Locked rotor error</td></tr> <tr><td>0x0008</td><td>Overheating error</td></tr> <tr><td>0x0010</td><td>Parameter reading error</td></tr> <tr><td>0x0020</td><td>Multiturn counting error</td></tr> <tr><td>0x0040</td><td>Some errors with inverter temperature sensor </td></tr> <tr><td>0x0080</td><td>CAN communication error</td></tr> <tr><td>0x0100</td><td>Some errors with motor temperature sensor</td></tr> <tr><td>0x0200</td><td>Step of position mode is over 1</td></tr> <tr><td>0x0400</td><td>DRV protection</td></tr> <tr><td>other</td><td>error with equipment</td></tr> <tr><td>explanation</td><td>Many errors can be reported at the same time. If the return data is 0005, then the error will be reported as 0001 
Overvoltage abnormality and 0004 locked rotor error.</td></tr></tbody></table>

## Appendix D: Version Table

<table class="tableizer-table">
<thead><tr class="tableizer-firstrow"><th style=background:PaleTurquoise>SCA Models</th><th style=background:PaleTurquoise>Current full measuring ranges</th><th style=background:PaleTurquoise>Motor full speed measuring ranges</th><th style=background:PaleTurquoise>Output in full speed measuring ranges</th></tr></thead><tbody>
 <tr><td>QDD Pro-8108-50</td><td>33A</td><td>1500RPM</td><td>30RPM</td></tr> <tr><td>QDD-8108-6</td><td>33A</td><td>1500RPM</td><td>250RPM</td></tr> <tr><td>DD-8108</td><td>33A</td><td>1500RPM</td><td>1500RPM</td></tr> <tr><td>QDD Pro-6010-50</td><td>33A</td><td>4200RPM</td><td>84RPM</td></tr> <tr><td>QDD-6010-36</td><td>33A</td><td>4200RPM</td><td>117RPM</td></tr> <tr><td>DD-6010</td><td>33A</td><td>4200RPM</td><td>4200RPM</td></tr> <tr><td>QDD Pro-3510-50</td><td>16.5A</td><td>6000RPM</td><td>120RPM</td></tr> <tr><td>QDD-3510-6</td><td>16.5A</td><td>6000RPM</td><td>1000RPM</td></tr> <tr><td>QDD-3510-36</td><td>16.5A</td><td>6000RPM</td><td>166.7RPM</td></tr> <tr><td>DD-3510</td><td>16.5A</td><td>6000RPM</td><td>6000RPM</td></tr> <tr><td>QDD-2305-6</td><td>16.5A</td><td>6000RPM</td><td>1000RPM</td></tr> <tr><td>QDD-2305-36</td><td>16.5A</td><td>6000RPM</td><td>166.7RPM</td></tr> <tr><td>DD-2305</td><td>16.5A</td><td>6000RPM</td><td>6000RPM</td></tr></tbody></table>

*   Output is in different speed because some model of SCA has reducer inside to lower the maximum speed of output and make the torque improve. Motor full speed measuring ranges counts in IQ values

##  Version change records


Version changes recorded as below:


<table class="tableizer-table">
<thead><tr class="tableizer-firstrow"><th style=background:PaleTurquoise>Version</th><th style=background:PaleTurquoise>Update time</th><th style=background:PaleTurquoise>Changed type</th></tr></thead><tbody>
 <tr><td>V1.0.0</td><td>18.04.28</td><td>position</td></tr></tbody></table>
