Communication method based on CAN bus
=====

*    The INNFOS SCA can communicate directly with the CAN interface of the embedded control board.
*   INNFOS SCA can be controlled by connecting your own embedded control board
*    Two common connection examples for embedded development boards are provided as follows.

## Hardware requirements and connections

### Connection based on ST development board


**Hardware requirements**

<img src="../img/01can.jpg" style="width:600px">

*   From left to right: `INNFOS SCA`, `ST development board (self-provided)`, `terminating resistor`, `actuator cable`, `DC stabilized voltage supply`
*   You can use your own ST development board to implement CAN communication and control with the actuator
*   Optional emergency stop switch depending on usage

Note: The components can be plugged in only after power-down, otherwise they may be damaged. <br>Please make sure that your DC power supply voltage is consistent with the actuator voltage range, or may cause an overvoltage or under-voltage error.


**Connect ST development board to SCA integrated cabls**


*   Take the actuator integrated cable

<img src="../img/02can.jpg" style="width:600px"> 

*   Cut one end of the actuator integrated cable.
 

The red thick line is the positive; the black thick one is the negative line. Cut the twisted pair shielded wire, where the red thin line is CAN_H; the black thin one is CAN_L; The silver line is CAN_GND.

<img src="../img/03can.jpg" style="width:600px"> 

*    Connect the red thin line CAN_H and the black thin line CAN_L to the corresponding positions on the ST development board.

<img src="../img/04can.jpg" style="width:600px"> 

*    Connect the red power positive line and the black power negative line to the positive and negative terminals as shown.

<img src="../img/05can.jpg" style="width:600px"> 


**Connecting SCA**

*    Connect the other end of the integrated cable to the actuator.

<img src="../img/06can.jpg" style="width:600px"> 

*    Plug the terminal resistor to the SCA in tail-end

<img src="../img/Actuator-C2.jpg" style="width:600px">

*    After the connection is completed, the power can be turned on for subsequent debugging

<img src="../img/07can.jpg" style="width:600px"> 


### Connection based on Arduino development board

**Hardware requirements**

<img src="../img/08can.jpg" style="width:600px">

*   From left to right: `INNFOS SCA`, `Arduino development board (self-provided)`, `terminating resistor`, `ECB cable`, `actuator  cable`, `DC stabilized power supply`
*   You can use your own Arduino development board to communicate and control CAN with the actuator
*  Optional emergency stop switch depending on usage

Note: The components can only be plugged in after power-down, otherwise they may be damaged.<br> Please make sure that your DC power supply voltage is consistent with the actuator voltage range, or may cause an overvoltage or under-voltage error.


**Connect the Arduino development board to the actuator integrated cable**

*   Take the actuator integrated cable。

<img src="../img/09can.jpg" style="width:600px"> 

*   Cut one end of the actuator integrated cable. 
The red thick line is the positive; the black thick one is the negative line. Cut the twisted pair shielded wire, where the red thin line is CAN_H; the black thin one is CAN_L; The silver line is CAN_GND.

<img src="../img/03can.jpg" style="width:600px"> 

*    Carefully cut the ECB cable and cut the red thin wire CAN_H of the integrated cable, black thin wire CAN_L, the silver thin wire CAN_GND,and then connect the corresponding pins as shown in the figure. Wielding firmly and prevent short circuit by heat shrink tube or insulating tape.

<img src="../img/10can.jpg" style="width:600px"> 

<img src="../img/11can.jpg" style="width:600px">

*    Connect the red power positive line and the black power negative line to the positive and negative terminals as shown.

<img src="../img/05can.jpg" style="width:600px"> 

*     Plug the other end of the ECB cable into the Arduino board to complete the connection.


**Connecting actuator**

*    Connect the other end of the actuator integrated cable to the actuator.

<img src="../img/06can.jpg" style="width:600px"> 

*    End effector plug-in termination resistor

<img src="../img/Actuator-C2.jpg" style="width:600px">

*    After the connection is completed, the power can be turned on for subsequent debugging

<img src="../img/12can.jpg" style="width:600px"> 

## Software installating and using instruction


**Download IAS**

*   If the computer system is linux, please visit [IAS(linux)](https://github.com/innfos/INNFOS-Actuator-Studio-linux.git) to get the latest version of IAS(INNFOS Actuator Studio)(Linux),If the system is window, please visit [IAS(windows)](https://github.com/innfos/INNFOS-Actuator-Studio-windows.git).

**Configure IP address**

*   For configuration steps, please refer to [Ethernet communication configuration](Ethernet_Configuration.md)

**Install IAS**

*   Install IAS, please refer to [IAS installation](INNFOS_Actuator_Studio_IAS_instruction.md)

**Usage** 

<img src="../img/2-2.png" style="width:600px"> 

After successful installation, start IAS, click the "OK" button to enable the "Next" button, and then click "Next" until the following interface appears:

<img src="../img/2-6.png" style="width:600px"> 

Click the "1" or "2" button to start the actuator, and the button "1" is green meaning successful starting up. Click on the message box or click on the "Details" button (located under button "1") to enter the actuator debug interface.


<img src="../img/2-9.png" style="width:600px"> 


 **Position control**

*   Click the `Profile Position Mode`button on the left sidebar and then click`Activate Profile Position Mode`.Then enter the position value in "Settings" in units of R (range -127R~127R).

<img src="../img/Fig6-1.png" style="width:600px"> 

<img src="../img/Fig6-3.png" style="width:600px"> 


For more information on IAS, please visit the[INNFOS Actuator Studio(IAS)instructions](#!pages/INNFOS_Actuator_Studio_IAS_instruction.md).

# Version Information
<table class="tableizer-table"><thead><tr class="tableizer-firstrow" style="background: PaleTurquoise; color: black;width:500px"><th >version</td><td>date</td><td>Modify content</td></tr>
 <tr><td>V1.0.0</td><td>2019-05</td><td>The first version</td></tr>
</tbody></table>
