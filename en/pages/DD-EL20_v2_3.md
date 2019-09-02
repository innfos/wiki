# Parameter introduction 
## DD-EL20 Parameter Diagram[mm]
![DD-EL20]( ../img/DD_EL20_v2_3sanshitu.png ) 
### 3D model 
[Model file]( ../img/DD-EL20_v2_3.step.zip )


## DD-EL20 Parameter
<table style="width:850px"><thead><tr><th colspan="4" style="background: PaleTurquoise; color: black;">DD-EL20 parameter</th></tr></thead><tbody><tr><td colspan="2" width=60%><b>Working parameters at norminal voltage</b></td><td colspan="2" width=40%><b>Mechanical parameters</b></td></tr><tr><td>Motor power</td><td>36 W</td><td>Diameter</td><td>35mm</td></tr><tr><td>Norminal voltage</td><td>42 VDC</td><td>Length</td><td>22.5mm</td></tr><tr><td>No load speed</td><td>6000 RPM</td><td>Weight</td><td>54 g</td></tr><tr><td>Norminal speed</td><td>4000 RPM</td><td>Rotational inertia of rotor</td><td>22.5254g*cm²</td></tr><tr><td>Nominal torque</td><td>0.023 Nm</td><td>Static load capacity</td><td>  40N</td></tr><tr><td>Peak torque</td><td>0.069 Nm</td><td>Version number</td><td>v2.3</td></tr><tr><td>Torque coefficient</td><td>0.0345 Nm/A</td><td colspan="2"><b>Work area</b></td></tr><tr><td>Full range of phase current</td><td>2A</td><td colspan="2" rowspan="14"><img src="../img/DD-EL20quxian.png" style="width:300px"></td></tr><tr><td>Nominal power current</td><td>0.86 A</td></tr><tr><td>Quiescent Current</td><td>0.08 A</td></tr><tr><td colspan="2"><b>Basic parameters</b></td></tr><tr><td>Motor type</td><td>
Brushless servo motor</td></tr><tr><td>Voltage range</td><td>24~45 VDC</td></tr><tr><td>Resolution</td><td>16384(14bit) Step/turn</td></tr><tr><td>Encoder system</td><td>Multiturn absoulute encoder</td></tr><tr><td>Interface</td><td>Non-isolated CAN</td></tr><tr><td>Angle of rotation</td><td>> 360.0 °</td></tr><tr><td>Ambient temperature range</td><td>-20~+80 °C</td></tr><tr><td>Noise level</td><td><= 70 dB(A)</td></tr></tbody></table>

 Note: Encoder counter range: ±127turns; Motor protection temperature settable range: 25-120 °C; Inverter protection temperature settable range: 25-120 °C

### Connector Pin Layout
<table class="tableizer-table" style="width:700px">
<thead><tr class="tableizer-firstrow"><th colspan="4" style="background: PaleTurquoise; color: black;">Connector Pin Layout</th></tr></thead><tbody><tr><td>Pin NO.</td><td>Color</td><td>Signal</td><td>Terminal pin distribution</td></tr><tr><td>1</td><td>PVDD</td><td>Black</td><td rowspan="9"><img src="../img/配线2-3.png" style="width:450px"></td></tr><tr><td>3</td><td>PVDD</td><td>Black</td></tr><tr><td>5</td><td>PVDD</td><td>Black</td></tr><tr><td>2</td><td>GND</td><td>Black</td></tr><tr><td>4</td><td>GND</td><td>Black</td></tr><tr><td>6</td><td>CAN-GND</td><td>Gray</td></tr><tr><td>7</td><td>CAN-L</td><td>Gray</td></tr><tr><td>8</td><td>CAN-H</td><td>Gray</td></tr></tbody></table>

## Version Updating Records


<table style="width:400px"><thead><tr style="background:PaleTurquoise"><th style="width:100px">Version number</th><th style="width:150px">Update time</th><th style="width:150px">Update content</th></tr></thead><tbody><tr><td>v2.3.0</td><td>2019.07.18</td><td>Updated inner structure</th></tr></thead><tbody><tr><td><a href="http://innfos.com/wiki/en/index.html#!pages/DD-EL20_v2_2.md">v2.2.0 </a></td><td>2019.05.09</td><td>Full text added</th></tr></thead><tbody><tr><td>v1.0.0</td><td>2019.04.11</td><td>Full text added</td></tbody></table>
