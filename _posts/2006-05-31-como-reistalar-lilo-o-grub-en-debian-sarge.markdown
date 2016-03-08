---
layout: post
title: Como reistalar LILO o Grub en Debian Sarge
date: '2006-05-31 17:24:00'
---


Ya… aqui les dejo este TIPS para los que tengan este problema a la hora de reinstalar wintendo y tengan Linux y algunos de estos dos gestores de arranque.  
Espero que les guste.  
———————-

En las siguientes lineas les voy a explicar como reinstalar LILO o Grub (para los que no tengan un disquet de arranque de su maquina, cosa que el 99.9% no hace :-P), cosa muy comÃƒÂºn cuando tenemos wintendo y Linux en nuestro PC y se nos funa wintendo y tenemos que instalarlo de nuevo y perdemos nuestro gestor de arranque.

Debemos tener acceso al booteo desde el cd-rom, de no tenerlo debes configurarlo desde tu BIOS, no voy a explicar como se hace por razones obvias, no todos tienen la misma BIOS :-P.

Booteamos con nuestro cd de Debian Sarge, en mi caso use el binario 1 (es la ultima version testing que salio antes de ser frozen), para comenzar la instalaciÃƒÂ³n, debes tratar de que sean los mismos pasos de la instalaciÃƒÂ³n que tienes, en mi caso arranque con la opciÃƒÂ³n “expert” (es por que da mayor control de la instalaciÃƒÂ³n, no por otra cosa :D).

Configuramos lo que nos pida el menÃƒÂº hasta cargar el instalador.

 – Configurar lenguaje  
 – Configurar paÃƒÂ­s o regiÃƒÂ³n  
 – Configurar teclado  
 – Detectar y montar CD-ROM

Con esto carga el instalador de Debian.

…Y cargamos los componentes desde el cdrom…

Una vez cargado el instalador y sus componentes, se debe particionar el disco que contiene Debian, tal y como se hizo al instalar la vez anterior (para mayor seguridad de que nos quede bien), ahora seleccionamos el particionador de discos y damos ENTER.

Al seleccionar esta opciÃƒÂ³n el sistema auto detectara el hardware de nuestro equipo, en mi caso me detecta los discos duros y la tarjeta de red, y a continuaciÃƒÂ³n carga el particionador.

Una vez cargado, seleccionamos **“Manually edit partition table”** (Editar manualmente la tabla de particiones).

Listo esto, seleccionamos la particiÃƒÂ³n donde esta instalado Debian, en mi caso tengo lo siguiente:

” ”  
<span style="font-family:courier new,monospace;"> IDE1 Master (hda) – 3.2 GB ST33210A  
 #primary 1.6 GB fat32  
 #logical 1.6 GB fat32  
 IDE1 Slave (hdb) – 4.3 GB ST43310A  
 #primary 3.0 GB reisefs  
 #primary 1.1 GB fat32  
 #primary 213.9 MB swap swap</span>

Entonces selecciono la particiÃƒÂ³n reiserfs, luego aparece el menÃƒÂº para la ediciÃƒÂ³n de la particiÃƒÂ³n, selecciono **“Use As”**, y aquÃƒÂ­ selecciono el mismo sistema de archivos que tengo en mi particiÃƒÂ³n Debian, la opciÃƒÂ³n **“format the partition”** (formato de la particiÃƒÂ³n) la dejamos con la opciÃƒÂ³n **“no, keep existing data”**(mantener datos existentes), el punto de montaje en este caso es **“/”** ya que instalo todo en una sola particiÃƒÂ³n, lo demÃƒÂ¡s (mount option y booteable flag) los dejo como estÃƒÂ¡n, por que en la instalaciÃƒÂ³n no los modifique.

Una vez terminado, finalizamos el particionado y escribimos los datos en el HD. DespuÃƒÂ©s de esto, pregunta si es que se desea formatear la particiÃƒÂ³n SWAP, a lo que respondemos que si.

Una vez terminado todo y escritos los cambios en el disco, volvemos al menÃƒÂº principal del instalador y ahora seleccionamos **“install the LILO boot loader on a hard disk”** (Instalar el cargador de arranque LILO en el disco duro). Luego pregunta si es que queremos proceder la instalaciÃƒÂ³n del sistema base sobre nuestra instalaciÃƒÂ³n vieja, a lo que respondemos que NO, pero no seleccionamos la opciÃƒÂ³n “NO’, sino que seleccionamos “GO BACK” (atrÃƒÂ¡s).

Con esto nos sale el menÃƒÂº de instalaciÃƒÂ³n de LILO. Ahora seleccionamos donde queremos instalar nuestro LILO, en mi caso lo hago en “/dev/hda”.

Y listo ^_^ se instala nuevamente LILO en nuestro MBR (bueno, o donde lo queramos).

Luego, abortamos la instalacion y reseteamos nuestro PC booteando esta vez desde el HD para ver el resultado 😀

Una cosa mas o menos importante es que al hacer todo esto el archivo **“fstab”** se modifica a como es por defecto asÃƒÂ­ que conviene antes de eliminar LILO, hacer un respaldo de este archivo, si no, deberÃƒÂ¡s modificar fstab cada vez que hagas esto (cosa que si tienes wintrusho sera bien seguido :P).

ACTUALIZACION!!!!

Bueno ya probe con GRUB y tambien funciona, lo unico que hay que hacer es que en vez de seleccionar **“install the LILO boot loader on a hard disk”** seleccionamos la opcion para instalar GRUB

Bueno amigos, espero que les sirva este mini howto de restauraciÃƒÂ³n de LILO o GRUB

Version 1 Publicado en foros.tux.cl [aquÃƒÂ­](http://foros.tux.cl/viewtopic.php?t=5662&sid=9a367c0ef4afcb93de72de0586b0baf6)  
Version 2 para wiki.tux.cl [aquÃƒÂ­](http://www.tux.cl/doku.php?id=articulos:configuracion:como_reinstalar_lilo_o_grub_en_debian_sarge)


