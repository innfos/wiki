# Parameter introduction 
## QDD Lite-EL20-36 Parameter Diagram[mm]
![QDD Lite-EL20-36]( ../img/Qdd_C_EL20_36_v1_8sanshitu.png ) 
### 3D model 
[Model file]( ../img/QDD Lite-EL20-36_v1_8.step.zip )


## QDD Lite-EL20-36 Parameter

<table style="width:650px"><thead><tr><th colspan="4" style="background: PaleTurquoise; color: black;">QDD Lite-EL20-36 parameter</th></tr></thead><tbody><tr><td colspan="2"><b>Working parameters at norminal voltage</b></td><td colspan="2"><b>Basic parameters</b></td></tr><tr><td style="width:175px">Motor power</td><td style="width:135px">36 W</td><td style="width:130px">Resolution</td><td style="width:220px">589824(19bit) Step/turn</td></tr><tr><td>Norminal voltage</td><td>42 VDC</td><td style="width:130px">Encoder system</td><td style="width:220px">Multiturn absoulute encoder</td></tr><tr><td>No load speed</td><td>167 RPM</td><td>Interface</td><td>Isolated CAN</td></tr><tr><td>Norminal speed</td><td>111 RPM</td><td>Angle of rotation</td><td>> 360.0 °</td></tr><tr><td>Nominal torque</td><td>0.4 Nm</td><td>Ambient temperature range</td><td>0~+50 °C</td></tr><td>Peak torque</td><td>3.2 Nm</td><td>Noise level</td><td><= 70 dB(A)</td></tr><tr><td>Torque coefficient</td><td>1.242 Nm/A</td><td colspan="2"><b>Mechanical parameters</b></td></tr><tr><td>Full range of phase current</td><td>2A</td><td style="width:175px">Diameter</td><td style="width:175px">35mm</td></tr><tr><td>Nominal power current</td><td>0.86 A</td><td>Length</td><td>45mm</td></tr><tr><td>Quiescent Current</td><td>0.08 A</td><td>Weight</td><td>79.7 g</td></tr> <tr><td colspan="2"><b>Basic parameters</b></td><td>Backlash</td><td>8 Arc min</td></tr><tr><td>Motor type</td><td>Brushless servo motor</td><td>Maximum axial load</td><td>200N</td></tr><tr><td>Voltage range</td><td>24~45 VDC</td><td>Maximum radial load</td><td>800N</td></tr><tr><td>Gear ratio</td><td>36:1</td><td>Version number</td><td>v1.8</td></tr></tbody></table>


 Note: Encoder counter range: ±127turns; Motor protection temperature settable range: 25-90 °C; Inverter protection temperature settable range: 25-120 °C


### Connector Pin Layout

<img src="../img/配线2-2.png" style="width:600px">

### Terminal pin function

<table class="tableizer-table" style="width:390px">
 <thead><tr class="tableizer-firstrow"><th colspan="4" style="background: PaleTurquoise; color: black;">Terminal pin function</th></tr></thead><tbody><tr><td>Label</td><td>Signal</td><td>colour</td><td>Features </td></tr><tr><td>1</td><td>PVDD</td><td>Black</td><td rowspan="3">Positive power supply </td></tr><tr><td>3</td><td>PVDD</td><td>Black</td></tr><tr><td>5</td><td>PVDD</td><td>Black</td></tr><tr><td>2</td><td>GND</td><td>Black</td> <td rowspan="2">Power supply grounding</td></tr><tr><td>4</td><td>GND</td><td>Black</td></tr><tr><td>6</td><td>CAN-GND</td><td>Gray</td><td>CAN communication signal ground</td></tr><tr><td>7</td><td>CAN-L</td><td>Gray</td><td>CAN communication low signal line</td></tr><tr><td>8</td><td>CAN-H</td><td>Gray</td><td>CAN communication high signal line</td></tr></tbody></table>
 </tbody></table>


## Version Updating Records


<table style="width:500px"><thead><tr style="background:PaleTurquoise"><th style="width:100px">Version number</th><th style="width:150px">Update time</th><th style="width:3800px">Update content</th></tr></thead><tbody><tr><td>v1.8.1</td><td>2019.07.30</td><td>Updated the values of no load speed <br>Updated the values of norminal speed <br>Updated the values of nominal torque <br>Updated the values of peak torque <br>Updated the values of torque coefficient</th></tr></thead><tbody><tr><td>v1.8.0</td><td>2019.06.20</td><td>Full text added</th></tr></thead><tbody><tr><td>v1.0.0</td><td>2019.04.11</td><td>Full text added</td></tbody></table>
