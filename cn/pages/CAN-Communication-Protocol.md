[English](CAN_Communication_Protocol "wikilink")

# 产品信息

## **CAN协议概述**

*   CAN 是Controller Area Network 的缩写（以下称为CAN），是ISO国际标准化的串行通信协议。

*   本公司产品设计服从于CAN2.0A协议标准，本文详细介绍了本公司产品的产品CAN通信协议格式，及产品CAN通信结构。

## **综合性能参数**

<table>
<tbody>
<tr class="odd">
<td align="left">

**表1-1综合性能参数说明**
</td>
</tr>
<tr class="even">
<td align="left">

项目
</td>
</tr>
<tr class="odd">
<td align="left">

链路层协议
</td>
</tr>
<tr class="even">
<td align="left">

CAN-ID类型
</td>
</tr>
<tr class="odd">
<td align="left">

波特率
</td>
</tr>
<tr class="even">
<td align="left">

最大站点数
</td>
</tr>
<tr class="odd">
<td align="left">

CAN帧长度
</td>
</tr>
<tr class="even">
<td align="left">

应用层CAN帧类型
</td>
</tr>
<tr class="odd">
<td align="left">

终端匹配电阻
</td>
</tr>
</tbody>
</table>

本通信协议波特率为1Mbit/s，对于CAN通信，不同线的线缆对传输距离影响不大，但是要求线径尽量粗，最大节点数为64，本公司产品采用0.205mm²线径，最大传输距离为25m。



# 配线

<div class="figure">
![图2-1： CAN通信接口](配线2-1.png "图2-1： CAN通信接口")

图2-1： CAN通信接口

</div>

*   INNFOS执行器的插线接口为CAN通信接口，接口如下图所示。名称相同的端口内部引脚连接在一起，其接口定义表2-1所示。CAN接口连接器至少配有CANH、CANL、CGND引脚。
<table>
<tbody>
<tr class="odd">
<td align="left">

**表2-1通信信号连接器引脚定义**
</td>
</tr>
<tr class="even">
<td align="left">

针脚号
</td>
</tr>
<tr class="odd">
<td align="left">

1
</td>
</tr>
<tr class="even">
<td align="left">

3
</td>
</tr>
<tr class="odd">
<td align="left">

5
</td>
</tr>
<tr class="even">
<td align="left">

2
</td>
</tr>
<tr class="odd">
<td align="left">

4
</td>
</tr>
<tr class="even">
<td align="left">

6
</td>
</tr>
<tr class="odd">
<td align="left">

7
</td>
</tr>
<tr class="even">
<td align="left">

8
</td>
</tr>
<tr class="odd">
<td align="left">

外壳
</td>
</tr>
</tbody>
</table>

公共地CGND 的连接，对提高CAN接口的抗干扰性能有很大提升。

## **CAN通信的总线和多节点的连接方式**

CAN通信网络的连接方式为总线连接方式，图2-3 所示 ![图2-3：CAN通信网络拓扑结构](配线2-3.png "fig:图2-3：CAN通信网络拓扑结构")

各个CAN收发设备挂接在总线上，每个分支长度要小于0.3m，否则会引起反射，造成通信问题。 ![图2-4：CAN配线示意图](配线2-4.png "fig:图2-4：CAN配线示意图")

*   推荐使用带屏蔽双绞线连接，总线两端分别连接两个120Ω终端匹配电阻防止信号反射，屏蔽层一般使用单点可靠接地。
*   用万用表测量CANH和CANL之间的阻值可以确认现场两端接电阻是否正确，正常阻值应为60Ω左右（两个电阻的并联值）。
*   挂接设备数量最多为64个。
*   CAN设备长距离通信时，须将不同CAN电路的公共地CGND相互连接，以保证不同通信设备之间参考电位相等。
*   CGND是指CAN通信中的公共地，可用作信号电平参考，提升抗干扰能力；GND是执行器三相电源中的公共地，汇集三相功率电源的大电流至负极。

## **CAN通信的线缆推荐使用双绞线**

CAN通信网络推荐使用双绞线缆，双绞线对高频磁场噪声干扰有很好的抵抗能力，也能减小线缆对外的辐射，图2-5所示。

<div class="figure">
![图2-5：双绞线示意图](配线2-5.png "图2-5：双绞线示意图")

图2-5：双绞线示意图

</div>

*   双绞线的扭矩D应小于2cm，扭矩越小抗干扰效果越好。
*   短距离低速通信时，为了增加抗干扰能力可以使用双绞屏蔽线，屏蔽层双端接PE。
*   长距离高速通信时，不建议使用屏蔽线。因为屏蔽层和信号线之间存在较大分布电容，会导致传输信号延迟。

## **其他设备没有外接CAN_GND 端口配线说明**

### 设备为非隔离CAN,与其他信号共用GND或是COM端口

将该设备GND或是COM与我公司设备CAN_GND连接，如2-11图所示： ![图2-11：与其他电路共用的连接方式](配线2-11.png "fig:图2-11：与其他电路共用的连接方式")

# 通信协议

## **CAN通信协议格式**

![图3-1](配线2-13.png "fig:图3-1")

如图3-1：设备地址对应标识符位，CAN总线标准数据帧标识符位为11位，本协议只用了其中8位，占一个字节，数据长度对应DLC,占半字节，指令符参数内容同在数据域，指令符在前参数内容在后，高字节在前，低字节在后。数据长度等于指令符加上参数内容。

**设备地址**

一个字节，标识要与之通讯的设备地址，0x01～0xff 可用。0x00为广播地址。

**数据长度**

半个字节，标识要通讯的具体数据的个数，范围 0x00～0x0F，超出范围的不作处理

**指令符**

一个字节，标识主机与从机进行的具体操作，取值范围 0x00~0xff。

**参数内容**

某条指令的具体参数内容，其长度等于数据长度减一。有些指令不含具体数据，其数据位数位也应为 1。

### IQmath简介

*   我们使用的处理器一般情况下，要么直接支持硬件的浮点运算，比如某些带有FPU的器件，要么就只支持定点运算，此时对浮点数的处理需要通过编译器来完成。在支持硬件浮点处理的器件上，对浮点运算的编程最快捷的方法就是直接使用浮点类型，比如单精度的float来完成。但是在很多情况下，限于成本、物料等因素，可供我们使用的只有一个定点处理器时，直接使用float类型进行浮点类型的运算会使得编译器产生大量的代码来完成一段看起来十分简单的浮点数学运算，造成的后果是程序的执行时间显著加长，且其占用的资源量也会成倍地增加，这就涉及到了如何在定点处理器上对浮点运算进行高效处理的问题。

*   既然是定点处理器，那么其对定点数，或者说字面意义上的“整数”进行处理的效率就会比它处理浮点类型的运算要高的多。所以在定点处理器上，我们使用定点的整数来代表一个浮点数，并规定整数位数和小数位数，从而方便地对定点数和浮点数进行转换。以一个32位的定点数为例，假设转换因子为Q，即32位中小数的位数为Q，整数位数则为31-Q(有符号数的情况)，则定点数与浮点数的换算关系为：

![详见 IQ-MATH Library文档](3-1通信协议.png "fig:详见 IQ-MATH Library文档") 参考文献：

<embed src="C28x IQmath Library.pdf" title="fig:C28x IQmath Library.pdf" />

<embed src="IQ-MATH Library.pdf" title="fig:IQ-MATH Library.pdf" />

定点数=浮点数×2^Q

例如，浮点数-2.0转换到Q为24的定点数时，结果为：定点数=-2×2^24=-33554432

32位有符号数的表示范围是：-2147483648到2147483647。如果我们把有符号定点数的最大值2147483647转换为Q为24对应的浮点数，则结果为：浮点数2147483647/2^24=127.999999940。

*   IQ值换算的具体方法参见附录E。
<table>
<tbody>
<tr class="odd">
<td align="left">

**Data Type**
</td>
<td align="left">

**Range**
</td>
<td align="left">

**Resolution/Precision**
</td>
</tr>
<tr class="even">
<td align="left">

Min
</td>
<td align="left">

Max
</td>
</tr>
<tr class="odd">
<td align="left">

_iq30
</td>
<td align="left">

-2
</td>
<td align="left">

1.999 999 999
</td>
</tr>
<tr class="even">
<td align="left">

_iq29
</td>
<td align="left">

-4
</td>
<td align="left">

3.999 999 998
</td>
</tr>
<tr class="odd">
<td align="left">

_iq28
</td>
<td align="left">

-8
</td>
<td align="left">

7.999 999 996
</td>
</tr>
<tr class="even">
<td align="left">

_iq27
</td>
<td align="left">

-16
</td>
<td align="left">

15.999 999 993
</td>
</tr>
<tr class="odd">
<td align="left">

_iq26
</td>
<td align="left">

-32
</td>
<td align="left">

31.999 999 985
</td>
</tr>
<tr class="even">
<td align="left">

_iq25
</td>
<td align="left">

-64
</td>
<td align="left">

63.999 999 970
</td>
</tr>
<tr class="odd">
<td align="left">

**_iq24(INNFOS主要应用)**
</td>
<td align="left">

**-128**
</td>
<td align="left">

**127.999 999 940**
</td>
</tr>
<tr class="even">
<td align="left">

_iq23
</td>
<td align="left">

-256
</td>
<td align="left">

255.999 999 981
</td>
</tr>
<tr class="odd">
<td align="left">

_iq22
</td>
<td align="left">

-512
</td>
<td align="left">

511.999 999 762
</td>
</tr>
<tr class="even">
<td align="left">

_iq21
</td>
<td align="left">

-1024
</td>
<td align="left">

1023.999 999 523
</td>
</tr>
<tr class="odd">
<td align="left">

_iq20
</td>
<td align="left">

-2048
</td>
<td align="left">

2047.999 999 046
</td>
</tr>
<tr class="even">
<td align="left">

_iq19
</td>
<td align="left">

-4096
</td>
<td align="left">

4095.999 998 093
</td>
</tr>
<tr class="odd">
<td align="left">

_iq18
</td>
<td align="left">

-8192
</td>
<td align="left">

8191.999 996 185
</td>
</tr>
<tr class="even">
<td align="left">

_iq17
</td>
<td align="left">

-16384
</td>
<td align="left">

16383.999 992 371
</td>
</tr>
<tr class="odd">
<td align="left">

_iq16
</td>
<td align="left">

-32768
</td>
<td align="left">

32767.999 984 741
</td>
</tr>
<tr class="even">
<td align="left">

_iq15
</td>
<td align="left">

-65536
</td>
<td align="left">

65535.999 969 482
</td>
</tr>
<tr class="odd">
<td align="left">

_iq14
</td>
<td align="left">

-131072
</td>
<td align="left">

131071.999 938 965
</td>
</tr>
<tr class="even">
<td align="left">

_iq13
</td>
<td align="left">

-262144
</td>
<td align="left">

262143.999 877 930
</td>
</tr>
<tr class="odd">
<td align="left">

_iq12
</td>
<td align="left">

-524288
</td>
<td align="left">

524287.999 755 859
</td>
</tr>
<tr class="even">
<td align="left">

_iq11
</td>
<td align="left">

-1048576
</td>
<td align="left">

1048575.999 511 719
</td>
</tr>
<tr class="odd">
<td align="left">

_iq10
</td>
<td align="left">

-2097152
</td>
<td align="left">

2097151.999 023 437
</td>
</tr>
<tr class="even">
<td align="left">

_iq9
</td>
<td align="left">

-4194304
</td>
<td align="left">

4194303.998 046 875
</td>
</tr>
<tr class="odd">
<td align="left">

_iq8
</td>
<td align="left">

-8388608
</td>
<td align="left">

8388607.996 093 750
</td>
</tr>
<tr class="even">
<td align="left">

_iq7
</td>
<td align="left">

-16777216
</td>
<td align="left">

16777215.992 187 500
</td>
</tr>
<tr class="odd">
<td align="left">

_iq6
</td>
<td align="left">

-33554432
</td>
<td align="left">

33554431.984 375 000
</td>
</tr>
<tr class="even">
<td align="left">

_iq5
</td>
<td align="left">

-67108864
</td>
<td align="left">

67108863.968 750 000
</td>
</tr>
<tr class="odd">
<td align="left">

_iq4
</td>
<td align="left">

-134217728
</td>
<td align="left">

134217727.937 500 000
</td>
</tr>
<tr class="even">
<td align="left">

_iq3
</td>
<td align="left">

-268435456
</td>
<td align="left">

268435455.875 000 000
</td>
</tr>
<tr class="odd">
<td align="left">

_iq2
</td>
<td align="left">

-536870912
</td>
<td align="left">

536870911.750 000 000
</td>
</tr>
<tr class="even">
<td align="left">

_iq1
</td>
<td align="left">

-1073741824
</td>
<td align="left">

1 073741823.500 000 000
</td>
</tr>
</tbody>
</table>

## **CAN通信协议命令应用举例**

**示例1.读命令**

<table>
<tbody>
<tr class="odd">
<td align="left">

**读取执行器电机ID为0x01的当前速度值**
</td>
</tr>
<tr class="even">
<td align="left">

设备地址
</td>
</tr>
<tr class="odd">
<td align="left">

0x01
</td>
</tr>
</tbody>
</table>

设备地址： 0x01 = 读取的对象ID

数据长度：0x1 = 数据长度

指令符： 0x05 = 读取的当前速度指令

参数内容：无 = 发送的参数内容

发送内容： 0x05

<table>
<tbody>
<tr class="odd">
<td align="left">

**应答命令**
</td>
</tr>
<tr class="even">
<td align="left">

设备地址
</td>
</tr>
<tr class="odd">
<td align="left">

0x01
</td>
</tr>
</tbody>
</table>

返回设备地址：0x01 = 应答对象ID

数据长度：0x5 = 应答的数据长度5位

指令符：0x05 = 应答当前速度指令（与发送指令符相同）

参数内容：0xXX 0xXX 0xXX 0xXX = 应答的参数内容

应答内容：0x05 0xXX 0xXX 0xXX 0xXX

说明：参数内容data[3~0]高位在前，低位在后。为_IQ24格式。_IQ(-1.0)~_IQ(1.0)代表反转速度满量程和正转速度满量程。满量程为6000RPM。若data=_IQ(0.5)。则为0.5*6000=3000RPM。

**示例2.写命令**

<table>
<tbody>
<tr class="odd">
<td align="left">

**设置执行器电机ID为0x01的当前位置值**
</td>
</tr>
<tr class="even">
<td align="left">

设备地址
</td>
</tr>
<tr class="odd">
<td align="left">

0x01
</td>
</tr>
</tbody>
</table>

设备地址： 0x01 = 设置对象ID

数据长度：0x5 = 数据长度

指令符： 0x0A = 设置的位置

参数内容：0x05 0x00 0x00 0x00 = 发送的参数内容

发送内容：0x0A 0x05 0x00 0x00 0x00

说明：参数内容data[3~0]高位在前，低位在后。为_IQ24格式。_IQ(-128.0)~_IQ(127.999999940)代表反向位置值满量程和正向位置值满量程。若data=_IQ(5.0),则设置当前位置为5。

<table>
<tbody>
<tr class="odd">
<td align="left">

**应答命令**
</td>
</tr>
<tr class="even">
<td align="left">

设 备 地 址
</td>
</tr>
<tr class="odd">
<td align="left">

0x01
</td>
</tr>
</tbody>
</table>

返回设备地址：0x01 = 应答对象ID

数据长度：0x00 = 应答的数据长度

指令符：无

参数内容：无

应答内容：无

* * *

*   使用指令模式的一般步骤：

（1）开机，指令：0x2A 01；

（2）选择使用模式，指令：电流环0x07 01，速度环0x07 02，位置环0X07 03，S-位置模式0X07 06，S-速度模式0X07 07，HOMING模式 0X07 08；

（3）设定相关参数，指令参考说明书附录部分。对于电流值，速度值，位置的参数来说，不为0则启动，为0则停止；

（4）使用结束，关机，指令：0X2A 00。断电前必须先发送关机指令，否则可能造成零位丢失。

* * *

<div class="figure">
![3-2通信协议-1.png](3-2通信协议-1.png "3-2通信协议-1.png")

3-2通信协议-1.png

</div>

*   注释：
*   上位机所设置的上限幅值（Maximum）最高为_IQ(1.0)，下限幅值（Minimal）最低为_IQ(-1.0)，起到限幅作用（原理图如图3-2）。例：（如图:3-2用位置环的输出经过限幅模块为速度环的输入，假设_IQ（0.5），_IQ（-0.5）则位置环输出最大速度应为±0.5x6000=±3000RPM）
*   比例积分设置值上限为_IQ(128.0)，设定值下限为_IQ(-128.0)，但设置值根据实际操作情况调节（原理图: 3-2）
*   电流环设置电流值范围为_IQ(-1.0)~_IQ(1.0)之间，电流实际值为IQ值乘以满量程，例：（MSC-80型号执行器满量程电流值为33A ，_IQ(0.5) 实际电流值则为0.5x33A=16.5A，见附录D:型号表）
*   速度环设置速度值范围为_IQ(-1.0)~_IQ(1.0)之间，速度实际值为IQ值乘以满量程（见 ）。例：（_IQ(0.5)则实际速度为0.5*6000=3000RPM）
*   位置环因为是_IQ24格式，所以正向满量程为_IQ(127.999999940)，反向满量程为_IQ(-128.0)，IQ值即实际值，例：<span style="color: red">（_IQ（60.0）则实际位置为60R，即零位置正向转60转的位置。）</span>
*   速度环曲线模式和位置环曲线模式，可以通过设置加速度，减速度的大小，相对平滑的达到自己预设的速度值和位置，可以避免操作时瞬间电流过大，触发执行器过流保护或者供电电源过流保护。

## **CAN通信协议命令参考**

### 读取命令

<table>
<tbody>
<tr class="odd">
<td align="left">

**<span id="Q"></span>3.3.1.1 发送数据1字节， 返回数据2字节**
</td>
</tr>
<tr class="even">
<td align="left">

命令名称
</td>
</tr>
<tr class="odd">
<td align="left">

说明
</td>
</tr>
<tr class="even">
<td align="left">

指令符
</td>
</tr>
<tr class="odd">
<td align="left">

数据长度
</td>
</tr>
<tr class="even">
<td align="left">

数据内容
</td>
</tr>
<tr class="odd">
<td align="left">

指令符（返回值）
</td>
</tr>
<tr class="even">
<td align="left">

数据长度 (返回值)
</td>
</tr>
<tr class="odd">
<td align="left">

下位机返回数据
</td>
</tr>
<tr class="even">
<td align="left">

0x00：失败/失能/关机/异常
</td>
</tr>
</tbody>
</table>
<table>
<tbody>
<tr class="odd">
<td align="left">

**<span id="W"></span>3.3.1.2 发送数据1字节，返回数据3字节**
</td>
</tr>
<tr class="even">
<td align="left">

命令名称
</td>
</tr>
<tr class="odd">
<td align="left">

说明
</td>
</tr>
<tr class="even">
<td align="left">

指令符
</td>
</tr>
<tr class="odd">
<td align="left">

数据长度
</td>
</tr>
<tr class="even">
<td align="left">

数据内容
</td>
</tr>
<tr class="odd">
<td align="left">

指令符（返回值）
</td>
</tr>
<tr class="even">
<td align="left">

数据长度 (返回值)
</td>
</tr>
<tr class="odd">
<td align="left">

下位机返回数据
</td>
</tr>
</tbody>
</table>
<table>
<tbody>
<tr class="odd">
<td align="left">

**'<span id="E"></span>3.3.1.3 发送数据1字节，返回数据5字节**
</td>
</tr>
<tr class="even">
<td align="left">

命令名称
</td>
</tr>
<tr class="odd">
<td align="left">

说明
</td>
</tr>
<tr class="even">
<td align="left">

指令符
</td>
</tr>
<tr class="odd">
<td align="left">

数据长度
</td>
</tr>
<tr class="even">
<td align="left">

数据内容
</td>
</tr>
<tr class="odd">
<td align="left">

指令符（返回值）
</td>
</tr>
<tr class="even">
<td align="left">

数据长度 (返回值)
</td>
</tr>
<tr class="odd">
<td align="left">

下位机返回数据
</td>
</tr>
</tbody>
</table>

### 写入命令

<table>
<tbody>
<tr class="odd">
<td align="left">

**3.3.2.1发送数据2字节，返回数据2字节**
</td>
</tr>
<tr class="even">
<td align="left">

命令名称
</td>
</tr>
<tr class="odd">
<td align="left">

说明
</td>
</tr>
<tr class="even">
<td align="left">

指令符
</td>
</tr>
<tr class="odd">
<td align="left">

数据长度
</td>
</tr>
<tr class="even">
<td align="left">

数据内容
</td>
</tr>
<tr class="odd">
<td align="left">

0x00：失能/关机
</td>
</tr>
<tr class="even">
<td align="left">

指令 (返回值)
</td>
</tr>
<tr class="odd">
<td align="left">

数据长度(返回值)
</td>
</tr>
<tr class="even">
<td align="left">

下位机返回数据
</td>
</tr>
<tr class="odd">
<td align="left">

0x00：失败
</td>
</tr>
</tbody>
</table>
<table>
<tbody>
<tr class="odd">
<td align="left">

**3.3.2.2发送数据3字节，返回数据2字节**
</td>
</tr>
<tr class="even">
<td align="left">

命令名称
</td>
</tr>
<tr class="odd">
<td align="left">

说明
</td>
</tr>
<tr class="even">
<td align="left">

指令符
</td>
</tr>
<tr class="odd">
<td align="left">

数据长度
</td>
</tr>
<tr class="even">
<td align="left">

数据内容
</td>
</tr>
<tr class="odd">
<td align="left">

0x00：失能/关机
</td>
</tr>
<tr class="even">
<td align="left">

指令 (返回值)
</td>
</tr>
<tr class="odd">
<td align="left">

数据长度(返回值)
</td>
</tr>
<tr class="even">
<td align="left">

下位机返回数据
</td>
</tr>
<tr class="odd">
<td align="left">

0x00：失败
</td>
</tr>
</tbody>
</table>
<table>
<tbody>
<tr class="odd">
<td align="left">

**3.3.2.3发送数据5字节，返回数据2字节或更少**
</td>
</tr>
<tr class="even">
<td align="left">

命令名称
</td>
</tr>
<tr class="odd">
<td align="left">

说明
</td>
</tr>
<tr class="even">
<td align="left">

指令符
</td>
</tr>
<tr class="odd">
<td align="left">

数据长度
</td>
</tr>
<tr class="even">
<td align="left">

数据内容
</td>
</tr>
<tr class="odd">
<td align="left">

指令 (返回值)
</td>
</tr>
<tr class="even">
<td align="left">

数据长度(返回值)
</td>
</tr>
<tr class="odd">
<td align="left">

下位机返回数据
</td>
</tr>
<tr class="even">
<td align="left">

0x00：失败
</td>
</tr>
</tbody>
</table>
<table>
<tbody>
<tr class="odd">
<td align="left">

**3.3.2.4发送数据1字节，返回数据2字节**
</td>
</tr>
<tr class="even">
<td align="left">

命令名称
</td>
</tr>
<tr class="odd">
<td align="left">

说明
</td>
</tr>
<tr class="even">
<td align="left">

指令符
</td>
</tr>
<tr class="odd">
<td align="left">

数据长度
</td>
</tr>
<tr class="even">
<td align="left">

数据内容
</td>
</tr>
<tr class="odd">
<td align="left">

指令 (返回值)
</td>
</tr>
<tr class="even">
<td align="left">

数据长度(返回值)
</td>
</tr>
<tr class="odd">
<td align="left">

下位机返回数据
</td>
</tr>
<tr class="even">
<td align="left">

0x00：失败
</td>
</tr>
</tbody>
</table>

# 附录A

## **A.1读取指令编码定义表**

<table>
<tbody>
<tr class="odd">
<td align="left">

**<span id="A.1.1 读取指令1"></span>A.1.1 读取指令1**
</td>
</tr>
<tr class="even">
<td align="left">

指令符
</td>
</tr>
<tr class="odd">
<td align="left">

0x00 ：
</td>
</tr>
<tr class="even">
<td align="left">

0x55：
</td>
</tr>
<tr class="odd">
<td align="left">

0xB0
</td>
</tr>
<tr class="even">
<td align="left">

0x71：
</td>
</tr>
<tr class="odd">
<td align="left">

0x75：
</td>
</tr>
<tr class="even">
<td align="left">

0x79：
</td>
</tr>
<tr class="odd">
<td align="left">

0x2B
</td>
</tr>
</tbody>
</table>
<table>
<tbody>
<tr class="odd">
<td align="left">

**<span id="A.1.1 读取指令2"></span>A.1.2 读取指令2**
</td>
</tr>
<tr class="even">
<td align="left">

指令符
</td>
</tr>
<tr class="odd">
<td align="left">

0x73：
</td>
</tr>
<tr class="even">
<td align="left">

0x77：
</td>
</tr>
<tr class="odd">
<td align="left">

0x7B：
</td>
</tr>
<tr class="even">
<td align="left">

0x5F
</td>
</tr>
<tr class="odd">
<td align="left">

0x60
</td>
</tr>
<tr class="even">
<td align="left">

0x62
</td>
</tr>
<tr class="odd">
<td align="left">

0x64
</td>
</tr>
<tr class="even">
<td align="left">

0xFF
</td>
</tr>
</tbody>
</table>
<table>
<tbody>
<tr class="odd">
<td align="left">

**<span id="A.1.3 读取指令3"></span>A.1.3 读取指令3**
</td>
</tr>
<tr class="even">
<td align="left">

指令符
</td>
</tr>
<tr class="odd">
<td align="left">

0x04：
</td>
</tr>
<tr class="even">
<td align="left">

0x05：
</td>
</tr>
<tr class="odd">
<td align="left">

0x06：
</td>
</tr>
<tr class="even">
<td align="left">

0x15：
</td>
</tr>
<tr class="odd">
<td align="left">

0x16：
</td>
</tr>
<tr class="even">
<td align="left">

0x17：
</td>
</tr>
<tr class="odd">
<td align="left">

0x18：
</td>
</tr>
<tr class="even">
<td align="left">

0x19：
</td>
</tr>
<tr class="odd">
<td align="left">

0x1A：
</td>
</tr>
<tr class="even">
<td align="left">

0x1C：
</td>
</tr>
<tr class="odd">
<td align="left">

0x1D：
</td>
</tr>
<tr class="even">
<td align="left">

0x1E：
</td>
</tr>
<tr class="odd">
<td align="left">

0x22：
</td>
</tr>
<tr class="even">
<td align="left">

0x23：
</td>
</tr>
<tr class="odd">
<td align="left">

0x24：
</td>
</tr>
<tr class="even">
<td align="left">

0x34：
</td>
</tr>
<tr class="odd">
<td align="left">

0x35：
</td>
</tr>
<tr class="even">
<td align="left">

0x36：
</td>
</tr>
<tr class="odd">
<td align="left">

0x37：
</td>
</tr>
<tr class="even">
<td align="left">

0x38：
</td>
</tr>
<tr class="odd">
<td align="left">

0x39：
</td>
</tr>
<tr class="even">
<td align="left">

0x7D：
</td>
</tr>
<tr class="odd">
<td align="left">

0x85：
</td>
</tr>
<tr class="even">
<td align="left">

0x86：
</td>
</tr>
<tr class="odd">
<td align="left">

0x8A：
</td>
</tr>
<tr class="even">
<td align="left">

0x92：
</td>
</tr>
<tr class="odd">
<td align="left">

0x93：
</td>
</tr>
<tr class="even">
<td align="left">

0x7F：
</td>
</tr>
</tbody>
</table>

## **A.2 写入命令编码值定义表**

<table>
<tbody>
<tr class="odd">
<td align="left">

**A.2.1写入指令1**
</td>
</tr>
<tr class="even">
<td align="left">

指令符
</td>
</tr>
<tr class="odd">
<td align="left">

0x07：
</td>
</tr>
<tr class="even">
<td align="left">

0x70：
</td>
</tr>
<tr class="odd">
<td align="left">

0x74：
</td>
</tr>
<tr class="even">
<td align="left">

0x78：
</td>
</tr>
<tr class="odd">
<td align="left">

0x2A：
</td>
</tr>
</tbody>
</table>
<table>
<tbody>
<tr class="odd">
<td align="left">

**A.2.2写入指令2**
</td>
</tr>
<tr class="even">
<td align="left">

指令符
</td>
</tr>
<tr class="odd">
<td align="left">

0x72：
</td>
</tr>
<tr class="even">
<td align="left">

0x76：
</td>
</tr>
<tr class="odd">
<td align="left">

0x7A：
</td>
</tr>
<tr class="even">
<td align="left">

0x61：
</td>
</tr>
<tr class="odd">
<td align="left">

0x63：
</td>
</tr>
</tbody>
</table>
<table>
<tbody>
<tr class="odd">
<td align="left">

**A.2.3写入指令3**
</td>
</tr>
<tr class="even">
<td align="left">

指令符
</td>
</tr>
<tr class="odd">
<td align="left">

0x08：
</td>
</tr>
<tr class="even">
<td align="left">

0x09：
</td>
</tr>
<tr class="odd">
<td align="left">

0x0A：
</td>
</tr>
<tr class="even">
<td align="left">

0x0E：
</td>
</tr>
<tr class="odd">
<td align="left">

0x0F：
</td>
</tr>
<tr class="even">
<td align="left">

0x10：
</td>
</tr>
<tr class="odd">
<td align="left">

0x11：
</td>
</tr>
<tr class="even">
<td align="left">

0x12：
</td>
</tr>
<tr class="odd">
<td align="left">

0x13：
</td>
</tr>
<tr class="even">
<td align="left">

0x1F：
</td>
</tr>
<tr class="odd">
<td align="left">

0x20：
</td>
</tr>
<tr class="even">
<td align="left">

0x21：
</td>
</tr>
<tr class="odd">
<td align="left">

0x25：
</td>
</tr>
<tr class="even">
<td align="left">

0x26：
</td>
</tr>
<tr class="odd">
<td align="left">

0x27：
</td>
</tr>
<tr class="even">
<td align="left">

0x2E：
</td>
</tr>
<tr class="odd">
<td align="left">

0x2F：
</td>
</tr>
<tr class="even">
<td align="left">

0x30：
</td>
</tr>
<tr class="odd">
<td align="left">

0x31：
</td>
</tr>
<tr class="even">
<td align="left">

0x32：
</td>
</tr>
<tr class="odd">
<td align="left">

0x33：
</td>
</tr>
<tr class="even">
<td align="left">

0x83：
</td>
</tr>
<tr class="odd">
<td align="left">

0x84：
</td>
</tr>
<tr class="even">
<td align="left">

0x87：
</td>
</tr>
<tr class="odd">
<td align="left">

0x89：
</td>
</tr>
<tr class="even">
<td align="left">

0x90：
</td>
</tr>
<tr class="odd">
<td align="left">

0x91：
</td>
</tr>
<tr class="even">
<td align="left">

0x7E：
</td>
</tr>
</tbody>
</table>
<table>
<tbody>
<tr class="odd">
<td align="left">

**A.2.4写入指令4**
</td>
</tr>
<tr class="even">
<td align="left">

指令符
</td>
</tr>
<tr class="odd">
<td align="left">

0xFE：
</td>
</tr>
<tr class="even">
<td align="left">

0x88
</td>
</tr>
<tr class="odd">
<td align="left">

0x0D
</td>
</tr>
</tbody>
</table>

# 附录B :模式表

<table>
<tbody>
<tr class="odd">
<td align="left">

**指令符**
</td>
<td align="left">

**指令符**
</td>
</tr>
<tr class="even">
<td align="left">

0x01
</td>
<td align="left">

电流模式
</td>
</tr>
<tr class="odd">
<td align="left">

0x02
</td>
<td align="left">

速度模式
</td>
</tr>
<tr class="even">
<td align="left">

0x03
</td>
<td align="left">

位置模式
</td>
</tr>
<tr class="odd">
<td align="left">

0x06
</td>
<td align="left">

位置梯形模式（S曲线）
</td>
</tr>
<tr class="even">
<td align="left">

0x07
</td>
<td align="left">

速度梯形模式（S曲线）
</td>
</tr>
<tr class="odd">
<td align="left">

0x08
</td>
<td align="left">

homing模式
</td>
</tr>
</tbody>
</table>

# 附录C：报警指令表

<table>
<tbody>
<tr class="odd">
<td align="left">

**指令符**
</td>
<td align="left">

**指令符**
</td>
</tr>
<tr class="even">
<td align="left">

0x0001
</td>
<td align="left">

过压异常
</td>
</tr>
<tr class="odd">
<td align="left">

0x0002
</td>
<td align="left">

欠压异常
</td>
</tr>
<tr class="even">
<td align="left">

0x0004
</td>
<td align="left">

堵转异常
</td>
</tr>
<tr class="odd">
<td align="left">

0x0008
</td>
<td align="left">

过热异常
</td>
</tr>
<tr class="even">
<td align="left">

0x0010
</td>
<td align="left">

读写参数异常
</td>
</tr>
<tr class="odd">
<td align="left">

0x0020
</td>
<td align="left">

多圈计数异常
</td>
</tr>
<tr class="even">
<td align="left">

0x0040
</td>
<td align="left">

逆变器温度传感器异常
</td>
</tr>
<tr class="odd">
<td align="left">

0x0080
</td>
<td align="left">

CAN通信异常
</td>
</tr>
<tr class="even">
<td align="left">

0x0100
</td>
<td align="left">

电机温度传感器异常
</td>
</tr>
<tr class="odd">
<td align="left">

0x0200
</td>
<td align="left">

位置模式阶跃大于1
</td>
</tr>
<tr class="even">
<td align="left">

0x0400
</td>
<td align="left">

DRV保护
</td>
</tr>
<tr class="odd">
<td align="left">

其他
</td>
<td align="left">

设备异常
</td>
</tr>
<tr class="even">
<td align="left">

注释
</td>
<td align="left">

可同时报警多个错误，如返回数据为0005，

则错误为0001过压异常与0004堵转异常
</td>
</tr>
</tbody>
</table>

# 附录D：型号表

<table>
<tbody>
<tr class="odd">
<td align="left">

**执行器型号**
</td>
<td align="left">

**电流满量程**
</td>
<td align="left">

**电机端速度满量程**
</td>
<td align="left">

**输出端速度满量程**
</td>
</tr>
<tr class="even">
<td align="left">

QDD Pro-6010-50
</td>
<td align="left">

33A
</td>
<td align="left">

6000RPM
</td>
<td align="left">

120RPM
</td>
</tr>
<tr class="odd">
<td align="left">

QDD-6010-6
</td>
<td align="left">

33A
</td>
<td align="left">

6000RPM
</td>
<td align="left">

1000RPM
</td>
</tr>
<tr class="even">
<td align="left">

QDD-6010-36
</td>
<td align="left">

33A
</td>
<td align="left">

6000RPM
</td>
<td align="left">

166.7RPM
</td>
</tr>
<tr class="odd">
<td align="left">

DD-6010
</td>
<td align="left">

33A
</td>
<td align="left">

6000RPM
</td>
<td align="left">

6000RPM
</td>
</tr>
<tr class="even">
<td align="left">

QDD Pro-3510-50
</td>
<td align="left">

16.5A
</td>
<td align="left">

6000RPM
</td>
<td align="left">

120RPM
</td>
</tr>
<tr class="odd">
<td align="left">

QDD-3510-6
</td>
<td align="left">

16.5A
</td>
<td align="left">

6000RPM
</td>
<td align="left">

1000RPM
</td>
</tr>
<tr class="even">
<td align="left">

QDD-3510-36
</td>
<td align="left">

16.5A
</td>
<td align="left">

6000RPM
</td>
<td align="left">

166.7RPM
</td>
</tr>
<tr class="odd">
<td align="left">

DD-3510
</td>
<td align="left">

16.5A
</td>
<td align="left">

6000RPM
</td>
<td align="left">

6000RPM
</td>
</tr>
</tbody>
</table>

*   输出端速度不同是因为个别型号执行器内置减速器，使输出的最大转速降低，提高扭矩。IQ换算时按照电机端速度满量程的值计算。

# 附录E:指令发送与IQ值换算方法

*   说明书的注释部分表明：在位置模式中，IQ值即为实际值，即实际值的范围为-128~127. 999999940。这时只需要将对应的位置值转换成IQ值即可输入到参数内容中。在速度和电流模式中，转换IQ值之前需要将对应的参数值进行换算，如设定当前速度值为100RPM，则需要将设定的当前值除以最大值，即100/6000=0.01666666，然后再将0.016666666进行IQ换算，得到的值即为参数值。
*   例如我们要设定当前的位置为60R（注意位置模式中阶跃响应的限制，若设定位置与当前位置差值超过1R则不响应），先寻找对应的指令。附录中A中第三类写入命令（写入命令3）表明，设定当前位置值的指令为0x0A。找到指令后寻找指令的对应发送格式，在“CAN通信协议命令参考”中3.3.2.3小节对应第三类写入指令，发送数据长度为5，即一个字节的指令+4个字节的参数内容。数据内容应用IQ24格式，则直接对60进行IQ换算，即60*2^24= 1006632960，再统一转换为16进制（根据测试软件需要），3C 00 00 00。根据CAN总线的数据帧格式说明，指令参数要在最高位，参数内容在后，则我们发送的指令内容 为0x 0A 3C 00 00 00，这也对应了说明中的数据长度为5（字节）。到此指令发送完毕。
*   相应地，若要发送电流或者速度模式的设定值，需要先将参数值进行换算（各自除以对应的最大值），得到一个-1~1范围内的数，再进行IQ换算即可。发送命令的步骤与方法与位置模式相同，需要注意的是每个指令使用的数据格式，若为IQ8格式，则将公式中2^24改为2^8后再进行换算即可。

# 附录F:版本变更记录

**下表简单描述了版本变更记录**

<table>
<tbody>
<tr class="odd">
<td align="left">

**版本号**
</td>
<td align="left">

**更新时间**
</td>
<td align="left">

**更改类型**
</td>
<td align="left">

**位置**
</td>
<td align="left">

**更新内容**
</td>
</tr>
<tr class="even">
<td align="left">

V1.0.4
</td>
<td align="left">

18.12.14
</td>
<td align="left">

增加
</td>
<td align="left">

附录E
</td>
<td align="left">

指令发送与IQ值换算方法
</td>
</tr>
<tr class="odd">
<td align="left">

V1.0.3
</td>
<td align="left">

18.03.19
</td>
<td align="left">

增加
</td>
<td align="left">

第三章通信协议
</td>
<td align="left">

较上一版本多加了更多的执行器参数信息指令，执行器的温度信息指令，

查询上次关机状态指令，Homing指令。
</td>
</tr>
<tr class="even">
<td align="left">

增加
</td>
<td align="left">

第三章通信协议
</td>
<td align="left">

增加了储存参数指令
</td>
</tr>
<tr class="odd">
<td align="left">

修改
</td>
<td align="left">

第三章通信协议
</td>
<td align="left">

修改了第三章全章的排版
</td>
</tr>
<tr class="even">
<td align="left">

增加
</td>
<td align="left">

第三章通信协议
</td>
<td align="left">

增加了储存参数指令
</td>
</tr>
<tr class="odd">
<td align="left">

V1.0.2
</td>
<td align="left">

18.01.30
</td>
<td align="left">

修改
</td>
<td align="left">

全文
</td>
<td align="left">

微伺服更名为INNFOS执行器
</td>
</tr>
<tr class="even">
<td align="left">

增加
</td>
<td align="left">

第三章通信协议
</td>
<td align="left">

较上一版本多加了报警指令
</td>
</tr>
<tr class="odd">
<td align="left">

V1.0.1
</td>
<td align="left">

17.12.29
</td>
<td align="left">

修改
</td>
<td align="left">

第三章通讯协议
</td>
<td align="left">

更新了通信协议的数据长度，数据长度较之前加1
</td>
</tr>
<tr class="even">
<td align="left">

V1.0.0
</td>
<td align="left">

17.12.15
</td>
<td align="left">

修改
</td>
<td align="left">

第二章通配线
</td>
<td align="left">

更新了CAN接口定义
</td>
</tr>
<tr class="odd">
<td align="left">

增加
</td>
<td align="left">

第三章通信协议
</td>
<td align="left">

增加了开关机指令
</td>
</tr>
</tbody>
</table>
