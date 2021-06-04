以太网通信
=====



## 硬件需求与连接

**硬件需求**

<img src="../../img/all.png" style="width:600px">

从前到后、从左到右依次为：网线、急停开关+电源、执行器综合线缆、插好终端电阻和回馈制动电容的ECB+HUB、执行器两台。

**连接电源**

*   连接电源与`ECB+HUB`

<img src="../../img/cdy.jpg" style="width:600px">
<img src="../../img/cwdy.jpg" style="width:600px">

**连接执行器及其配件**

*   连接`执行器综合线缆`

<img src="../../img/cx.jpg" style="width:600px">
<img src="../../img/cwx.jpg" style="width:600px">

**连接执行器**

*   用`执行器综合线缆`连接`HUB`与执行器

<img src="../../img/Actuator-C1.png" style="width:600px">


*   末端执行器安插`终端电阻`

<img src="../../img/Actuator-C2.jpg" style="width:600px">

**连接电脑**

*   用网线连接`ECB`与电脑

<img src="../../img/pc-c.png" style="width:600px">

**开启电源**

*   开启电源. 执行器的供电电压范围为直流24V-45V.

<img src="../../img/poweron.png" style="width:600px">

*   上电以后，执行器LED状态灯会变成黄色闪烁，启动执行器后，LED会变成绿色闪烁，这时就可以与执行器进行通信了。如果执行器内部出现错误，LED灯会变为红色闪烁，请检查执行器错误代码。

<img src="../../img/poweron2.png" style="width:600px">

<img src="../../img/connect2.png" style="width:600px">

## EL20连接方式

**硬件需求**

从前到后、从左到右依次为：急停开关+电源、JST转MOLEX转接线、EL20系列综合线缆、插好终端电阻和回馈制动电容的ECB+HUB、EL20执行器、T型三通转换器（JST）、多圈计数编码器电池、终端电阻（JST）。

<img src="../../img/bzt.jpg" style="width:600px">

**连接电源**

*   连接电源与`ECB+HUB`

<img src="../../img/cdy.jpg" style="width:600px">
<img src="../../img/cwdy.jpg" style="width:600px">

**连接执行器及其配件**

*   连接`JST转MOLEX转接线`

<img src="../../img/cx.jpg" style="width:600px">
<img src="../../img/cwx.jpg" style="width:600px">

*   连接`T型三通转换器（JST）`

<img src="../../img/ctxt.jpg" style="width:600px">

*   连接`多圈计数编码器电池`

<img src="../../img/cdc.jpg" style="width:600px">

*   连接`终端电阻（JST）`

<img src="../../img/cdz.jpg" style="width:600px">

*   连接`EL20执行器`

<img src="../../img/czxq.jpg" style="width:600px">

*   单台`EL20执行器`连接

<img src="../../img/dtzxq.jpg" style="width:600px">

*   多台`EL20执行器`连接

<img src="../../img/3tzxq.jpg" style="width:600px">

 Note: EL20为非隔离CAN通信，暂时不推荐和其他系列SCA混连。即将推出CAN隔离转不隔离模组，届时即可混连。

## 软件安装与使用


**下载IAS**

*   如果电脑系统为Linux,访问[IAS(Linux)](https://github.com/mintasca/INNFOS-Actuator-Studio-linux.git)获取最新版本的IAS(MINTASCA Actuator Studio)(Linux),如果电脑系统是Windows请访问[IAS(Windows)](https://github.com/mintasca/INNFOS-Actuator-Studio-windows.git).

**配置IP地址**

*   配置步骤请参考[以太网通信配置](Ethernet_Configuration.md)

**安装IAS**

*   安装IAS请参考[IAS安装](INNFOS_Actuator_Studio_IAS_instruction.md)

**使用** 


<img src="../../img/new11.png" style="width:600px"> 

安装成功后，启动`IAS`,单击“确认”按钮启用“下一步”按钮，然后单击“下一步”直到出现如下界面: 


<img src="../../img/new15.png" style="width:600px"> 

单击“1”或“2”按钮启动执行器，按钮“1”变为绿色表示您已成功启动执行器。单击消息框或单击“详细信息”按钮（位于按钮“1”下方） 进入执行器调试界面。 

<img src="../../img/new18.png" style="width:600px"> 


 **位置控制**

*   单击左侧栏上的`Profile Position Mode`按钮，然后单击右侧的`Activate Profile Position Mode`。之后，您可以在“设置”中输入位置值，单位是R(范围是-127R~127R)。

<img src="../../img/new61.png" style="width:600px"> 

<img src="../../img/new63.png" style="width:600px"> 


### 其他

想了解更多关于`IAS`的信息 , 请访问[MINTASCA Actuator Studio(IAS)说明](#!pages/INNFOS_Actuator_Studio_IAS_instruction.md).

## 版本变更记录
<table style="width:400px"><thead><tr style="background:PaleTurquoise"><th style="width:100px">版本号</th><th style="width:150px">更新时间</th><th style="width:150px">更新内容</th></tr></thead><tbody><tr><td>V1.0.1</td><td>2019.09</td><td>增加EL20连接方式</td></tr><tr><td>V1.0.0</td><td>2019.04</td><td>第一个版本</td></tbody></table>


