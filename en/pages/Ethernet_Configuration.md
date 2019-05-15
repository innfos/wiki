Ethernet Configuration
=======


## linux platform environment configuration

*   available for ubuntu16.04 LTS and above
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
*   If the computer firewall turned on, open the Control Panel, select System and Security, open the Windows Defender Firewall, click Advanced Settings on the left, and click Inbound Rules.
<img src="../img/001.png" style="width:600px">

New rule 

<img src="../img/002.png" style="width:600px">

Select the port and click Next

<img src="../img/003.png" style="width:600px">

Select udp ，select all local ports, and click Next 

<img src="../img/004.png" style="width:600px">

Allow connection, click next 

<img src="../img/005.png" style="width:600px">

By default, all settings are checked and click Next.

<img src="../img/006.png" style="width:600px">

Fill in the name and click “complete” 

<img src="../img/007.png" style="width:600px">

Ip address configuration,

Open the Control Panel, select Network and Internet, then choose Network and Sharing Center, then select Change Adapter Settings, right click on Ethernet, select Property

<img src="../img/008.png" style="width:600px">

Select TCP/IPv4, then select Property, and configuration is shown as:

119 of 192.168.1.119 in the ip address can be replaced with any integer between 100 and 200, and then click Enter after configuration.

<img src="../img/009.png" style="width:600px">

## Version Change Records

<table><tbody><tr class="odd"><td align="left">
version</td><td align="left">	update time</td><td align="left">	update content</td></tr><tr class="even"><td align="left">V1.0.0</td><td align="left">18.12.25</td><td align="left">全文</td></tr></tbody></table>
