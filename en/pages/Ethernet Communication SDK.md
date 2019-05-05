Ethernet Communication SDK
=========

## Instruction

*   the api provides a user-friendly interface that includes serial or ethernet communication (recommended) with multiple innfos actuators to send commands to multiple actuators simultaneously or to obtain actuator status and parameter information.
*   it is recommended that users who are new to the api should read the examples in the sdk first.

## Sdk download and directory description


#### download

*   visit the link download link to[download link](https://github.com/innfos/ActuatorController_SDK.git)•	download the sdk related files or execute the following command directly


```sh
$ git clone https://github.com/innfos/ActuatorController_SDK.git
```
    
## API related documentation

*   notes and related documentation please go to document link[document link](http://innfos.com/doc/index.html)

## SCA connection

<img src="../img/connect2.png" style="width:600px">

Connect the device as shown above and turn it on again. 
Warning: do not plug or unplug all cables with electricity, otherwise the device may be damaged.

## Environment configuration and sample code compilation run

### linux

#### environment configuration

Please refer to<a href="#!pages/Ethernet_Configuration.md#linux平台环境配置">the Linux environment configuration</a>


#### Sample code compilation

* open the terminal and go to the`…\example`example directory, which has`CMakeLists.txt`

```bash
$ cmake CMakeLists.txt
$ make
```

*   after the input command is executed, a bin folder is generated in this directory, which stores the generated sample program.
*   after confirming that the actuator is properly connected and powered, the actuator will flash yellow and the sample code can be tested.

#### Sample program test

*   after proper connection and powered on, sca will flash yellow and can be tested the sample code

##### find connected actuators

*   open the terminal and enter the bin directory, enter the command

```bash
$./lookupActuators -e
```
*   this window will display the number of currently connected actuators. You can end the program with`ctrl+c`

<img src="../img/022.png" style="width:600px">

**code description**

*   select different communication methods according to different parameters. The default is ethernet communication.

Note:the controller must be initialized before other operations can be performed.

``` cpp
//initialize controller
if(strcmp(argv[1],"-s")==0)
    ActuatorController::initController(Actuator::Via_Serialport);
elseif(strcmp(argv[1],"-e")==0)
    ActuatorController::initController();
```
*   associate the operation completion signal. After the user operates successfully, the signal will be triggered. According to different operationtype, the corresponding operation will be performed. In this example, the number of identified actuators will be printed after the automatic identification is completed.

``` cpp
//associated controller operation signal
int nOperationConnection = pController->m_sOperationFinished->s_Connect([=](uint8_t nDeviceId,uint8_t operationType){
   switch (operationType) {
   case Actuator::Recognize_Finished://automatic identification completed
       if(pController->hasAvailableActuator())
        {
            vector<uint8_t> idArray = pController->getActuatorIdArray();
            cout <<"Number of connected actuators:" << idArray.size() << endl;
        }
       break;
   default:
       break;
    }
});
```
*   the complete application must be associated with an error signal in order to receive feedback and respond accordingly when an error occurs inside the actuator. When`nDeviceId`is 0, the error is not specific to the actuator (eg unconnected error)
```cpp
//associated error signal
int nErrorConnection = pController->m_sError->s_Connect([=](uint8_t nDeviceId,uint16_t nErrorType,string errorInfo){
   if(nDeviceId==0)
    {
        cout <<"Error: " << (int)nErrorType <<" " << errorInfo << endl;
    }
   else
    {
        cout <<"Actuator " << (int)nDeviceId <<" " <<"error " << (int)nErrorType <<" " << errorInfo << endl;
    }
});
```

*   after the necessary signals are associated, the next corresponding operation is to identify the connected actuators.

```cpp
//automatically identify connected actuators
pController->autoRecoginze();
```

*   The event loop is a necessary step to ensure the internal communication of sdk. It is necessary to ensure that the event loop is not blocked so that sdk can trigger various signals.

```cpp
//execution controller event loop
while (!bExit)
{
    ActuatorController::processEvents();
}
```

*   finally disconnect the signal from all signals before the end of the program

```cpp
//disconnect the signal
pController->m_sOperationFinished->s_Disconnect(nOperationConnection);
pController->m_sError->s_Disconnect(nErrorConnection);

```

##### monitor actuator status

*   open the terminal, go to the `example/bin` directory, enter the command

```bash
$./monitorActuator -e
```

*   the actuator id is the `Actuator ID`, the attribute id is the monitored executor `attribute ID`, and the attribute value is the corresponding `attribute value`. You can end the program with `ctrl+c`

<img src="../img/023.png" style="width:600px">

**code description**

*   all actuators are automatically turned on after automatic recognition. After each actuator is successfully turned on, the actuator::launch_finished signal is triggered. When all actuators are turned on, automatic refresh is started and the actuator data is read.

```cpp
int nLaunchedActuatorCnt =0;
//associated controller operation signal
int nOperationConnection = pController->m_sOperationFinished->s_Connect([&amp;](uint8_t nDeviceId,uint8_t operationType){
   switch (operationType) {
   case Actuator::Recognize_Finished://automatic identification completed
       if(pController->hasAvailableActuator())
        {
            vector<uint8_t> idArray = pController->getActuatorIdArray();
        cout <<"Number of connected actuators:" << idArray.size() << endl;
           for (uint8_t id: idArray) {
               if(pController->getActuatorAttribute(id,Actuator::ACTUATOR_SWITCH)==Actuator::ACTUATOR_SWITCH_OFF)
                {//Start the SCA if it is off
                    pController->launchActuator(id);
                }
               else
                {
                    ++ nLaunchedActuatorCnt;
                   if(nLaunchedActuatorCnt == pController->getActuatorIdArray().size())//all actuators have been started
                    {
                        autoRefresh();
                    }
                }
            }
        }
       break;
   case Actuator::Launch_Finished:
       if(++nLaunchedActuatorCnt == pController->getActuatorIdArray().size())//all actuators have been started
        {
            autoRefresh();
        }
       break;
   default:
       break;
    }
});
```

*   In order to monitor the change of the properties of the actuator, the signal`m_sActuatorAttrChanged`is required. When the user requests to read the properties of the actuator, a successful return will trigger the signal.

    
	
```cpp
//actuator attribute change signal controlled by the associated controller
int nAttrConnection =pController->m_sActuatorAttrChanged->s_Connect([=](uint8_t nDeviceId,uint8_t nAttrId,double value){
    cout <<"Actuator ID: " << (int)nDeviceId << endl;
    cout <<"atribute ID: " << (int)nAttrId << endl;
    cout <<"atribute value: " << value << endl;
    cout <<"----------------------------"<<endl;
});
```

#### control actuator

*   open the terminal, go to the `example/bin`directory, enter the command

```bash
$./operateActuator -e
```

<img src="../img/024.png" style="width:600px">


*   indicate that the actuator has been found. Enter the command  `l 0 ` to start all connected actuators. If the startup is successful, the actuator will flash green, indicating successful startup. The terminal window is displayed as follows.

<img src="../img/025.png" style="width:600px">

*  the corresponding mode of sca can be activated at this time. For example, input ` a 6`can activate the profile position mode, then input `p 5`, the actuator will rotate to 5 positions; input`a 7` can activate the `profile velocity` mode, then enter`v 500`, execute the device will rotate at 500rpm and stop rotating input`v 0`; input `a 1` can activate current mode, then input `c 0.6`, the actuator will rotate at a constant current of 0.6a (if the actuator does not move, you can gently turn it with your hand) actuator), you can `ctrl+c` and then`ctrl+d`to end the program (because there are multiple threads waiting for keyboard input) 

    
<img src="../img/026.png" style="width:600px">
     

**code description**

*   the actuator can be operated after successfully started. `getActuatorIdArray` can get the short id of all actuators. The user can specify any id and operate. The actuator has multiple modes such as speed, current and position （`Actuator::ActuatorMode`）. The corresponding mode must be activated before the corresponding operation can be performed.


```cpp
 vector<uint8_t> idArray = controllerInst->getActuatorIdArray();
switch (directive)
{
case'a'://Activate actuator specified mode, command format: a mode id (actuator::actuatormode)
    controllerInst->activeActuatorMode(idArray, Actuator::ActuatorMode((int)value));
   break;
case'p'://specify the actuator position, command format: p laps (-127 to 127)
   for (int i =0; i < idArray.size(); ++i)
    {
        controllerInst->setPosition(idArray.at(i), value);
    }
   break;
case'c'://Specify actuator current, command format: c current value（A）
   for (int i =0; i < idArray.size(); ++i)
    {
        controllerInst->setCurrent(idArray.at(i), value);
    }
   break;
case'v'://Specify actuator speed, command format: v speed value（RPM）
   for (int i =0; i < idArray.size(); ++i)
    {
        controllerInst->setVelocity(idArray.at(i), value);
    }
   break;
case'l'://Start the specified executor, the format of the instruction: l executor id (id is 0 to start all actuators)
   if(uint8_t(value)==0)
    {
        controllerInst->launchAllActuators();
    }
   else
    {
        controllerInst->launchActuator(uint8_t(value));
    }
   //cout << "launch"<<endl;
   break;
case's'://Close the specified executor, the format of the instruction: l executor id (id is 0 to start all actuators)

   if(uint8_t(value)==0)
    {
        controllerInst->closeAllActuators();
    }
   else
    {
        controllerInst->closeActuator(uint8_t(value));
    }
   //cout << "close"<<endl;
   break;
default:
   break;
}
```

#### controller parameter adjustment

*   open the terminal, go to the`example/bin`directory, enter the command

```bash
$./tuneActuator -e
```

*  this sample program automatically starts the actuator and sets the position loop output to 3000 rpm, and the maximum current output of the speed loop is 16.5a.

If you use the `profile position` mode to rotate the actuator, the maximum speed of the actuator will not exceed 3000rpm; if you use the `profile velocity` mode to rotate the actuator, the maximum current of the actuator will not exceed 16.5a, you can end the program with `ctrl+c`

  
    
<img src="../img/027.png" style="width:600px"> 
    
**code description**
    

*   •	This sample program automatically starts the actuator. After successful startup, the actuator properties can be adjusted. The speed loop current output adjusts the actuator torque under the speed loop. The position loop speed output adjusts the speed of the position loop. See the sca quick start instructions for details.

    
    
```cpp
//Actuator property adjustment, the adjustment is successful, will trigger the actuator property change signal

void tuneActuator()
{
    ActuatorController * pController = ActuatorController::getInstance();
    vector<uint8_t> idArray = pController->getActuatorIdArray();
   for (uint8_t id: idArray) {
       //adjust actuator speed loop minimum current output
        pController->setMinOutputCurrent(id,-10);
       //adjust actuator speed loop maximum current output
        pController->setMaxOutputCurrent(id,10);
       //adjust actuator position loop minimum speed output
        pController->setMinOutputVelocity(id,-2000);
       //adjust the maximum speed output of the actuator position loop, the maximum value is greater than the minimum value	
        pController->setMaxOutputVelocity(id,2000);
       //mode_profile_pos Mode_Profile_Posadjust the maximum speed（RPM）
        pController->setActuatorAttribute(id,Actuator::PROFILE_POS_MAX_SPEED,1000);
    }
}
```

#### actuator zero

*   open the terminal, go to the`example/bin`directory, enter the command

```bash
$./homingActuator -e
```


*   indicate that the current position of the actuator has been set to zero, the range is -9.5r to 9.5r, and the position limit is turned on. If the position is outside the range in the `profile position` mode, the actuator will not rotate, `ctrl+c` end program
 

<img src="../img/028.png" style="width:600px">

**code description**

*   after the autostart is completed, `setHomingPosition` sets the current position `getActuatorAttribute(id,Actuator::ACTUAL_POSITION)` to 0, `setMaxPosLimit` and `setMinPosLimit` sets the maximum and minimum position limits, `setActuatorAttribute(id,Actuator::POS_OFFSET,0.5)` set the limit offset.
	
```cpp
    //actuator 0 bit and limit adjustment
void setActuatorLimitation()
{
    ActuatorController * pController = ActuatorController::getInstance();
    vector<uint8_t> idArray = pController->getActuatorIdArray();
   for (uint8_t id : idArray) {
       //the current position of the actuator is changed to 0, and the minimum and maximum positions are set to -10, 10, the offset is set to 0.5, and the actuator's range of motion becomes (-9.5, 9.5).
        pController->setHomingPosition(id,pController->getActuatorAttribute(id,Actuator::ACTUAL_POSITION));
        pController->setMinPosLimit(id,-10);
        pController->setMaxPosLimit(id,10);
        pController->setActuatorAttribute(id,Actuator::POS_OFFSET,0.5);
    }
    bSetLimitation =true;
}
```

*   the parameter setting is completed and the parameters are saved. Otherwise, the parameter settings will be discarded after shutdown.

```cpp
pController->saveAllParams(nDeviceId);
```

#### actuator length id

*   open the terminal and enter the`example/bin`directory, enter the command

```bash
$./longIdAndByteId -e
```

*   it is possible to acquire and convert long and short ids, and to obtain communication ip addresses by long id.

**code description**

*   the signal variable ends with an l. The signal is associated with the actuator length id and can be communicated with a long id. The difference between the long and short id is that the long id contains the communication address and the short id, and can be converted to each other (if different ip addresses have the same short id executor, the short id conversion long id will randomly convert one long under one ip address id).
    

```cpp
//associated controller's longid operation signal
int nOperationConnection = pController->m_sOperationFinishedL->s_Connect([&amp;](uint64_t nDeviceId,uint8_t operationType){
   switch (operationType) {
   case Actuator::Recognize_Finished://automatic identification completed
       if(pController->hasAvailableActuator())
        {
           //get the longid array get the longid array
            vector<uint64_t> longIdArray = pController->getActuatorLongIdArray();
           //get the byteid array
            vector<uint8_t> idArray = pController->getActuatorIdArray();
           for (uint64_t id: longIdArray) {
           //get the communication ip address in the long id
                cout <<"Communication IP is " << pController->toString(id) << endl;
               //convert longid to byteid
                cout <<"Long id " << id <<" convert to byte id " << (int)pController->toByteId(id) << endl;
            }
           for(uint8_t id : idArray)
            {
               //convert byteid to longid
                cout <<"Byte id " << (int)id <<" convert to long id " << pController->toLongId(id) << endl;
            }
        }
       break;
   default:
       break;
    }
});
```

#### synchronous response

* open the terminal and enter the `example/bin`directory, enter the command

```bash
$./feedback_sync -e
```

*   getactuatorattributewithack and setactuatorattributewithack are the interfaces of the two synchronous responses provided by sdk. Corresponding to getactuatorattribute and setactuatorattribute, the properties of the executor can be get synchronously. Calling getactuatorattributewithack and setactuatorattributewithack will block the current program until the result is returned (regardless of success or failure).

**code description**

*   `getActuatorAttributeWithACK` and `setActuatorAttributeWithACK`are the interfaces of the two synchronous responses provided by sdk. Corresponding to`getActuatorAttribute` and `setActuatorAttribute`，you can get or set the properties of the executor synchronously. Calling`getActuatorAttributeWithACK` and `setActuatorAttributeWithACK`will block the current program until the result is returned (regardless of success or failure).

```cpp

ActuatorController * pController = ActuatorController::getInstance();
    vector<uint8_t> idArray = pController->getActuatorIdArray();
   for (uint8_t id: idArray) {
       bool bSuccess =false;
       //read current and wait for return if read fails bsuccess is false
       double current = pController->getActuatorAttributeWithACK(id,Actuator::ACTUAL_CURRENT,&amp;bSuccess);
       if(bSuccess)
            cout <<"current is " << current << endl;
       //Set the maximum current output of the speed loop and wait for the return. If the setting fails, the value of bsuccess is false. (this interface cannot be used to set speed, position, current)
        bSuccess = pController->setActuatorAttributeWithACK(id,Actuator::VEL_OUTPUT_LIMITATION_MAXIMUM,10);
       if(bSuccess)
            cout <<"Set VEL_OUTPUT_LIMITATION_MAXIMUM to 10A" << endl;
    }
```

### windows

#### environment configuration


Please refer to the <a href="#!pages/Ethernet_Configuration.md#windows平台环境配置"> windowsenvironment configuration</a>


#### •	Sample code compilation

*   run cmake-gui to appear as the right interface:
*   the source path is `…\example` in the directory structure, containing the cmakelists.txt file. The build path can be customized, being used to generate the project file. After the path is configured, click the generate button to pop up the following interface.

<img src="../img/011.png" style="width:600px">


*   if the red box is not a 64-bit generator, click on the drop-down triangle, select the 64-bit generator, and then click the finish button. Once successful, the visual studio project file will be formed and can be compiled with visual studio. Compiling the complete project to generate a bin directory, there is a debug or release folder (corresponding to the compiled version), the file in the directory structure `…\sdk\lib\windows_x64\debug`或`…\sdk\lib\windows_x64\release` is copied to the debug or release directory under the bin of the corresponding version. Double-clicking the exe in the directory will run the sample program normally.

<img src="../img/012.png" style="width:600px">


#### Sample program test


##### Find connected actuators

*    after confirming that the actuator is properly connected and powered, the actuator will flash yellow and the sample code can be tested.

Open a command line window and go to the bin directory, enter the command ./lookupactuators.exe -e


```bash
./lookupActuators.exe -e 
```


<img src="../img/013.png" style="width:600px">


##### •	Monitor actuator status


*   open a command line window and go to the bin directory and enter the command ./monitoractuator.exe -e

```bash
./monitorActuator.exe -e
```


<img src="../img/014.png" style="width:600px">


##### Control sca


*   open a command line window, go to the bin directory and enter the command 


```bash
./operateActuator.exe -e
```

<img src="../img/015.png" style="width:600px">


This indicates that the actuator has been found. Enter the command l 0 to start all connected scas. If startup is successful, the actuator will flash green, the cmd window is displayed as shown below.


<img src="../img/016.png" style="width:600px">


*    the corresponding mode of sca can be activated at this time,for example, input a 6 can activate profile position mode, then inputting p 10 will lead to rotate to 10 turns; input a 7 can activate profile velocity mode, then input v 500, sca will rotate at 500rpm and stop rotating input v0; input a 1 can activate current mode, then input c 0.6, the actuator will rotate at a constant current of 0.6a (if the actuator does not move, you can gently turn it with your hand) actuator), the program will be ended with ctrl+c.


<img src="../img/017.png" style="width:600px">


##### Actuator parameter adjustmen

*   open a command line window, go to the bin directory and enter the command 

```bash
./tuneActuator.exe -e
```

*   this sample program will automatically starts the actuator and sets the position loop output to 3000 rpm. The maximum current output of the speed loop is 16.5 a. If the actuator is rotated using the `profile position` mode, the maximum speed of the actuator will not exceed 3000 rpm; if `profile velocity` is used mode rotation actuator, the maximum current of the actuator will not exceed 16.5a, and the program can be terminated by `ctrl+c`.

<img src="../img/018.png" style="width:600px">

##### Sca zero

*   open a command line window, go to the bin directory and enter the command

```bash
./homingActuator.exe -e
```

*   as shown in the figure, the current position of the actuator has been set to zero, the range is -9.5r to 9.5r, and the position limit is turned on if the `profile position` mode, enter a position outside this range, the actuator will not rotate, the program can be ended with`ctrl+c`


<img src="../img/LongId_w.png" style="width:600px">


##### Sca length id


*   open a command line window, go to the bin directory, enter the command

```bash
./longIdAndByteId.exe -e
```

The acquisition of the length id and the mutual conversion can be performed, and the communication ip address can be obtained by the long id.

<img src="../img/Feedback_w.png" style="width:600px">

##### 	Synchronous response

*   open a command line window, go to the bin directory and enter the command

```bash
./feedback_sync.exe -e
```

*   run`feedback_sync.exe`，to associate the corresponding signal. The operation in the callback is an asynchronous response and does not block the current program. Synchronous response will block the current program until sdk returns the result. In comparison, the synchronous response is simple but inefficient because it needs to wait for the actuator response (and the actuator part does not have a synchronous response, such as setting position, speed, current etc.) If the efficiency requirements are high, an asynchronous response is recommended.

## SDK instructions

### overview

*   SDK provides an interface for communication with the actuator. It can search, status query, property adjustment and custom control of the connected actuator through serial port or ethernet. If you want to quickly understand the basic content and usage of sdk, please see the relevant code in example/src

### Use sdk in the project


*   this sdk follows the `c++11` standard, so make sure the compile option supports `c++11`（before building the project (eg -std=c++11 in gcc);
*   the basic steps to integrate sdk into your project (preferably refer to cmakelists.txt in example):
*   add sdk/include, sdk/include/asio to the project's include directory to associate methods in the shared library;
*   the library file directory sdk/lib/linux_x86_64 (the windows directories are sdk/lib/debug and sdk/lib/release) so that the executable can be linked to the shared library and the runtime can be associated with the shared library;
*   add the necessary elements to the build process (such as target_link_libraries in cmake)

### Namespaces


* the namespace actuator is defined in ../sdk/include/`Actuator` define.h and enumerates all the types and type values used in sdk:

<table style="width:600px"><thead><tr><th colspan="2" style=background:PaleTurquoise>Connection status for connection status determination of actuator and can[ConnectStatus]</th></tr></thead><tbody>
 <tr><td>command byte</td><td>description</td></tr> <tr><td>NO_CONNECT,</td><td>no connection</td></tr> <tr><td>CAN_CONNECTED=0x02,</td><td>CANcommunication connection succeeded</td></tr> <tr><td>ACTUATOR_CONNECTED=0x04,</td><td>actuator connection succeeded</td></tr></tbody></table>

<table style="width:600px">
<thead><tr class="tableizer-firstrow"><th  colspan="2" style=background:PaleTurquoise>Channel id, the channel index used to identify the actuator chart data[Channel_ID]</th></tr></thead><tbody>
 <tr><td>command byte</td><td>description</td> <tr><td>channel_1=0,</td><td>Chart data 1 channel, given ideal curve</td></tr> <tr><td>channel_2,</td><td>Chart data 2 channels, actual current curve</td></tr> <tr><td>channel_3,</td><td>Chart data 3 channels, actual speed curve</td></tr> <tr><td>channel_4,</td><td>Chart data 4 channels, actual location</td></tr> <tr><td>channel_cnt</td><td></td></tr></tbody></table>

<table style="width:600px">
<thead><tr class="tableizer-firstrow"><th  colspan="2" style=background:PaleTurquoise>Error type definition, defines error codes such as actuator internals and connections[ErrorsDefine] </th></tr></thead><tbody>
 <tr><td>command byte</td><td>description</td> <tr><td>ERR_NONE = 0,</td><td>no error</td></tr> <tr><td>ERR_ACTUATOR_OVERVOLTAGE=0x01,</td><td>Actuator overvoltage error</td></tr> <tr><td>ERR_ACTUATOR_UNDERVOLTAGE=0x02,</td><td>Actuator undervoltage error</td></tr> <tr><td>RR_ACTUATOR_LOCKED_ROTOR=0x04,</td><td>Actuator locked error</td></tr> <tr><td>ERR_ACTUATOR_OVERHEATING=0x08</td><td>Actuator overheating error</td></tr> <tr><td>enum OnlineStatus{</td><td>Actuator read or write error</td></tr> <tr><td>ERR_ACTUATOR_MULTI_TURN=0x20,</td><td>Actuator multi-turn count error</td></tr> <tr><td>ERR_INVERTOR_TEMPERATURE_SENSOR=0x40,</td><td>Actuator inverter temperature error</td></tr> <tr><td>ERR_CAN_COMMUNICATION=0x80,</td><td>Actuator inverter temperature error</td></tr> <tr><td>ERR_ACTUATOR_TEMPERATURE_SENSOR=0x100,</td><td>执行器 CAN 通信错误</td></tr> <tr><td>ERR_DRV_PROTECTION=0x400,</td><td>执行器 DRV 保护</td></tr> <tr><td>ERR_ID_UNUNIQUE=0x800</td><td>执行器 ID 不唯一错误</td></tr> <tr><td>ERR_ACTUATOR_DISCONNECTION=0x801,</td><td>执行器未连接错误</td></tr> <tr><td>ERR_CAN_DISCONNECTION=0x802,</td><td>CAN 通信转换板未连接错误</td></tr> <tr><td>ERR_IP_ADDRESS_NOT_FOUND=0x803,</td><td>无可用 ip 地址错误</td></tr> <tr><td>ERR_ABNORMAL_SHUTDOWN=0x804,</td><td>执行器非正常关机错误</td></tr> <tr><td>ERR_SHUTDOWN_SAVING=0x805,</td><td>执行器关机时参数保存错误</td></tr> <tr><td>ERR_UNKOWN=0xffff</td><td>未知错误</td></tr></tbody></table>

<table style="width:600px">
<thead><tr class="tableizer-firstrow"><th colspan="2"style=background:PaleTurquoise>在线状态，用于标识执行器是否处于连接状态[OnlineStatus]</th></tr></thead><tbody>
 <tr><td>指令符</td><td>说明</td></tr> <tr><td>Status_Online=0x00,</td><td>执行器在线</td></tr> <tr><td>Status_Offline=0x01,</td><td>执行器离线</td></tr></tbody></table>

<table style="width:600px">
<thead><tr class="tableizer-firstrow"><th colspan="2"style=background:PaleTurquoise>开关状态，标识执行器的开关机状态[SwitchStatus]</th></tr></thead><tbody>
 <tr><td>指令符</td><td>说明</td></tr> <tr><td>ACTUATOR_SWITCH_OFF=0,</td><td>执行器已关机</td></tr> <tr><td>ACTUATOR_SWITCH_ON=1,</td><td>执行器已开机</td></tr></tbody></table>

<table style="width:600px">
<thead><tr class="tableizer-firstrow"><th colspan="2"style=background:PaleTurquoise>图表开关，用于标识执行器图表功能的开启或关闭[ChartSwitchStatus]</th></tr></thead><tbody>
 <tr><td>指令符</td><td>说明</td></tr> <tr><td>CHART_SWITCH_OFF=0,</td><td>图表功能关闭，不会产生图表数据</td></tr> <tr><td>CHART_SWITCH_ON=1,</td><td>图表功能开启，触发图表阈值会产生图表数据</td></tr></tbody></table>

<table style="width:600px">
<thead><tr class="tableizer-firstrow"><th colspan="2"style=background:PaleTurquoise>电流环图表索引，用于标识电流图表是IQ值还是ID值[CurrnetChart]</th></tr></thead><tbody>
 <tr><td>指令符</td><td>说明</td></tr> <tr><td>IQ_CHART=0,</td><td>图表数据2通道，实际电流IQ曲线</td></tr> <tr><td>ID_CHART=1,</td><td>图表数据2通道，实际电流ID曲线</td></tr></tbody></table>

<table style="width:600px">
<thead><tr class="tableizer-firstrow"><th colspan="2"style=background:PaleTurquoise>通信方式，可通过以太网或者串口两种方式与执行器通信，初始化执行器控制器时候要指定方式，默认为以太网通信[CommunicationType]</th></tr></thead><tbody>
 <tr><td>指令符</td><td>说明</td></tr> <tr><td>Via_Ethernet,</td><td>以太网通信</td></tr> <tr><td>Via_Serialport,</td><td>串口通信</td></tr></tbody></table>

<table style="width:600px">
<thead><tr class="tableizer-firstrow"><th colspan="2"style=background:PaleTurquoise>操作标识，标识操作完成，可用于判断执行器控制器的指令执行状态[OperationFlags]</th></tr></thead><tbody>
 <tr><td>指令符</td><td>说明</td></tr> <tr><td>Recognize_Finished</td><td>识别完成</td></tr> <tr><td>Launch_Finished</td><td>执行器启动完成（如果连接的是多个执行器，会触发多次启动完成信号）</td></tr> <tr><td>Close_Finished</td><td>执行器关闭完成（如果连接的是多个执行器，会触发多次关闭完成信号）</td></tr> <tr><td>Save_Params_Finished</td><td>执行器参数保存完成（如果连接的是多个执行器，会触发多次参数保存完成信号）</td></tr> <tr><td>Save_Params_Failed</td><td>执行器参数保存失败</td></tr> <tr><td>Attribute_Change_Finished</td><td>暂未实现</td></tr></tbody></table>

<table style="width:600px">
<thead><tr class="tableizer-firstrow"><th colspan="2"style=background:PaleTurquoise>执行器模式，标识当前执行器的模式[ActuatorMode]</th></tr></thead><tbody>
 <tr><td>指令符</td><td>说明</td></tr> <tr><td>Mode_None</td><td>&nbsp;</td></tr> <tr><td>Mode_Cur</td><td>电流模式</td></tr> <tr><td>Mode_Vel</td><td>速度模式</td></tr> <tr><td>Mode_Pos</td><td>位置模式</td></tr> <tr><td>Mode_Teaching</td><td>暂未实现</td></tr> <tr><td>Mode_Profile_Pos=6</td><td>profile位置模式，比较于位置模式，该模式有加速减速过程</td></tr> <tr><td>Mode_Profile_Vel</td><td>profile速度模式，比较于速度模式，该模式有加速减速过程</td></tr> <tr><td>Mode_Homing</td><td>归零模式</td></tr></tbody></table>

<table style="width:600px">
<thead><tr class="tableizer-firstrow"><th colspan="2"style=background:PaleTurquoise>执行器属性，标识了执行器所有相关属性[ActuatorAttribute]</th></tr></thead><tbody>
 <tr><td>指令符</td><td>说明</td></tr> <tr><td>CUR_IQ_SETTING</td><td>电流IQ值</td></tr> <tr><td>CUR_PROPORTIONAL</td><td>电流比例</td></tr> <tr><td>CUR_INTEGRAL</td><td>电流积分</td></tr> <tr><td>CUR_ID_SETTING</td><td>电流ID值</td></tr> <tr><td>CUR_MINIMUM</td><td>预留</td></tr> <tr><td>CUR_MAXIMUM</td><td>预留</td></tr> <tr><td>CUR_NOMINAL</td><td>预留</td></tr> <tr><td>CUR_OUTPUT</td><td>预留</td></tr> <tr><td>CUR_MAXSPEED</td><td>电流环最大速度</td></tr> <tr><td>ACTUAL_CURRENT</td><td>当前电流值</td></tr> <tr><td>VEL_SETTING</td><td>速度设置</td></tr> <tr><td>VEL_PROPORTIONAL</td><td>速度比例</td></tr> <tr><td>VEL_INTEGRAL</td><td>速度积分</td></tr> <tr><td>VEL_OUTPUT_LIMITATION_MINIMUM</td><td>速度环输出最小电流比例</td></tr> <tr><td>VEL_OUTPUT_LIMITATION_MAXIMUM</td><td>速度环输出最大电流比例</td></tr> <tr><td>ACTUAL_VELOCITY</td><td>速度值</td></tr> <tr><td>POS_SETTING</td><td>位置设置</td></tr> <tr><td>POS_PROPORTIONAL</td><td>位置比例</td></tr> <tr><td>POS_INTEGRAL</td><td>位置积分</td></tr> <tr><td>POS_DIFFERENTIAL</td><td>位置微分</td></tr> <tr><td>POS_OUTPUT_LIMITATION_MINIMUM</td><td>位置环输出最小速度比例</td></tr> <tr><td>POS_OUTPUT_LIMITATION_MAXIMUM</td><td>位置环输出最大速度比例</td></tr> <tr><td>POS_LIMITATION_MINIMUM</td><td>最小位置限制</td></tr> <tr><td>POS_LIMITATION_MAXIMUM</td><td>最大位置限制</td></tr> <tr><td>HOMING_POSITION</td><td>归零位置</td></tr> <tr><td>ACTUAL_POSITION</td><td>当前位置</td></tr> <tr><td>PROFILE_POS_MAX_SPEED</td><td>profile position 模式最大速度</td></tr> <tr><td>PROFILE_POS_ACC</td><td>profile position 模式加速度</td></tr> <tr><td>PROFILE_POS_DEC</td><td>profile position 模式减速速度</td></tr> <tr><td>PROFILE_VEL_MAX_SPEED</td><td>profile velocity 模式最大速度</td></tr> <tr><td>PROFILE_VEL_ACC</td><td>profile velocity 模式加速度</td></tr> <tr><td>PROFILE_VEL_DEC</td><td>profile velocity 模式减速速度</td></tr> <tr><td>CHART_FREQUENCY</td><td>图像频率</td></tr> <tr><td>CHART_THRESHOLD</td><td>图像阈值</td></tr> <tr><td>CHART_SWITCH</td><td>图像开关</td></tr> <tr><td>POS_OFFSET</td><td>位置偏移</td></tr> <tr><td>VOLTAGE</td><td>电压</td></tr> <tr><td>POS_LIMITATION_SWITCH</td><td>开启或关闭位置限制</td></tr> <tr><td>HOMING_CUR_MAXIMUM</td><td>归零最大电流</td></tr> <tr><td>HOMING_CUR_MINIMUM</td><td>归零最小小电流</td></tr> <tr><td>CURRENT_SCALE</td><td>物理最大电流值</td></tr> <tr><td>VELOCITY_SCALE</td><td>速度最大电流值</td></tr> <tr><td>FILTER_C_STATUS</td><td>电流环滤波是否开启</td></tr> <tr><td>FILTER_C_VALUE</td><td>电流环滤波值</td></tr> <tr><td>FILTER_V_STATUS</td><td>速度环滤波是否开启</td></tr> <tr><td>FILTER_V_VALUE</td><td>速度环滤波值</td></tr> <tr><td>FILTER_P_STATUS</td><td>位置环滤波是否开启</td></tr> <tr><td>FILTER_P_VALUE</td><td>位置环滤波值</td></tr> <tr><td>INERTIA</td><td>惯量</td></tr> <tr><td>LOCK_ENERGY</td><td>堵转保护能量</td></tr> <tr><td>ACTUATOR_TEMPERATURE</td><td>执行器温度</td></tr> <tr><td>INVERTER_TEMPERATURE</td><td>逆变器温度</td></tr> <tr><td>ACTUATOR_PROTECT_TEMPERATURE</td><td>执行器保护温度</td></tr> <tr><td>ACTUATOR_RECOVERY_TEMPERATURE</td><td>执行器恢复温度</td></tr> <tr><td>INVERTER_PROTECT_TEMPERATURE</td><td>逆变器保护温度</td></tr> <tr><td>INVERTER_RECOVERY_TEMPERATURE</td><td>逆变器恢复温度</td></tr> <tr><td>CALIBRATION_SWITCH</td><td>预留</td></tr> <tr><td>CALIBRATION_ANGLE</td><td>预留</td></tr> <tr><td>ACTUATOR_SWITCH</td><td>执行器开关机</td></tr> <tr><td>FIRMWARE_VERSION</td><td>执行器固件版本</td></tr> <tr><td>ONLINE_STATUS</td><td>执行器是否在线</td></tr> <tr><td>DEVICE_ID</td><td>执行器 Id</td></tr> <tr><td>SN_ID</td><td>执行器 SN 号</td></tr> <tr><td>MODE_ID</td><td>执行器当前模式</td></tr> <tr><td>ERROR_ID</td><td>错误代码</td></tr> <tr><td>RESERVE_0</td><td>预留</td></tr> <tr><td>RESERVE_1</td><td>预留</td></tr> <tr><td>RESERVE_2</td><td>预留</td></tr> <tr><td>RESERVE_3</td><td>预留</td></tr> <tr><td>DATA_CNT</td><td>属性数量</td></tr> <tr><td>DATA_CHART</td><td>预留</td></tr> <tr><td>DATA_INVALID</td><td>非法属性值</td></tr></tbody></table>

## 版本信息

<table class="tableizer-table">
<thead><tr class="tableizer-firstrow"><th>版本</th><th>日期</th><th>修改内容</th></tr></thead><tbody>
 <tr><td>V2.0.0</td><td>2019-03-09</td><td>第二版本</td></tr> <tr><td>V1.0.0</td><td>2018-04-17</td><td>第一版本</td></tr></tbody></table>

