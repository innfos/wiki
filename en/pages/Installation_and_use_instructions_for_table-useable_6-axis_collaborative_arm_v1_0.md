Installation and use instructions for table-useable 6-axis collaborative arm
=====

## Introduction

*   The instruction is for the use of table-useable 6-axis collaborative arm
*   Please read the instruction carefully before use. 

<br>All the joints of the collaborative arm are built by INNFOS QDD Lite series actuators. Its arm length is up to 430mm and the load is 500g. QDD Lite series actuators are made of composite materials, greatly reducing research and development cost of high-end robots. The collaborative arm is mainly used in education, schools, laboratories, research institutes, competitions, etc.
                                                                
<img src="../img/桌面级6轴机械臂（QDD Lite-NE30-36版）_v1_0.png" style="width:720px">                                                                          

## Engineering parameters diagram
<br>[单位：毫米]

<img src="../img/桌面级6轴机械臂（QDD Lite-NE30-36版）_v1_0.md三视图.png" style="width:720px">


### 3D model
[model file]( ../img/桌面级6轴机械臂（QDD Lite-NE30-36版）_v1_0.step.zip )


## Basic parameters

<table style="width:500px"><thead><tr><th colspan="2" style="background: PaleTurquoise; color: black;">Parameters of collaborative arm with 6 NE30 LITE SCAs</th></tr></thead><tbody></tr><tr><td>load</td><td>500g</td></tr>
<tr><td>Self weight</td><td>3.7kg(with working platform）；2.5kg（without working platform）</td></tr><tr><td>DOF</td><td>6</td></tr><tr><td>Working radius</td><td>421mm</td></tr><tr><td>Joint range</td><td>+/-170°</td></tr><tr><td>Maximum speed</td><td>2m/s</td></tr><tr><td>Repeated positioning precison</td><td>+/-0.1mm</td></tr><tr><td>voltage</td><td>42v</td></tr><tr><td>Power dissipation</td><td>Generally about120w</td></tr><tr><td>material</td><td>Aluminum alloy/carbon fiber tube</td></tr><tr><td>Working temperature</td><td>10-50°</td></tr><tr><td>Working environment humidity</td><td>5%~95%</td></tr><tr><td>Level of protection</td><td>IP54</td></tr><tr><td>Communication port</td><td>CAN/Ethernet</td></tr><tr><td>demonstrator</td><td>PC/MT</td></tr></td></tbody></table>


## Product photograph

<img src="../img/Robot_DOF6/13.jpg" style="width:600px">

## Hardware requirements and connections

**Hardware requirements**

<img src="../img/12.png" style="width:600px">

From front to back, from left to right: HUB, ECB, ECB cable, one terminal resistance, net cable, collaborative arm, regenerative braking capacitor, emergency stop switch + power supply.

**Connect ECB**

**Connect power supply**

*  Connect power supply and `ECB+HUB`

<img src="../img/cdy.jpg" style="width:600px">
<img src="../img/cwdy.jpg" style="width:600px">

** Connecting actuators and the accessories**

*  Connect `INNFOA SCA cable`

<img src="../img/cx.jpg" style="width:600px">
<img src="../img/cwx.jpg" style="width:600px">

**Connect the collaborative arm**

*   Connect `HUB` and actuator with SCA cable

<img src="../img/5.png" style="width:600px">

**•	Connect computer**

*   Connect`ECB`to computer with net cable

<img src="../img/7.png" style="width:600px">

**Overall view after successful connection**

<img src="../img/12.png" style="width:600px">


**Turn on the power**

*   Turn on the power, and the actuator's supply voltage range is DC 24V-45V.

<img src="../img/poweron.png" style="width:600px">

*   With power on, the actuator LED status light will flash yellow. When the actuator is activated, the LED will flash green and communication with the actuator can be realized . If an error occurs inside the actuator, the LED will flash red, and please check the actuator error code.


## Software installation and usage


**  Use of IAS software**

* `IAS`(INNFOS Actuator Studio)is an upper computer  software for configuring the collaborative arm. Please visit[INNFOS Actuator Studio(IAS)instructions](#!pages/INNFOS_Actuator_Studio_IAS_instruction.md).

**Use of motor function**

* Demonstrating- reproduction function


### Downloading and installation

运行环境：linux-x86-64

访问该链接[download link](https://github.com/innfos/robot_controller-6-NE30-.git)下载机械臂软件或者直接执行以下命令
```sh
$ git clone https://github.com/innfos/robot_controller-6-NE30-.git
```
访问该链接[download link](https://github.com/innfos/ActuatorController_SDK.git)下载SDK相关文件或者直接执行以下命令
```sh
$ git clone https://github.com/innfos/ActuatorController_SDK.git
```

Note: The two folders need to be placed in a same directory.

### Operating mode
The collaborative arm provides the following operations mode0,mode1,mode2,mode3,mode4

Enter the home directory
```sh
$ cd robot_controller-6-NE30-/
```
Configure environment variables：
```sh
$ . environment
```
Note: 每次打开终端都需执行此命令，如不执行,终端会提示找不到动态库“libActuatorController.so”

<br>可执行文件为robotserver
<br>根据运行模式在终端输入： 
```sh
$ ./robotserver xx
```
"xx" represents mode0, mode1, mode2, mode3, mode4 ;

若执行时提示没有“robotserver”文件，表明该文件没有权限，执行以下命令更改权限：
```sh
$ chmod +x robotserver
```

<br>其中file文件夹用于存储路径文件

* mode0
•	The function of this mode is to disable the collaborative arm.

<br>Execute the command
```sh
$ ./robotserver mode0
```
Note: The command needs to be executed before turning off the power of the collaborative arm .

* mode1
The function of this mode is to continuously record tracks
<br>Execute the command 
```sh
$ ./robotserver mode1
```
At this time , the terminal will show：

<img src="../img/桌面级6轴机械臂（QDD Lite-NE30-36版）_v1_0_10.png" style="width:600px">

<br> Enter "start" to start recording.
<br>The recording can be ended with CTRL + C  , at which point the trace file is stored in file/trajectory.txt.


* mode2
Reproduce the track file file/trajectory.txt generated by "mode1"
This mode will run circularly.
<br>Execute the command 
```sh
$ ./robotserver mode2
```
At this time , the terminal will show：

<img src="../img/桌面级6轴机械臂（QDD Lite-NE30-36版）_v1_0_20.png" style="width:600px">

<br>The value is the reproduction speed ratio, which ranges from 0.1 to 1, that is, 10% to 100%. After entering the correct value, press Enter to proceed to the next step. It is recommended that use a low reproduction speed ratio for the first operation , and after confirming that the path is correct, a higher reproduction speed ratio can be used.

The circular operation can be ended with CTRL + C , then the terminal will remind：

<img src="../img/桌面级6轴机械臂（QDD Lite-NE30-36版）_v1_0_21.png" style="width:600px">

<br>Entering "end" will make the collaborative arm enter the current mode. Hold the arm with your hand please.

* mode3
The path point can be recorded step by step in this mode and stored in the file file/data.txt.
<br>Execute the command
```sh
$ ./robotserver mode3
```
At this time the terminal will remind：

<img src="../img/桌面级6轴机械臂（QDD Lite-NE30-36版）_v1_0_30.png" style="width:600px">

<br>This option belongs to selection and interpolation type. You can choose to input “MOVJ”, “MOVL”, “MOVC”, and enter other values to exit the program.

MOVJ:
Joint interpolation. The end motion trajectory is uncertain, only planning in the joint space, terminally input "MOVJ"


MOVL:
Linear interpolation. The end motion track is a straight line, and terminally input "MOVL"


MOVC:
Circular interpolation. The end motion track is an arc. Circular interpolation needs to record two points, one being auxiliary point, input “MOVC” and record the auxiliary point. The terminal remind is as follows. Enter “YES” to record the end point of the arc at this time .Enter others to exit the program.

<img src="../img/桌面级6轴机械臂（QDD Lite-NE30-36版）_v1_0_31.png" style="width:600px">


* mode4
•	Reproduce and operate according to the path file file/data.txt generated by the mode "mode3".
<br>Execute the command
```sh
$ ./robotserver mode4
```
At this time the terminal will show：

<img src="../img/桌面级6轴机械臂（QDD Lite-NE30-36版）_v1_0_40.png" style="width:600px">

<br>The value is the reproduction speed ratio, which ranges from 0.1 to 1, that is, 10% to 100%. After entering the correct value, press Enter to proceed to the next step. It is recommended that use a low reproduction ratio for the first operation, and after confirming that the path is correct, a higher reproduction speed ratio can be used. After determining the reproduction speed ratio, the terminal will display:

<img src="../img/桌面级6轴机械臂（QDD Lite-NE30-36版）_v1_0_41.png" style="width:600px">

<br> This option belongs to selection and reproduction mode. “STEP”, “CYCLE”, “CONTINUOUS” can be chose to input, and enter other values to exit the program.

STEP:
Single step operation mode, in which you can enter "FORWARD" to run to the next point, or enter "BACKWARD" to run to the previous point. Enter other values to exit the program.

<img src="../img/桌面级6轴机械臂（QDD Lite-NE30-36版）_v1_0_42.png" style="width:600px">

CYCLE:
Single circular operation mode means only running the program once. In this mode, the following interface will appear at the terminal. Enter “YES” to reproduce the path in a smooth manner (note that the path will be deformed), and input others to run in the normal motion mode (that is, point-to-point motion speed will be reduced to zero).

<img src="../img/桌面级6轴机械臂（QDD Lite-NE30-36版）_v1_0_43.png" style="width:600px">

CONTINUOUS:
Continuous circular operation mode will continuously reproduce the path of “mode3” demonstrates. In this mode, the following interface will appear at the terminal. Enter “YES” to reproduce the path in a smooth manner (note that the path will be deformed), and input others to run in the normal motion mode (that is, point-to-point motion speed will be reduced to zero).

<img src="../img/桌面级6轴机械臂（QDD Lite-NE30-36版）_v1_0_44.png" style="width:600px">

<br>The programs in the above modes can be ended by pressing CTRL + C .

### NOTE:
With the collaborative arm stopped, hold the arm with your hand and execute mode0 to turn off the motor before the power is turned off.


## Version change record
**The following table briefly describes the version change record.**

<table style="width:400px"><thead><tr style="background:PaleTurquoise"><th style="width:100px">version</th><th style="width:150px">updated time</th><th style="width:150px">Updated content</th></tr></thead><tbody><tr><td>v1.0.0</td><td>2019.09.05</td><td>Full text</td></tbody></table>



