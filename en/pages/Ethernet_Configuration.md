Ethernet Configuration
=======


## linux platform environment configuration

*   available for ubuntu 16.04 LTS and above
*   cmake installation: open terminal & input command

```sh
$ sudo apt-get install cmake
```

*   ip address configuration: open terminal and input

```sh
$ ifconfig
```

* Check network configuration 

<img src="../img/020.png" style="width:600px">

* In the example, the name of the wired network card is enp0s25, enter the command

```sh
$ sudo ifconfig enp0s25 static 192.168.1.111
```


After the configuration, enter`ifconfig`to see the ip address.

<img src="../img/020.png" style="width:600px">

##  Windows platform environment configuration

*   requires 64-bit Windows operating system above win7 sp1

A new inbound rule need setting if the computer firewall is turned on:

Enter cmd in the search bar, right click on the command prompt, select Run as administrator and open a command window

<img src="../img/cmd.png" style="width:600px">

Enter the new inbound rule command
```sh
netsh advfirewall firewall add rule name="Actuator" protocol=UDP dir=in action=allow
```


Run the delete rule command if it is no longer needed
```sh
netsh advfirewall firewall delete rule name="Actuator" protocol=UDP dir=in
```

IP address configuration:
Enter cmd in the search bar, right click on the command prompt, select Run as administrator, open a command prompt window

<img src="../img/cmd.png" style="width:600px">

View the Ethernet NIC name
```sh
ipconfig
```

<img src="../img/ipconfig.jpg" style="width:600px">


Ethernet NIC name in the above figure is `Ethernet`, modify the IP address of NIC, and enter the command.

```sh
netsh interface ip set address name="Ethernet" source=static addr=192.168.1.111  mask=255.255.255.0  gateway=192.168.1.1 
```
<img src="../img/staticIP.png" style="width:600px">


The `111` in `addr=192.168.1.111` can be modified to other values to avoid IP address conflicts (recommended 100~200)

If reset the IP address to automatic assignment, enter the command

```sh
netsh interface ip set address name="Ethernet" source=dhcp
```

<img src="../img/dhcp.png" style="width:600px">



# Version Information
<table><thead><tr style="background:PaleTurquoise"><th>Version</th><th>	Update time</th><th>	update contents</th></tr></thead><tbody><tr><td>V2.2.0</td><td>2019-05-09</td><td>Current version</td></tr><tr><td>V1.0.0</td><td>18.12.25</td><td>The first version</td></tr>
</tbody></table>
