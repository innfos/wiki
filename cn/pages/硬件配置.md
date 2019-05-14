硬件配置
=====
*基于ECB通信的硬件配置*

<img src="../img/all.jpg" style="width:600px">

从前到后、从左到右依次为：ECB、HUB、终端电阻2个、回馈制动电容、ECB连接线、INNFOS执行器、执行器连接线，急停开关+电源。

**连接电源**

*   连接电源与`HUB`.

<img src="../img/power.jpg" style="width:600px">

Note: 必须先断电然后再插拔部件.  否则可能损坏部件.


**连接ECB**

*   连接`HUB`与`ECB`

![ECB-C1.jpg](../img/ECB-C1.jpg "fig:ECB-C1.jpg") ![ECB-C2.jpg](../img/ECB-C2.jpg "fig:ECB-C2.jpg")

*   HUB安插回馈制动电容与终端电阻

![ECB-C3.jpg](../img/ECB-C3.jpg "fig:ECB-C3.jpg") ![ECB-C4.jpg](../img/ECB-C4.jpg)

**连接执行器**

*   用执行器连接线连接`HUB`与执行器

<img src="../img/Actuator-C1.jpg" style="width:600px">


*   末端执行器安插终端电阻

<img src="../img/Actuator-C2.jpg" style="width:600px">

**连接电脑**

*   用网线连接`ECB`与电脑

<img src="../img/pc-c.jpg" style="width:600px">

**开启电源**

*   开启电源. 执行器的供电电压范围为直流24V-45V.

<img src="../img/poweron.jpg" style="width:600px">

*   上电以后，执行器LED状态灯会变成黄色闪烁，启动执行器后，LED会变成绿色闪烁，这时就可以与执行器进行通信了。如果执行器内部出现错误，LED灯会变为红色闪烁，请检查执行器错误代码。

<img src="../img/poweron2.jpg" style="width:600px">

<img src="../img/connect2.png" style="width:600px">

*基于CAN通信的硬件配置*


<img src="../img/08can.jpg" style="width:600px">

*   从左到右依次为：INNFOS 执行器、Arduino开发板（需自备）、终端电阻、ECB连接线、执行器综合线缆，直流稳压电源
*   您可以使用自己的Arduino开发板实现与执行器间的CAN通信及控制
*   根据使用情况自行选配急停开关

Note: 必须先断电然后再插拔部件.  否则可能损坏部件.</br>请确认您的直流电源电压与执行器电压范围是否一致，否则会导致执行器出现过压或欠压错误。


**连接Arduino开发板与执行器综合线缆**

*   取出执行器综合线缆和ECB连接线。

<img src="../img/09can.jpg" style="width:600px"> 

*   将执行器综合线缆的一端剪开。
红色粗线为电源正极线；黑色粗线为电源负极线，将双绞屏蔽线剪开，其中红色细线为 CAN_H;黑色细线为 CAN_L; 银色细线为CAN_GND。

<img src="../img/03can.jpg" style="width:600px"> 

*    将ECB连接线小心剪开，并与剪开综合线缆的红色细线 CAN_H，黑色细线 CAN_L; 银色细线为CAN_GND
如图所示找好对应引脚进行连接，焊接牢固 ，并用热缩管或绝缘胶带包好以防止短路。

<img src="../img/10can.jpg" style="width:600px"> 

<img src="../img/11can.jpg" style="width:600px">

*    将红色电源正极线与黑色电源负极线按图所示接入电源正负极。

<img src="../img/05can.jpg" style="width:600px"> 

*    将ECB连接线的另一端插入Arduino开发板，完成连接。


**连接执行器**

*    将执行器综合线缆另一端连接执行器。

<img src="../img/06can.jpg" style="width:600px"> 

*    末端执行器安插终端电阻

<img src="../img/Actuator-C2.jpg" style="width:600px">


*    完成连接，即可接通电源，进行后续调试

<img src="../img/12can.jpg" style="width:600px"> 


