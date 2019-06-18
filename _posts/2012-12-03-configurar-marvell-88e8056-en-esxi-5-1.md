---
layout: post
title: Configurar Marvell 88e8056 en ESXi 5.1
date: '2012-12-03 19:00:54'
---


Hoy me tocó instalar un ESXi 5.1 en una maquina, hasta ahí ningún problema, el problema empezó cuando el CD inició y arrojo un lindo mensaje “**No network adapters**“.

Como la maquina tenia Ubuntu rápidamente a reiniciar y aplicar lspci, el cual arrojó esto:

04:00.0 Ethernet controller: Marvell Technology Group Ltd. 88E8056 PCI-E Gigabit Ethernet Controller

Buscando en donde todos sabemos, se menciona que ESXi 5 y 5.1 no tienen el driver de esta tarjeta, indagando un poco más, encontré que hay que agregarle el driver al ISO de instalación de ESXi,  
 así que buscando encontré [ESXi-Customizer](http://www.v-front.de/p/esxi-customizer.html) (para Windows), lo bajamos y además nos descargamos el driver desde [acá](http://www.mediafire.com/?tw765wwoq5d3jl8).

Ya que tenemos los 2 componentes, ejecutamos ESXi-Customizer seleccionamos las iso de ESXi, luego el fichero con el driver y le damos a “Run”.

![](http://3.bp.blogspot.com/-wHJ3a_3pdiI/T0PrYw5D5UI/AAAAAAAAAHo/7nvcu2367AQ/s400/ESXi-Customizer-2.7-GUI.jpg "ESXi-Customizer-2.7-GUI")  
 Esto nos creará una nueva iso que podemos quemar en un CD y proceder a la instalación.

Una ver instalado ESXi, todavía no nos muestra la tarjeta, para hacerla funcionar activamos la shell del ESXi, y realizamos lo siguiente:

lspci -v

Y nos fijamos en

00:05:00.0 Ethernet controller Network controller: Marvell Technologies, Inc. 88E8056 PCI-E Gigabit Ethernet Controller [vmnic0] Class 0200: 11ab:4364

Lo que nos interesa es el 11ab:4364, ahora entramos a picar… dentro de la shell hacemos:

~# cp /bootbank/net-sky2.v00 /tmp/ ~# cd /tmp ~# vmtar -x net-sky2-v00 -o foo.tar ~# mkdir test ~# cp foo.tar test/ ~# cd test ~# tar -xvf foo.tar ~# cd etc/vmware/driver.map.d/ ~# vi sky2.map

Y añadimos lo siguiente al final del archivo

regtype=linux,bus=pci,id=11ab:4364 0000:0000,driver=sky2,class=network

Guardamos y salimos con “:wq”

~# cd /tmp/test ~# tar -cf bar.tar etc usr ~# vmtar -c bar.tar -o /tmp/net-sky.v00-new ~# cd /bootbank ~# mv net-sky2.v00 net-sky2.v00.bak ~# cp /tmp/net-sky.v00-new net-sky2.v00

Y reiniciamos.

Una vez iniciado ESXi podemos ver que ya está la tarjeta operativa y lista para configurar.

Eso sería, chaolín!


