---
layout: post
title: Vaciar cache en Linux
date: '2010-09-01 00:33:30'
---


Bueh!

Suelo tener el pc prendido varios dí­as, y por ende los programas en cache aumentan considerablemente, la forma común de vaciar el cache el derechamente apagando el pc, pero hay otra forma más técnica y es ejecutando el siguiente comando en consola como root

> echo 3 > /proc/sys/vm/drop_caches

Con eso vaciamos el cache y nuestra pc quedará “livianito”

Y ya sabe, si le sirvió, comente =B


