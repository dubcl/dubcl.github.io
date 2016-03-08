---
layout: post
title: Por fin configure mi DWL-AG122 en linux
date: '2007-11-20 23:01:00'
---


<span style="font-family:arial;">SIIIIII!!!</span>  
<span style="font-family:arial;">Acabo de instalar el maldito USB Wireless ke me regalo el jimmy (gracias denuevo XD), me base en una guia de </span>[este](http://msdark.atwebpages.com/instalar-adaptador-redes-inalambricas-usb-d-link-dwl-g122-ralink-rt73-ubuntu-gutsy)<span style="font-family:arial;"> sitio para ubuntu, los pasos a seguir en debian son los siguentes:</span>

<span style="font-family:arial;">1.- nos bajamos este drivers: </span>[http://rt2x00.serialmonkey.com/rt73-cvs-daily.tar.gz](http://rt2x00.serialmonkey.com/rt73-cvs-daily.tar.gz)

<span style="font-family:arial;">2.- nos vamos a /lib/module<span style="font-size:100%;">s/</span></span><span style="color: rgb(0, 0, 0);font-family:arial;font-size:100%;">2</span><span style="color: rgb(0, 0, 0);font-family:arial;font-size:100%;">.</span><span style="color: rgb(0, 0, 0);font-family:arial;font-size:100%;">6</span><span style="color: rgb(0, 0, 0);font-family:arial;font-size:100%;">.</span><span style="color: rgb(0, 0, 0);font-family:arial;font-size:100%;">18</span><span style="color: rgb(0, 0, 0);font-family:arial;font-size:100%;">–</span><span style="color: rgb(0, 0, 0);font-family:arial;font-size:100%;">5</span><span style="font-family:arial;"><span style="font-size:100%;">-686/kernel/</span>net/ y borramos cualkier archivo o carpeta ke comiense con “rt” (el nombre de la carpeta del kernel puede variar dependiendo de tu version del kernel)</span>

<span style="font-family:arial;">3.- descomprimimos el driver en la carpera en donde lo tengamos</span>

<span style="font-family:arial;"> $ tar -zxvf rt73-cvs-daily.tar.gz</span>

4.- nos vamos a la carpeta en donde se descomprimio

 $ cd rt73-cvs-xxxx/Module/

<span style="font-family:arial;"> (xxx es la fecha varia dependiendo de cuando lo bajaste)</span>

<span style="font-family:arial;">5.- y hacemos un make</span>

<span style="font-family:arial;"> $ make</span>

<span style="font-family:arial;">6.- luego sudo make install</span>

<span style="font-family:arial;">7.- luego hay ke copiar el firmware</span>

<span style="font-family:arial;"> $ sudo cp -v rt73.bin /lib/firmware</span>

<div id="code-8" style="font-family:arial;"><div class="code"> $ sudo cp -v rt73.<span style="">bin</span> /lib/firmware/$<span style="color: rgb(0, 102, 0); font-weight: bold;">(</span>uname -r<span style="color: rgb(0, 102, 0); font-weight: bold;">)</span>8.- cargamos todos los modulos

 $ sudo depmod -a

9.- eliminamos los otros modulos ke puedan dar conflicto con nuestro drivers

 $ sudo modprobe -r rt73usb  
 $ sudo modprobe -r rt2570  
 $ sudo modprobe -r rt2500usb  
 $ sudo modprobe -r rt2ÃƒÂ—00lib

10.- hay ke agregarlos en /etc/modprobe.<span style="">d</span>/blacklist para ke no se cargen al inicio

 $ sudo gedit /etc/modprobe.<span style="">d</span>/blacklist

11.- agregamos esto al final del archivos

<span style="">blacklist</span> rt73usb  
 blacklist rt2570  
 blacklist rt2500usb  
 blacklist rt2ÃƒÂ—00lib

 con esto evitamos la carga de estos modulos

12.- hay ke insertar el modulo

 $ sudo modprobe -v rt73

13.- ahora revisamos ke este disponible el adaptador (si no esta conectado ahora tienes ke hacerlo)

 $ lsusb

saldra algo como esto:

<span style="font-size:85%;"> Bus 004 Device 002: ID 07d1:3c03 D-Link System  
 Bus 004 Device 001: ID 0000:0000  
 Bus 003 Device 001: ID 0000:0000  
 Bus 002 Device 001: ID 0000:0000  
 Bus 001 Device 001: ID 0000:0000</span>

14.-vemos la configuracion inalambrica del equipo

 $ /sbin/iwconfig

saldra algo como esto:

<span style="font-size:85%;"> lo no wireless extensions.</span>

 eth0 no wireless extensions.

 sit0 no wireless extensions.  
<span style="font-size:85%;">  
 wlan0 RT73 WLAN ESSID:”routerwifi”  
 Mode:Managed Frequency=2.462 GHz Access Point: 0A:00:3C:18:85:9F  
 Bit Rate:48 Mb/s  
 RTS thr:off Fragment thr:off</span>  
<span style="font-size:85%;"> Encryption key:off  
 Link Quality=73/100 Signal level:-66 dBm Noise level:-99 dBm  
 Rx invalid nwid:0 Rx invalid crypt:0 Rx invalid frag:0  
 Tx excessive retries:0 Invalid misc:0 Missed beacon:0</span>

15.- ahora ke esta funcionando habilitamos el adaptador

 $ sudo /sbin/ifconfig wlan0 up

16.- editamos el archivos /etc/network/interfaces para iniciar la conexion al inicio de sesion

 $ sudo gedit /etc/network/interfaces

17.- y agregamos esto

 auto wlan0  
 iface wlan0 inet dhcp

18.- probamos si esta el modulo bien

 $ lsmod | grep rt

si sale rt73, todo esta funcionando bien.

y listo.

esto lo hice en debian 4.0r1 etch con kernel 2.6.18

ojala le sirva a alguien mas XD

<div style="text-align: center;">[![](http://bp1.blogger.com/_WLj4OeHg5Rg/R0PVh86JxlI/AAAAAAAAAIM/MbxKDnr6JxI/s200/screenshot.png)](http://bp1.blogger.com/_WLj4OeHg5Rg/R0PVh86JxlI/AAAAAAAAAIM/MbxKDnr6JxI/s1600-h/screenshot.png)<span style="font-size:85%;">screenshot</span></div></div></div>
