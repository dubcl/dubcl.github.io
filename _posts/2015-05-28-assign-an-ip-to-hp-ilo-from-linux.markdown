---
layout: post
title: Assign an IP to HP iLO or IBM System X from Linux
date: '2015-05-28 15:06:34'
---


If you have you iLO or IMM unconfigured and you server is up, you don’t need restart to configure iLO / IMM, you need the follow.

Verify if you have **ipmitool** installed, if not, do:

```language-bash
apt-get install ipmitool
```

Then execute

```language-bash
modprobe ipmi_msghandler  
modprobe ipmi_devintf  
modprobe ipmi_si
```
To ensure the modules are up, now run

```language-bash
ipmitool lan print
```

If you see the follow

```language-bash
Set in Progress         : Set Complete  
Auth Type Support       :   
Auth Type Enable        : Callback :   
                        : User     :   
                        : Operator :   
                        : Admin    :   
                        : OEM      :   
IP Address Source       : DHCP Address  
IP Address              : 0.0.0.0  
Subnet Mask             : 0.0.0.0  
MAC Address             : 9c:b6:54:71:08:16  
BMC ARP Control         : ARP Responses Enabled, Gratuitous ARP Disabled  
Default Gateway IP      : 0.0.0.0  
802.1q VLAN ID          : Disabled  
802.1q VLAN Priority    : 0  
Cipher Suite Priv Max   : Not Available
```
You have ipmitool run correctly 😉

Now we need find the correct channel to set the IP address of iLO, if you execute the follow:

```language-bash
for i in `seq 1 14`; do ipmitool lan print $i 2>/dev/null | grep -q ^Set && echo Channel $i; done
```

That return the channel number, in my case show:

```language-bash
foo@server:~|⇒  for i in `seq 1 14`; do ipmitool lan print $i 2>/dev/null | grep -q ^Set && echo Channel $i; done  
 Channel 2
```

Now we know the channel, then go to setting, the commands are:

```language-bash
ipmitool lan set 2 ipsrc static  
ipmitool lan set 2 ipaddr xxx.xxx.xxx.xxx  
ipmitool lan set 2 netmask xxx.xxx.xxx.xxx  
ipmitool lan set 2 defgw ipaddr xxx.xxx.xxx.xxx
```

Once configure, we need restart iLO, we need do:

For iLO

```language-bash
ipmitool mc reset warm
```

For IMM

```language-bash
ipmitool bmc reset cold
```

That’s all, now we can verify the config execute the first command

```language-bash
ipmitool lan print
```

Now we can open a browser and go to the IP URL and login with the credential configured.

EXAMPLE:

```language-bash
root@server:~|⇒  apt-get install ipmitool  
 Reading package lists... Done  
 Building dependency tree         
 Reading state information... Done  
 The following extra packages will be installed:  
   libopenipmi0 openipmi  
 The following NEW packages will be installed:  
   ipmitool libopenipmi0 openipmi  
 0 upgraded, 3 newly installed, 0 to remove and 132 not upgraded.  
 Need to get 1,061 kB of archives.  
 After this operation, 3,652 kB of additional disk space will be used.  
 Do you want to continue? [Y/n]   
 Get:1 http://ftp.debian.org/debian/ jessie/main ipmitool amd64 1.8.14-4 [376 kB]  
 Get:2 http://ftp.debian.org/debian/ jessie/main libopenipmi0 amd64 2.0.16-1.4 [494 kB]                                                                   
 Get:3 http://ftp.debian.org/debian/ jessie/main openipmi amd64 2.0.16-1.4 [191 kB]                                                                       
 Fetched 1,061 kB in 7s (137 kB/s)                                                                                                                            
 Selecting previously unselected package ipmitool.  
 (Reading database ... 30138 files and directories currently installed.)  
 Preparing to unpack .../ipmitool_1.8.14-4_amd64.deb ...  
 Unpacking ipmitool (1.8.14-4) ...  
 Selecting previously unselected package libopenipmi0.  
 Preparing to unpack .../libopenipmi0_2.0.16-1.4_amd64.deb ...  
 Unpacking libopenipmi0 (2.0.16-1.4) ...  
 Selecting previously unselected package openipmi.  
 Preparing to unpack .../openipmi_2.0.16-1.4_amd64.deb ...  
 Unpacking openipmi (2.0.16-1.4) ...  
 Processing triggers for man-db (2.7.0.2-4) ...  
 Setting up ipmitool (1.8.14-4) ...  
 Job for ipmievd.service failed. See 'systemctl status ipmievd.service' and 'journalctl -xn' for details.  
 invoke-rc.d: initscript ipmievd, action "start" failed.  
 Unable to start ipmievd during installation.  Trying to disable.  
 Setting up libopenipmi0 (2.0.16-1.4) ...  
 Setting up openipmi (2.0.16-1.4) ...  
 Processing triggers for libc-bin (2.19-13) ...  
  
 root@server:~|⇒  modprobe ipmi_msghandler  
  
 root@server:~|⇒  modprobe ipmi_devintf  
  
 root@server:~|⇒   modprobe ipmi_si  
  
 root@server:~|⇒  ipmitool lan print  
 Set in Progress         : Set Complete  
 Auth Type Support       :   
 Auth Type Enable        : Callback :   
                         : User     :   
                         : Operator :   
                         : Admin    :   
                         : OEM      :   
 IP Address Source       : DHCP Address  
 IP Address              : 0.0.0.0  
 Subnet Mask             : 0.0.0.0  
 MAC Address             : 99:99:99:99:99:99  
 BMC ARP Control         : ARP Responses Enabled, Gratuitous ARP Disabled  
 Default Gateway IP      : 0.0.0.0  
 802.1q VLAN ID          : Disabled  
 802.1q VLAN Priority    : 0  
 Cipher Suite Priv Max   : Not Available  
  
 root@server:~|⇒  for i in `seq 1 14`; do ipmitool lan print $i 2>/dev/null | grep -q ^Set && echo Channel $i; done  
 Channel 2  
  
 root@server:~|⇒  ipmitool lan set 2 ipsrc static  
  
 root@server:~|⇒  ipmitool lan set 2 ipaddr 192.1.1.10  
 Setting LAN IP Address to 192.1.1.10  
  
 root@server:~|⇒  ipmitool lan set 2 netmask 255.255.255.0  
 Setting LAN Subnet Mask to 255.255.255.0  
  
 root@server:~|⇒  ipmitool lan set 2 defgw ipaddr 192.1.1.1  
 Setting LAN Default Gateway IP to 192.1.1.1  
  
 root@server:~|⇒  ipmitool mc reset warm   
 Sent warm reset command to MC  
  
 root@server:~|⇒  ipmitool lan print  
 Get Device ID command failed: 0xff </div></td></tr></tbody></table></div>Unspecified error  
 Set in Progress         : Set Complete  
 Auth Type Support       :   
 Auth Type Enable        : Callback :   
                         : User     :   
                         : Operator :   
                         : Admin    :   
                         : OEM      :   
 IP Address Source       : Static Address  
 IP Address              : 192.1.1.10  
 Subnet Mask             : 255.255.255.0  
 MAC Address             : 99:99:99:99:99:99  
 BMC ARP Control         : ARP Responses Enabled, Gratuitous ARP Disabled  
 Default Gateway IP      : 192.1.1.1  
 802.1q VLAN ID          : Disabled  
 802.1q VLAN Priority    : 0  
 Cipher Suite Priv Max   : Not Available
```

NOTE: Added IMM


