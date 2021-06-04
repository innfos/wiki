# ECB & HUB
## Introduction

ECB is an Ethernet to CAN controller that acts as a bridge between Ethernet and CAN communication. It uses STM32F429VET6 master chip and has rich expansion interfaces. The Ethernet port is a standard RJ45 Ethernet interface with the speed of 10/100 Mbps. The default IP address is 192.168.1.30.The Ethernet communication protocol uses UDP protocol with the default port number 2000. ECB has two independent lines to directly connect to a control bus and uses a CAN isolation scheme with 1 Mbps communication rate. Through two independent CAN buses, the bandwidth of CAN communication of the system can be increased to reduce the communication delay and increase the real-time performance of the system. That will make the controlling of a complex closed-loop environment where multiple SCAs are connected.

ECB's schematic, BOM and Ethernet communication protocols are all open source and can be directly developed on the ECB according to users’ needs, greatly saving new products R&D time, thereby accelerating the time to go to the market.

<img src="../../img/ECB&HUB_v2_2PCBA1.png" style="width:600px">

![ECB&HUB_v2_2PCBA2.png](../../img/ECB&HUB_v2_2PCBA2.png) ![ECB&HUB_v2_2PCBA3.png](../../img/ECB&HUB_v2_2PCBA3.png)



## Functions

* CPU:STM32F429VET6
* RAM:256K
* Flash:512K
* 10/100M Ethernet：1
* CAN：2
* LEDs X12: Power Indicator LED X3, User LED X5, USB Transceiver Data LED X2, Link * activity LED X1, Link Speed LED X1
* Molex interface X6: CAN communication interface
* 2 rows of 2.54mm double row pins, including:
* I2C
* SPI
* USART
* Reserved master chip pin X29


 Note: 
The product power supply must not exceed the maximum input voltage; be stored in a dry environment, avoid to store under the sun or in the rain, being thrown or fallen.<br>It is sensitive to static electricity which may cause permanent damage to the chip. <br>Please discharge the static electricity carried by the body before touching the product, such as ,by human body static eliminator or putting hands on the wall for a while;

## Interface Description

### Core board pin definition
P1 pin definition
<table style="width:500px"><thead><tr class="tableizer-firstrow" style="background: PaleTurquoise; color: black"><th>P1 PIN#</th><th>Name</th><th>P1 PIN#</th><th>Name</th></tr></thead><tbody><tr><td>1</td><td>PC0</td><td>2</td><td>PB1</td></tr><tr><td>3</td><td>PA15</td><td>4</td><td>PB15</td></tr><tr><td>5</td><td>PB14</td><td>6</td><td>PB8</td></tr> <tr><td>7</td><td>PE10</td><td>8</td><td>PB7</td></tr><tr><td>9</td><td>PE8</td><td>10</td><td>PE9</td></tr><tr><td>11</td><td>PE4</td><td>12</td><td>PE5</td></tr><tr><td>13</td><td>PD15</td><td>14</td><td>PE3</td></tr><tr><td>15</td><td>PD13</td><td>16</td><td>PD14</td></tr><tr><td>17</td><td>PD3</td><td>18</td><td>PD4</td></tr><tr><td>19</td><td>PD1</td><td>20</td><td>PD2</td></tr></tbody></table>


P2 pin definition
<table style="width:500px"><thead><tr class="tableizer-firstrow" style="background: PaleTurquoise; color: black"><th>P1 PIN#</th><th>Name</th><th>P1 PIN#</th><th>Name</th></tr></thead><tbody><tr><td>1</td><td>PA5</td><td>2</td><td>PA3</td></tr><tr><td>3</td><td>PA6</td><td>4</td><td>PA4</td></tr><tr><td>5</td><td>AGND</td><td>6</td><td>PA0</td></tr><tr><td>7</td><td>PB3</td><td>8</td><td>PB4</td></tr><tr><td>9</td><td>PD3</td><td>10</td><td>PB9</td></tr><tr><td>11</td><td>PI2</td><td>12</td><td>PI3</td></tr><tr><td>13</td><td>PA8</td><td>14</td><td>PC9</td></tr><tr><td>15</td><td>PD6</td><td>16</td><td>VCC_5V</td></tr><tr><td>17</td><td>PD5</td><td>18</td><td>PB0</td></tr><tr><td>19</td><td>GND</td><td>20</td><td>PC7</td></tr></tbody></table>


### Amass XT60、molex、MicroUSB、Network port
Amass XT60PT-M：power input

Molex 430450827：communication interface，CAN1-J1、J2、J3；CAN2-J4、J5、J6

MicroUSB ROHE_U-F-M5DD-Y-L：USB function interface reserved

Network port LIANDA_L60055-14: connect the host computer



## Dimensions

![ECB_v2_2PCB.png](../../img/ECB_v2_2PCB.png) ![ECB_HUB_v2_2PCB.png](../../img/ECB_HUB_v2_2PCB.png)


## How to connect ECB and ECB_HUB

Method 1:

<img src="../../img/ECB&HUB_v2_2PCBA4.png" style="width:600px">

Method 2:

<img src="../../img/ECB&HUB_v2_2PCBA5.png" style="width:600px">


## Connect multiple ECBs

<img src="../../img/ECB&HUB_v2_2PCBA6.png" style="width:600px">


Note: When multiple ECBs are connected to the same computer, the IP and MAC addresses of the ECB cannot be duplicated. Modify the IP and MAC addresses of the ECB,please [modify the IP and MAC addresses](#!pages/ECB&HUB_v2_2.md#Modify_IP_and_MAC_address "wikilink").

## Modify IP and MAC address
#### download


*   Visit the link[download link](https://github.com/mintasca/ipChangeTool .git)o download the SDK related files or execute the following command directly

```sh
$ git clone https://github.com/mintasca/ipChangeTool.git
```
    
2.  Enter the ipChangeTool directory and modify the permissions of ipChange:

```sh
chmod 777 ipChange
```
3.  It is confirmed that there is only one ECB or ECU connected to the computer and powered up, and then execute the command:

```sh
./ipChange -ip=<1~255> -mac=<1~255>
```
*   Please note that only the last number of IP or MAC addresses can be modified, for example, the IP address of the ECB is 192.168.1.30, and only 30 can be modified to other number.

## Resource
* [ECB_SCH]( ../../img/ECB_v2_2.pdf ) [ECB_HUB_SCH]( ../../img/ECB_HUB_v2_2.pdf ) [ECB_Core]( ../../img/ECB_Core_v2_0.pdf )
* [STM32F429 data sheet]( ../../img/STM32F429VIT6.PDF )



## Version updating records
<table class="tableizer-table">
<thead><tr class="tableizer-firstrow" style="background: PaleTurquoise; color: black;width:600px"><th >Version</th><th>Update time</th><th>Change type</th><th>Position</th><th>Content</th></tr></thead><tr><td>V2.2.4</td><td>2019.07.05</td><td>add</td><td>Resource</td><td>Add ECB_Core Schematic</td></tr><tr><td rowspan="2">V2.2.3</td><td rowspan="2">2019.05.30</td><td>revise</td><td>How to connect ECB and ECB_HUB</td><td>Edit image</td></tr><tr><td>revise</td><td>Connect multiple ECBs</td><td>Edit image</td></tr><tr><td rowspan="3">V2.2.2</td><td rowspan="3">2019.05.29</td><td>revise</td><td>Introduction</td><td>Edit image</td></tr><tr><td>revise</td><td>Dimensions</td><td>Edit image</td></tr><tr><td>add</td><td>Amass XT60、molex、MicroUSB、Network port</td><td>Add specific model</td></tr><tr><td>V2.2.1</td><td>2019.05.28</td><td>delete</td><td>Core board pin definition</td><td>delete Alternate functions</td></tr><tr><td>V2.2.0</td><td>2019-05</td><td>add</td><td>ECB&HUB</td><td>the first version</td></tr></tbody></table>
