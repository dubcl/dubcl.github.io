---
layout: post
title: Agregando WinXP a Grub2
date: '2009-10-16 21:20:20'
---


A mÃƒÂ¡s de alguno debe haberle pasado…

En mi desktop tengo 2 discos duros, uno SATA con windows xp (si, si… los juegos) y otro IDE donde acabo de instalar Debian Squeeze, en la instalaciÃƒÂ³n de Debian no tuve ningÃƒÂºn problema, pero al reiniciar una vez terminada la instalaciÃƒÂ³n, en el menu de GRUB no estaba la entrada para booter a windows xp, solucionar esto es muy simple.

Estando de nuestro Debian, logueamos como root, e instalamos os-prober

> #apt-get install os-prober

Luego ejecutamos os-prober

> #os-prober

si todo saliÃƒÂ³ bien nos mostrarÃƒÂ¡ una linea parecida a esta:

> Windows XP (loader) (on /dev/sda1)

Ahora actualizamos GRUB…

> #update-grub2

Luego para probar reiniciamos y ya tenemos nuestra entrada para bootear Windows XP desde GRUB 2.

*Si le sivio, comente…*


