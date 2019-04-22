[中文](INNFOS_Actuator_Studio（IAS）使用说明 "wikilink")

# INNFOS Actuator Studio(IAS)

## Overview

IAS is a visual debug control software for INNFOS actuator, the main functions of which include control, ID modification, visual graphic data regulation, motion editing, etc. It can intuitively modify and control INNFOS actuators in a convenient way.It does not require the programming skills of users when using IAS, but is unsuitable for complex function combinations.

## Download

### linux

*   visit this link [download link](https://github.com/innfos/INNFOS-Actuator-Studio-linux.git) or you can use command blow:
<div class="sourceCode">

    $ <span class="kw">git</span> clone https://github.com/innfos/INNFOS-Actuator-Studio-linux.git`</pre></div>

    ### windows

*   visit this link [download link](https://github.com/innfos/INNFOS-Actuator-Studio-windows.git) to download Setup.exe file or you can use command blow:
    <div class="sourceCode"><pre class="sourceCode bash">`$ <span class="kw">git</span> clone https://github.com/innfos/INNFOS-Actuator-Studio-windows.git`</pre></div>

    ## IAS installation

    ### linux plantform

    1. Unzip the IAS to your desired location</br> 2. Enter the IAS folder</br> 3. Launch the program by either double clicking the INNFOS Actuator Studio icon or using the command

    <div class="sourceCode"><pre class="sourceCode bash">`$ <span class="kw">./INNFOS\ Actuator\ Studio</span>
</div>

### Windows plantform

1.Double-click the installation software &quot;Setup.exe&quot; ![1-1](软件的安装01.jpg "fig:1-1")

2.After entering the installation interface, click &quot;Next&quot; ![1-2](1-2.png "fig:1-2")

3.click “I Agree” ![1-3](1-3.png "fig:1-3")

4.Select the installation location and click &quot;Install&quot; ![1-3](1-4.png "fig:1-3")

5.Wait for the completion of the installation ![1-4](1-5.png "fig:1-4")

6.If encounter an alarm from anti-virus software, please select &quot;Allow this operation&quot;. ![1-5](1-6.png "fig:1-5")

7.Click &quot;Finish&quot; to complete the software installation. ![1-6](1-7.png "fig:1-6")

## IAS boot

1、Double-click to run the software and enter the user interface. ![2-1](软件的安装02.jpg "fig:2-1")

2.Click &quot;confirm that you've read the document&quot;, then click &quot;next&quot; to enter the next interface. </br>(Note:Please click“show the document!” to read the software instructions when use the product for the first time.) ![2-2](2-2.png "fig:2-2")

3.Select the actuator communication mode (The default setting is Ethernet communication), then click &quot;next&quot;

(Note: Please confirm that the static IP is correctly configured(See Appendix B for details) before start using Ethernet communication.) ![2-3](2-3.png "fig:2-3")

*   When the USB to CAN is not connected or connected abnormally, an error message will appear.

![2-4](2-4.png "fig:2-4")

*   When the external actuator is not connected or connected abnormally, an error message will appear.

![2-5](2-5.png "fig:2-5")

*   When the external system is connected correctly, it enters running interface of the actuator. The red area is OFF. As shown in figure 2-6, OFF at mark 1 is a single actuator switch, ON at mark 2 is a main switch, when the actuators are connected at the same time, click on mark 2 to control all actuators.

![2-6](2-6.png "fig:2-6")

*   After clicking OFF, the messages in the red area showed in figure 2-7 will pop up.

![2-7](2-7.png "fig:2-7")

*   In about three seconds, as shown in figure 2-8, mark 1 for the actuator ID number, mark 2 is the error clear key, mark 3 for the enter operation interface key, and mark 4 for the actuator's information display area.
<div class="figure">
![2-8](2-8.png "2-8")

2-8

</div>

4.Click on message box or click “Detail” to enter the current loop mode.

![2-9](2-9.png "fig:2-9")

* * *

## Current loop mode

Logic block diagram of the INNFOS actuator system:

![Logic block diagram of the INNFOS actuator system](微伺服软件界面最终00-44 3-1.png "fig:Logic block diagram of the INNFOS actuator system")

Description: after the mixed practice of the current setting value and current feedback value, passing through the PI module, the optional filter and the limiting module to drive the motor, the motor feeds back the current parameter to the system to form a closed loop.

### Function Descriptions of Current Loop Mode

（1）Current loop mode

（2）Simple diagram of current loop mode

（3）Status activation in current mode

（4）parameter settings

（5）INNFOS SCA status parameter values

（6）Error warning

（7）Square wave generator parameter value setting

（8）INNFOS actuator current connection status

（9）Oscilloscope switch

<div class="figure">
![Fig3-2](3-2.png "Fig3-2")

Fig3-2

</div>

### Description of basic parameters

（1）Iq axial force setting

（2）Proportional setting

（3）Integration settings

（4）Id axial force setting

（5）Limit minimum setting

（6）Limit maximum setting

<span style="color: red">[Note: In current loop mode, the Id axial force is generally set to 0.

For&quot;Minimal&quot;set a fixed value of -0.82, for&quot;Maximal&quot;set a fixed value of 0.82.]</span> ![Fig3-3](3-3.png "fig:Fig3-3")

### Current loop usage

1.Click on“Active Current Mode”to activate the current current loop mode. ![Fig3-4](3-4.png "fig:Fig3-4")

2.Parameter setting: application mode

*   Enter the current value in&quot;Iq Setting&quot;(Mark 1), press&quot;Enter&quot; or &quot;Set Current&quot; to start the INNFOS actuator,

    then the actuator will output the corresponding torque.

    If the load is not heavy enough, the INNFOS actuator will running in high speed.
*   After rotating, you can see the current status in the INNFOS actuator parameter values.(Mark 3)
*   Press the “Halt” to stop the rotation of the INNFOS actuator.(Mark 2)
*   The maximum current value can be set in the Limit parameter.
<div class="figure">
![Fig3-5](3-5.png "Fig3-5")

Fig3-5

</div>

3.Click on &quot;View Graph&quot; to open the oscilloscope ![Fig3-6](3-6.png "fig:Fig3-6")

4.Oscilloscope Function Description

*   “prescalar” in the right picture can set the time of the entire waveform (Mark 1),

    “trig_value” can be set(Mark 2).

    The setting parameters can be saved, paused and automatically scaled in(Mark 3);
*   channel1 is the offset and magnification of the given waveform of the INNFOS actuators (Mark 4);
*   channel2 is the offset and amplification of the INNFOS actuator current (Mark 5);
*   channel3 is the offset and magnification of the INNFOS actuator speed (Mark 6);
*   channel4 is the offset and magnification of the INNFOS actuator position (Mark 7).
*   Appendix C is for detailed instructions of oscilloscope.
<div class="figure">
[Fig3-7](3-7.png "Fig3-7")

Fig3-7

</div>

5.Square wave generator parameter setting

*   Enter the current value 1 in Value1(Mark 1)
*   Enter the current value 2 in Value2 (Mark 2)
*   Enter the time (unit: ms) in Interval (Mark 3).
*   Click “IqTrigger” to set the axial force to q axis or d axis(Mark5).
*   Select “Start”(Mark 4), and the square wave generator will press the set time ( Interval value), continuously validate Value1 and Value2 to the specified position (Iq Setting or Id Setting) until the button is closed.
*   [Note: When adjusting the PI value of the current loop mode, the axial force of the square wave generator needs to be changed to IdTrigger. At this point there is a waveform in the oscilloscope and the actuator should be at rest, otherwise it will need to be recalibrated. ]
<div class="figure">
![Fig3-8](3-8.png "Fig3-8")

Fig3-8

</div>

6.Click “View Graph” to open the oscilloscope window, you can view the given (channel1 current square wave generator), current(channel2), speed(channel3), position(channel4) four-channel parameter waveform, as shown on the right. ![Fig3-9](3-9.png "fig:Fig3-9")

7.Adjust the values of Proportional and Integral (PI) to observe the debugging effect through oscilloscope. ![Fig3-10](3-10.png "fig:Fig3-10")

8.Click the “Stop” button to stop the square wave generator. ![Fig3-11](3-11.png "fig:Fig3-11")

* * *

## Speed loop mode

Logic block diagram of the INNFOS actuator system:

![• Logic diagram of INNFOS actuation system](微伺服软件界面最终00-43 4-1.png "fig:• Logic diagram of INNFOS actuation system")

Description: After the speed value setting and the speed feedback value are added and subtracted, the PI module is passed through the optional filter and then the module outputs the current to the current loop. When the current loop mode is ensured to operate correctly, the motor is driven by the current loop. The encoder feeds the speed parameter back to the system to form a closed loop.

* * *

### Click on &quot;Velocity Regulation&quot; to enter speed loop mode

<div class="figure">
![Fig 4-2](4-2.png "Fig 4-2")

Fig 4-2

</div>

### Description of Speed Loop Mode Functions

(1)Simple diagram of speed loop mode

(2)Activation in current mode

(3)Basic parameter settings

(4)INNFOS SCA parameter values

(5)Error warning

(6)Square-wave generator parameter value setting

(7)INNFOS actuator connection status

(8)Oscilloscope switch ![Fig 4-3](4-3.png "fig:Fig 4-3")

### Speed loop usage

1.Click on &quot;Active Velocity Mode&quot; to activate the current speed loop mode. ![Fig 4-4](4-4.png "fig:Fig 4-4")

2.Speed loop basic parameter settings:

*   Enter the speed value (unit: RPM) in the &quot;Setting&quot; box. Press Enter or click on &quot;Set Velocity&quot; on the right, then INNFOS SCA starts to rotate.
*   After rotating, the status value column, as shown in the figure, can be seen as the parameter values of different INNFOS SCA.
*   Adjust the Proportional box and the Integral box to adjust the PI value(Mark 2).
*   The Mininal box and Maximum box shows the output limit for speed loop (followed by Current loop input),

    for example, current up to 33A（Model 6010 is 33A and Model 3510 is 16.5A. See Appendix D of the CAN Bus Communication Protocol for details.）, input value is 0.5；When the INNFOS actuator current is increased to 33*0.5, the current value will be limited without increasing.
*   Press the “Halt” button to stop the rotation of the INNFOS actuator
<div class="figure">
![Fig 4-5](4-5.png "Fig 4-5")

Fig 4-5

</div>

3.Click on &quot;View Graph&quot; to open the oscilloscope ![Fig 4-6](4-6.png "fig:Fig 4-6")

4.Introduction to Speed Loop Oscilloscope

*   “prescalar” sets the time of the entire waveform (Mark 1)
*   “trig_value” sets the trigger value (Mark 2).
*   Set the function as save, pause, and auto-scale (Mark 3);
*   channel1 sets the offset and magnification of the given waveform (Mark 4),
*   channel2 is the offset and amplification of the INNFOS actuator current (Mark 5),
*   channel3 is the offset and magnification of the INNFOS actuator speed (Mark 6)
*   channel4 is the offset and magnification of the INNFOS actuator position (Mark 7)
<div class="figure">
![Fig 4-7](4-7.png "Fig 4-7")

Fig 4-7

</div>

5.Setting of Square-wave Gnerator Prameter Value

*   Enter the number of revolutions in Value1. (Unit: RPM)
*   Enter the reverse number in Value2. (Unit: RPM)
*   Enter the unit time (in ms) in Interval to set the parameters of the INNFOS actuator square wave generator.
*   Select “Start” to turn the INNFOS actuator on.
<div class="figure">
![Fig 4-8](4-8.png "Fig 4-8")

Fig 4-8

</div>

6.Set the parameters in the &quot;View Graph&quot; view to better check the current INNFOS SCA different parameter waveforms, adjusting the value of Proportional and Integral (PI), so that the performance will be reflected in the form of waveform in the oscilloscope.

<span style="color: red">Note: The unused channel offset is set to 0 and the amplification is set to 1 (channel2 and channel4 in the figure) or click the OFF to shut it down.</span> ![Fig 4-9](4-9.png "fig:Fig 4-9")

7.Click “Stop” to stop the square-wave generator. ![Fig 4-10](4-10.png "fig:Fig 4-10")

## Position Loop Mode

Logic block diagram of the INNFOS actuator system：

![Logic block diagram of the INNFOS actuator system:](微伺服软件界面最终00-44 5-1.png "fig:Logic block diagram of the INNFOS actuator system:")

Introduction of the block diagram:

In the case of ensuring the accuracy of the current loop and the speed loop, the set position value and the feedback value, through addition and subtraction, passed through the PI module and then output the speed value through the optional filter. After that, the speed loop drives the motor through the current loop, and the motor feeds back the position parameters to the system via the encoder. All this form a closed loop.

### Click “position” to enter the position loop mode

<div class="figure">
![Fig 5-2](5-2.png "Fig 5-2")

Fig 5-2

</div>

### Description of Position Loop Mode Function

(1) Position loop mode diagram

(2) Status activation in current mode

(3) Basic parameter settings

(4) INNFOS actuator status parameter values

(5) Error warning

(6) Square wave generator parameter value setting

(7) INNFOS actuator connection status

(8) Oscilloscope switch ![Fig 5-3](5-3.png "fig:Fig 5-3")

### Position Loop Usage

1.Click on “Active Position Mode” to activate the current position loop mode. ![Fig 5-4](5-4.png "fig:Fig 5-4")

2.Position loop basic parameter settings:

*   Enter the position value (unit: R) in the “Setting” box（Mark.1）, Press &quot;Set Position&quot; (Mark.4)and then the INNFOS actuator starts to rotate.

    INNFOS actuator will stop rotate after arrives the assigned input position.
*   After rotating, the status value column (Mark. 5) can see the current parameter values.
*   Adjust the Proportional box to change the scale value (Mark. 2).
*   The Mininal box and Maximum box (Mark. 3)are the speed limit of the speed loop for the position loop, for example, speed is up to 6000RPM, input value is 0.5, then the maximum speed of the INNFOS actuator rise to 6000*0.5=3000R/min, the speed value will be limited and will not increase.
<div class="figure">
![Fig 5-5](5-5.png "Fig 5-5")

Fig 5-5

</div>

3.Click on &quot;View Graph&quot; to open the oscilloscope ![Fig 5-6](5-6.png "fig:Fig 5-6")

4.Oscilloscope Function Description

*   &quot;Prescalar&quot; can set the time of the entire waveform (Mark 1);
*   &quot;trig_value&quot; sets the trigger value (Mark 2);
*   Position at the Fig.3 saves, pauses, and automatically scales the parameters;
*   Channel1 sets the offset and magnification of the given waveform (Mark 4);
*   Channel2 sets the offset and amplification of the INNFOS actuator current (Mark 5);
*   Channel3 is the offset and magnification of the INNFOS actuator speed (Mark 6);
*   Channel4 is the offset and magnification of the INNFOS actuator position (Mark 7).
<div class="figure">
![Fig 5-7](5-7.png "Fig 5-7")

Fig 5-7

</div>

5.Setting of Square wave-generator parameter values

*   Enter the positional value 1 in Value1 (unit: R)
*   Enter positional value 2 in Value2 (unit: R)
*   Enter the time (unit: ms) in “Interval”, the input parameter is of the rotating for one time (for example, Value1 is 2, Value2 is -2, and Interval is 1000. After startup, INNFOS Actuator first goes to position 2, 1000mS and then goes to position-2.Go to position 2 again after 1000ms, and then run it repeatedly until the user clicks &quot;Stop&quot;).
*   Click the &quot;Start&quot; button to turn on the INNFOS actuator.
<div class="figure">
![Fig 5-8](5-8.png "Fig 5-8")

Fig 5-8

</div>

6. Click &quot;View Graph&quot; to open the oscilloscope window, you can view the given (this the time is the square wave generator), current, speed, position four-channel parameter waveform. <span style="color: red">Note: No the channel offset used is set to and the zoom is set to 1 (as in channel 2 and in the image to the right) Channel3）</span> ![Fig 5-9](5-9-1.png "fig:Fig 5-9")

7.Click the “Stop” to stop the square wave generator. ![Fig 5-10](5-10.png "fig:Fig 5-10")

8.Click the “Stop” button to stop the square wave generator. ![Fig 5-11](5-11.png "fig:Fig 5-11")

## Position loop S-curve mode

### Click on &quot;Profile Velocity Mode&quot; to enter position loop S-curve mode

<div class="figure">
![Fig 6-1](6-1.png "Fig 6-1")

Fig 6-1

</div>

### position loop S-curve mode functional descriptions

(1) position loop S-curve mode schematic diagram

(2) Status activation in current mode

(3) Basic parameter setting

(4) INNFOS actuator status parameter value

(5) Error warning

(6) INNFOS actuator current connection status ![Fig 6-2](6-2.png "fig:Fig 6-2")

### position loop S-curve mode

1.Click on “Active Profile Velocity Mode” to activate position loop S-curve mode ![Fig 6-3](6-3.png "fig:Fig 6-3")

2.Basic parameters of position loop S-curve mode:

*   Enter the position of the rotation in the &quot;Target&quot; box (unit: R) and the INNFOS actuator will start to rotate to the specified position.
*   After the INNFOS actuator rotating, the values of the current INNFOS actuator can be seen in the status value column(right in Figure 4).
*   Accelerate box and Decelerate box, at the right picture 2, are the rise and fall of speed in the S curve mode. For example, the larger the Accelerate value is, the shorter time the INNFOS actuator reaches the maximum speed needs; and the smaller the Accelerate value is , the longer time that INNFOS actuator reaches the maximum speed is needed. The larger the Decelerate value, the shorter the time that the INNFOS actuator will decrease from maximum speed to zero. The smaller the Decelerate value, the longer the INNFOS actuator will decrease from maximum speed to zero.
*   “Max” limits the maximum speed of the INNFOS actuator and increases as the value increases. As shown in the three figures on the right, the current maximum speed is 1000 RPM.
*   关于位置环S曲线模式的原理分析参见附录D。
<div class="figure">
![Fig 6-4](6-4.png "Fig 6-4")

Fig 6-4

</div>

* * *

## Velocity loop S-curve mode

### Click on &quot;Profile Velocity Mode&quot; to enter the velocity loop S-curve mode

<div class="figure">
![Fig 7-1](7-1.png "Fig 7-1")

Fig 7-1

</div>

### Velocity loop curve mode functional descriptions

(1) Velocity loop S-mode schematic diagram

(2) Status activation in current mode

(3) Basic parameter setting

(4) INNFOS actuator status parameter value

(5) Error warning

(6) INNFOS actuator current connection status ![Fig 7-2](7-2.png "fig:Fig 7-2")

### Velocity loop S-curve mode

1.Click on “Active Profile Velocity Mode” to activate the Velocity loop S-mode ![Fig 7-3](7-3.png "fig:Fig 7-3")

2.Basic parameters of Velocity loop S-mode:

*   Enter the speed value of the INNFOS actuator (unit: RPM) in the &quot;Target&quot; box and the INNFOS actuator will start to rotate until the input value is reached.
*   After the INNFOS actuator rotating, the values of the current INNFOS actuator can be seen in the status value column, (right in Figure 3).
*   The &quot;Accelerate&quot;, &quot;Decelerate&quot; and &quot;Max&quot; items at 2 in the right figure are the rectified parameters of the S curve.
<div class="figure">
![Fig 7-4](7-4.png "Fig 7-4")

Fig 7-4

</div>

## Homing mode

### Click on &quot;Homing Mode&quot; to enter the homing mode

<div class="figure">
![Figure：8-1](8-1.png "Figure：8-1")

Figure：8-1

</div>

### Usage of homing mode

Click on “Active Homing Mode” to activate the current homing mode. ![Figure：8-2](8-2.png "fig:Figure：8-2")

### Velocity loop curve mode functional descriptions

1.Automatic calibration of left and right limits

*   Click the Clear and Homing buttons one after the other, and repeat the current left and right limits twice, until the data in Figure 8-1 shows the following large value (the upper and lower limits of the software limit). Then adjust the right picture of Figure 8-1 to the following large value (this is the current limit, such as the need for a larger current when the load increased, the current limit needs to be released). After that, click on the Auto button and the INNFOS actuator will automatically turn clockwise until it touches the mechanical left limit (here defines the mechanical limit for clockwise touch to the left limit and counterclockwise for the right limit), then automatically counterclockwise until touch the mechanical right limit to stop.
<div class="figure">
![Figure：8-3](8-3.png "Figure：8-3")

Figure：8-3

</div>

*   At this point, the value of the left and right limits is returned to 1 in Figure 8-1. Then manually control to rotate the INNFOS actuator to the desired zero point (for example, 2 in the left figure in Figure 8-2), and finally click the Homing button, then the current position becomes zero (as shown in Figure 3-2 on the right side of Figure 03) 2)) The left and right limits of the 1st position on the right side of Figure 8-2 will be offset according to the position before clicking Homing (compare the two sides in Figure 8-2). This ensures the consistency of software limits and mechanical limits.
<div class="figure">
![Figure：8-4](8-4.png "Figure：8-4")

Figure：8-4

</div>

*   Then, set the margin offset to the left and right limits (3 in the right figure in Figure 8-2), then the actual motion range is the left and right limit minus the offset (the right side of Figure 8-2: left software limit) The bit is 33.774918-1.4=32.374918; the right software limit is -32.4932+1.4=-31.0932.) Finally, confirm that the software limit is turned on as shown in the right side of Figure 8-2, click the Download button to save. Current parameter.

### Manual calibration of left and right limits

1.Click on the red box position &quot;Active Homing Mode&quot; on the right to enter the homing mode. ![Fig 9-1](手动校准01.png "fig:Fig 9-1")

2.Click the Clear and Homing buttons one after the other, and to clear the current left and right limits using this operation twice. Until the data in the red box 1 on the right is changed to the large value (this is the upper and lower limits of the software limit). Then adjust the right picture 2 to the following large value (this is the current limit, such as the need for a larger current when the load is increased, and the current limit needs to be released). ![Fig 9-2](手动校准02.png "fig:Fig 9-2")

3.Manually adjust the joint to the left mechanical limit and click on &quot;Max_Set&quot;, at which point the value at the &quot;Max Pos&quot; will change. ![Fig 9-3](手动校准03.png "fig:Fig 9-3")

4.Manually adjust the joint to the right mechanical limit and click on &quot;Min_Set&quot;. The value of the &quot;Min Pos&quot; column will change. ![Fig 9-4](手动校准05.png "fig:Fig 9-4")

5.Manually adjust the joint to zero point, click 2, and then 1 will become 0. ![Fig 9-5](手动校准06.png "fig:Fig 9-5")

6.Set the left and right limit offset ![Fig 9-6](手动校准07.png "fig:Fig 9-6")

7.Click the &quot;Download&quot; button to save the current parameters. ![Fig 9-7](手动校准08.png "fig:Fig 9-7")

## Error warning

### When an error occurs, the error message will be displayed in the box.

As shown in the figure, an error message is displayed.

<span style="color: red">（Note: If you use the latest version of the host computer software, the alarm will be detailed.）</span> ![9-1.png](9-1.png "fig:9-1.png")

### Error handling

Click &quot;OK&quot; and &quot;Clear Errors&quot; to solve the problem. After clearing, the INNFOS actuator enters current loop mode. ![9-2.png](9-2.png "fig:9-2.png")

# Version Change Record

The following table briefly describes the version change records
<table class="tableizer-table">
<thead><tr class="tableizer-firstrow";style="background: PaleTurquoise;"><th>Version No.</th><th>Update time</th><th>update contents</th></tr></thead><tbody>
 <tr><td>V1.0.0</td><td>2019-04</td><td>The First Version</td></tr>
</tbody></table>
