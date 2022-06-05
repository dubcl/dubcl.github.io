---
layout: post
title: Cambiar hostname sin reiniciar
date: '2014-02-10 11:02:02'
---


Fácil, por ejemplo nuestra máquina se llama servidor-foo y queremos ponerle servidor-bar hacemos lo siguiente:

Editamos /etc/hostname y cambiamos el nombre a servidor-bar, luego en /etc/hosts cambiamos el nombre en la linea de la IP

192.168.0.100 servidor-foo.dominio.com servidor-foo

por

192.168.0.100 servidor-bar.dominio.com servidor-bar

Con esto lo cambiarmos de forma permanente para cuando se reinicie la máquina, para cambiarla inmediatamente sin reiniciar ejecutamos:

hostname servidor-bar

Luego nos deslogeamos y logeamos y ya está nuestro nuevo hostname operativo.

No olviden reiniciar los servicios que dependan del hostname ![:)](http://carlos.debianchile.cl/blog/wp-includes/images/smilies/simple-smile.png)

see ya!


