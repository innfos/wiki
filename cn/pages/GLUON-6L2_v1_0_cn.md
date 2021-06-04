
桌面级6轴机械臂安装使用说明书
=====

## 介绍

*   本说明书是针对GLUON-6L2的使用说明。
*   在使用之前请仔细阅读本说明书内容。

<br>所有关节采用QDD Lite系列执行器搭建。其臂长活动范围最大425mm，末端负载500g。因QDD Lite系列执行器采用了复合材料，大大降低了高端机器人本机研发成本，主要应用于教育领域，学校、实验室、研究所、竞赛等。
                                                                          
                                                                        

## 工程参数图
<br>[单位：毫米]

<img src="../../img/桌面级6轴机械臂（QDD Lite-NE30-36版）_v1_0.md三视图.png" style="width:720px">

### 工作空间
<img src="../../img/桌面级6轴机械臂（QDD Lite-NE30-36版）_v1_0.md工作空间.jpg" style="width:720px">

### 3D模型
[模型文件]( ../../3DModel/桌面级6轴机械臂（6L3）_v1_0.zip )


## 基本参数

<table style="width:500px"><thead><tr><th colspan="3" style="background: PaleTurquoise; color: black;">GLUON-6L2参数</th></tr></thead><tbody></tr><td rowspan="8">规格</td></tr><tr><td>末端负载</td><td>500g</td></tr><tr><td>自重</td><td>3.7kg（带底座）；2.5kg（不带底座）</td></tr><tr><td>自由度</td><td>6</td></tr><tr><td>长宽高</td><td>162.15 ̽ 100  ̽ 555.5mm</td></tr><tr><td>安装方式</td><td>桌面/框架/倒置/倾斜</td></tr><tr><td>防护等级</td><td>IP54</td></tr><tr><td>结构件材料</td><td>铝合金/碳纤维</td></tr></tr><td rowspan="7">工作范围</td></tr><td>第1轴</td><td>-140°~140°</td></tr><td>第2轴</td><td>-90°~90°</td></tr><td>第3轴</td><td>-140°~140°</td></tr><td>第4轴</td><td>-140°~140°</td></tr><td>第5轴</td><td>-140°~140°</td></tr><td>第6轴</td><td>-360°~360°</td></tr></tr><td rowspan="7">最大速度</td></tr><td>第1轴</td><td>302°/s</td></tr><td>第2轴</td><td>302°/s</td></tr><td>第3轴</td><td>302°/s</td></tr><td>第4轴</td><td>302°/s</td></tr><td>第5轴</td><td>302°/s</td></tr><td>第6轴</td><td>902°/s</td></tr><td>重复定位精度</td><td colspan="3" >2mm</td></tr></tr><td rowspan="6">工作环境</td></tr><td>电压</td><td>42V</td></tr><td>功耗</td><td>普通工况约120W</td></tr><td>工作温度</td><td>10°~50°</td></tr><td>工作环境湿度</td><td>5%~95%</td></tr><td>通信端口</td><td>CAN/以太网</td></tr></tbody></table>


## 产品实拍效果图

<img src="../../img/13.jpg" style="width:600px">

## 硬件需求与连接

**硬件需求**

<img src="../../img/12.png" style="width:600px">

从前到后、从左到右依次为：六轴机械臂一台、插好终端电阻和回馈制动电容的ECB+HUB、急停开关+电源、电脑。


**连接ECB**

**连接电源**

*   连接电源与`ECB+HUB`

<img src="../../img/cdy.jpg" style="width:600px">
<img src="../../img/cwdy.jpg" style="width:600px">

**连接执行器及其配件**

*   连接`执行器综合线缆`

<img src="../../img/cx.jpg" style="width:600px">
<img src="../../img/cwx.jpg" style="width:600px">

**连接机械臂**

*   用执行器连接线连接`HUB`与执行器

<img src="../../img/5.png" style="width:600px">

**连接电脑**

*   用网线连接`ECB`与电脑

<img src="../../img/7.png" style="width:600px">

**连接后整体视图**

<img src="../../img/12.png" style="width:600px">


**开启电源**

*   开启电源. 执行器的供电电压范围为直流24V-45V.

<img src="../../img/poweron.png" style="width:600px">

*   上电以后，执行器LED状态灯会变成黄色闪烁，启动执行器后，LED会变成绿色闪烁，这时就可以与执行器进行通信了。如果执行器内部出现错误，LED灯会变为红色闪烁，请检查执行器错误代码。


## 软件安装与使用
### 介绍
IRS是一款MINTASCA机械臂调试软件，主要功能包括位置校准功能、示例动作播放功能、示教-再现功能，用户不需要太多编程经验就可控制机械臂完成基本动作。

**运动功能使用**

* 示教-再现功能
  

### 下载安装

目前支持linux-x86-64版本和linux-树莓派版本

x86-64版本：
推荐使用64位ubuntu16.04、ubuntu18.04等系统
访问该链接[download link](https://github.com/mintasca/robot-controller-GL-6L3.git)下载机械臂软件或者直接执行以下命令
```sh
$ git clone https://github.com/mintasca/robot-controller-GL-6L3.git
```
树莓派版本：
适用于Raspberry Pi 3 Model B 和 Raspberry Pi 3 Model B+
访问该链接[download link](https://github.com/mintasca/robot-controller-GL-6L3-raspi.git)下载机械臂软件或者直接执行以下命令
```sh
$ git clone https://github.com/mintasca/robot-controller-GL-6L3-raspi.git
```

### 使用前检查

*   检查执行器指示灯是否正常，若执行器指示灯绿色或黄色为正常，若不亮或者其他颜色则表示异常。

*   检查各关节是否松动，转动关节查看关节是否有异响或松动现象。

*   检查零位是否丢失，将机械臂摆到竖直状态，使用IAS检查每个轴的位置值（如下图），正常状态位置值应该在0到±1之间。
            
<img src="../../img/00A.png">

进入到主目录
```sh
$ cd robot_controller-GL-6L3/
```
第一次运行此软件时需要获取权限，请输入下面命令      
```sh
$ chmod 777 *
```

Note: 此命令只有初次使用或者更新软件的情况下需要输入一次

配置环境变量：
```sh
$ . environment
```
Note: 每次打开终端都需执行此命令，如不执行,终端会提示找不到动态库“libActuatorController.so”
Attention: 零位若丢失，会导致机械臂运动异常


### 运行模式
机械臂提供以下运行 tutorials，mode0,mode1,mode2,mode3,mode4

进入到主目录
```sh
$ cd robot_controller-GL-6L3/
```
配置环境变量：
```sh
$ . environment
```
Note: 每次打开终端都需执行此命令，如不执行,终端会提示找不到动态库“libActuatorController.so”

<br>可执行文件为tutorials 和robotserver

<br>根据运行模式在终端输入： 

```sh
$ ./tutorials
```
若执行时提示没有“tutorials”文件，表明该文件没有权限，执行以下命令更改权限：
```sh
$ chmod +x tutorials
```
<br>tutorials模式可以按照引导使机械臂按照预先设定动作运动

<br>执行命令
```sh
$ ./tutorials
```
<br>机械臂会运动到到原点位置

此时终端会显示：

<img src="../../img/tutro.png" style="width:600px">

<br>1、2、3、4为4套预设动作，输入其中任意数字即可让机械臂运动，播放完该动作自动后，可重新选择动作模式

输入stop会退出引导程序，此时终端会显示：

<img src="../../img/STOP.png" style="width:600px">


扶住机械臂，按enter键后执行器失能，引导程序结束

Note: 请注意一定要先扶住机械臂再按enter

<br>根据运行模式在终端输入： 
```sh
$ ./robotserver xx
```
其中“xx”为mode0,mode1,mode2,mode3,mode4

若执行时提示没有“robotserver”文件，表明该文件没有权限，执行以下命令更改权限：
```sh
$ chmod +x robotserver
```

<br>其中file文件夹用于存储路径文件

* mode0
此模式的作用是关掉机械臂使能状态
<br>执行命令
```sh
$ ./robotserver mode0
```

Note: 机械臂断电之前，需执行此命令，然后才能关掉电源


* mode1
此模式的作用是连续记录轨迹
<br>执行命令 
```sh
$ ./robotserver mode1
```

此时终端会显示：

<img src="../../img/MODE1.png" style="width:600px">

<br>输入“start”开始记录。
<br>CTRL + C可停止记录，此时轨迹文件存储在file/trajectory.txt里。


* mode2
再现“mode1”生成的轨迹文件file/trajectory.txt。
该模式会循环运行
<br>执行命令 
```sh
$ ./robotserver mode2
```
此时终端会显示：

<img src="../../img/MODE2.png" style="width:600px">

<br>该值为再现速度比例，取值范围为0.1-1，即10%-100%，输入正确的值后按Enter键进行下一步。建议第一次运行采用低的再现速度比例，确认路径无误后，可采用较高的再现速度比例。

CTRL + C可停止运行。
此时若不再使用机器人，可执行./robotserver mode0使机器人失能，后关闭电源。


* mode3
此模式下会逐步记录路径点位，并存储在文件file/data.txt中。
<br>执行命令 
```sh
$ ./robotserver mode3
```
此时终端会提示：

<img src="../../img/MODE3.png" style="width:600px">

<br>该选项功能为选择插补类型或停止记录，可选择输入字符“MOVJ”、“MOVL”、“MOVC”、“STOP”，改选项大小写不敏感（即可全用小写输入）。

MOVJ:
关节插补，末端运动轨迹具有不确定性，仅在关节空间进行规划，终端输入“MOVJ”

MOVL:
直线插补，末端运动轨迹为直线，终端输入“MOVL”

MOVC:
圆弧插补，末端运动轨迹为圆弧，圆弧插补需要记录两个点，一个为辅助点，输入“MOVC”
<br>后记录下辅助点，终端如下提示，此时输入“YES”记录圆弧终点，输入其他则退出程序。

<img src="../../img/MOVC.png" style="width:600px">

STOP:
停止记录，退出程序

* mode4
按模式“mode3”生成的路径文件file/data.txt进行再现运行。
<br>执行命令
```sh
$ ./robotserver mode4
```
此时终端会显示：

<img src="../../img/MODE4.png" style="width:600px">

<br>该值为再现速度比例，取值范围为0.1-1，即10%-100%，输入正确的值后按Enter键进行下一步。建议第一次运行采用低的再现速度比例，确认路径无误后，可采用较高的再现速度比例。
<br>确定再现速度比例后终端会显示：

<img src="../../img/1a.png" style="width:600px">

<br>该选项为选择再现运行模式，可选择输入“STEP”、“CYCLE”、“CONTINUOUS”，输入其它值则退出程序。

STEP:
单步运行模式，该模式下可输入“FORWARD”运行到下一个点，或者输入“BACKWARD”运行到上一个点，输入其它值则退出程序。

<img src="../../img/STEP.png" style="width:600px">

CYCLE:
单循环运行模式，即只运行程序一遍，此模式下终端会出现以下界面，输入“YES”以平滑的方式再现路径（注意路径会变形），输入其他则按正常运动方式运行（即点到点运动速度降低为零）。

<img src="../../img/CYCLE.png" style="width:600px">

CONTINUOUS:
连续循环运行模式，连续再现“mode3”示教的路径，此模式下终端会出现以下界面，输入“YES”以平滑的方式再现路径（注意路径会变形），输入其他则按正常运动方式运行（即点到点运动速度降低为零）

<img src="../../img/CONTINUOUS.png" style="width:600px">

<br>以上模式均可按下CTRL + C终止程序运行


### 注意事项
在机械臂停止的状态下，在断电之前，请用手托住机械臂并执行mode0关闭电机使能。



## 版本变更记录
**下表简单描述了版本变更记录**

<table style="width:400px"><thead><tr style="background:PaleTurquoise"><th style="width:100px">版本号</th><th style="width:150px">更新时间</th><th style="width:150px">更新内容</th></tr></thead><tbody><tr><td>v1.0.1</td><td>2019.10.23</td><td>参数表格修改</td>
  <tr><td>v1.0.0</td><td>2019.09.05</td><td>全文添加</td></tbody></table>



