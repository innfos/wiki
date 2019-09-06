
桌面级6轴机械臂安装使用说明书
=====

## 介绍

*   本说明书是针对桌面级6轴机械臂
*   在使用之前请仔细阅读本说明书内容。

<br>所有关节采用QDD Lite系列执行器搭建。其臂长活动范围最大430mm，末端负载500g。因QDD Lite系列执行器采用了复合材料，大大降低了高端机器人本机研发成本，主要应用于教育领域，学校、实验室、研究所、竞赛等。
                                                                          
<img src="../img/桌面级6轴机械臂（QDD Lite-NE30-36版）_v1_0.png" style="width:720px">                                                                          

## 桌面级6轴机械臂（QDD Lite-NE30-36版）工程参数图
<br>[单位：毫米]

<img src="../img/桌面级6轴机械臂（QDD Lite-NE30-36版）_v1_0.md三视图.png" style="width:720px">


### 3D 模型
[模型文件]( ../img/桌面级6轴机械臂（QDD Lite-NE30-36版）_v1_0.step.zip )


## 桌面级6轴机械臂（QDD Lite-NE30-36版）参数

<table style="width:500px"><thead><tr><th colspan="2" style="background: PaleTurquoise; color: black;">桌面级6轴机械臂（QDD Lite-NE30-36版）参数</th></tr></thead><tbody></tr><tr><td>末端负载</td><td>500g</td></tr>
<tr><td>自重</td><td>3.7kg（带底座）；2.5kg（不带底座）</td></tr><tr><td>自由度</td><td>6</td></tr><tr><td>工作半径</td><td>421mm</td></tr><tr><td>关节范围</td><td>+/-170°</td></tr><tr><td>工具最大速度</td><td>2m/s</td></tr><tr><td>重复定位精度</td><td>+/-0.1mm</td></tr><tr><td>供电电压</td><td>42v</td></tr><tr><td>功耗</td><td>普通功耗约120w</td></tr><tr><td>结构件材料</td><td>铝合金/碳纤维管</td></tr><tr><td>工作环境温度</td><td>10-50°</td></tr><tr><td>工作环境湿度</td><td>5%~95%</td></tr><tr><td>防护等级</td><td>IP54</td></tr><tr><td>通信端口</td><td>通信端口</td></tr><tr><td>示教器</td><td>电脑或者移动终端</td></tr></td></tbody></table>


## 开箱

<img src="../img/Robot_DOF6/13.jpg" style="width:600px">

## 硬件需求与连接

**硬件需求**

<img src="../img/Robot_DOF6/12.jpg" style="width:600px">

从前到后、从左到右依次为：HUB、ECB、ECB连接线、终端电阻1个、网线、 机械臂、回馈制动电容、急停开关+电源。

**连接电源**

*   连接电源与`HUB`.

<img src="../img/power.jpg" style="width:600px">

Note: 必须先断电然后再插拔部件.  否则可能损坏部件.


**连接ECB**

*   连接`HUB`与`ECB`

![ECB-C1.jpg](../img/ECB-C1.jpg "fig:ECB-C1.jpg") ![ECB-C2.jpg](../img/ECB-C2.jpg "fig:ECB-C2.jpg")

*   HUB安插回馈制动电容与终端电阻

![ECB-C3.jpg](../img/ECB-C3.jpg "fig:ECB-C3.jpg") ![ECB-C4.jpg](../img/ECB-C4.jpg)

**连接机械臂**

*   用执行器连接线连接`HUB`与执行器

<img src="../img/Robot_DOF6/5.jpg" style="width:600px">

**连接电脑**

*   用网线连接`ECB`与电脑

<img src="../img/Robot_DOF6/7.jpg" style="width:600px">

**连接后整体视图**

<img src="../img/Robot_DOF6/10.jpg" style="width:600px">


**开启电源**

*   开启电源. 执行器的供电电压范围为直流24V-45V.

<img src="../img/poweron.jpg" style="width:600px">

*   上电以后，执行器LED状态灯会变成黄色闪烁，启动执行器后，LED会变成绿色闪烁，这时就可以与执行器进行通信了。如果执行器内部出现错误，LED灯会变为红色闪烁，请检查执行器错误代码。


## 软件安装与使用


**IAS软件的使用**

* `IAS`(INNFOS Actuator Studio)的为配置机械臂的上位机软件 , 请访问[INNFOS Actuator Studio(IAS)说明](#!pages/INNFOS_Actuator_Studio_IAS_instruction.md).

**运动功能使用**

* 示教-再现功能
  

### 其他
















## 版本变更记录
**下表简单描述了版本变更记录**

<table style="width:400px"><thead><tr style="background:PaleTurquoise"><th style="width:100px">版本号</th><th style="width:150px">更新时间</th><th style="width:150px">更新内容</th></tr></thead><tbody><tr><td>v1.0.0</td><td>2019.09.05</td><td>全文添加</td></tbody></table>



