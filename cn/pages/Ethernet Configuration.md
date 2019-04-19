[中文](以太网配置 "wikilink")

# Linux platform environment configuration

*   available for ubuntu16.04 LTS and above
*   cmake installation: open terminal &amp; input command
<div class="sourceCode">

    $ <span class="kw">sudo</span> apt-get install cmake`</pre></div>

*   ip address configuration: open terminal and input
    <div class="sourceCode"><pre class="sourceCode bash">`$ <span class="kw">ifconfig</span>`</pre></div>

    Check network configuration [none|thumb|400px](file:020.png "wikilink") [none|thumb|400px](file:021.png "wikilink")

    In the example, the name of the wired network card is enp0s25, enter the command

    <div class="sourceCode"><pre class="sourceCode bash">`$ <span class="kw">sudo</span> ifconfig enp0s25 static 192.168.1.111
</div>

After the configuration, enter ifconfig to see the ip address.

# Windows platform environment configuration

*   requires 64-bit Windows operating system above win7 sp1
*   If the computer firewall turned on, open the Control Panel, select System and Security, open the Windows Defender Firewall, click Advanced Settings on the left, and click Inbound Rules.

[none|thumb|400px](file:001.png "wikilink")

New rule [none|thumb|400px](file:002.png "wikilink")

Select the port and click Next

[none|thumb|400px](file:003.png "wikilink")

Select udp ，select all local ports, and click Next [none|thumb|400px](file:004.png "wikilink")

Allow connection, click next, [none|thumb|400px](file:005.png "wikilink")

By default, all settings are checked and click Next. [none](file:006.png "wikilink")

Fill in the name and click “complete” [none](file:007.png "wikilink")

Ip address configuration,

Open the Control Panel, select Network and Internet, then choose Network and Sharing Center, then select Change Adapter Settings, right click on Ethernet, select Property [008.png](008.png "wikilink")

Select TCP/IPv4, then select Property, and configuration is shown as:

119 of 192.168.1.119 in the ip address can be replaced with any integer between 100 and 200, and then click Enter after configuration. [009.png](009.png "wikilink")

# Version Change Records

The following table briefly describes the version change records.

<table>
<tbody>
<tr class="odd">
<td align="left">

**version**
</td>
<td align="left">

**update time**
</td>
<td align="left">

**update content**
</td>
</tr>
<tr class="even">
<td align="left">

V1.0.0
</td>
<td align="left">

18.12.25
</td>
<td align="left">

full text
</td>
</tr>
</tbody>
</table>