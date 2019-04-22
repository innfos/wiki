以太网通信协议
=======

[English](以太网通信协议 "wikilink")


## 概述

*   以太网是目前使用最广泛的局域网技术。由于其简单、成本低、可扩展性强、与IP网能够很好地结合等特点。

*   本公司产品设计基于UDP协议标准，本文详细介绍了本公司产品的产品以太网通信协议格式，及产品以太网通信结构。

## 执行器连接

![connect.png](../img/connect2.png "连接拓扑图")

按上图连接好设备，再接通电源。

警告：所有线缆拔插严禁带电操作，否则容易损坏设备。

## 通信方式

本协议分为物理层，数据链路层和用户层

*   物理层

电气接口标准为Ethernet，IEEE 802.3-2002 标准、100M 全双工通讯。

*   数据链路层

数据链路层规定了数据帧的具体格式，上位机与从机采用相同的数据格式，数据中的每个字段采用16位进制表示。

*   用户层

用户层定义了从机与主机通讯的命令接口。

## 通信协议

### 通信协议格式

<table class="tableizer-table">
<thead><tr class="tableizer-firstrow"><th>帧头</th><th>设备地址</th><th>指令符</th><th>数据位数</th><th>数据内容</th><th>CRC 校验码</th><th>帧尾</th></tr></thead><tbody>
 <tr><td>1 字节</td><td>1 字节</td><td>1 字节</td><td>2 字节</td><td>N 字节</td><td>2 字节</td><td>1 字节</td></tr>
</tbody></table>

**帧头**

*固定字节 0xEE，标识一个传输帧的开始。

**设备地址**

*一个字节标识要与之通讯的设备地址，0x01～0xff 可用。0x00 为广播地址。

**指令符**

*一个字节标识主机与从机进行的具体操作，取值范围 0x00~0xff。详见用户层具体 描述。

**数据位数**

*两个字节标识要通讯的具体数据的个数，范围 0x0000~0xffff，超出范围的不作处理。

**数据内容**

*某条指令的具体数据内容，其长度与之前的数据位数位保持一致。有些 指令不含具 体数据，其数据位数位也应为 0。

**CRC校验码**

*两个字节标识对通讯中数据内容的 CRC16 校验结果，若命令中无数据，则无 CRC校验位,CRC计算方法请参考[CRC校验码计算方法](#CRC校验码计算方法 "wikilink")

**帧尾**

*固定字节 0XED，标识一个传输帧的结束。

### **以太网通信协议命令应用举例**

#### 协议示例

示例1.读命令4

<table>
	<tr><th colspan="6">读取执行器ID为0x01的当前速度值</th></tr>
	<tr><td >帧头</td><td >设备地址</td><td >指令符</td><td >数据长度（2字节）</td><td >参数内容</td><td >帧尾</td></tr>
	<tr><td >0xEE</td><td >0x01</td><td >0x5</td><td >0x00 0x00</td><td >无</td><td >0xED</td></tr>
</table>

帧头 ：0xEE = 协议头

设备地址：0x01 = 读取的对象ID

指 令 符：0x05 = 读取的当前速度指令

数据长度：0x0 = 数据长度

参数内容：无 = 发送的参数内容

帧尾 ：0xED = 协议尾

发送内容：0x05

<table class="tableizer-table">
<tbody>
 <tr><td  colspan="7"style=background:PaleTurquoise>应答命令</td></tr>
 <tr><td>帧头</td><td>设备地址</td><td>指令符</td><td>数据长度（2字节）</td><td>参数内容</td><td>CRC校验</td><td>帧尾</td></tr>
 <tr><td>0xEE</td><td>0x01</td><td>0x5</td><td>0x00 0x04</td><td>4字节数据</td><td>2字节数据</td><td>0xED</td></tr>
</tbody></table>
帧头 ：0xEE = 协议头

设备地址：0x01 = 读取的对象ID

指 令 符：0x05 = 读取的当前速度指令

数据长度：0x04 = 数据长度

参数内容：四字节速度数据 = 发送的参数内容

校验位 ：两字节数据 = 校验位

帧尾 ：0xED = 协议尾

应 答 内 容 ：0x05 0xXX 0xXX 0xXX 0xXX

说明：参数内容data[0~3]高位在前，低位在后。为_IQ24格式。_IQ(-1.0)~_IQ(1.0)代表反转速度满量程和正转速度满量程。满量程为

6000RPM。若data=_IQ(0.5)。则为0.5*6000=3000RPM。

**示例2.写命令**

<table class="tableizer-table">
<thead ><tr class="tableizer-firstrow"><th  colspan="7" style=background:PaleTurquoise>设置执行器ID为0x01的电流环的比例P（设置值为5）</th></tr></thead><tbody>
 <tr><td>帧头</td><td>设备地址</td><td>指令符</td><td>数据长度</td><td>参数内容</td><td>CRC校验</td><td>帧尾</td></tr>
 <tr><td>0xEE</td><td>0x01</td><td>0x0E</td><td>0x4</td><td>0x05 0x00 0x00 0x00</td><td>2字节数据</td><td>0xED</td></tr>
</tbody></table>
帧头 ：0xEE = 协议头

设备地址：0x01 = 设置对象ID

数据长度：0x4 = 数据长度

指 令 符：0x0E = 设置的位置

参数内容：0x05 0x00 0x00 0x00 = 发送的参数内容

校验位 ：两字节数据 = 校验位

帧尾 ：0xED = 协议尾

发送内容：0x0E 0x05 0x00 0x00 0x00

说明：参数内容data[0~3]高位在前，低位在后。为_IQ24格式。_IQ(-128.0)~_IQ(127.999999940)代表反向位置值满量程和正向位置值满量程。若data=_IQ(5.0),则比例为5。

<table class="tableizer-table">
<thead><tr class="tableizer-firstrow"><th colspan="7" style=background:PaleTurquoise>应答命令</th></tr></thead><tbody>
 <tr><td>帧头</td><td>设备地址</td><td>指令符</td><td>数据长度</td><td>参数内容</td><td>帧尾</td></tr>
 <tr><td>0xEE</td><td>0x01</td><td>0x0E</td><td>0x1</td><td>0x01</td><td>0xED</td></tr>
</tbody></table>

帧头 ：0xEE = 协议头

返回设备地址：0x01 = 应答对象ID

数 据 长 度 ：0x1 = 应答的数据长度

指 令 符 ：0x0E = 应答设置当前位置指令（与发送对应）

参 数 内 容 ：0x01 = 应答的参数内容（0x01表示写入成功）

帧尾 ：0xED = 协议尾

应 答 内 容 ：0x0E 0x01

## 发送流程

### 通信配置

以太网通信方式采用udp通信，ECB固定了ip地址，为192.168.1.30(默认)，可以通过相关协议修改该ip地址。PC端需修改网络配置，ip地址修改为192.168.1.xxx，xxx为需大于100，以避免和ECB地址冲突，子网掩码255.255.255.0，默认网关192.168.1.1，配置成功并且连接成功通电以后，可以ping到ECB的ip地址，这样就表示连接成功，通信端口为2000，可以通过该端口与执行器通信。

### 与ECB握手

使用以太网通信需要先与ECB握手，待ECB成功回复后，发送查询执行器地址指令，成功返回执行器地址指令，才能开始发送指令控制和调节执行器。

发送指令：</br> EE 00 44 00 00 ED到ECB</br> 通信成功会收到返回指令:</br> EE 00 44 00 01 01 ED</br> 如果不知道ECB的ip地址，可通过广播方式发送该协议(即向192.168.1.255发送该协议)，确认ECB的ip地址后，即可通过该ip地址发送其他指令。

### 查询执行器

发送指令:</br> EE 00 02 00 00 ED</br> 通信成功会返回所有执行器的ID和mac地址信息，由于要轮询查找执行器，本条指令大约需要0.5s左右才能返回执行器id，如果长时间收不到执行器地址信息，可认为没有执行器成功连接。返回指令实例:</br> EE 06 02 00 04 01 64 5A DF 3B 3F ED</br> 其中06即为执行器的ID，01 64 5A DF为执行器mac地址。(当有多个执行器成功连接后，会多次返回该指令)

### 与执行器通信

成功查询到执行器后，即可根据执行器ID与执行器进行通信，例如启动ID为6的执行器的指令为：</br> EE 06 2A 00 01 01 7E 80 ED</br> 其中06为执行器ID,2A为启动或关闭执行器的指令，00 01是数据长度，01即为开机（00是关机），7E 80 为[CRC校验码](#CRC校验码计算方法 "wikilink")。

### 控制执行器

##### 位置控制

发送激活梯形位置模式指令:</br> EE 06 07 00 01 06 3F 42 ED</br> 数据06为梯形位置模式（参见[模式表](#模式表 "wikilink")），3F 42为[CRC校验码](#CRC校验码计算方法 "wikilink")，激活成功后会收到返回：</br> EE 06 07 00 01 01 ED</br> 这时可以发送速度指令：</br> EE 06 0A 00 04 00 01 00 00 01 D8 ED</br> 其中0A位设置速度值的指令，00 01 00 00位设置的位置值，该值是设置目标位置1R,通过公式：目标位置/128*（2^24）计算取整获得的IQ24值，关于IQ24的介绍请参考[ IQmath简介](#IQmath简介 "wikilink")。

### 其他

注意，设置速度电流位置值的命令均无返回，其他指令都有返回，更多与执行器通信指令请参考[以太网通信协议命令参考](#以太网通信协议命令参考 "wikilink")。

## **以太网通信协议命令参考**

### 读取命令
<table class="tableizer-table">
<thead><tr class="tableizer-firstrow"></tr></thead><tbody>
 <tr><td  colspan="3" style=background:PaleTurquoise>2.3.1.1 发送数据0字节， 返回数据1字节</td></tr>
 <tr><td>命令名称</td><td colspan="2">读取命令</td></tr>
 <tr><td>说明</td><td colspan="2">此命令类发送数据长度为1，返回数据长度为2</td></tr>
 <tr><td>指令符</td><td colspan="2"><p><a href="#以太网通信协议命令参考">见读取指令1</a> </p></td></tr>
 <tr><td>数据长度</td><td colspan="2">0</td></tr>
 <tr><td>数据内容</td><td colspan="2">无</td></tr>
 <tr><td>指令符（返回值）</td><td colspan="2">见读取指令1</td></tr>
 <tr><td>数据长度 (返回值)</td><td colspan="2">1</td></tr>
 <tr><td rowspan="2">下位机返回数据</td><td>0x01：成功/使能/开机/正常</td><td rowspan="2">模式查询返回数据见模式表</td></tr>
 <tr><td>0x00：失败/失能/关机/异常</td></tr>
</tbody></table>

<table class="tableizer-table">
<thead><tr class="tableizer-firstrow"></tr></thead><tbody>
 <tr><td colspan="3" style=background:PaleTurquoise>2.3.1.2 发送数据0字节，返回数据2字节</td></tr>
 <tr><td >命令名称</td><td colspan="2">读取命令</td></tr>
 <tr><td>说明</td><td  colspan="2">此命令类发送数据长度为1，返回数据长度为3，读取执行器参数值，高位在前。数值为真实值的2^8倍。（一条特殊指令指令表内已特殊标注）</td></tr>
 <tr><td>指令符</td><td  colspan="2">见读取指令2</td></tr>
 <tr><td>数据长度</td><td  colspan="2">0</td></tr>
 <tr><td>数据内容</td><td  colspan="2">无</td></tr>
 <tr><td>指令符（返回值）</td><td  colspan="2">见读取指令2</td></tr>
 <tr><td>数据长度 (返回值)</td><td  colspan="2">2</td></tr>
 <tr><td>下位机返回数据</td><td>数据为IQ8格式</td><td>或见报警指令表</td></tr>
</tbody></table>

<table class="tableizer-table">
<thead><tr class="tableizer-firstrow"></tr></thead><tbody>
 <tr><td  colspan="2" style=background:PaleTurquoise>2.3.1.3 发送数据0字节，返回数据4字节</td></tr>
 <tr><td>命令名称</td><td>读取命令</td></tr>
 <tr><td>说明</td><td>此命令类发送数据长度为1，返回数据长度为5，读取执行器参数值，高位在前。数值为真实值的2^24倍。（一条特殊指令指令表内已特殊标注）</td></tr>
 <tr><td>指令符</td><td>见读取指令3</td></tr>
 <tr><td>数据长度</td><td>0</td></tr>
 <tr><td>数据内容</td><td>无</td></tr>
 <tr><td>指令符（返回值）</td><td>见读取指令3</td></tr>
 <tr><td>数据长度 (返回值)</td><td>4</td></tr>
 <tr><td>下位机返回数据</td><td>数据为IQ24格式。(一条特殊指令指令表内已特殊标注)）</td></tr>
</tbody></table>

### 写入命令

<table class="tableizer-table">
<thead><tr class="tableizer-firstrow"></tr></thead><tbody>
 <tr><td colspan="3"style=background:PaleTurquoise>2.3.2.1发送数据1字节，返回数据1字节</td></tr>
 <tr><td>命令名称</td><td colspan="2">写入命令</td></tr>
 <tr><td>说明</td><td colspan="2">此命令类发送数据长度为2，返回数据长度为2，发送数据后一个字节表示要写入参数内容。(注：上电后先发送开机指令才能使用，断电前必须先发送关机指令，否则零位可能丢失)</td></tr>
 <tr><td>指令符</td><td colspan="2">见写入指令1</td></tr>
 <tr><td>数据长度</td><td colspan="2">1</td></tr>
 <tr><td rowspan="2">数据内容</td><td>0x01：使能/开机</td><td rowspan="2">模式设置见模式表</td></tr>
 <tr><td>0x00：失能/关机</td></tr>
 <tr><td>指令 (返回值)</td><td colspan="2">见写入指令1</td></tr>
 <tr><td>数据长度(返回值)</td><td colspan="2">1</td></tr>
 <tr><td rowspan="2">下位机返回数据</td><td colspan="2">0x01：成功</td></tr>
 <tr><td colspan="2">0x00：失败</td></tr>
</tbody></table>

<table class="tableizer-table">
<thead><tr class="tableizer-firstrow"></tr></thead><tbody>
 <tr><td colspan="2"style=background:PaleTurquoise>2.3.2.2发送数据2字节，返回数据1字节</td></tr>
 <tr><td>命令名称</td><td>写入命令</td></tr>
 <tr><td>说明</td><td>此命令类发送数据长度为3字节，返回数据长度为2字节，发送数据后2个字节表示要写入参数内容，高位在前。数值为真实值的2^8倍。</td></tr>
 <tr><td>指令符</td><td>见写入指令2</td></tr>
 <tr><td>数据长度</td><td>2</td></tr>
 <tr><td rowspan="2">数据内容</td><td>数值为IQ8格式</td></tr>
 <tr><td>0x00：失能/关机</td></tr>
 <tr><td>指令 (返回值)</td><td>见写入指令2</td></tr>
 <tr><td>数据长度(返回值)</td><td>1</td></tr>
 <tr><td rowspan="2">下位机返回数据</td><td>0x01：成功</td></tr>
 <tr><td>0x00：失败</td></tr>
</tbody></table>

<table class="tableizer-table">
<thead><tr class="tableizer-firstrow"><th  colspan="3"style=background:PaleTurquoise>2.3.2.3发送数据4字节，返回数据1字节或更少</th></tr></thead><tbody>
 <tr><td>命令名称</td><td colspan="2">写入命令</td></tr>
 <tr><td>说明</td><td  colspan="2">此命令类发送数据长度为5，返回数据长度为2，发送数据后4个字节表示要写入的参数内容，数值为真实值的2^24倍。(一条特殊指令指令表内已特殊标注)</td></tr>
 <tr><td>指令符</td><td  colspan="2">见写入指令3</td></tr>
 <tr><td>数据长度</td><td  colspan="2">4</td></tr>
 <tr><td>数据内容</td><td  colspan="2">数据为IQ24格式。(一条特殊指令指令表内已特殊标注)</td></tr>
 <tr><td>指令 (返回值)</td><td  colspan="2">见写入指令3</td></tr>
 <tr><td>数据长度(返回值)</td><td  colspan="2">1或0</td></tr>
 <tr><td  rowspan="2">下位机返回数据</td><td>0x01：成功</td><td  rowspan="2">(三条特殊指令无返回数据，指令表内已标注)。</td></tr>
 <tr><td  colspan="1">0x00：失败</td></tr>
</tbody></table>

<table class="tableizer-table">
<thead><tr class="tableizer-firstrow"><th colspan="2"style=background:PaleTurquoise>2.3.2.4发送数据0字节，返回数据1字节</th></tr></thead><tbody>
 <tr><td>命令名称</td><td>写入命令</td></tr>
 <tr><td>说明</td><td>此命令类发送数据长度为1，返回数据长度为2</td></tr>
 <tr><td>指令符</td><td>见写入指令4</td></tr>
 <tr><td>数据长度</td><td>0</td></tr>
 <tr><td>数据内容</td><td>无</td></tr>
 <tr><td>指令 (返回值)</td><td>见写入指令4</td></tr>
 <tr><td>数据长度(返回值)</td><td>1</td></tr>
 <tr><td rowspan="2">下位机返回数据</td><td>0x01：成功</td></tr>
 <tr><td>0x00：失败</td></tr>
</tbody></table>

## 附录A

#### IQmath简介

*   我们使用的处理器一般情况下，要么直接支持硬件的浮点运算，比如某些带有FPU的器件，要么就只支持定点运算，此时对浮点数的处理需要通过编译器来完成。在支持硬件浮点处理的器件上，对浮点运算的编程最快捷的方法就是直接使用浮点类型，比如单精度的float来完成。但是在很多情况下，限于成本、物料等因素，可供我们使用的只有一个定点处理器时，直接使用float类型进行浮点类型的运算会使得编译器产生大量的代码来完成一段看起来十分简单的浮点数学运算，造成的后果是程序的执行时间显著加长，且其占用的资源量也会成倍地增加，这就涉及到了如何在定点处理器上对浮点运算进行高效处理的问题。

*   既然是定点处理器，那么其对定点数，或者说字面意义上的“整数”进行处理的效率就会比它处理浮点类型的运算要高的多。所以在定点处理器上，我们使用定点的整数来代表一个浮点数，并规定整数位数和小数位数，从而方便地对定点数和浮点数进行转换。以一个32位的定点数为例，假设转换因子为Q，即32位中小数的位数为Q，整数位数则为31-Q(有符号数的情况)，则定点数与浮点数的换算关系为：

![详见 IQ-MATH Library文档](3-1通信协议.png "fig:详见 IQ-MATH Library文档") <embed src="C28x IQmath Library.pdf" title="fig:C28x IQmath Library.pdf" />

*   定点数=浮点数×2^Q

*   例如，浮点数-2.0转换到Q为24的定点数时，结果为：定点数=-2×2^24=-33554432

*   32位有符号数的表示范围是：-2147483648到2147483647。如果我们把有符号定点数的最大值2147483647转换为Q为24对应的浮点数，则结果为：浮点数2147483647/2^24=127.999999940

<table class="tableizer-table">
<thead><tr class="tableizer-firstrow"></tr></thead><tbody>
 <tr><td rowspan="2"style=background:PaleTurquoise>Data Type</td><td colspan="2"style=background:PaleTurquoise>Range</td><td  rowspan="2"style=background:PaleTurquoise>Resolution/Precision</td></tr>
 <tr><td>Min</td><td>Max</td></tr>
 <tr><td>_iq30</td><td>-2</td><td>1.999 999 999</td><td>0.000 000 001</td></tr>
 <tr><td>_iq29</td><td>-4</td><td>3.999 999 998</td><td>0.000 000 002</td></tr>
 <tr><td>_iq28</td><td>-8</td><td>7.999 999 996</td><td>0.000 000 004</td></tr>
 <tr><td>_iq27</td><td>-16</td><td>15.999 999 993</td><td>0.000 000 007</td></tr>
 <tr><td>_iq26</td><td>-32</td><td>31.999 999 985</td><td>0.000 000 015</td></tr>
 <tr><td>_iq25</td><td>-64</td><td>63.999 999 970</td><td>0.000 000 030</td></tr>
 <tr><td>_iq24</td><td>-128</td><td>127.999 999 940</td><td>0.000 000 060</td></tr>
 <tr><td>_iq23</td><td>-256</td><td>255.999 999 981</td><td>0.000 000 119</td></tr>
 <tr><td>_iq22</td><td>-512</td><td>511.999 999 762</td><td>0.000 000 238</td></tr>
 <tr><td>_iq21</td><td>-1024</td><td>1023.999 999 523</td><td>0.000 000 477</td></tr>
 <tr><td>_iq20</td><td>-2048</td><td>2047.999 999 046</td><td>0.000 000 954</td></tr>
 <tr><td>_iq19</td><td>-4096</td><td>4095.999 998 093</td><td>0.000 001 907</td></tr>
 <tr><td>_iq18</td><td>-8192</td><td>8191.999 996 185</td><td>0.000 003 815</td></tr>
 <tr><td>_iq17</td><td>-16384</td><td>16383.999 992 371</td><td>0.000 007 629</td></tr>
 <tr><td>_iq16</td><td>-32768</td><td>32767.999 984 741</td><td>0.000 015 259</td></tr>
 <tr><td>_iq15</td><td>-65536</td><td>65535.999 969 482</td><td>0.000 030 518</td></tr>
 <tr><td>_iq14</td><td>-131072</td><td>131071.999 938 965</td><td>0.000 061 035</td></tr>
 <tr><td>_iq13</td><td>-262144</td><td>262143.999 877 930</td><td>0.000 122 070</td></tr>
 <tr><td>_iq12</td><td>-524288</td><td>524287.999 755 859</td><td>0.000 244 141</td></tr>
 <tr><td>_iq11</td><td>-1048576</td><td>1048575.999 511 719</td><td>0.000 488 281</td></tr>
 <tr><td>_iq10</td><td>-2097152</td><td>2097151.999 023 437</td><td>0.000 976 563</td></tr>
 <tr><td>_iq9</td><td>-4194304</td><td>4194303.998 046 875</td><td>0.001 953 125</td></tr>
 <tr><td>_iq8</td><td>-8388608</td><td>8388607.996 093 750</td><td>0.003 906 250</td></tr>
 <tr><td>_iq7</td><td>-16777216</td><td>16777215.992 187 500</td><td>0.007 812 500</td></tr>
 <tr><td>_iq6</td><td>-33554432</td><td>33554431.984 375 000</td><td>0.015 625 000</td></tr>
 <tr><td>_iq5</td><td>-67108864</td><td>67108863.968 750 000</td><td>0.031 250 000</td></tr>
 <tr><td>_iq4</td><td>-134217728</td><td>134217727.937 500 000</td><td>0.062 500 000</td></tr>
 <tr><td>_iq3</td><td>-268435456</td><td>268435455.875 000 000</td><td>0.125 000 000</td></tr>
 <tr><td>_iq2</td><td>-536870912</td><td>536870911.750 000 000</td><td>0.250 000 000</td></tr>
 <tr><td>_iq1</td><td>-1073741824</td><td>1 073741823.500 000 000</td><td>0.500 000 000</td></tr>
</tbody></table>

<div class="figure">
![3-2通信协议-1.png](3-2通信协议-1.png "3-2通信协议-1.png")

3-2通信协议-1.png

</div>

*   注释：
*   上位机所设置的上限幅值（Maximum）最高为_IQ(1.0)，下限幅值（Minimal）最低为_IQ(-1.0)，起到限幅作用（原理图如图3-2）。例：（如图:3-2用位置环的输出经过限幅模块为速度环的输入，假设_IQ（0.5），_IQ（-0.5）则位置环输出最大速度应为±0.5x6000=±3000RPM）
*   比例积分设置值上限为_IQ(128.0)，设定值下限为_IQ(-128.0)，但设置值根据实际操作情况调节（原理图: 3-2）
*   电流环设置电流值范围为_IQ(-1.0)~_IQ(1.0)之间，电流实际值为IQ值乘以满量程，例：（QDD-6010 型号执行器满量程电流值为33A ，_IQ(0.5) 实际电流值则为0.5x33A=16.5A，见附录D:型号表）
*   速度环设置速度值范围为_IQ(-1.0)~_IQ(1.0)之间，速度实际值为IQ值乘以满量程（见 ）。例：（_IQ(0.5)则实际速度为0.5*6000=3000RPM）
*   位置环因为是_IQ24格式，所以正向满量程为_IQ(127.999999940)，反向满量程为_IQ(-128.0)，IQ值即实际值，例：<span style="color: red">（_IQ（60.0）则实际位置为60R，即零位置正向转60转的位置。）</span>
*   速度环曲线模式和位置环曲线模式，可以通过设置加速度，减速度的大小，相对平滑的达到自己预设的速度值和位置，可以避免操作时瞬间电流过大，触发执行器过流保护或者供电电源过流保护。

### **CRC校验码计算方法**

CRC校验只计算数据内容，即数据长度之后到crc校验之前的所有内容，计算方法采用查表法。

CRC校验码计算方法（c++）:

    const uint8_t chCRCHTalbe[] =                                 // CRC 高位字节值表
    {
        0x00, 0xC1, 0x81, 0x40, 0x01, 0xC0, 0x80, 0x41, 0x01, 0xC0, 0x80, 0x41,
        0x00, 0xC1, 0x81, 0x40, 0x01, 0xC0, 0x80, 0x41, 0x00, 0xC1, 0x81, 0x40,
        0x00, 0xC1, 0x81, 0x40, 0x01, 0xC0, 0x80, 0x41, 0x01, 0xC0, 0x80, 0x41,
        0x00, 0xC1, 0x81, 0x40, 0x00, 0xC1, 0x81, 0x40, 0x01, 0xC0, 0x80, 0x41,
        0x00, 0xC1, 0x81, 0x40, 0x01, 0xC0, 0x80, 0x41, 0x01, 0xC0, 0x80, 0x41,
        0x00, 0xC1, 0x81, 0x40, 0x01, 0xC0, 0x80, 0x41, 0x00, 0xC1, 0x81, 0x40,
        0x00, 0xC1, 0x81, 0x40, 0x01, 0xC0, 0x80, 0x41, 0x00, 0xC1, 0x81, 0x40,
        0x01, 0xC0, 0x80, 0x41, 0x01, 0xC0, 0x80, 0x41, 0x00, 0xC1, 0x81, 0x40,
        0x00, 0xC1, 0x81, 0x40, 0x01, 0xC0, 0x80, 0x41, 0x01, 0xC0, 0x80, 0x41,
        0x00, 0xC1, 0x81, 0x40, 0x01, 0xC0, 0x80, 0x41, 0x00, 0xC1, 0x81, 0x40,
        0x00, 0xC1, 0x81, 0x40, 0x01, 0xC0, 0x80, 0x41, 0x01, 0xC0, 0x80, 0x41,
        0x00, 0xC1, 0x81, 0x40, 0x00, 0xC1, 0x81, 0x40, 0x01, 0xC0, 0x80, 0x41,
        0x00, 0xC1, 0x81, 0x40, 0x01, 0xC0, 0x80, 0x41, 0x01, 0xC0, 0x80, 0x41,
        0x00, 0xC1, 0x81, 0x40, 0x00, 0xC1, 0x81, 0x40, 0x01, 0xC0, 0x80, 0x41,
        0x01, 0xC0, 0x80, 0x41, 0x00, 0xC1, 0x81, 0x40, 0x01, 0xC0, 0x80, 0x41,
        0x00, 0xC1, 0x81, 0x40, 0x00, 0xC1, 0x81, 0x40, 0x01, 0xC0, 0x80, 0x41,
        0x00, 0xC1, 0x81, 0x40, 0x01, 0xC0, 0x80, 0x41, 0x01, 0xC0, 0x80, 0x41,
        0x00, 0xC1, 0x81, 0x40, 0x01, 0xC0, 0x80, 0x41, 0x00, 0xC1, 0x81, 0x40,
        0x00, 0xC1, 0x81, 0x40, 0x01, 0xC0, 0x80, 0x41, 0x01, 0xC0, 0x80, 0x41,
        0x00, 0xC1, 0x81, 0x40, 0x00, 0xC1, 0x81, 0x40, 0x01, 0xC0, 0x80, 0x41,
        0x00, 0xC1, 0x81, 0x40, 0x01, 0xC0, 0x80, 0x41, 0x01, 0xC0, 0x80, 0x41,
        0x00, 0xC1, 0x81, 0x40
    };
    const uint8_t chCRCLTalbe[] =                                 // CRC 低位字节值表
    {
        0x00, 0xC0, 0xC1, 0x01, 0xC3, 0x03, 0x02, 0xC2, 0xC6, 0x06, 0x07, 0xC7,
        0x05, 0xC5, 0xC4, 0x04, 0xCC, 0x0C, 0x0D, 0xCD, 0x0F, 0xCF, 0xCE, 0x0E,
        0x0A, 0xCA, 0xCB, 0x0B, 0xC9, 0x09, 0x08, 0xC8, 0xD8, 0x18, 0x19, 0xD9,
        0x1B, 0xDB, 0xDA, 0x1A, 0x1E, 0xDE, 0xDF, 0x1F, 0xDD, 0x1D, 0x1C, 0xDC,
        0x14, 0xD4, 0xD5, 0x15, 0xD7, 0x17, 0x16, 0xD6, 0xD2, 0x12, 0x13, 0xD3,
        0x11, 0xD1, 0xD0, 0x10, 0xF0, 0x30, 0x31, 0xF1, 0x33, 0xF3, 0xF2, 0x32,
        0x36, 0xF6, 0xF7, 0x37, 0xF5, 0x35, 0x34, 0xF4, 0x3C, 0xFC, 0xFD, 0x3D,
        0xFF, 0x3F, 0x3E, 0xFE, 0xFA, 0x3A, 0x3B, 0xFB, 0x39, 0xF9, 0xF8, 0x38,
        0x28, 0xE8, 0xE9, 0x29, 0xEB, 0x2B, 0x2A, 0xEA, 0xEE, 0x2E, 0x2F, 0xEF,
        0x2D, 0xED, 0xEC, 0x2C, 0xE4, 0x24, 0x25, 0xE5, 0x27, 0xE7, 0xE6, 0x26,
        0x22, 0xE2, 0xE3, 0x23, 0xE1, 0x21, 0x20, 0xE0, 0xA0, 0x60, 0x61, 0xA1,
        0x63, 0xA3, 0xA2, 0x62, 0x66, 0xA6, 0xA7, 0x67, 0xA5, 0x65, 0x64, 0xA4,
        0x6C, 0xAC, 0xAD, 0x6D, 0xAF, 0x6F, 0x6E, 0xAE, 0xAA, 0x6A, 0x6B, 0xAB,
        0x69, 0xA9, 0xA8, 0x68, 0x78, 0xB8, 0xB9, 0x79, 0xBB, 0x7B, 0x7A, 0xBA,
        0xBE, 0x7E, 0x7F, 0xBF, 0x7D, 0xBD, 0xBC, 0x7C, 0xB4, 0x74, 0x75, 0xB5,
        0x77, 0xB7, 0xB6, 0x76, 0x72, 0xB2, 0xB3, 0x73, 0xB1, 0x71, 0x70, 0xB0,
        0x50, 0x90, 0x91, 0x51, 0x93, 0x53, 0x52, 0x92, 0x96, 0x56, 0x57, 0x97,
        0x55, 0x95, 0x94, 0x54, 0x9C, 0x5C, 0x5D, 0x9D, 0x5F, 0x9F, 0x9E, 0x5E,
        0x5A, 0x9A, 0x9B, 0x5B, 0x99, 0x59, 0x58, 0x98, 0x88, 0x48, 0x49, 0x89,
        0x4B, 0x8B, 0x8A, 0x4A, 0x4E, 0x8E, 0x8F, 0x4F, 0x8D, 0x4D, 0x4C, 0x8C,
        0x44, 0x84, 0x85, 0x45, 0x87, 0x47, 0x46, 0x86, 0x82, 0x42, 0x43, 0x83,
        0x41, 0x81, 0x80, 0x40
    };
    
    static uint16_t CRC16_1(uint8_t* pchMsg, int16_t wDataLen)
    {
        uint8_t chCRCHi = 0xFF; // 高CRC字节初始化
        uint8_t chCRCLo = 0xFF; // 低CRC字节初始化
        int16_t wIndex;            // CRC循环中的索引
        while (wDataLen--)
        {
            // 计算CRC
            wIndex = chCRCHi ^ *pchMsg++;
            chCRCHi = chCRCLo ^ chCRCHTalbe[wIndex];
            chCRCLo = chCRCLTalbe[wIndex];
        }
        return ((chCRCHi << 8) | chCRCLo);
    }

CRC16_1方法中，pchMsg指向要校验内容的地址，wDataLen为要校验内容的字节长度，该方法会返回两字节的crc校验码，将校验码加入到发送的指令中的对应位置即可。收到返回带crc校验码的指令，也可以通过该方法计算出校验码并与返回指令中的校验码比对，验证数据的有效性。

**示例**

执行器开机指令:

EE 06 2A 00 01 01 7E 80 ED

其中EE为帧头，06是执行器ID，2A为开机指令符，00 01 为数据长度，01为数据内容，ED为帧尾，其中数据内容01通过上述方法计算出的校验码即为7E 80。

### **A.1读取指令编码定义表**

<table class="tableizer-table">
<thead><tr class="tableizer-firstrow"></tr></thead><tbody>
 <tr><td colspan="3"style=background:PaleTurquoise>A.1.1 读取指令1</td></tr>
 <tr><td>指令符</td><td>定义</td><td>说明</td></tr>
 <tr><td>0x00 ：</td><td>握手</td><td>上位机发送本指令，下位机响应返回，说明下位机已经准备好与上位机通信也可作为心跳协议，实时查询从机的状态。</td></tr>
 <tr><td>0x55：</td><td>查询执行器当前模式</td><td>读取下位机所管理的执行器的当前的模式。</td></tr>
 <tr><td>0xB0</td><td>查询执行器上次关机状态</td><td>读取执行器的上次关机状态，正常/异常</td></tr>
 <tr><td>0x71：</td><td>电流环滤波器状态</td><td>读取指定ID执行器的电流环滤波器使能/失能</td></tr>
 <tr><td>0x75：</td><td>速度环滤波器状态</td><td>读取指定ID执行器的电流环滤波器使能/失能</td></tr>
 <tr><td>0x79：</td><td>位置环滤波器状态</td><td>读取指定ID执行器的电流环滤波器使能/失能</td></tr>
 <tr><td>0x2B</td><td>电流环滤波器状态</td><td>读取指定ID执行器开机/停机状态。</td></tr>
</tbody></table>

<table class="tableizer-table">
<thead><tr class="tableizer-firstrow"></tr></thead><tbody>
 <tr><td  colspan="3"style=background:PaleTurquoise>A.1.2 读取指令2</td></tr>
 <tr><td>指令符</td><td>定义</td><td>说明</td></tr>
 <tr><td>0x73：</td><td>电流环滤波器的带宽</td><td>读取指定ID执行器电流环滤波器的带宽(Hz)</td></tr>
 <tr><td>0x77：</td><td>速度环滤波器的带宽</td><td>读取指定ID执行器速度环滤波器的带宽(Hz)</td></tr>
 <tr><td>0x7B：</td><td>位置环滤波器的带宽</td><td>读取指定ID执行器速度环滤波器的带宽(Hz)</td></tr>
 <tr><td>0x5F</td><td>读取执行器电机的温度</td><td>读取指定ID执行器电机温度℃</td></tr>
 <tr><td>0x60</td><td>读取逆变器温度</td><td>读取指定ID执行器的逆变器温度℃</td></tr>
 <tr><td>0x62</td><td>读取执行器保护温度</td><td>读取指定ID执行器的保护温度℃</td></tr>
 <tr><td>0x64</td><td>读取执行器恢复温度</td><td>读取指定ID执行器的恢复温度℃</td></tr>
 <tr><td>0xFF</td><td>报警指令(特殊指令)</td><td>下位机的报警信息</td></tr>
</tbody></table>

<table class="tableizer-table">
<thead><tr class="tableizer-firstrow"></tr></thead><tbody>
 <tr><td  colspan="3"style=background:PaleTurquoise>A.1.3 读取指令3</td></tr>
 <tr><td>指令符</td><td>定义</td><td>说明</td></tr>
 <tr><td>0x04：</td><td>当前电流值</td><td>读取指定ID执行器的当前电流值，电流真实值需要乘以电流满量程（见附录D），单位为A</td></tr>
 <tr><td>0x05：</td><td>当前速度值</td><td>读取指定ID执行器的当前速度值，速度真实值需要乘以速度满量程（见附录D），单位为RPM</td></tr>
 <tr><td>0x06：</td><td>当前位置值</td><td>读取指定ID执行器的当前位置值，单位为R</td></tr>
 <tr><td>0x15：</td><td>电流环的P</td><td>读取指定ID执行器的当前电流环的P</td></tr>
 <tr><td>0x16：</td><td>电流环的I</td><td>读取指定ID执行器的当前电流环的I</td></tr>
 <tr><td>0x17：</td><td>速度环的P</td><td>读取指定ID执行器的当前速度环的P</td></tr>
 <tr><td>0x18：</td><td>速度环的I</td><td>读取指定ID执行器的当前速度环的I</td></tr>
 <tr><td>0x19：</td><td>位置环的P</td><td>读取指定ID执行器的当前位置环的P</td></tr>
 <tr><td>0x1A：</td><td>位置环的I</td><td>读取指定ID执行器的当前位置环的I</td></tr>
 <tr><td>0x1C：</td><td>位置梯形曲线的最大速度</td><td>读取指定ID执行器的当前位置梯形曲线的最大速度</td></tr>
 <tr><td>0x1D：</td><td>位置梯形曲线的加速度</td><td>读取指定ID执行器的当前位置梯形曲线的最大加速度</td></tr>
 <tr><td>0x1E：</td><td>位置梯形曲线的减速度</td><td>读取指定ID执行器的当前位置梯形曲线的最大减速度</td></tr>
 <tr><td>0x22：</td><td>速度梯形曲线的最大速度</td><td>读取指定ID执行器的当前速度梯形曲线的最大速度</td></tr>
 <tr><td>0x23：</td><td>速度梯形曲线的加速度</td><td>读取指定ID执行器的当前速度梯形曲线的最大加速度</td></tr>
 <tr><td>0x24：</td><td>速度梯形曲线的减速度</td><td>读取指定ID执行器的当前速度梯形曲线的最大减速度</td></tr>
 <tr><td>0x34：</td><td>电流环输出的下限</td><td>读取指定ID执行器的当前电流环输出的下限</td></tr>
 <tr><td>0x35：</td><td>电流环输出的上限</td><td>读取指定ID执行器的当前电流环输出的上限</td></tr>
 <tr><td>0x36：</td><td>速度环输出的下限</td><td>读取指定ID执行器的当前速度环输出的下限</td></tr>
 <tr><td>0x37：</td><td>速度环输出的上限</td><td>读取指定ID执行器的当前速度环输出的上限</td></tr>
 <tr><td>0x38：</td><td>位置环输出的下限</td><td>读取指定ID执行器的当前位置环输出的下限</td></tr>
 <tr><td>0x39：</td><td>位置环输出的上限</td><td>读取指定ID执行器的当前位置环输出的上限</td></tr>
 <tr><td>0x7D：</td><td>惯量</td><td>读取指定ID执行器的惯量</td></tr>
 <tr><td>0x85：</td><td>执行器位置的上限</td><td>读取指定ID执行器的位置上限值</td></tr>
 <tr><td>0x86：</td><td>执行器位置的下限</td><td>读取执行ID执行器的位置下限值</td></tr>
 <tr><td>0x8A：</td><td>执行器位置偏置位置</td><td>读取指定ID执行器的位置偏置值</td></tr>
 <tr><td>0x92：</td><td>执行器自动归零时电流的下限</td><td>读取指定ID执行器自动归零时电流的下限</td></tr>
 <tr><td>0x93：</td><td>执行器自动归零时电流的上限</td><td>读取指定ID执行器自动归零是电流的上限</td></tr>
 <tr><td>0x7F：</td><td>堵转能量</td><td>读取指定ID执行器的堵转能量。 （数值为真实值的75.225倍）堵转后发热能量，单位为J。</td></tr>
</tbody></table>

### **A.2 写入命令编码值定义表**

<table class="tableizer-table">
<thead><tr class="tableizer-firstrow"><th colspan="3"style=background:PaleTurquoise>A.2.1写入指令1</th></tr></thead><tbody>
 <tr><td>指令符</td><td>定义</td><td>说明</td></tr>
 <tr><td>0x07：</td><td>设置指定ID执行器的模式</td><td>设置指定ID执行器的当前的模式。</td></tr>
 <tr><td>0x70：</td><td>电流环滤波器状态</td><td>设置指定ID执行器的电流环滤波器使能/失能</td></tr>
 <tr><td>0x74：</td><td>速度环滤波器状态</td><td>设置指定ID执行器的速度环滤波器使能/失能</td></tr>
 <tr><td>0x78：</td><td>位置环滤波器状态</td><td>设置指定ID执行器的位置环滤波器使能/失能</td></tr>
 <tr><td>0x2A：</td><td>执行器的开关机状态</td><td>设置指定ID执行器开机/关机</td></tr>
</tbody></table>

<table class="tableizer-table">
<thead><tr class="tableizer-firstrow"><th colspan="3"style=background:PaleTurquoise>A.2.2写入指令2</th></tr></thead><tbody>
 <tr><td>指令符</td><td>定义</td><td>说明</td></tr>
 <tr><td>0x72：</td><td>电流环滤波器的带宽</td><td>设置指定ID执行器电流环滤波器的带宽(Hz)</td></tr>
 <tr><td>0x76：</td><td>速度环滤波器的带宽</td><td>设置指定ID执行器速度环滤波器的带宽(Hz)</td></tr>
 <tr><td>0x7A：</td><td>位置环滤波器的带宽</td><td>设置指定ID执行器位置环滤波器的带宽(Hz)</td></tr>
 <tr><td>0x61：</td><td>执行器的保护温度</td><td>设置指定ID执行器的保护温度℃</td></tr>
 <tr><td>0x63：</td><td>执行器的恢复温度</td><td>设置指定ID执行器的恢复温度℃</td></tr>
</tbody></table>

<table class="tableizer-table">
<thead><tr class="tableizer-firstrow"><th colspan="3"style=background:PaleTurquoise>A.2.3写入指令3</th></tr></thead><tbody>
 <tr><td>指令符</td><td>定义</td><td>说明</td></tr>
 <tr><td>0x08：</td><td>当前电流值</td><td>设置指定ID执行器的当前电流值。 (注：无返回数据)</td></tr>
 <tr><td>0x09：</td><td>当前速度值</td><td>设置指定ID执行器的当前速度值。 (注：无返回数据）</td></tr>
 <tr><td>0x0A：</td><td>当前位置值</td><td>设置指定ID执行器的当前位置值。 (注：无返回数据）</td></tr>
 <tr><td>0x0E：</td><td>电流环的P</td><td>更改指定ID执行器电流环的P值</td></tr>
 <tr><td>0x0F：</td><td>电流环的I</td><td>设置指定ID执行器电流环的I值</td></tr>
 <tr><td>0x10：</td><td>速度环的P</td><td>设置指定ID执行器速度环的P值</td></tr>
 <tr><td>0x11：</td><td>速度环的I</td><td>设置指定ID执行器速度环的I值</td></tr>
 <tr><td>0x12：</td><td>位置环的P</td><td>设置指定ID执行器位置环的P值</td></tr>
 <tr><td>0x13：</td><td>位置环的I</td><td>设置指定ID执行器位置环的I值</td></tr>
 <tr><td>0x1F：</td><td>位置梯形曲线的最大速度</td><td>更改指定ID执行器位置梯形曲线的最大速度</td></tr>
 <tr><td>0x20：</td><td>位置梯形曲线的加速度</td><td>更改指定ID执行器位置梯形曲线的最大加速度</td></tr>
 <tr><td>0x21：</td><td>位置梯形曲线的减速速度</td><td>更改指定ID执行器位置梯形曲线的最大减速度</td></tr>
 <tr><td>0x25：</td><td>速度梯形曲线的最大速度</td><td>更改指定ID执行器速度梯形曲线的最大速度</td></tr>
 <tr><td>0x26：</td><td>速度梯形曲线的加速度</td><td>更改指定ID执行器速度梯形曲线的加速度</td></tr>
 <tr><td>0x27：</td><td>速度梯形曲线的减速度</td><td>更改指定ID执行器速度梯形曲线的减速度</td></tr>
 <tr><td>0x2E：</td><td>电流环输出的下限</td><td>更改指定ID执行器电流环输出的下限</td></tr>
 <tr><td>0x2F：</td><td>电流环输出的上限</td><td>更改指定ID执行器电流环输出的上限</td></tr>
 <tr><td>0x30：</td><td>速度环输出的下限</td><td>更改指定ID执行器速度环输出的下限</td></tr>
 <tr><td>0x31：</td><td>速度环输出的上限</td><td>更改指定ID执行器速度环输出的上限</td></tr>
 <tr><td>0x32：</td><td>位置环输出的下限</td><td>更改指定ID执行器位置环输出的下限</td></tr>
 <tr><td>0x33：</td><td>位置环输出的上限</td><td>更改指定ID执行器位置环输出的上限</td></tr>
 <tr><td>0x83：</td><td>执行器位置的上限</td><td>更改指定ID执行器的位置上限值</td></tr>
 <tr><td>0x84：</td><td>执行器位置的下限</td><td>更改指定ID执行器的位置下限值</td></tr>
 <tr><td>0x87：</td><td>执行器的Home值</td><td>设置指定ID执行器的Home值</td></tr>
 <tr><td>0x89：</td><td>执行器的位置偏置</td><td>设置指定ID执行器的位置偏置值</td></tr>
 <tr><td>0x90：</td><td>执行器自动归零时电流的下</td><td>设置指定ID执行器自动归零时电流的下限</td></tr>
 <tr><td>0x91：</td><td>执行器自动归零时电流的上</td><td>设置指定ID执行器自动归零时电流的上限</td></tr>
 <tr><td>0x7E：</td><td>堵转能量</td><td>设置指定ID执行器的堵转能量。 (数值为真实值的75.225倍)堵转后发热能量，单位为J</td></tr>
</tbody></table>

<table class="tableizer-table">
<thead><tr class="tableizer-firstrow"><th   colspan="3"style=background:PaleTurquoise>A.2.4写入指令4</th></tr></thead><tbody>
 <tr><td>指令符</td><td>定义</td><td>说明</td></tr>
 <tr><td>0xFE：</td><td>消除下位机的报警</td><td>消除下位机的报警动作，接收到命令后，下位机停止报警，否则下位机不可操作</td></tr>
 <tr><td>0x88</td><td>清除Homing数据</td><td>清除Homing数据</td></tr>
 <tr><td>0x0D</td><td>存储参数</td><td>存储参数到EEPROM</td></tr>
</tbody></table>

## <span id="模式表"></span>附录B :模式表

<table class="tableizer-table">
<thead><tr class="tableizer-firstrow"><th style=background:PaleTurquoise>指令符</th><th style=background:PaleTurquoise>指令符</th></tr></thead><tbody>
 <tr><td>01</td><td>电流模式</td></tr>
 <tr><td>02</td><td>速度模式</td></tr>
 <tr><td>03</td><td>位置模式</td></tr>
 <tr><td>04</td><td>示教模式</td></tr>
 <tr><td>05</td><td>回放模式</td></tr>
 <tr><td>06</td><td>梯形位置模式</td></tr>
 <tr><td>07</td><td>梯形速度模式</td></tr>
 <tr><td>08</td><td>homing模式</td></tr>
</tbody></table>

## 附录C：<span id="报警指令表"></span>报警指令表

<table class="tableizer-table">
<thead><tr class="tableizer-firstrow"><th style=background:PaleTurquoise>指令符</th><th style=background:PaleTurquoise>指令符</th></tr></thead><tbody>
 <tr><td>0x0001</td><td>过压异常</td></tr>
 <tr><td>0x0002</td><td>欠压异常</td></tr>
 <tr><td>0x0004</td><td>堵转异常</td></tr>
 <tr><td>0x0008</td><td>过热异常</td></tr>
 <tr><td>0x0010</td><td>读写参数异常</td></tr>
 <tr><td>0x0020</td><td>多圈计数异常</td></tr>
 <tr><td>0x0040</td><td>逆变器温度传感器异常</td></tr>
 <tr><td>0x0080</td><td>CAN通信异常</td></tr>
 <tr><td>0x0100</td><td>电机温度传感器异常</td></tr>
 <tr><td>0x0200</td><td>位置模式阶跃大于1</td></tr>
 <tr><td>0x0400</td><td>DRV保护</td></tr>
 <tr><td>其他</td><td>设备异常</td></tr>
 <tr><td>注释</td><td>可同时报警多个错误，如返回数据为0005，则错误为0001过压异常与0004堵转异常</td></tr>
</tbody></table>

## 附录D：<span id="型号表"></span>型号表

<table class="tableizer-table">
<thead><tr class="tableizer-firstrow"><th style=background:PaleTurquoise>执行器型号</th><th style=background:PaleTurquoise>电流满量程</th><th style=background:PaleTurquoise>电机端速度满量程</th><th style=background:PaleTurquoise>输出端速度满量程</th></tr></thead><tbody>
 <tr><td>QDD Pro-8108-50</td><td>33A</td><td>1500RPM</td><td>30RPM</td></tr>
 <tr><td>QDD-8108-6</td><td>33A</td><td>1500RPM</td><td>250RPM</td></tr>
 <tr><td>DD-8108</td><td>33A</td><td>1500RPM</td><td>1500RPM</td></tr>
 <tr><td>QDD Pro-6010-50</td><td>33A</td><td>4200RPM</td><td>84RPM</td></tr>
 <tr><td>QDD-6010-36</td><td>33A</td><td>4200RPM</td><td>117RPM</td></tr>
 <tr><td>DD-6010</td><td>33A</td><td>4200RPM</td><td>4200RPM</td></tr>
 <tr><td>QDD Pro-3510-50</td><td>16.5A</td><td>6000RPM</td><td>120RPM</td></tr>
 <tr><td>QDD-3510-6</td><td>16.5A</td><td>6000RPM</td><td>1000RPM</td></tr>
 <tr><td>QDD-3510-36</td><td>16.5A</td><td>6000RPM</td><td>166.7RPM</td></tr>
 <tr><td>DD-3510</td><td>16.5A</td><td>6000RPM</td><td>6000RPM</td></tr>
 <tr><td>QDD-2305-6</td><td>16.5A</td><td>6000RPM</td><td>1000RPM</td></tr>
 <tr><td>QDD-2305-36</td><td>16.5A</td><td>6000RPM</td><td>166.7RPM</td></tr>
 <tr><td>DD-2305</td><td>16.5A</td><td>6000RPM</td><td>6000RPM</td></tr>
</tbody></table>

*   输出端速度不同是因为个别型号执行器内置减速器，使输出的最大转速降低，提高扭矩。IQ换算时按照电机端速度满量程的值计算。

## 版本变更记录

下表简单描述了版本变更记录

<table class="tableizer-table">
<thead><tr class="tableizer-firstrow"><th style=background:PaleTurquoise>版本号</th><th style=background:PaleTurquoise>更新时间</th><th style=background:PaleTurquoise>更新内容</th></tr></thead><tbody>
 <tr><td>V1.0.0</td><td>18.04.28</td><td>增加100报警指令</td></tr>
</tbody></table>
