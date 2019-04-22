[English](https://github.com/innfos/wiki/blob/master/en/pages/INNFOS_Actuator_StudioIAS_instruction.md)


# 软件的使用

## 软件的安装

1.双击安装软件“Setup V3.2.2exe”（V3.2.2为当前软件版本）

![install01.jpg](../img/install01.jpg )


> 软件安装.


2.进入安装界面后，点击“Next”

![next](https://github.com/innfos/wiki/cn/img/1-2.png)

3.点击“I Agree”

![next](https://github.com/innfos/wiki/cn/img/1-3.png)

4.选择安装位置，然后点击“Install”

![next](https://github.com/innfos/wiki/cn/img/1-4.png)

5.等待安装完成

![next](https://github.com/innfos/master/cn/img/1-5.png)
6.如遇到有杀毒软件提示报警时，请选择“允许本次操作”，

![next](https://github.com/innfos/master/cn/img/1-6.png)


7.点击“Finish”，完成软件的安装

![next](https://github.com/innfos/wiki/cn/img/1-7.png)

> Innfos SCA.

## 软件的开机

1、双击运行软件 启动用户界面

![next](https://github.com/innfos/wiki/cn/img/install02.jpg)

2.点击“confirm that you’ve read the document”，然后点击“next”，进入下一界面，（如果是初次对本产品使用者，请点击show the document！ ,阅读软件使用说明）

![next](https://github.com/innfos/wiki/cn/img/2-2.png)


3.选择执行器通信方式（默认为以太网通信），然后继续点击“next”（注：如果是初次使用以太网通信，应配置静态IP,具体配置见附录B）

![next](https://github.com/innfos/wiki/cn/img/2-3.png)


*   当USB转CAN未连接或连接不正常时，会出现如图错误提示。

![next](https://github.com/innfos/wiki/cn/img/2-4.png)

*   当外部执行器没有连接或连接不正常时，会出现如图错误提示

![next](https://github.com/innfos/wiki/cn/img/2-5.png)

*   当外部系统连接正确，系统进入执行器运行界面，单机红色区域OFF，如图，标记1处OFF为单个执行器开关，2处ON为总开关，比如多个执行器同时连接时，点击总开关即可控制所有执行器开关机。

![next](https://github.com/innfos/master/cn/img/2-6.png)

*   点击OFF开机后，弹出右图中红色区域提示信息

![next](https://github.com/innfos/master/cn/img/2-7.png)


*   等待三秒后，如图，标记一处为该执行器ID号，标记2处为错误清除键，标记3处为Detail键可进入执行器操作界面，标记4处为该执行器的信息显示区域。

![next](https://github.com/innfos/wiki/cn/img/2-8.png)

4.双击执行器信息框或者点击“Detail”键，进入电流环模式。

![next](https://github.com/innfos/wiki/blob/master/cn/img/2-9.png)


## 电流环模式

INNFOS执行器系统的逻辑框图：

![next](https://github.com/innfos/wiki/blob/master/cn/img/current.jpg)

![INNFOS执行器系统的逻辑框图](微伺服软件界面最终00-44 3-1.png "fig:INNFOS执行器系统的逻辑框图")


框图的介绍：电流设置值与电流反馈值做加减运算后经过PI模块后经可选的滤波器再经限幅模块以驱动电机，电机经反馈把电流参数反馈给系统，使之形成闭环。

### 电流环模式各项功能描述

*   文字序号与图中序号对应

（1）电流环模式

（2）电流环模式简易示意图

（3）当前模式下状态激活

（4）参数设置

（5）INNFOS执行器状态参数值

（6）错误警告

（7）方波发生器参数值设定

（8）INNFOS执行器当前连接状态

（9）示波器开关


![next](https://github.com/innfos/wiki/cn/img/Fig3-2.png)

### 基本参数的描述

*   文字序号与图中序号对应

（1）Iq轴向力设置

（2）比例设置

（3）积分设置

（4）Id轴向力设置

（5）限幅最小值设置

（6）限幅最大值设置

<span style="color: red">[注:电流环模式中，Id轴向力一般设置为0，Minimal设置固定值-0.82，Maximum设置固定值0.82。]</span> 

![next](https://github.com/innfos/wiki/cn/img/Fig3-3.png)


### 电流环使用方式

1.点击“Active Current Mode”激活当前电流环模式。

![next](https://github.com/innfos/wiki/cn/img/Fig3-4.png)


2.参数设置：应用方式

*   在“Iq Setting”中输入电流值大小（右图中1处），按回车键或”Set Current”键，INNFOS执行器开始输出相应扭矩。若负载不够大，INNFOS执行器会高速运转。
*   INNFOS执行器开始转动后，在状态值栏可以看到当前INNFOS执行器的各项参数值。(如右图中3处)
*   按“Halt”键可停止INNFOS执行器的转动。（右图中2处）
*   Limit参数栏中可以设置最大电流值。

![next](https://github.com/innfos/wiki/cn/img/Fig3-5.png)

3.点击“View Graph”可打开示波器

![next](https://github.com/innfos/wiki/cn/img/Fig3-6.png)

4.示波器各项功能描述

*   右图中“prescalar”可设置波形的预分频系数（图1处），“trig_value”可设置触发数值（图2处），图 3处设置参数的保存、暂停、自动缩放；
*   channel1为INNFOS执行器给定波形的偏置和放大倍数（图4处）；
*   channel2为INNFOS执行器电流波形的偏置和放大倍数（图5处）；
*   channel3为INNFOS执行器速度波形的偏置和放大倍数（图6处）；
*   channel4为INNFOS执行器位置波形的偏置和放大倍数（图7处）。
*   示波器的详细使用说明请见附录C。

![next](https://github.com/innfos/wiki/cn/img/3-7.png)

<span style="color: red">[注：不用的通道偏置设置为0，放大设置为1，或者直接点击OFF关闭其显示]</span> !

5.方波发生器参数值设定

*   在Value1中输入电流值1（单位：A）（右图1处）
*   在Value2中输入电流值2（单位：A）（右图2处）
*   在Interval内输入时间（单位：ms）（右图3处）
*   点击“IqTrigger”按钮，可设置轴向力为q轴还是d轴（右图5处）
*   选择点击“Start”键（右图4处），方波发生器会按设定的时间（Interval值），连续生效Value1和Value2到指定的位置（Iq Setting或者Id Setting），直到关闭此按钮。

<span style="color: red">[注:在调节电流环模式的PI值时，需要将方波发生器的轴向力更改为IdTrigger。此时示波器中有波形，执行器应处于静止状态，否则需要重新校准。]</span> 

![next](https://github.com/innfos/wiki/cn/img/Fig3-8.png)

6.点击“View Graph”按钮打开示波器窗口，可以查看给定（channel 1，此时为方波发生器）、电流（channel 2）、速度（channel 3）、位置（channel 4）四通道参数波形，如右图 

![next](https://github.com/innfos/wiki/cn/img/3-9.png)

7.利用方波发生器来调节Proportional和Integral（PI）的数值，可通过示波器观测调试效果。

![next](https://github.com/innfos/wiki/cn/img/Fig3-10.png)

8.点击“Stop”键，可停止方波发生器的运行。

![next](https://github.com/innfos/wiki/cn/img/Fig3-11.png)

## 速度环模式

INNFOS执行器系统的逻辑框图：

![next](https://github.com/innfos/wiki/cn/img/velocity.jpg)

框图的介绍： 速度值设置与速度反馈值做加减后经PI模块后经可选的滤波器再经模块输出电流给电流环，在确保电流环模式运行正确的情况下，通过电流环驱动电机，经编码器把速度参数反馈给系统，使之形成闭环。

* * *

### 点击“Velocity Regulation”进入速度环模式

![next](https://github.com/innfos/wiki/cn/img/Fig4-2.png)

### 速度环模式各项功能描述

*   文字序号与图中序号对应

（1）速度环模式简易示意图

（2）当前模式下状态激活

（3）基本参数设置

（4）INNFOS执行器状态参数值

（5）错误警告

（6）方波发生器参数值设定

（7）INNFOS执行器连接状态

（8）示波器开关 

![next](https://github.com/innfos/wikicn/img/Fig4-3.png)


### 速度环使用方式

1.点击“Active Velocity Mode”，激活当前速度环模式。

![next](https://github.com/innfos/wiki/cn/img/Fig4-4.png)

2.速度环基本参数设置：

*   右图1处“Setting”框中输入转速值大小（单位：RPM），按回车键或点击右图4处的”Set Velocity”键，INNFOS执行器开始转动。若转速值为负值则反向转动。
*   INNFOS执行器开始转动后，右图5处的状态值栏可以看到当前INNFOS执行器的各项参数值。
*   调节Proportional框和Integral框可调节PI值，右图2处。
*   右图3处的Mininal框和Maximum框为速度环输出限幅（后接电流环的输入），例如：电流最大值为33A（6010型为33A，3510型为16.5A，具体参见《CAN总线通信协议》附录D），输入值为0.5，那么INNFOS执行器电流增加到33*0.5的时候，电流值将受限，不再增加。
*   按“Halt”键可停止INNFOS执行器的转动。

![next](https://github.com/innfos/wiki/cn/img/Fig4-5.png)

3.点击“View Graph”可打开示波器,参数界面介绍同上。

![next](https://github.com/innfos/wiki/cn/img/Fig4-6.png)


4.方波发生器参数值设定

*   在Value1中输入转速1。(单位:RPM)
*   在Value2中输入转速2。(单位:RPM)
*   在Interval内输入单位时间（单位：ms），可设置INNFOS执行器方波发生器的参数。
*   选择点击“Start”键，开启INNFOS执行器转动。

![next](https://github.com/innfos/wiki/cn/img/Fig4-8.png)


5.设置“View Graph”视图里的参数，可以更好的查看当前INNFOS执行器 各项参数波形，调节INNFOS执行器Proportional和Integral（PI） 的数值，其性能会在示波器中以波形方式反应出来。

<span style="color: red">注：不用的通道偏置设置为0，放大设置为1（右图中channel2和channel4），或者直接点击OFF关闭其显示</span>

![next](https://github.com/innfos/wiki/cn/img/4-9.png)

## 位置环模式

INNFOS执行器系统的逻辑框图：

![next](https://github.com/innfos/wiki/cn/img/position.jpg)

框图的介绍： 在确保电流环和速度环准确的情况下，位置设置值与位置反馈值做加减运算后经过PI模块后经可选的滤波器再经限幅模块输出速度值，然后速度值经速度环再经电流环驱动电机，电机经编码器把位置参数反馈给系统，使之形成闭环。

### 点击“Position Regulation”进入位置环模式


![next](https://github.com/innfos/wiki/cn/img/Fig5-2.png)

### 位置环模式各项功能描述

*   文字序号与图中序号对应

（1）位置环模式示意图

（2）当前模式下状态激活

（3）基本参数设置

（4）INNFOS执行器状态参数值

（5）错误警告

（6）方波发生器参数值设定

（7）INNFOS执行器连接状态

（8）示波器开关 


![next](https://github.com/innfos/wiki/cn/img/Fig5-3.png)


### 位置环使用方式

1.点击“Active Position Mode”，激活当前位置环模式。 


![](https://github.com/innfos/master/cn/img/Fig5-4.png)

2.位置环基本参数设置：

*   右图1处“Setting”框中输入位置值大小（单位：R），在右图4处按&quot;Set Position”键，INNFOS执行器开始转动，INNFOS执行器转到输入位置后，停止。
*   INNFOS执行器开始转动后，右图5处状态值栏可以看到当前INNFOS执行器的各项参数值。
*   调节Proportional框可调节比例值，如右图2处。
*   右图的3处的Mininal框和Maximum框为位置环输出给速度环的速度限制。执行器速度最大为6000RPM，例如输入值为0.5，那么INNFOS执行器最大速度增加到6000*0.5=3000R/分钟的时候，速度值将受限，不再增加。

![next](https://github.com/innfos/master/cn/img/Fig5-5.png)

3.点击“View Graph”可打开示波器，参数界面介绍同上 


![next](https://github.com/innfos/wiki/cn/img/Fig5-6.png)

4.方波发生器参数值设定

*   在Value1中输入位置值1(单位:R)
*   在Value2中输入位置值2(单位:R)
*   在Interval内输入时间（单位：ms），输入参数为转动一次的时间。（例：Value1为2，Value2为-2，Interval为1000，启动后，INNFOS执行器先转到位置2，1000mS后转到位置-2，在过1000ms再次转到位置2，如此反复运行直至用户点击“Stop”)。
*   点击“Start”键，开启INNFOS执行器转动。

![next](https://github.com/innfos/master/cn/img/Fig5-8.png)

5.点击“View Graph”按钮打开示波器窗口，可以查看给定（此 时为方波发生器）、电流、速度、位置四通道参数波形。



6.调节“Proportional”，其性能会在示波器中以波形方式反应出来。


![next](https://github.com/innfos/master/cn/img/Fig5-10.png)

7.点击“Stop”键，可停止方波发生器的运行。


![next](https://github.com/innfos/wiki/cn/img/Fig5-11.png)


## 位置环S曲线模式

### 点击“Profile Position Mode”进入位置环S曲线模式

![next](https://github.com/innfos/wiki/cn/img/Fig6-1.png)

### 位置环S曲线模式各项功能描述

*   文字序号与图中序号对应

（1）位置环S曲线模式简易示意图

（2）当前模式下状态激活

（3）基本参数设置

（4）INNFOS执行器状态参数值

（5）错误警告

（6）INNFOS执行器当前连接状态 

![next](https://github.com/innfos/wiki/cn/img/Fig6-2.png)


### 位置环S曲线模式使用方式

1.点击“Active Profile Position Mode” 激活当前位置环S曲线模式 

![next](https://github.com/innfos/wiki/cn/img/Fig6-3.png)

2.位置环S曲线模式基本参数设置：

*   在“Target”框中输入转动的位置（单位：R），INNFOS执行器开始转动到指定位置。
*   INNFOS执行器开始转动后，在状态值栏可以看到当前INNFOS执行器的各项参数值，右图4处。
*   右图2处的Accelerate框和Decelerate框为S曲线模式下的速度上升和下降的平缓度，例如：Accelerate值越大，INNFOS执行器达到最大速度的时间越短，Accelerate值越小，INNFOS执行器达到最大转速的时间越长。Decelerate值越大，INNFOS执行器从最大速度降低到零的时间越短，Decelerate值越小，INNFOS执行器从最大速度降低到零的时间越长。
*   “Max”限制了INNFOS执行器的最大转速，随数值增加而增加，如右图的3处，当前最大转速为1000RPM。
*   关于位置环S曲线模式的原理分析参见附录D。


![next](https://github.com/innfos/wiki/cn/img/Fig6-4.png)

## 速度环S曲线模式

### 点击“Profile Velocity Mode”进入速度环S曲线模式

![next](https://github.com/innfos/wiki/cn/img/Fig7-1.png)

*   文字序号与图中序号对应

（1）速度环S曲线模式简易示意图

（2）当前模式下状态激活

（3）基本参数设置

（4）INNFOS执行器状态参数值

（5）错误警告

（6）INNFOS执行器当前连接状态 

![next](https://github.com/innfos/wiki/cn/img/Fig7-2.png)


### 速度环S曲线模式使用方式

1.点击“Active Profile Velocity Mode”，激活当前速度环S曲线模式。 

![next](https://github.com/innfos/wiki/cn/img/Fig7-3.png)


2.速度环S曲线模式基本参数设置：

*   在“Target”框中输入INNFOS执行器的速度值（单位：RPM），INNFOS执行器开始转动，直至达到输入值。
*   INNFOS执行器开始转动后，在状态值栏可以看到当前INNFOS执行器的各项参数值，右图3处。
*   右图中2处的Accelerate、Decelerate和Max项为S曲线的调整参数。

![next](https://github.com/innfos/wiki/cn/img/Fig7-4.png)

## 归位模式

### 点击“Homing Mode”进入归位模式

![next](https://github.com/innfos/wiki/cn/img/Fig8-1.png)

### 归位模式使用方式

点击“Active Homing Mode”，激活当前归位模式。

![next](https://github.com/innfos/wiki/cn/img/Fig8-2.png)

### 速度环S曲线模式各项功能描述

1.自动校准左右极限

*   先后点击Clear和Homing按键，重复两次清除当前左右极限，直到右图8-1图1处数据变为如下大数值（这是软件限位的上下限）。然后将右图8-1图2处调为如下大数值（这是限流，比如加大负载时需要较大电流，需要放开电流限制）。然后点击Auto按钮，INNFOS执行器就会自动顺时针转动，直到触碰机械左极限（这里定义顺时针碰的机械限位为左极限，逆时针的为右极限），然后自动逆时针转动直到触碰机械右极限停止。

![next](https://github.com/innfos/wiki/cn/img/Fig8-3.png)

*   此时会返回左右极限的值到图8-1的1处。然后手动控制转动INNFOS执行器到想要的零点（例如图8-2中左侧图的2处），最后点击Homing按键，则当前位置变为零点（如图8-2中右侧图03的2处），图8-2中右侧图的1处的左右极限会根据点击Homing前的位置进行偏移（对比图8-2中两侧图）。这样就保证了软件限位和机械限位的一致性。

![next](https://github.com/innfos/wiki/cn/img/Fig8-4.png)

*   然后，设置到左右极限的余量偏置（图8-2中右侧图的3处），则实际运动范围为左右极限减去偏置，(图8-2中右侧图：左软件限位为33.774918-1.4=32.374918；右软件限位为-32.4932+1.4=-31.0932。)最后，确认软件限位开启如如图8-2中右侧图的4处后，点击Download按钮即可保存当前参数。

### 手动校准左右极限

1.点击右图红框位置&quot;Active Homing Mode&quot;进入归位模式。

![next](https://github.com/innfos/wiki/cn/img/Fig9-1.png)

2.先后点击&quot;Clear&quot;和&quot;Homing&quot;按键，重复两次可清除当前左右极限，并使当前位置变为零位。直到右图红框1处数据变为如图大数值（这是软件限位的上下限）。然后将右图2处调为如下大数值（这是限流，比如加大负载时需要较大电流，需要放开电流限制）。

![next](https://github.com/innfos/wiki/cn/img/Fig9-2.png)

3.手动将关节或执行器调节到左机械极限，点击&quot;Max_Set&quot;，此时&quot;Max Pos&quot;栏处的数值会改变，左机械极限设定完毕。（此处也可以手动输入极限数值，单位：R）

![next](https://github.com/innfos/wiki/cn/img/Fig9-3.png)

4.手动将关节或执行器调节到右机械极限，点击&quot;Min_Set&quot;，此时&quot;Min Pos&quot;栏处的数值会改变，右机械极限设定完毕。（此处也可以手动输入极限数值，单位：R）

![next](https://github.com/innfos/wiki/cn/img/Fig9-4.png)

注意：位置模式使用时，应注意当前限位范围，如果当前位置在限位范围外，发位置指令时，位置则会回到限位范围内。


5.若只设定零点，则手动将关节或执行器调节至想要的零点，点击2处的Homing按键，1处的当前位置值会变为0。

![next](https://github.com/innfos/wiki/cn/img/Fig9-5.png)

6.设置左右极限偏置 

![next](https://github.com/innfos/wiki/cn/img/Fig9-6.png)

7.点击&quot;Download&quot;按钮即可保存当前参数 

![next](https://github.com/innfos/wiki/cn/img/Fig9-7.png)

## 错误提示

### 当有错误出现时，错误框内会提示错误内容

如图，弹出错误提示信息。

<span style="color: red">（注：如用最新版上位机软件会报警详细错误提示）</span>

![next](https://github.com/innfos/wiki/cn/img/File9-1.png)



### 错误处理方式

点击“OK”，再点击“Clear Errors”可清除错误，清除错误后，INNFOS执行器进入电流环模式。

![next](https://github.com/innfos/wiki/cn/img/File9-2.png)


# 版本信息
<table class="tableizer-table">
<thead><tr class="tableizer-firstrow"><th>Version No.</th><th>Update time</th><th>update contents</th></tr></thead><tbody>
 <tr><td>V1.0.0</td><td>2019-04</td><td>The First Version</td></tr>
</tbody></table>
