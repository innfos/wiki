以太网通信
=====


## 硬件需求与连接

**硬件需求**

![all.jpg](../img/all.jpg)


从前到后、从左到右依次为：ECB、HUB、终端电阻2个、回馈制动电容、ECB连接线、INNFOS执行器、执行器连接线，急停开关+电源。

**连接电源**

*   连接电源与HUB.

![power.jpg](../img/power.jpg )

**必须先断电然后再插拔部件.** 否则可能损坏部件.


**连接ECB**

*   连接HUB与ECB

![ECB-C1.jpg](../img/ECB-C1.jpg "fig:ECB-C1.jpg") ![ECB-C2.jpg](../img/ECB-C2.jpg "fig:ECB-C2.jpg")

*   HUB安插回馈制动电容与终端电阻

![ECB-C3.jpg](../img/ECB-C3.jpg "fig:ECB-C3.jpg") ![ECB-C4.jpg](../img/ECB-C4.jpg) **连接执行器**

*   用执行器连接线连接HUB与执行器

![Actuator-C1.jpg](../img/Actuator-C1.jpg )


*   末端执行器安插终端电阻

![Actuator-C2.jpg](../img/Actuator-C2.jpg "fig:Actuator-C2.jpg")

**连接电脑**

*   用网线连接ECB与电脑

![pc-c.jpg](../img/pc-c.jpg "fig:pc-c.jpg") **开启电源**

*   开启电源. 执行器的供电电压范围为直流24V-45V.

![poweron.jpg](../img/poweron.jpg "fig:poweron.jpg")

*   上电以后，执行器LED状态灯会变成黄色闪烁，启动执行器后，LED会变成绿色闪烁，这时就可以与执行器进行通信了。如果执行器内部出现错误，LED灯会变为红色闪烁，请检查执行器错误代码。

![poweron2.jpg](../img/poweron2.jpg "fig:poweron2.jpg") 

![connect2.png](../img/connect2.png "fig:connect2.png") 

## 软件安装与使用


**下载IAS**

*   如果电脑系统为linux,访问[IAS(linux)](https://github.com/innfos/INNFOS-Actuator-Studio-linux.git)获取最新版本的IAS(INNFOS Actuator Studio)(Linux),如果电脑系统是window请访问[IAS(windows)](https://github.com/innfos/INNFOS-Actuator-Studio-windows.git).

**配置IP地址**

*   配置步骤请参考[以太网通信配置](Ethernet_Configuration.md)

**安装IAS**

*   安装IAS请参考[IAS安装](INNFOS_Actuator_Studio_IAS_instruction.md)

**使用** 

![2-2.png](../img/2-2.png "fig:2-2.png")


安装成功后，启动IAS,单击“确认”按钮启用“下一步”按钮，然后单击“下一步”直到出现如下界面: 

![2-6.png](../img/2-6.png "fig:2-6.png") 

 单击“1”或“2”按钮启动执行器，按钮“1”变为绿色表示您已成功启动执行器。单击消息框或单击“详细信息”按钮（位于按钮“1”下方） 进入执行器调试界面。 

![2-9.png](../img/2-9.png "fig:2-9.png") 

 **位置控制**

*   单击左侧栏上的“Profile Position Mode”按钮，然后单击右侧的“Activate Profile Position Mode”。之后，您可以在“设置”中输入位置值，单位是R(范围是-127R~127R)。

![6-1.png](../img/Fig6-1.png )

![6-3.png](../img/Fig6-3.png )

### 其他

想了解更多关于IAS的信息 , 请访问[INNFOS Actuator Studio(IAS) instruction](INNFOS_Actuator_Studio(IAS)_instruction "wikilink").

## 版本变更记录


版本号| 更新时间 | 更新内容
---|---|---
V1.0.0 | 2019.04| 第一版


