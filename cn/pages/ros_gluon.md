Gluon ROS软件包
=====

这些软件包支持Moveit！，RViz和与Gluon的LAN通信。

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
在进行ROS控制之前，请确保机械手处于"homing"位置。将您的胶子连接到局域网（192.168.1.xxx）

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
