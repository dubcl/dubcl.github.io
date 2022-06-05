---
layout: post
title: Compartir el WiFi a otro pc y otras yerbas
date: '2009-12-20 02:57:11'
---


Pasa lo siguiente…

La vecina con la que compartÃƒÂ­a Internet, decidiÃƒÂ³ cerrar el plan y dejarme sin Internet, asÃƒÂ­ que me puse a <span style="text-decoration: line-through;">crackear</span> hacer unaÃ‚Â auditoriaÃ‚Â a las redes de las cercanÃƒÂ­a, asÃƒÂ­ que me tope con una que no tenia password, pero tenia filtrado MAC, la soluciÃƒÂ³n, clonar alguna *[MAC](http://es.wikipedia.org/wiki/DirecciÃƒÂ³n_MAC "DirecciÃƒÂ³n MAC")*, para ello conosco 2 formas, asignar la *MAC* en el archivo */etc/network/interfaces* o usar *macchanger*, opte por la primera opciÃƒÂ³n por que obviamente no tenia como instalar el ultimo.

**Como saber alguna MAC aceptada en la redÃ‚Â <span style="font-weight: normal;"><span style="text-decoration: line-through;">**crackear**</span>**auditada****.**</span>**

Para saber que *MAC* valida asignarle a nuestra tarjeta de red, debemos “snifiar” la red, esto lo hacemos con la suite de auditoria inalÃƒÂ¡mbrica *aircrack-ng*, primero debemos poner la tarjeta inalÃƒÂ¡mbrica en modo monitor, esto lo hacemos con *airmon-ng* de la siguiente manera:

> #airmon-ng start wlan0

nos saldrÃƒÂ¡ algo como esto:

> Found 3 processes that could cause trouble.  
>  If airodump-ng, aireplay-ng or airtun-ng stops working after  
>  a short period of time, you may want to kill (some of) them!  
>  PID<span style="white-space: pre;"></span>Name  
>  1613<span style="white-space: pre;"></span>avahi-daemon  
>  1614<span style="white-space: pre;"></span>avahi-daemon  
>  6204<span style="white-space: pre;"></span>dhclient3  
>  Process with PID 6204 (dhclient3) is running on interface wlan0
> 
> Interface<span style="white-space: pre;"></span>Chipset<span style="white-space: pre;"></span>Driver  
>  wlan0<span style="white-space: pre;"></span>Broadcom<span style="white-space: pre;"></span>b43 – [phy2]  
> <span style="white-space: pre;"></span>(monitor mode enabled on mon0)

ya tenemos nuestra tarjeta en *modo monitor*, en este caso me asignÃƒÂ³ **mon0** como la interfaz monitor, ahora veremos las redes del area, dentro de las cuales esta la que estamos auditando, y veremos los que estÃƒÂ¡n conectados a los AP correcpondientes, para ello usamos el comando

> #airomon-ng mon0

esto nos mostrarÃƒÂ¡ algo como esto:

<div id="_mcePaste">[![](http://carlos.debianchile.cl/wp-content/uploads/2009/12/airodump-ng.png "airodump-ng")](http://carlos.debianchile.cl/wp-content/uploads/2009/12/airodump-ng.png)</div>En la columna *[BSSID](http://es.wikipedia.org/wiki/BSSID "BSSID")* estÃƒÂ¡n las *MAC’s* de las redes delÃ‚Â ÃƒÂ¡rea, en la parte de abajo estÃƒÂ¡n las asociaciones, en la columna *STATION* estÃƒÂ¡n las *MAC’s* que ya estan asociadas a una red en particular y las que nosotros necesitamos saber para poder asignarle a nuestra tarjeta inalÃƒÂ¡mbrica.

**Asignar una MAC a una targeta de red.**

En este casoÃ‚Â fueÃ‚Â cambiarle la *MAC* a laÃ‚Â tarjetaÃ‚Â inalÃƒÂ¡mbrica por alguna que ya estuviera conectada a la red, para poder pasar el filtro de la red <span style="text-decoration: line-through;">crackeada</span> auditada, entonces editamos (como root) el archivo *interfaces* y agregamos lo siguiente:

> # The wireless network interface  
>  allow-hotplug wlan0  
>  iface wlan0 inet dhcp  
>  hwaddress ether 00:1E:XX:XX:XX:XX

Luego reiniciamos las interfaces con

> #/etc/init.d/networking restart

Para ver si se realizÃƒÂ³ el cambio revisamos con ifconfig, deberiamos ver algo como esto:

> wlan0 Ã‚Â  Ã‚Â  Link encap:Ethernet Ã‚Â HWaddr 00:1E:XX:XX:XX:XX

y listo, ya tenemos clonada la MAC.

**Compartir Internet a otro PC.**

Estado de la red:

1 Laptop con 2 tarjetas de red, 1 wireless (*wlan0*) y otra normal (*eth0*) y un pc desktop con 1 tarjeta de red.

Bueno, la idea es obtener Internet desde la red <span style="text-decoration: line-through;">crackeada</span> auditada (*wlan0*) y compartirla a travez de la *eth0*, para ello configuramos una IP fija a *eth0* en */etc/network/interfaces* de la siguienre forma:

> # The primary network interface  
>  auto eth0  
>  allow-hotplug eth0  
>  iface eth0 inet static  
>  address 192.168.2.1  
>  netmask 255.255.255.0  
>  network 192.168.2.0  
>  broadcast 192.168.2.255

Por Ejemplo….

En resumen el archivo */etc/network/interfaces* quedarÃƒÂ­a algo como esto:

> # This file describes the network interfaces available on your system  
>  # and how to activate them. For more information, see interfaces(5).
> 
> # The loopback network interface  
>  auto lo  
>  iface lo inet loopback
> 
> # The primary network interface  
>  auto eth0  
>  allow-hotplug eth0  
>  iface eth0 inet static  
>  address 192.168.2.1  
>  netmask 255.255.255.0  
>  network 192.168.2.0  
>  broadcast 192.168.2.255
> 
> # The wireless network interface
> 
> allow-hotplug wlan0  
>  iface wlan0 inet dhcp  
>  hwaddress ether 00:1E:XX:XX:XX:XX

<div>Ahora la magia estÃƒÂ¡ en hacer un puente *[NAT](es.wikipedia.org/wiki/Network_Address_Translation "NAT")* desde *eth0* hacia *wlan0*, esto se hace con *[IPTABLES](es.wikipedia.org/wiki/Netfilter/iptables "IPTABLES")*, para ello no hay que instalar nada, ya que *IPTABLES* viene por defecto en el [Kernel Linux](http://es.wikipedia.org/wiki/Linux_(nÃƒÂºcleo) "Linux").  
 Podemos crear un archivo [*puente*] (para no estar escribiendo todo cada vez que queramos Ã‚Â compartir la conexiÃƒÂ³n) con el siguiente contenido:</div><div>> <div>#!/bin/bash</div><div>#Creacion del Puente</div><div>echo 1 > /proc/sys/net/ipv4/ip_forward</div><div>iptables -t nat -A POSTROUTING -o wlan0 -j MASQUERADE</div>

</div><div>le damos permisos de ejecuciÃƒÂ³n con</div>> <div># chmod 777 puente</div>

<div>y lo ejecutamos con</div>> <div>#./puente</div>

<div>y listo.</div><div>Ahora, para poder configurar los equipos clientes se deben configurar *IP’s* estaticas en cada uno de ellos basado en la configuraciÃƒÂ³n que le realizamos a *eth0*, por ejemplo:</div><div></div>> <div>Cliente 1</div><div>IP: 192.168.2.2</div><div>NETMASK: 255.255.255.0</div><div>GATEWAY: 192.168.2.1</div><div>DNS1: el que quieran</div><div>DNS2:Ã‚Â el que quieran</div>

<div></div><div>Eso es todo por fin, ahora solo resta probar la conexiÃƒÂ³n Ã‚Â en el PC cliente.</div><div>Espero que a alguien le sea ÃƒÂºtil, y ya saben, si le sirviÃƒÂ³, **comente**.</div>
