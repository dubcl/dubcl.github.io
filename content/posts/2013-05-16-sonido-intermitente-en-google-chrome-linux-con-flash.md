---
layout: post
title: Sonido intermitente en Google-Chrome Linux con flash
date: '2013-05-16 14:18:47'
---


Configurando un Dell Inspiron 14z me tope con que el sonido de cualquier cosa relacionada con flash player se escuchaba intermitente, averiguando resulta que chrome ya tiene un plugin para flash, el “libpepflashplayer.so” entonces cuando instalas “flashplugin-nonfree” quedan los dos disponibles, por tanto se pisan los talones probocando tal intermitencia en el sonido.

Para solucionarlo en la barra de navegación ponemos chrome://plugins, hacemos click en el boton “Details” (en la barra celeste a la derecha) y buscamos el item “Adobe Flash Player”, veremos algo como esto:

Adobe Flash Player – Version: 11.7.700.169  
 Shockwave Flash 11.7 r700  
 Name: Shockwave Flash  
 Description: Shockwave Flash 11.7 r700  
 Version: 11.7.700.169  
 Location: /opt/google/chrome/PepperFlash/libpepflashplayer.so  
 Type: PPAPI (out-of-process)  
 [Disable]  
 MIME types: MIME type Description File extensions  
 application/x-shockwave-flash Shockwave Flash .swf  
 application/futuresplash FutureSplash Player .spl

Hacemos click en “Disable” para “apagar” el plugin y dejar solo el libflashplayer.so (que debería estar más abajo), reiniciamos el navegador y listo, ahora el sonido debería salir como corresponde.


