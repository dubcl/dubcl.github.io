---
layout: post
title: Como reistalar LILO o Grub en Debian Sarge
date: '2006-05-31 17:24:00'
---


Ya… aqui les dejo este TIPS para los que tengan este problema a la hora de reinstalar wintendo y tengan Linux y algunos de estos dos gestores de arranque.  
Espero que les guste.  
———————-

En las siguientes lineas les voy a explicar como reinstalar LILO o Grub (para los que no tengan un disquet de arranque de su maquina, cosa que el 99.9% no hace :-P), cosa muy común cuando tenemos wintendo y Linux en nuestro PC y se nos funa wintendo y tenemos que instalarlo de nuevo y perdemos nuestro gestor de arranque.

Debemos tener acceso al booteo desde el cd-rom, de no tenerlo debes configurarlo desde tu BIOS, no voy a explicar como se hace por razones obvias, no todos tienen la misma BIOS :-P.

Booteamos con nuestro cd de Debian Sarge, en mi caso use el binario 1 (es la ultima version testing que salio antes de ser frozen), para comenzar la instalación, debes tratar de que sean los mismos pasos de la instalación que tienes, en mi caso arranque con la opción “expert” (es por que da mayor control de la instalación, no por otra cosa :D).

Configuramos lo que nos pida el menú hasta cargar el instalador.

 – Configurar lenguaje  
 – Configurar país o región  
 – Configurar teclado  
 – Detectar y montar CD-ROM

Con esto carga el instalador de Debian.

…Y cargamos los componentes desde el cdrom…

Una vez cargado el instalador y sus componentes, se debe particionar el disco que contiene Debian, tal y como se hizo al instalar la vez anterior (para mayor seguridad de que nos quede bien), ahora seleccionamos el particionador de discos y damos ENTER.

Al seleccionar esta opción el sistema auto detectara el hardware de nuestro equipo, en mi caso me detecta los discos duros y la tarjeta de red, y a continuación carga el particionador.

Una vez cargado, seleccionamos **“Manually edit partition table”** (Editar manualmente la tabla de particiones).

Listo esto, seleccionamos la partición donde esta instalado Debian, en mi caso tengo lo siguiente:

” ”  
<span style="font-family:courier new,monospace;"> IDE1 Master (hda) – 3.2 GB ST33210A  
 #primary 1.6 GB fat32  
 #logical 1.6 GB fat32  
 IDE1 Slave (hdb) – 4.3 GB ST43310A  
 #primary 3.0 GB reisefs  
 #primary 1.1 GB fat32  
 #primary 213.9 MB swap swap</span>

Entonces selecciono la partición reiserfs, luego aparece el menú para la edición de la partición, selecciono **“Use As”**, y aquí selecciono el mismo sistema de archivos que tengo en mi partición Debian, la opción **“format the partition”** (formato de la partición) la dejamos con la opción **“no, keep existing data”**(mantener datos existentes), el punto de montaje en este caso es **“/”** ya que instalo todo en una sola partición, lo demás (mount option y booteable flag) los dejo como están, por que en la instalación no los modifique.

Una vez terminado, finalizamos el particionado y escribimos los datos en el HD. DespuÃƒÂ©s de esto, pregunta si es que se desea formatear la partición SWAP, a lo que respondemos que si.

Una vez terminado todo y escritos los cambios en el disco, volvemos al menú principal del instalador y ahora seleccionamos **“install the LILO boot loader on a hard disk”** (Instalar el cargador de arranque LILO en el disco duro). Luego pregunta si es que queremos proceder la instalación del sistema base sobre nuestra instalación vieja, a lo que respondemos que NO, pero no seleccionamos la opción “NO’, sino que seleccionamos “GO BACK” (atrás).

Con esto nos sale el menú de instalación de LILO. Ahora seleccionamos donde queremos instalar nuestro LILO, en mi caso lo hago en “/dev/hda”.

Y listo ^_^ se instala nuevamente LILO en nuestro MBR (bueno, o donde lo queramos).

Luego, abortamos la instalacion y reseteamos nuestro PC booteando esta vez desde el HD para ver el resultado 😀

Una cosa mas o menos importante es que al hacer todo esto el archivo **“fstab”** se modifica a como es por defecto así que conviene antes de eliminar LILO, hacer un respaldo de este archivo, si no, deberás modificar fstab cada vez que hagas esto (cosa que si tienes wintrusho sera bien seguido :P).

ACTUALIZACION!!!!

Bueno ya probe con GRUB y tambien funciona, lo unico que hay que hacer es que en vez de seleccionar **“install the LILO boot loader on a hard disk”** seleccionamos la opcion para instalar GRUB

Bueno amigos, espero que les sirva este mini howto de restauración de LILO o GRUB

Version 1 Publicado en foros.tux.cl [aquí](http://foros.tux.cl/viewtopic.php?t=5662&sid=9a367c0ef4afcb93de72de0586b0baf6)  
Version 2 para wiki.tux.cl [aquí](http://www.tux.cl/doku.php?id=articulos:configuracion:como_reinstalar_lilo_o_grub_en_debian_sarge)


