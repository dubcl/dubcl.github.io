---
layout: post
title: InstalaciÃƒÂ³n y ConfiguraciÃƒÂ³n de Fluxbox.
date: '2006-06-05 17:56:00'
---


En este documento tratare (digo tratare por que esto es solo una referencia) de explicar algunos puntos de configuracion para que nuestro FluxBox se vea bien y nos sea facil y amigable de usar.

**Nota**  
Se asume que ya se tiene instalado algun servidor grafico.

Instalacion

**Desde apt**

Para instalar debemos hacer lo siguiente como root.

<span style="font-family:courier new,monospace;">#apt-get install fluxbox </span>

Opcionalmente tambien se piede instalar fluxconf que es una herramienta para configurar fluxbox.

<span style="font-family:courier new,monospace;">#apt-get install fluxconf  
</span>  
Si es que faltara alguna libreria u otro apt se encargara de resolverlo.

Una vez completada la instalacion estamos listos para usarlo.

**Desde source**

Primero debemos descargar el paquete con las fuentes, estos se encuentra en la pagina de fluxbox http://fluxbox.sourceforge.net/download.php

una vez descargado lo descomprimimos

<span style="font-family:courier new,monospace;">#tar xvzf fluxbox-0.1.12.tar.gz</span>

Con esto se creara un directorio con el codigo fuente del programa, ahora ingresamos al directorio creado

<span style="font-family:courier new,monospace;">#cd fluxbox-0.1.12</span>

(El nombre del directorio depende de la version)

Una vez dentro debemos ejecutar el configurador.

<span style="font-family:courier new,monospace;">#./configure</span>

Para las opciones de confiuracion vean el archivo **README** o **INSTALL**, no voy a explicar las opciones de configuracion por que eso depende de cada maquina.

Una vez que el <span style="font-family:courier new,monospace;">./configure</span> termine, si arroja algun error, vean de que se trata y traten de resolverlo. Si ha resultado con exito hacemos lo siguiente:

<span style="font-family:courier new,monospace;">#make</span>

Y luego como root…

<span style="font-family:courier new,monospace;">#make install</span>

y listo.

En general (<span style="font-family:courier new,monospace;">./configure, make, make install</span>) son los pasos para instalar cualquier programa desde sus fuentes.

**Inciar fluxbox**

Existen dos formas, una es logearse y ejecutar, startx si es que no tenemos instalado algun administrador de login, si lo tubieramos (wdm, gdm, kdm u otro), seleccionamos fluxbox y logeamos para entrar.

Una vez dentro se vera algo como esto.

[![](http://caralbornozc.googlepages.com/imagen01.png/imagen01-medium.jpg)](http://caralbornozc.googlepages.com/imagen01.png/imagen01-full.jpg)

Pero ustedes diran “Que feo!!!”, pues si, de primera no es muy lindo xD, pero ahora vamos a retocarlo y dejarlo mas o menos a nuestro gusto.

**Configuracion**  
**  
Wallpapers**

Fluxbox tiene varias herramientas de configuracion. Una de ellas es **fbsetbg** que sirve para colocar un wallpaper en nuestro escritorio. Por ejemplo, en nuestro home tenemos una carpeta llamda fondos con varios wallpapers, y hay uno (<span style="font-family:courier new,monospace;">wall01-1024×768.png</span>) que nos gusta y queremos colocarlo, para ello cargamos una consola y ejecutamos (asumiendo que estamos dentro de nuestro home):

<span style="font-family:courier new,monospace;">#fbsetbg -f fondos/wall01-1024×768.png</span>

y listo, ya tenemos un wallpaper en nuestro escritorio (la opcion **-f **indica fullscreen).

[![](http://caralbornozc.googlepages.com/imagen02.png/imagen02-medium.jpg)](http://caralbornozc.googlepages.com/imagen02.png/imagen02-full.jpg)

**Style**

Son lo que da la apariencia al panel, a los borces de las ventanas, etc… Por defecto fluxbox biene con varios styles, por ejemplo el que se ha visto hasta ahora de llama Minimal. Estos styles son cambiables desde el **menu -> Styles**

[![](http://caralbornozc.googlepages.com/imagen03.png/imagen03-medium.jpg)](http://caralbornozc.googlepages.com/imagen03.png/imagen03-full.jpg)

****  
Estos Styles se encuentras en <span style="font-family:courier new,monospace;">/usr/share/fluxbox/styles</span>, estos son los que estan disponibles para todos los usuarios, opcionalmente si queremos tener mas styles en el directorio <span style="font-family:courier new,monospace;">~/.fluxbox/styles</span> de nuestro home tambien podemos agregar mas, estos seran accesibles solo para el usuario. En la misma pagina de fluxbox se pueden bajar algunos.

**Iconos**

Fluxbox por defecto no tiene iconos, esto es lo que atrae a muchas personas a usarlo, pero tambien es una traba para las personas que vienen migrando desde el “Lado Oscuro de la Fuerza”. Afortunadamente fluxbox tiene una herramienta llamada **fbdesk**, pero existe otro programa llamado **idesk** (que me gusta mas que **fbdesk**) que tambien coloca iconos en nuestro desktop, y es la que vamos a utilizar.

Primero la instalamos, como root hacemos:

<span style="font-family:courier new,monospace;">#apt-get install idesk</span>

Este programa consta de un archivo de configuracion alojado en nuestro home llamado <span style="font-family:courier new,monospace;">.ideskrc</span> y una carpeta <span style="font-family:courier new,monospace;">.idesktop</span> que contiene los archivos de configuracion de cada icono (<span style="font-family:courier new,monospace;">*.lnk</span>) que nosotros queramos poner. Por defecto estos archivos no existen, asi que vamos a crearlos.  
En la carpeta <span style="font-family:courier new,monospace;">/usr/share/doc/examples/</span> estan los archivos por ejemplo de <span style="font-family:courier new,monospace;">.ideskrc</span> y de los <span style="font-family:courier new,monospace;">.lnk</span>, entonces ahora copiamos a nuestro home.

<span style="font-family:courier new,monospace;">#cp /usr/share/doc/examples/dot.ideskrc ~/.ideskrc</span>

Al <span style="font-family:courier new,monospace;">.ideskrc</span> no es necesario modificarlo.

Tambien debemos crear la carpeta que contiene los iconos a mostrar.

<span style="font-family:courier new,monospace;">#mkdir .idesktop</span>

Ahora copiamos el archivo de ejemplo de los <span style="font-family:courier new,monospace;">.lnk</span> a nuestro directorio

<span style="font-family:courier new,monospace;">#cp /usr/share/doc/examples/galeon.lnk ~/.idesktop/</span>

Entonces ahora entramos a **.idesktop**

<span style="font-family:courier new,monospace;">#cd .idesktop</span>

La estructura del erchivo .lnk es la siguiente:

<span style="font-family:courier new,monospace;">table Icon  
Caption:  
Command:  
Icon:  
X:  
Y:  
end </span>

Entonces, vamos a crear un icono para xmms (por ejemplo), para ello tendriamos que poner lo siguiente:

<span style="font-family:courier new,monospace;">table Icon  
Caption: Xmms  
Command: Xmms  
Icon: /usr/share/pixmap/apps/xmms.png  
X: 50  
Y: 50  
end </span>

…Y ya tenemos nuestro primer icono xD, ahora no nos queda mas que seguir agregando iconos a nuestro gusto.

[![](http://caralbornozc.googlepages.com/imagen04.png/imagen04-medium.jpg)](http://caralbornozc.googlepages.com/imagen04.png/imagen04-full.jpg)

Como pueden ver en la imagen los iconos se ven semi-transparentes, eso se logra configurando el erchivo <span style="font-family:courier new,monospace;">.ideksrc</span>, no lo voy a comentar ya que el archivo por si solo es bastante sencillo de comprender.

**La Slit y los DockApps**

Los DockApp son mini-programas que tienen diversas utilidades, estos son originarios de **WindowMaker**, por eso los nombres de la mayoria de estos empiezan con “*wm*“.  
La gran gracias que tienen estos DockApp’s es que casi no cosumen recursos.

La Slit (originaria de **BlackBox**) es una especie de barra de herramientas en donde son alojados los DockApp.

**Instalando DockApp.**

Por ejemplo yo uso los siguientes DockApp:

wmix -> Sirve para controlar el volumen de dispocitivos OSS y ALSA.  
wmcpuload -> Muestra el uso de la CPU.  
wmmemmon -> Muestra el uso de la memoria RAM y la SWAP.  
fbpager -> Es el paginador de escritorios virtuales de FluxBox.

La instalacion de estos es igual a la de cualquier programa en debian, siempre y cuando esten en los repositorios. En este caso los voy a instalar todos de una vez.

<span style="font-family:courier new,monospace;">#apt-get install wmix wmcpuload wmmemmon fbpager</span>

Tambien estan disponibles en formato source.  
Entonces una vez instalado quedarian de la siguiente manera.

[![](http://caralbornozc.googlepages.com/imagen05.png/imagen05-medium.jpg)](http://caralbornozc.googlepages.com/imagen05.png/imagen05-full.jpg)

de abajo hacia arriba: wmmemmon – wmcpuload – wmix – fbpager

**El MenÃƒÂº**

El menÃƒÂº en Fluxbox es solo un archivo de texto con algunas etiquetas que permiten crear submenues, ejecutar aplicaciones, controlar lor workspaces, configurar FluxBox y salir del mismo.  
Una estructura bÃƒÂ¡sica setia algo asi:

<span style="font-family:courier new,monospace;">[begin] (MenuTitle) {}  
[submenu] (SubMenuName) {SubMenuTitle}  
[exec] (CommandName) {command}  
[include] (/path/del/menu) <icono>  
[end]  
[nop] (————)  
#comentario  
[config] (FluxBoxConfiguration) {}  
[stylesdir] (/path/de/los/styles) {}  
[workspaces] (Workspaces) {}  
[reconfig] (Reconfigure) {}  
[restart] (Restart) {}  
[exit] (Exit) {}  
[end]</span>

Los include deben comenzar con un <span style="font-family:courier new,monospace;">[begin]</span> y terminar con un <span style="font-family:courier new,monospace;">[end] </span>

<span style="font-family:courier new,monospace;">[ ]</span> -> es un comando de fluxbox.  
<span style="font-family:courier new,monospace;">( )</span> -> es el nombre que se muestra en el menu.  
<span style="font-family:courier new,monospace;">{ }</span> -> es el comando que se ejecuta al hacer click a la entrada.  
<span style="font-family:courier new,monospace;">< ></span> -> es la path del icono, este debe estar en formato xpm.  
<span style="font-family:courier new,monospace;">[nop]</span> -> permite poner separadores.  
<span style="font-family:courier new,monospace;">[config]</span> -> muestra la configuracion de fluxbox.  
<span style="font-family:courier new,monospace;">[reconfig]</span> -> si se usa el menu <span style="font-family:courier new,monospace;">[config]</span> para editar los parametros de fluxbox, al cerrar fluxbox, las configuraciones hechas se pierden, este comando sirve para guardar los cambios realizados (<span style="font-family:courier new,monospace;">~/.fluxbox/init</span>).  
<span style="font-family:courier new,monospace;">[workspaces]</span> -> muestra los escritorios virtuales y su contenido.  
<span style="font-family:courier new,monospace;">[restart]</span> -> reinicia FluxBox.  
<span style="font-family:courier new,monospace;">[exit]</span> -> solo sale de FluxBox.

Ya con esta informacion es solo cosa de ponerse a meter mano y crear su propio menu.

**KeyGrabber**

Esta es, a mi pareser, una exelente herramienta. Se trata de combinaciones de teclas para ejecutar cosas en FluxBox.

Un archivo comÃƒÂºn de KeyGrabber se verÃƒÂ­a asÃƒÂ­.

<span style="font-family:courier new,monospace;">Mod1 Tab :NextWindow  
Mod1 Shift Tab : PrevWindow  
Mod1 F1 :Workspace 1  
Mod1 F2 :Workspace 2  
Mod1 F3 :Workspace 3  
Mod1 F4 :Workspace 4  
Mod4 r :ExecCommand fbrun</span>

**Nombre de las letras.**

Existe una aplicacion llamada xev, que al ejecutarce muestra una ventana con un cuadro blanco y una consola que muestra la salida de los eventos que se aplican al programa.

Por ejemplo se ve lo que sale a presionar la tecla “p”.

<span style="font-family:courier new,monospace;"><span style="font-size:85%;">KeyPress event, serial 28, synthetic NO, window 0x1c00001, root 0x3b, subw 0x0, time 10788530, (69,-10), root:(282,218), state 0x10, keycode 33 (keysym 0x70, p), same_screen YES, XLookupString gives 1 bytes: “p”</span>  
</span>  
Lo que estÃƒÂ¡ despues de *keysym 0x70* viene siendo el nombre de la tecla, en este caso “**p**“.

Si es que, por ejemplo, ubieramos apretado Enter, el nombre seria “**Return**“.

Los Modificadores por defecto son: Control, Mod1 (Alt), Shift, Mod4 (la tecla Super).

Con esto y el nombre de las teclas podermos empezar a crear las combinaciones que queramos, por ejemplo:

<span style="font-family:courier new,monospace;font-size:85%;">Mod1 Tab :NextWindow -> muestra la ventana siguiente  
Mod1 Shift Tab : PrevWindow -> muestra la ventana anterior  
Mod1 F1 :Workspace 1 -> muestra el escritorio virtual 1  
Mod1 F2 :Workspace 2 -> muestra el escritorio virtual 2  
Mod1 F3 :Workspace 3 -> muestra el escritorio virtual 3  
Mod1 F4 :Workspace 4 -> muestra el escritorio virtual 4  
Mod4 r :ExecCommand fbrun -> ejecuta fbrun </span>

Existen otras acciones que se pueden realizar, pero no las pondre para ahorar espacio :P, si quieren verlas, bajense el **fluxbook**, que es la documentaciÃƒÂ³n de FluxBox disponible en la pagina principal de FluxBox.

**AutomatizaciÃƒÂ³n de aplicaciones.**

Cada vez que iniciamos FluxBox los DockApp o el Wallpaper no se cargan al inicio, y es muy tedioso y molesto tener que iniciarlas cada vez que entramos FluxBox.

Para ello debemos editar el archivo de configuracion de nuestro FluxBox (<span style="font-family:courier new,monospace;">~/.fluxbox/init</span>), ubicamos la linea que dice <span style="font-family:courier new,monospace;">session.screen0.rootCommand </span>y ahÃƒÂ­ aÃƒÂ±adimos las aplicaciones que queremos que se inicien al iniciar FluxBox. Por Ejemplo:

<span style="font-family:courier new,monospace;">session.screen0.rootCommand: wmix & wmcpuload & wmmemmon & fbpager -w & fbsetbg -f fondos/wall01-1024×768.png  
</span>  
Con esto cargamos al iniciar FluxBox las aplicaciones que se han mencionado en este howto.

**Otras Herramientas**

Con esto del menu, algunos diran, “Pero es una lata hacer eso a mano”. Para ellos que pienzan asÃƒÂ­, se creo una utilidad llamada **FluxMenu**.

[![](http://caralbornozc.googlepages.com/imagen06.png/imagen06-medium.jpg)](http://caralbornozc.googlepages.com/imagen06.png/imagen06-full.jpg)

Esta nos permite crear menues de manera mas facil, no necesita mas explicacion ya que es muy intuitivo.

Los KeyGrabber se pueden crear facilmente con **Fluxkeys** no necesita mas explicacion ya que es muy intuitivo.

[![](http://caralbornozc.googlepages.com/imagen07.png/imagen07-medium.jpg)](http://caralbornozc.googlepages.com/imagen07.png/imagen07-full.jpg)

**Links**

PÃƒÂ¡gina principal de FluxBox  
[http://fluxbox.sourceforge.net](http://fluxbox.sourceforge.net/)

DockApps

[http://dockapps.org/](http://dockapps.org/)

Themes

[http://www.freshmeat.net](http://themes.freshmeat.net/browse/962/)

Bueno amigos con esto ya podemos editar FluxBox a nuestro gusto, los demas queda a la imaginacion de cada uno.

El mio estÃƒÂ¡ asÃƒÂ­ (por ahora).

[![](http://caralbornozc.googlepages.com/imagen08.png/imagen08-medium.jpg)](http://caralbornozc.googlepages.com/imagen08.png/imagen08-full.jpg)

Este HowTo estÃƒÂ¡ basado en la documentacion de FluxBox disponible en su pÃƒÂ¡gina y en mi experiencia en el.  
Las configuraciones aqui mencionadas se han realizado sobre Debian GNU/Linux Sarge Testing.  
Disculpen las faltas ortograficas 😛


