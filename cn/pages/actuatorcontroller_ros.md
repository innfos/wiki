# ActuatorController_ROS
独立的ROS包，只限用于INNFOS执行器。





## 安装说明
### ROS
请参照此网址安装您想要的ROS版本： http://wiki.ros.org/ 。

### 安装
此软件包已在Ubuntu 16.04 与 ROS Luna 上测试通过。

先在终端里进入catkin工作空间的文件夹
如果您在此工作空间里有用到C++的以太网通信SDK, 建议您不要把此软件包放在同一个工作空间中。
此软件包使用的是以太网通信SDK已修改版本，可能会导致软件链接错误。 
第一步，先下载软件包:
```
$ git clone https://github.com/Rayckey/ActuatorController_ROS.git actuatorcontroller_ros
```
返回工作空间目录下进行编译：
```
$ catkin_make
```
如果系统版本较老，软件包可能在第一次编译时失败，如出现此情况，可进行多次尝试。  
如果您开了新的终端，请记得在运行此包裹的节点/信息/服务前先 `source`此工作空间的配置文件：
```
$ source devel/setup.bash
```
也可将此命令写在本地`.bashrc` 文件中, 使新的终端在初始化时强制配置环境。
现在您可以使用我们的ROS节点了!




## 示例
如果您是第一次使用INNFOS的产品, 建议您先阅读INNFOS的wiki百科网站： https://innfos.github.io/wiki/en/#!index.md  
确保您的机器与ECB之间的连接没有问题之后，就可以运行节点了！

新开一个终端，启动 ROS core:
```
$ roscore
```
第一次使用，建议使用`rosrun`的方式启动节点, 再新开一个终端，然后输入:
```
$ rosrun actuatorcontroller_ros innfos_actuator
```
启动后，先使用 `/INNFOS/GeneralQuery` 的服务检查一遍所有连接的执行器是否都在线:
```
$ rosservice call /INNFOS/GeneralQuery "isQuery: true" 
```
会收到类似这样的回复：
```
ActuatorList: [2, 5]
ActuatorSwitch: [0, 0]
```
本例中, 有两个执行器连接到了机器上, ID分别为2与5, 两个执行器都没有开机。
下一步，用ROS message 将执行器都打开。把ID设为0既能选择全部打开。
```
$ rostopic pub -1 /INNFOS/enableActuator actuatorcontroller_ros/ActuatorArray "JointIDs:
- 0" 
``` 
请注意执行器本身的ID不能为0。  
也可直接选择性地只开启一两个执行器, 把 `JointIDs` 设成您想要的ID号码即可  
执行器刚刚开机时会直接进入电流模式, 可调用一个服务检查一个执行器当前的状态:
```
$ rosservice call /INNFOS/AttributeQuery "ActuatorID: 2"
``` 
会收到类似的回复：
```
ACTUAL_CURRENT: 0.00266915559769
ACTUAL_VELOCITY: -6.74343109131
ACTUAL_POSITION: -0.251586914062
MODE_ID: 1
ACTUATOR_SWITCH: True
ONLINE_STATUS: True
INIT_STATE: True
```
此`MODE_ID` 变量就是执行器当前的模式。
如果对一些变量不太熟悉，不用担心，您可以调用我们的服务查看变量的说明
```
$ rosservice call /INNFOS/Dictionary "LookupTerm:
  data: 'MODE_ID'" 
```
此节点会返回此变量的详细使用说明。
````
TermType: 
  data: "Integer"
isChangeable: True
TermExplanation: 
  data: "The control mode of the actuator currently in effect. Options include: Mode_Cur (1),\
  \ Mode_Vel(2), Mode_Pos(3), Mode_Profile_Pos(4), Mode_Profile_Vel(5), Mode_Homing(6)"
````
根据此说明，共有6种控制模式可供选择。 
在本例中，先试一下位置控制:
```
$ rostopic pub -1 /INNFOS/setControlMode actuatorcontroller_ros/ActuatorModes "JointIDs:
- 2
ActuatorMode: 4" 
``` 
将2号执行器切换至 `Mode_Profile_Pos`模式,这种位置控制模式自带梯形曲线路径规划
现在位置控制的指令生效:
```
$ rostopic pub -1 /INNFOS/setTargetPosition actuatorcontroller_ros/ActuatorCommand "JointID: 2
TargetValue: 0.0"
```
此时，执行器开始转动。
如果觉得转速过快，可通过`rosparam`调整执行器的内部参数
首先，检查执行器在`Mode_Profile_pos`模式中的加速度:
```
$ rosparam get /INNFOS/Actuator/2/PROFILE_POS_ACC
``` 
可能会收到：
```
2000.0
```
唔，有够快的，您可能看到的值不太一样，没关系，我们先把它设到比较温和的值:
```
$ rosparam set /INNFOS/Actuator/2/PROFILE_POS_ACC 800.0
```
如果设置成功，运行着节点的终端应该有以下输出：
```
[ INFO] [1566789998.845573133]: Change Parameter PROFILE_POS_ACC for actuator 2 to 800.000000
```
好，可以再改几个参数:
```
$ rosparam set /INNFOS/Actuator/2/PROFILE_POS_DEC -800.0
$ rosparam set /INNFOS/Actuator/2/PROFILE_POS_MAX_SPEED 1200
```
现在重新设置一个位置，看它的转速：
```
$ rostopic pub -1 /INNFOS/setTargetPosition actuatorcontroller_ros/ActuatorCommand "JointID: 2
TargetValue: 10.0"
```
下一步试试更改执行器的零位。首先，将执行器设置成模式`Mode_Homing`：
```
$ rostopic pub -1 /INNFOS/setControlMode actuatorcontroller_ros/ActuatorModes "JointIDs:
- 2
ActuatorMode: 6"
```
这样2号执行器就进入了可以更改零位的`Mode_Cur`. 如果现在查看此执行器的 `MODE_ID`，显示的数据可能为1,不必担心，可手动转到您想要的零位
完成后，请确保执行器的位置不变，同时调用服务:
```
$ rosservice call /INNFOS/ZeroReset "JointID: 2"
```
如果零位的设置成功, 服务会有以下的回复：
```
isSuccessful: True
```
零位更改后不要忘记更改软件限位：
```
$ rosparam set /INNFOS/Actuator/2/POS_LIMITATION_MAXIMUM 127
$ rosparam set /INNFOS/Actuator/2/POS_LIMITATION_MINIMUM -127
```
更改参数之后,若想下次开机时也生效，需要先把参数下载到执行器上:
```
$ rosservice call /INNFOS/ParametersSave "ActuatorID: 2"
``` 
与 `/INNFOS/ZeroReset` 的服务一样,您应该会看见类似这样的回复：
```
isSuccessful: True
```
基本功掌握好了，您可以接着看此ROS节点都能提供什么样的服务


## 启动节点
启动节点的方式有好几种。节点的基本功能不会变, 但是用户可以通过更改一些参数来更改节点的效率
### rosrun 默认参数
与示例中一样，这种方式会使用默认的参数。
```
$ roscore
$ rosrun actuatorcontroller_ros innfos_actuator
```

### roslaunch 更改参数
用户可以用launch文件来更改节点的效率，在这里的launch文件均为简单的说明，不同的选项可同时使用
```
$ roslaunch actuatorcontroller_ros innfos_no_param.launch
```
此 launch 文件 在ROS的参数空间中加入了 `innfos_no_param` 参数.
此参数会阻止节点把执行器的参数放在参数空间中，若不想在空间中出现太多参数，或者不想让别人更改执行器的参数，您可以使用此选项
```
$ roslaunch actuatorcontroller_ros innfos_fixed_100hz.launch
```
此 launch 文件 在ROS的参数空间中加入了 `innfos_fixed_rate` 参数
此参数强制节点以一定频率请求返回执行器参数。可通过选项来提高您的控制频率或者降低cpu负载。实际可达到的最高控制频率取决于连接方式
```
$ roslaunch actuatorcontroller_ros innfos_use_cvp.launch
```
此 launch 文件 在ROS的参数空间中加入了 `innfos_use_cvp` 参数
若此参数是 true, 控制器在请求执行器参数时会用更加高效的协议。 但这样反馈值会有控制回路的延迟。 此参数最好与`innfos_fixed_rate`参数一起使用，并设到较高的频率以减少延迟

请注意! 如果节点已经开始运行，那么加入这些参数是不会起作用的! 参数必须在节点启动前加入到参数空间中，可以写一个类似的launch文件把想要的参数放进去。=

## ROS 信息, 服务 & 参数
### INNFOS 执行器的参数
每个执行器的参数被分为4组:  
1.常用可更改参数 
2.常用不可更改参数
3.不常用可更改参数 
4.不常用不可更改参数
常用可更改参数可用ROS信息与服务来查询或更改,不常用可更改参数只能用参数空间更改.=。 不可更改的参数只能用ROS信息与服务来读取。
可查询信息或服务的类型:
```
$ rostopic type ${TOPIC_NAME}
$ rosservice type ${SERVICE_NAME}
```

### 发布的主题

#### /INNFOS/actuator_states (`sensor_msgs::JointState`)
提供所有已开机的执行器的位置，速度与电流，单位分别为：`Rotations`, `RPM`, 和 `Amp`。

### Subscribed Topics
#### /INNFOS/enableActuator (`ActuatorController_ROS::ActuatorArray`)
打开指定的执行器，若输入为空或0，打开所有的执行器。

#### /INNFOS/disableActuator (`ActuatorController_ROS::ActuatorArray`)
关闭指定的执行器，若输入为空或0，关闭所有的执行器。 

#### /INNFOS/setControlMode (` ActuatorController_ROS::ActuatorModes`)
给指定的执行器设定指定的模式, 可通过`/INNFOS/Dictionary`查询可用的模式

#### /INNFOS/setTargetPosition (`ActuatorController_ROS::ActuatorCommand`)
给指定的执行器设定目标位置，只有在执行器模式正确时才会生效。


#### /INNFOS/setTargetVelocity (`ActuatorController_ROS::ActuatorCommand`)
给指定的执行器设定目标速度，只有在执行器模式正确时才会生效。


#### /INNFOS/setTargetCurrent (`ActuatorController_ROS::ActuatorCommand`)
给指定的执行器设定目标电流，只有在执行器模式正确时才会生效。 


### Services
#### /INNFOS/GeneralQuery (`ActuatorController_ROS::GeneralQuery`)
Function: 给用户查看所有在线的执行器与其开机状态。
Input: 一个变量，不需要赋值。
Output: 在线的执行器与其开机状态的列表。

#### /INNFOS/AttributeQuery (`ActuatorController_ROS::AttributeQuery`)
Function: 给用户查看一些常用可更改参数。 请使用对应的信息或服务更改这些参数 。 
Input: 指定的执行器ID。
Output: 指定执行器的一部分常用可更改参数。

#### /INNFOS/TriviaQuery (`ActuatorController_ROS::TriviaQuery`)
Function: 给用户查看一些常用不可更改参数。
Input: 指定的执行器ID。
Output: 指定执行器的一部分常用不可更改参数。

#### /INNFOS/DebugQuery (`ActuatorController_ROS::DebugQuery`) 
Function: 给用户查看一些不常用不可更改参数。
Input: 指定的执行器ID。
Output: 指定执行器的一部分不常用不可更改参数。 检查硬件时使用。  

#### /INNFOS/Dictionary (`ActuatorController_ROS::AttributeDictionary`)
Function: 让用户查询参数的含义与使用方法  
Input: 参数名 (比如`MODE_ID`)  
Output: 参数的解释与使用方法

#### /INNFOS/IDChange (`ActuatorController_ROS::IDModify`)
Function: 更改一个执行器的ID 
Input: 原执行器ID与新执行器ID
Output: 一个Bool告知用户操作是否成功

#### /INNFOS/ParametersSave (`ActuatorController_ROS::ParametersSave`)
Function: 把更改的参数下载到执行器上，确保以后开机也能生效
Input: 指定的执行器ID
Output: 一个Bool告知用户操作是否成功    


#### /INNFOS/ZeroReset (`ActuatorController_ROS::ZeroReset`)
Function: 把当前的位置设置为执行器的零位，执行器当前必须被设置成`Mode_Homing`方能生效
Input: 指定的执行器ID
Output: 一个Bool告知用户操作是否成功  


### 参数空间
用户可在参数空间内查看或更改不常用可更改参数。
由于每个执行器都有自己的参数,参数空间中的名字以一下格式命名:  
```
/INNFOS/Actuator/${ACTUATOR_ID}/${PARAMETER_NAME}
```
您可使用 `/INNFOS/Dictionary`服务查看参数的定义
注意！更改后的参数必须靠服务 `/INNFOS/ParametersSave` 保存到执行器里，下次开机才会生效。
如果更改失败，参数空间里的参数会变回原来的值。


## Change logs

<table style="width:500px"><thead><tr style="background:PaleTurquoise"><th style="width:100px">Version number</th><th style="width:150px">Update time</th><th style="width:3800px">Update content</th></tr></thead><tbody><tr><td>v1.0.3</td><td>2019.08.26</td><td> More Examples</td></tr></thead><tbody><tr><td>v1.0.2</td><td>2019.08.21</td><td> Included an example in readme </td></tr></thead><tbody><tr><td>v1.0.1</td><td>2019.08.09</td><td>Added readme</td></tr></thead><tbody><tr><td>v1.0.0</td><td>2019.08.09</td><td>Node tested with actuators on Ubuntu 16.04 with ROS Luna, Stable release</td></tbody></table>
