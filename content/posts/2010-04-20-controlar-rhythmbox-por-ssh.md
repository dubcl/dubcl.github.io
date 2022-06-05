---
layout: post
title: Controlar Rhythmbox por ssh
date: '2010-04-20 17:10:11'
---


Recuerdan en post sobre [compartir el WiFi de tu laptop](http://carlos.debianchile.cl/archives/463)?, pues bien resulta que mientras trabajo en el Desktop tengo corriendo [Rhythmbox](www.gnome.org/projects/rhythmbox) en el Laptop paraÃ‚Â amenizar un poco, pero es una lata estarÃ‚Â parÃƒÂ¡ndoseÃ‚Â Ã‚Â cuando quieres cambiar la canciÃƒÂ³n, ya que tengo el Laptop en otro lugar.

La soluciÃƒÂ³n, usar Rhythmbox remotamente, para ello haremos lo siguiente:

**Requisitos**

Tener instalado openssh-server, si no:

> apt-get install openssh-server

Conectarse por ssh a nuestra maquina, si estas en una maquina corriendo Linux, puedes hacerlo directamente desde una consola:

> $ssh IP_DE_LA_MAQUINA

Si estÃƒÂ¡s en Windows puedes usar [PuTTY](www.chiark.greenend.org.uk/.../putty/download.htm).

Ingresas tu usuario, contraseÃƒÂ±a y listo.

Verifica si tienes la variable de entorno de su sesiÃƒÂ³n grÃƒÂ¡fica (generalmente esÃ‚Â DISPLAY=:0.0) con:

> env |grep DISPLAY

Si no, creala con:

> $exportÃ‚Â DISPLAY=:0.0

Ahora la magia es usar el cliente de Rhythmbox, **rhythmbox-client**, por ejemplo, si quieres poner la siguiente canciÃƒÂ³n debes ejecutar:

> $rhythmbox-client –no-start –next

Algunas otras opciones son:

> <div id="_mcePaste">–next</div><div id="_mcePaste">–previous</div><div id="_mcePaste">–play</div><div id="_mcePaste">–pause</div><div id="_mcePaste">–volume-up</div><div id="_mcePaste">–volume-down</div>

<div>Para ver el resto de las opciones pueden ver el man de rhythmbox-client.</div><div>Y ya saben, si le sirviÃƒÂ³, **comente.**

</div>
