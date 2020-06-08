## Introduction

*   INNFOS CAN SDK STM32 version provides user-friendly interfaces, including the function of communication between the STM32F429 single-chip microcomputer and INNFOS SCA, that can send commands to multiple actuators or retrieve actuator status and parameters. The project files are open source and could be customed and modified.

*    First runner of this API is highly recommended to read the readme.txt description file in the project folder.

----

## Download SDK

Visit [Download Link](https://github.com/innfos/INNFOS_CAN_SDK_STM32.git)to acquire the MDK project files.

----

## File structure

<img src="../../img/cansdk1.png" style="width:600px">
<br>

<div class="md-text" style="text-align: center;"></div>

*  `BSP`：STM 32 Peripheral Underlying driver files.
*  `CORE`：Cortex-M4 Kernel control file and STM32 startup file.
*  `FWLIB`：STM32 standard Peripheral driver library 
*  `MDK`：MDK project files
*  `SCA`：INNFOS CAN protocol driver files and codes for application examples.
*  `SYSTEM`：Common interfaces for the STM32 programming environment. 
*  `USER`：Storage for main.c. etc.
*  `Keilkiller.bat`：erase intermediate files during compiling
*  `readme.txt`：relevant descriptions
<br>

### SCA文件目录说明

<img src="../../img/cansdk2.png" style="width:600px">

<div class="md-text" style="text-align: center;"></div>

*  `SCA_Protocol.c/h`： INNFOS CAN communication protocol layer. This layer completes procedures like data frame packing and unpacking, using CAN interface to send and receive data.
*  `SCA_API.c/h`：Communication protocol layer package, including API reading and writing for all parameters.
*  `SCA_APP.c/h`：Demo program.
<br>

----

## Example of compiling and running codes

*  Keil MDK on your PC, project version V5.21.1.0. Single-chip microcomputer model `STM32F429IGT6`。

<img src="../../img/cansdk3.png" style="width:600px">
<br>

<div class="md-text" style="text-align: center;"></div>

*  Open file `SCA_Controller.uvprojx`under MDK folder, it will show user interface and `main.c` code of MDK.  
<img src="../../img/cansdk4.png" style="width:600px">
<br>

<div class="md-text" style="text-align: center;"></div>

*  2 actuators are adopted in this demo, actuator 1 (ID `0x01`) connects to `CAN1`, actuator 2 (ID `0x02`) connects `CAN2`. There are multiple sentences in `SCA_APP.c` that adopted these IDs. Please adjust the ID number according to the actuator(s) you are using. If only 1 actuator is connected, please put the surplus codes into comments and adjust macro definition of `SCA_NUM_USE` under `SCA_API.c` to 1.


```sh
void SCA_Init()
{
	/* Initialize CAN port */
	CAN_Port1.CanPort = 1;			//Mark the port number
	CAN_Port1.Retry = 2;			//Number of retries
	CAN_Port1.Send = CAN1_Send_Msg;		//CAN1 send function
	
	CAN_Port2.CanPort = 2;			
	CAN_Port2.Retry = 2;			
	CAN_Port2.Send = CAN2_Send_Msg;		//CAN2 send function
	
	/* Set up SCA with ID and CAN port */
	setupActuators( 1, &CAN_Port1);		//ID1 bind CAN1 port
	setupActuators( 2, &CAN_Port2);		//ID2 bind CAN2 port
	
	/* Get the parameter pointer */
	pSCA_ID1 = getInstance(1);
	pSCA_ID2 = getInstance(2);
	
	/* Enable all SCA */
	enableAllActuators();
}
```

*  Make sure to connect the single-chip microcomputer to the PC via debugging tools like ST-LINK or J- LINK and confirm the microcomputer is in working order. Click compile all, if no error occurs, then click download to load to your single-chip microcomputer.
<img src="../../img/cansdk6.png" style="width:300px">
<br>

<div class="md-text" style="text-align: center;"></div>

*  After downloading is completed, connect serial port 1 (PA9 PA10) of the microcomputer to the PC via a USB to serial adapter. Open the virtual serial port terminal software, set the Baud rate to 115200. Data received will show as ASC codes. Data sent will show as Hex. Send number 7 to print out help information.

<img src="../../img/cansdk7.png" style="width:600px">
<br>
<div class="md-text" style="text-align: center;"></div>


*  Initialize the actuator(s) based on the prompt message, send commands in sequence. Observe the actuator’s movement and changes combine with codes under SCA_APP.c. When running the actuators for the first time, you can select function 1 to poll IDs, and adjust the ID number in the routine accordingly. 
<br>


## Advanced application

### Driver structure

* INNFOS CAN SDK STM32 splits the driver program into different layers.。

*  `SCA_Protocol.c/h` is the protocol layer that calls the interface of the STM32 CAN controller for sending and receiving data. It provides 5 types of software interfaces for reading and writing commands. Those interfaces will be called by functions in the API layer and packing/unpacking data according to the command. The head file includes macro definition for all commands, communication error type, and storage every actuator’s struct typedef handle of its parameter information. To support multiple CAN interfaces, we added a descriptive handle for CAN interface in this protocol layer. You can use this handle to define multiple interfaces for sending and receiving. Also you will need to define the sending function and retry times for each interface in the initialization program then bind to each SCA’s information handle. Moreover, this protocol layer provides unified data sending/receiving interface `canDispatch(CanRxMsg* RxMsg)` to make porting easier. This interface will be called and send date in when there is new CAN data pack received.  

*  `SCA_API.c/h` is the interface layer and provides reading and writing functions for all parameters. Users can directly call the API in this layer. Codes in this layer combine command & data, also call the corresponding API for data sending and receiving. Most of the APIs include return value that returns to the result of current communication if returned to `SCA_NoError` then the operation is successful. Detailed definition is under `SCA_Protocol.h`. The head file includes macro definition for six operating modes and 2 statuses of the actuator, as well as parameter configuration.

*  `SCA_APP.c/h` is the application layer, provides basic sample program and driver initialization. Users should focus on initialization program `SCA_Init()`, which includes configuration of CAN interface, binding SCA message handle and acquiring using of parameter pointers. 

*  To perform higher level control of the actuator, this routine enables switching of execution methods between `Block` and `Unblock`. API with parameter `isBlock` could modify this parameter to Block or Unblock to control the execution methods. When Block is executed, the command will wait for return of the actuator after it was sent. If overtime occurs, it will return an error code, which applies to lethal parameters(like switching operation mode). When unBlock is executed, the command will auto delay for 200us after it was sent, to avoid error in case of CAN bus line overload, this applies operations like parameter refreshing.

### 参数配置

*  During your project development, you will need to configure system parameters, relevant macro definition is under `SCA_API.h`. Due to this routine supports communication methods like Block, it will require adjusting Block overtime based on CPU speed. The time of switching on and off is a bit long, while other parameters have a very short return time. When executing programs under Unblock, a protective delay will be added in order to prevent busline overload. `SCA_Delay` is the interface of the delay function. `SendInterval` is the value of the delay time, default setting is `200us` after every Unblock sent.
```sh
/* Configuration */
#define SCA_NUM_USE		2		//The number of SCA used in this project
#define SCA_DEBUGER		1		//Enable the debug function
#define CanOvertime		0xFFFF		//Timeout of data (180Mhz)
#define CanPowertime		0xFFFFFF	//Timeout of power switch (180Mhz)
#define SendInterval		200		//Interval in unblock mode
#define SCA_Delay(x)		delay_us(x)	//Delay function

#ifndef SCA_NUM_USE
	#define SCA_NUM_USE	1		//Use 1 SCA in default
#endif

/* Debug port */
#if (SCA_DEBUGER == 1)
#define SCA_Debug(s,...)	printf("FILE: "__FILE__", LINE: %d: "s"", __LINE__, ##__VA_ARGS__)
#else
#define SCA_Debug(s,...)
#endif
```

*  When `SCA_DEBUGER` macro Define is 1, a debugging information interface will open. Default function is to call `printf` to output error code. It is suitable for debugging softwares.

### Calling API

*  Before calling `API` you will need to initialize the controller, you can refer to the `SCA_Init()` function under the application layer. First define the description handle of CAN interfaces based on their numbers, then assign values for those interfaces in the initialization function. Among them, `Retry`(times for resending if fails) and `Send`(sending function) must be defined, `Canport`(interface number) could be used for marking the interface number. After all CAN interface description handles are initialized, you will need to bind each ID and the CAN interface it calls with `setupActuators()` function. For each actuator, you only need to run this function once at every initialization, make sure that times of calling this function should not exceed the number defined in `SCA_NUM_USE`.

*  After initialization and switching on, you can use all functions in this layer of the interfaces normally. All `APIs` use `ID` to distinguish the actuators connected to the bus line, like the functions for reading and writing the position. When writing the position, input the ID of the actuator that need to be manipulated and its actual position value(+-125.0R); When reading the position, you only need to input the ID of the SCA you need to inquire, then the current position will be transferred to the corresponding information handle. Most of the APIs have a return value to return the result of current data communication. If returns `SCA_NoError(0)`, this this procession is successful, but if returns other result, please refer to the definition of error types under `SCA_Protocol.h`. 

<img src="../../img/cansdk9.png" style="width:600px">

<div class="md-text" style="text-align: center;"></div>

*  Most of the information handle defines initialization in the form of structure arrays, definition length is `SCA_NUM_USE`, this should be consistent with the actual SCA number used. In every API that distinguishes SCAs by their IDs, there will be a procession of finding the information handle through ID, which calls function `getInstance()`. This function will return the address of the Information handle of the targeted ID, if the ID does not exist then it returns NULL. If you wish to acquire the parameter for every actuator, then you should define a pointer called `SCA_Handler_t`. Use function `getInstance()` to acquire the address of the corresponding ID, you can check the corresponding parameter by this pointer. Meanwhile, this type of pointer can be transferred to function type `Fast`, to proceed orders real quick. Moreover, it will skip the procedure of finding the information handle, when the number of SCA connected is pretty big, we recommend you use this type of function. 


*  当修改完执行器的参数时，需要使用`saveAllParams()`函数将参数永久保存，否则下次开机后执行器内依然为未修改的参数。


### Software Porting
* If you need to port this driver software to other platforms, you will need to copy the SCA folder to the targeted project, and realize corresponding software interfaces. 

*  `1.` The platform supports CAN Low-Level-Driver, provides sending functions and pack the functions in Send_t form(Describe it in the head file of the protocol layer)。

*  `2.` Call `canDispatch(CanRxMsg*RxMsg)` function in the data receiving interface, to analyse data. `CanRxMsg` is a receiving structure for the CAN data package. When porting, please refer to your platform and define the structure type of `CanRxMsg`, the default structure is STM32 standard function.  

*  `3.` In the interface layer, to replace the macro definition for delay functions, you will need to realize Microsecond-level delay, if you choose millisecond as the unit, the processing of orders could be very unproductive. If you enabled debugging, you will also need to have the corresponding output function, default is `printf`. Based on CPU speed you can adjust the overtime value, if this value is too small, it could result in correctly receiving data, but the function will return as error.

*  `4.`Replace the corresponding head files, you can refer to the sample program.

----

## Versions History

<table class="tableizer-table"><thead><tr class="tableizer-firstrow" style=background:PaleTurquoise><th>Version</th><th>Update time</th><th>Content</th></tr></thead><tbody><tr><td>V1.2.0</td><td>2019.11.15</td><td>SDK version 1.5.3, More description added</td></tr><tr><td>V1.1.0</td><td>2019.08.21</td><td>SDK version 1.5.3, More description added</td></tr><tr><td>V1.0.0</td><td>2019.08.12</td><td>The first version</td></tr></tbody></table>

