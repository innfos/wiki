*To the right you will find two images, that are floated*. Lorem ipsum dolor sit amet, consectetuer adipiscing elit, sed diam nonummy nibh euismod tincidunt ut laoreet dolore magna aliquam erat volutpat. Ut wisi enim ad minim veniam, quis nostrud exerci tation ullamcorper suscipit lobortis nisl ut aliquip ex ea commodo consequat. Duis autem vel eum iriure dolor in hendrerit in vulputate velit esse molestie consequat, vel illum dolore eu feugiat nulla facilisis at vero eros et accumsan et iusto odio dignissim qui blandit praesent luptatum zzril delenit augue duis dolore te feugait nulla facilisi.
ipsum dolor sit amet, consectetuer adipiscing elit, sed diam nonummy nibh euismod tincidunt ut laoreet dolore magna aliquam erat volutpat. Ut wisi enim ad minim veniam, quis nostrud exerci tation ullamcorper suscipit lobortis nisl ut aliquip ex ea commodo consequat. Duis autem vel eum iriure dolor in hendrerit in vulputate velit esse molestie consequat, vel illum dolore eu feugiat nulla facilisis at vero eros et accumsan et iusto odio dignissim qui blandit praesent luptatum zzril delenit augue duis dolore te feugait nulla facilisi.





| Tables        | Are           | Cool  |
| ------------- |:-------------:| -----:|
| col 3 is      | right-aligned | <img src="../img/终端电阻_v1_0.png" style="width:300px"> |
| col 2 is      | centered      |   $12 |
| zebra stripes | are neat      |    $1 | 



<html>
 <head></head>
 <body>
  <table style="width:600px">
   <thead>
    <tr class="tableizer-firstrow"></tr>
   </thead>
   <tbody>
    <tr>
     <td colspan="3" style="background:PaleTurquoise">3.3.1.2 发送数据1字节，返回数据3字节</td>
    </tr>
    <tr>
     <td style="width:150px">命令名称</td>
     <td colspan="2">读取命令</td>
    </tr>
    <tr>
     <td>说明</td>
     <td colspan="2">此命令类发送数据长度为1，返回数据长度为3，读取执行器参数值，高位在前。数值为真实值的2^8倍。（`一条特殊指令指令表内已特殊标注`）</td>
    </tr>
    <tr>
     <td>指令符</td>
     <td colspan="2"><a href="#!pages/CAN_Communication_Protocol.md#读取指令2:">见读取指令2</a></td>
    </tr>
    <tr>
     <td>数据长度</td>
     <td colspan="2">1</td>
    </tr>
    <tr>
     <td>数据内容</td>
     <td colspan="2">无</td>
    </tr>
    <tr>
     <td>指令符（返回值）</td>
     <td colspan="2"><a href="#!pages/CAN_Communication_Protocol.md#读取指令2:">见读取指令2</a></td>
    </tr>
    <tr>
     <td>数据长度 (返回值)</td>
     <td colspan="2">3</td>
    </tr>
    <tr>
     <td>执行器返回数据</td>
     <td>数据为IQ8格式</td>
     <td>或见<a href="#!pages/CAN_Communication_Protocol.md#附录C:报警指令表">报警指令表</a></td>
    </tr>
   </tbody>
  </table>
 </body>
</html>


<table style="width:850px"><thead><tr><th colspan="4" style="background: PaleTurquoise; color: black;">QDD Lite-EL20-36参数表</th></tr></thead><tbody><tr><td colspan="2" width=50%><b>额定电压工作参数</b></td><td colspan="2" width=50%><b>机械参数</b></td></tr><tr><td>峰值机械功率</td><td>36 W</td><td>直径</td><td>35mm</td></tr><tr><td>额定电压</td><td>42 VDC</td><td>长度</td><td>45mm</td></tr><tr><td>空载转速</td><td>167 RPM</td><td>重量</td><td>79.7 g</td></tr><tr><td>额定转速</td><td>111 RPM</td><td>背隙</td><td> 8 Arc min</td></tr><tr><td>额定扭矩</td><td>0.4 Nm</td><td>最大轴向载荷</td><td>200 N</td></tr><tr><td>峰值扭矩</td><td>3.2 Nm</td><td>最大径向载荷</td><td>800 N</td></tr><tr><td>转矩系数</td><td>1.242 Nm/A</td><td>版本号</td><td>v1.8</td></tr><tr><td>相电流满量程</td><td>2A</td><td colspan="2"><b>工作区域</b></td></tr><tr><td>额定母线电流</td><td>0.86 A</td><td colspan="2" rowspan="18"></td></tr><tr><td>静态工作母线电流</td><td>0.08 A</td></tr><tr><td colspan="2"><b>基本参数</b></td></tr><tr><td>电机类型</td><td>无刷伺服电机</td></tr><tr><td>电压范围</td><td>24~45 VDC</td></tr><tr><td>减速比</td><td>36:1</td></tr><tr><td>分辨率</td><td>589824(19bit) Step/turn</td></tr><tr><td>编码器</td><td>多圈绝对值式编码器</td></tr><tr><td>通信接口</td><td>非隔离CAN</td></tr><tr><td>旋转角度</td><td>> 360.0 °</td></tr><tr><td>环境温度范围</td><td>0~+50 °C</td></tr><tr><td>噪声</td><td><= 70 dB(A)</td></tr></tbody></table>
