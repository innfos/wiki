# 参数介绍 
## DD-EL20工程参数图[单位：毫米]
![DD-EL20]( ../../img/DD_EL20_v2_3三视图.png ) 
### 3D 模型
[模型文件]( ../../3DModel/DD_EL20_v2_3.step.zip )

## DD-EL20参数

<table style="width:650px"><thead><tr><th colspan="4" style="background: PaleTurquoise; color: black;">DD-EL20参数表</th></tr></thead><tbody><tr><td colspan="2"><b>额定电压工作参数</b></td><td colspan="2"><b>基本参数</b></td></tr><tr><td style="width:175px">功率</td><td style="width:135px">36 W</td><td style="width:130px">分辨率</td><td style="width:220px">16384(14bit) Step/turn</td></tr><tr><td>额定电压</td><td>42 VDC</td><td>编码器</td><td>多圈绝对值式编码器</td></tr><tr><td>空载转速</td><td>6000 RPM</td><td>通信接口</td><td>非隔离CAN</td></tr><tr><td>额定转速</td><td>4000 RPM</td><td>旋转角度</td><td>> 360.0 °</td></tr><tr><td>额定扭矩</td><td>0.023 Nm</td><td>温度范围</td><td>-20~+80 °C</td></tr><td>峰值扭矩</td><td>0.069 Nm</td><td>噪声</td><td><= 70 dB(A)</td></tr><tr><td>转矩系数</td><td>0.0345 Nm/A</td><td colspan="2"><b>机械参数</b></td></tr><tr><td>相电流满量程</td><td>2 A</td><td style="width:175px">直径</td><td style="width:175px">35mm</td></tr><tr><td>额定母线电流</td><td>0.86 A</td><td>长度</td><td>22.5mm</td></tr><tr><td>静态工作母线电流</td><td>0.08 A</td><td>重量</td><td>54g</td></tr> <tr><td colspan="2"><b>基本参数</b></td><td>电机转子转动惯量</td><td>22.5254 g*cm²</td></tr><tr><td>电机类型</td><td>无刷伺服电机</td><td>额定静态载荷</td><td>40N</td></tr><tr><td>电压范围</td><td>24~45 VDC</td><td>版本号</td><td>v2.3</td></tr></tbody></table>

 Note: 编码器计数范围: ±127圈; 电机保护温度可设置范围: 25-120°C; 逆变器保护温度可设置范围: 25-120°C; 功率为电功率


### 接插件型号图

<img src="../../img/配线2-2.png" style="width:600px">

### 端子引脚功能描述

<table class="tableizer-table" style="width:390px">
 <thead><tr class="tableizer-firstrow"><th colspan="4" style="background: PaleTurquoise; color: black;">端子引脚功能描述</th></tr></thead><tbody><tr><td>标号</td><td>Signal</td><td>颜色</td><td>功能</td></tr><tr><td>1</td><td>PVDD</td><td>黑线</td><td rowspan="3">功率电源正极</td></tr><tr><td>3</td><td>PVDD</td><td>黑线</td></tr><tr><td>5</td><td>PVDD</td><td>黑线</td></tr><tr><td>2</td><td>GND</td><td>黑线</td> <td rowspan="2">功率电源地</td></tr><tr><td>4</td><td>GND</td><td>黑线</td></tr><tr><td>6</td><td>CAN-GND</td><td>灰线</td><td>CAN通讯信号地线</td></tr><tr><td>7</td><td>CAN-L</td><td>灰线</td><td>CAN通讯低位信号线</td></tr><tr><td>8</td><td>CAN-H</td><td>灰线</td><td>CAN通讯高位信号线</td></tr></tbody></table>
 </tbody></table>

## 版本变更记录
**下表简单描述了版本变更记录**

<table style="width:400px"><thead><tr style="background:PaleTurquoise"><th style="width:100px">版本号</th><th style="width:150px">更新时间</th><th style="width:150px">更新内容</th></tr></thead><tbody><tr><td>v2.3.2</td><td>2019.09.27</td><td>改变整体版式</td></tr><tr><td>v2.3.1</td><td>2019.08.09</td><td>添加电机保护温度可设置范围 <br>添加逆变器保护温度可设置范围 </td></tr><tr><td>v2.3.0</td><td>2019.07.18</td><td>内部结构更新</th></tr></thead><tbody><tr><td><a href="http://wiki.mintasca.com/wiki/cn/index.html#!pages/DD-EL20_v2_2.md">v2.2.0 </a></td><td>2019.05.09</td><td>全文添加</th></tr></thead><tbody><tr><td>v1.0.0</td><td>2019.04.11</td><td>全文添加</td></tbody></table>




