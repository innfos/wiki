ROS For Gluon 
=====

## 介绍

*   本说明书是针对胶子系列的使用说明。
*   在使用之前请仔细阅读本说明书内容。

## 产品实拍效果图

以GL_6L3为例:

<img src="../../img/gloun.jpg" style="width:600px">
<img src="../../img/gloun1.jpg" style="width:600px">
<img src="../../img/gloun3.jpg" style="width:600px">
<img src="../../img/gloun2.jpg" style="width:600px">

## 硬件需求与连接

**硬件需求**

<img src="../../img/gloun15.jpg" style="width:600px">

从前到后、从左到右依次为：六轴机械臂一台、插好终端电阻和回馈制动电容的ECB、急停开关+电源、电脑。


**连接ECB**

**连接电源**

*   连接电源与`ECB`

<img src="../../img/gloun4.jpg" style="width:600px">
<img src="../../img/gloun5.jpg" style="width:600px">

**连接执行器及其配件**

*   连接`执行器综合线缆`

<img src="../../img/gloun8.jpg" style="width:600px">
<img src="../../img/gloun9.jpg" style="width:600px">

**连接机械臂**

*   用执行器连接线连接`ECB`与执行器

<img src="../../img/gloun10.jpg" style="width:600px">
<img src="../../img/gloun11.jpg" style="width:600px">

**连接电脑**

*   用网线连接`ECB`与电脑

<img src="../../img/gloun14.jpg" style="width:600px">

**连接后整体视图**

<img src="../../img/gloun17.jpg" style="width:600px">


**开启电源**

*   开启电源. 执行器的供电电压范围为直流24V-45V.

<img src="../../img/poweron.png" style="width:600px">

*   上电以后，执行器LED状态灯会变成黄色闪烁，启动执行器后，LED会变成绿色闪烁，这时就可以与执行器进行通信了。如果执行器内部出现错误，LED灯会变为红色闪烁，请检查执行器错误代码。





## 下载并安装
[下载](https://github.com/innfos/ros_gluon.git) ros 软件包

```sh
$ git clone https://github.com/innfos/ros_gluon.git
```
然后手动将软件包文件夹gluon gluon_control、gluon_moveit_config和cm_moveit复制到catkin_ws / src中。

```sh
$ catkin_make
```


## 搭建环境
source setup.bash 以设置您的环境。

## 每次打ternimal时，系统都会自动配置ROS环境变量
```sh
echo "source /opt/ros/melodic/setup.bash" >> ~/.bashrc
echo "source ~/catkin_ws/devel/setup.bash" >> ~/.bashrc
source ~/.bashrc
```

## 仿真与控制
在进行ROS控制之前，请确保机械手处于"homing"位置。将您的六轴连接到局域网（192.168.1.xxx）

如果您使用的是运行Linux的虚拟机，请关闭图形硬件加速，否则程序可能无法正常启动。

### Rviz 控制模式：
在rviz中显示六轴的urdf模型，然后在rviz中拖动每个轴的滚动条以控制操纵器的运动。
```sh
roslaunch gluon display.launch
```

### Moveit + Rviz控制模式：
在rviz中显示六轴模型，然后使用moveit的rviz界面拖动操纵器进行运动计划，单击moveit中的“执行”按钮，并控制六轴随虚拟操纵器一起运动。
```sh
roslaunch gluon_moveit_config cm_demo.launch
```

### Moveit教程
Cartesian Paths 示例和控制六轴
```sh
roslaunch moveit_tutorials move_group_interface_tutorial.launch
```
