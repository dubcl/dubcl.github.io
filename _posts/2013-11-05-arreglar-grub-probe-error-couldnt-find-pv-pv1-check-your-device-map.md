---
layout: post
title: 'Arreglar grub-probe: error: Couldn’t find PV pv1. Check your device.map'
date: '2013-11-05 10:56:34'
---


Estaba actualizando unas máquinas de pruebas con Debian Wheezy clonadas con dd en un entorno KVM, entre los paquetes actualizados estaba Grub. Al terminar el upgrade vi en la consola el mensaje

 ... grub-probe: error: Couldn’t find PV pv1. Check your device.map ...

Si aparece ese error y luego reinicias la máquina se va a null, así que hay que reparar antes de reiniciar.  
 El problema es que el device.map se bugea, así que hay que generarlo nuevamente, entonces hacemos lo siguiente:

 cd /boot/grub mv device.map device.map-OLD grub-mkdevicemap update-grub

Con esto generamos un nuevo device.map y ya podemos reiniciar la VM si miedo ![:)](http://carlos.debianchile.cl/blog/wp-includes/images/smilies/simple-smile.png)

Saludos.


