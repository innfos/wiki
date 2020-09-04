Gluon ROS packages
=====


These packages support Moveit!, RViz and LAN communication with Gluon.

## Download and install
[Download](https://github.com/innfos/ros_gluon.git) ros packages for gluon

```sh
$ git clone https://github.com/innfos/ros_gluon.git
```
then manually copy package folders gluon gluon_control gluon_moveit_config and cm_moveit into a catkin_ws/src.

```sh
$ catkin_make
```


## Set up enviroment
Source all setup.bash files to set up your enviroment.

# System configure ROS environment variables automatically every time you open a ternimal
```sh
echo "source /opt/ros/melodic/setup.bash" >> ~/.bashrc
echo "source ~/catkin_ws/devel/setup.bash" >> ~/.bashrc
source ~/.bashrc
```

## Simulation and Control
Before ROS control, make sure that your manipulator is in the "homing" position. Connect your gluon to your Lan network(192.168.1.xxx)

If you are using a virtual machine running Linux, turn off graphics hardware acceleration, otherwise gazebo may not start properly.

### Rviz Control Mode:
Show the urdf model of gluon in rviz, then drag the scroll bar of each axis in rviz to control the movement of the manipulator.

roslaunch gluon display.launch

### Moveit+Rviz Control Mode:
Display the gluon model in rviz, then use the rviz interface of moveit to drag the manipulator for motion planning, click the "execute" button in moveit, and control the gluon to move with the virtual manipulator.
```sh
roslaunch gluon_moveit_config cm_demo.launch
```

### Moveit Tutorials
Cartesian Paths example and control gluon
```sh
roslaunch moveit_tutorials move_group_interface_tutorial.launch
```
