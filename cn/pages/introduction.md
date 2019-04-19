[English](Introduction "wikilink")

# 概述

*   INNFOS提供模块化机器人构建块，使您可以快速构建和编程自定义机器人系统。我们提供智能兼容执行器（SCA），数字和模拟接口板以及将这些组件连接在一起的机械和电气硬件（另请参阅[硬件配置](硬件配置 "wikilink")）。与硬件同样重要的是，INNFOS还提供软件工具和API来编程和控制从这些物理组件创建的机器人系统（有关详细信息，请参阅[Software &amp; Development](Main_Page#Learning "wikilink")），建议使用由INNFOS Actuator Studio（IAS）开发的INNFOS for SCA快速安全的调试。

[![](https://github.com/innfos/wiki/blob/master/cn/img/shouyesca1.png)](https://github.com/innfos/wiki/blob/master/cn/img/shouyesca1.png)

> Innfos SCA.


## INNFOS SCA

*   INNFOS SCA（Smart Compliant Actuator）是一种智能，高度集成和先进的伺服系统，具有灵活和安全的控制。它高度集成了伺服电机，伺服驱动器，减速器和编码器的核心部件。在相同性能下，其体积仅为传统伺服系统的十分之一。与传统的机器人驱动相比，SCA是一项革命性的突破。它有效地解决了各类机器人多关节连接的结构问题，保证了服务机器人的联合控制和安全使用。这使得服务机器人能够与人类一起工作和生活，这为第四次工业革命和即将到来的智能机器人时代提供了重要的核心技术。

[![](https://github.com/innfos/wiki/blob/master/cn/img/shouyesca2.jpeg)](https://github.com/innfos/wiki/blob/master/cn/img/shouyesca1.jpeg)



<div class="figure">


</div>

## 应用领域

*   INNFOS SCA包括带减速器的QDD Pro，使用行星减速器的QDD和不带减速器的DD。SCA可以应用于多种场景。最小的SCA可应用于三脚架头，无人机等，而最大的SCA可应用于机器人，机器人臂等。当然，SCA通常用于电动工具，CNC，3D打印机，AGV等。
<div class="figure">

</div>

# 版本变更记录

下表简单描述了版本变更记录

| 版本        | 	日期   |  	修改内容  |
| :--------:  | :-----:  | :----:  |
| V1.0.3      | 	2019-4-15   |   	修改原理图图片    |
| V1.0.2       |  2019-4-9  |   	添加型号: <br>DD-2305   |
| V1.0.1       |   2019-4-4    |  删除型号:<br>QDD-6010-8<br>QDD-6010-64 <br>QDD-8108-8 <br>QDD-8108-64<br>添加型号:<br>QDD-6010-6 <br>QDD-6010-36 <br>QDD-8108-6 <br>QDD-8108-36  |
| V1.0.0       |   2018-11-12  |  第一个版本 |


<table>
  <p>style=&quot;background: PaleTurquoise; color: black;width:75px&quot;</p>
  
  <thead>
        <td width=100px; style="backgroud-color:red">版本号</td> 
        <td width=100px; bgcolor="#AFEEEE">更新时间</td> 
        <td width=100px; bgcolor="#AFEEEE">更改类型</td>
        <td width=150px; bgcolor="#AFEEEE">更改类型</td>
        <td bgcolor="#AFEEEE">内容</td>
   </thead>
  <tbody>
    <tr>
        <td>V1.0.4</td>  
        <td>18.12.14</td> 
        <td>增加</td> 
        <td>附录E</td>
        <td>指令发送与IQ值换算方法</td>
    </tr>
    <tr>
        <td rowspan="4">V1.0.3</td> 
        <td rowspan="4">18.03.19</td> 
        <td>增加</td>
        <td>第三章通信协议</td>
        <td>较上一版本多加了更多的执行器参数信息指令，执行器的温度信息指令。<br/>查询上次关机状态指令，Homing指令。</td> 
    </tr>
      <tr> 
        <td>增加</td>
        <td>第三章通信协议</td>
        <td>增加了储存参数指令</td>   
    </tr>
      <tr> 
        <td>修改</td>
        <td>第三章通信协议</td>
        <td>修改了第三章全章的排版</td>   
    </tr> 
        <tr> 
        <td>增加</td>
        <td>第三章通信协议</td>
        <td>增加了储存参数指令</td>   
    </tr>
  <tr>
        <td rowspan="2">V1.0.2</td> 
        <td rowspan="2">18.01.20</td> 
        <td>修改</td>
        <td>全文</td>
        <td>微伺服更名为INNFOS执行器</td> 
    </tr>
    <tr>
        <td>增加</td>
        <td>第三章通信协议</td>
        <td>较上一版本多加了报警指令</td> 
    </tr>
  <tr> 
    <td>V1.0.1
    <td>17.12.29
    <td>修改	
    <td>第三章通讯协议	
    <td>更新了通信协议的数据长度，数据长度较之前加1
  </tr> 
  <tr>
        <td rowspan="2">V1.0.0</td> 
        <td rowspan="2">17.11.29</td> 
        <td>修改</td>
        <td>第二章通配线</td>
        <td>更新了CAN接口定义</td> 
    </tr>
    <tr>
        <td>增加</td>
        <td>第三章通信协议</td>
        <td>增加了开关机指令</td> 
    </tr>    
</tbody>
</table>    
