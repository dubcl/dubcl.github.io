---
layout: post
title: Error al actualizar Debian Sid (unstable) - console-tools
date: '2010-01-08 01:07:20'
---


Bueh… Acabo de hacer un “upgrade” a mi sistema y al terminar la configuraciÃƒÂ³n aparece el siguiente error:

> Configurando console-tools (1:0.2.3dbs-67) …  
>  insserv: warning: script ‘puente’ missing LSB tags and overrides  
>  Setting console screen modes and fonts.  
>  Setting console screen modes and fonts.  
>  invoke-rc.d: initscript console-screen.sh, action “start” failed.  
>  dpkg: error al procesar console-tools (–configure):  
>  el subproceso installed post-installation script devolviÃƒÂ³ el cÃƒÂ³digo de salida de error 1  
>  Se encontraron errores al procesar:  
>  console-tools  
>  E: Sub-process /usr/bin/dpkg returned an error code (1)

Aparentemente no tiene soluciÃƒÂ³n, por queÃ‚Â ***apt-get -f install*** arroja el mismo error yÃ‚Â ***dpkg-reconfigure console-tools*** arroja que el paquete no estÃƒÂ¡ instalado o configurado correctamente (obvio :P).  
 Afortunadamente este BugÃ‚Â [ya estÃƒÂ¡ reportado](http://bugs.debian.org/cgi-bin/bugreport.cgi?bug=563727) desde el 4 de Enero y alguien a encontrado la soluciÃƒÂ³n que paso a detallar a continuaciÃƒÂ³n.

Como root hay que editar el archivo /etc/init.d/console-screen.sh

#nano /etc/init.d/console-screen.sh

Ahora nos vamos a la linea nÃ‚Âº 82 donde encontrarÃƒÂ¡n algo como esto:

> <div id="_mcePaste">if [ ! $CONSOLE_TYPE = “serial” ] Ã‚Â ; then</div><div id="_mcePaste" style="padding-left: 30px;"><span style="color: #ff0000;"> readlink /proc/self/fd/0 | grep -q -e /dev/vc -e ‘/dev/tty[^p]’ -e /dev/console</span></div><div id="_mcePaste" style="padding-left: 30px;"><span style="color: #ff0000;"> if [ $? -eq 0 ] ; then</span></div><div id="_mcePaste" style="padding-left: 60px;"><span style="color: #ff0000;"> VT=”yes”</span></div><div id="_mcePaste" style="padding-left: 60px;"><span style="color: #ff0000;"> reset_vga_palette</span></div><div id="_mcePaste" style="padding-left: 30px;"><span style="color: #ff0000;"> fi</span></div><div id="_mcePaste">fi</div>

Lo que estÃƒÂ¡ en rojo deben comentarlo (Recomendada) o eliminarlo y agregar lo siguiente:

> <span style="color: #008000;">if readlink Ã‚Â /proc/self/fd/0 | grep -q -e /dev/vc -e ‘/dev/tty[^p]’ -e /dev/console; then</span>
> 
> <span style="color: #008000;">VT=”yes”  
>  reset_vga_palette</span>
> 
> <span style="color: #008000;">fi</span>
> 
> <div>Osea, el trozo de cÃƒÂ³digo quedarÃƒÂ­a de la siguiente forma:</div>

<div>> <div>if [ ! $CONSOLE_TYPE = “serial” ] Ã‚Â ; then</div><div><div id="_mcePaste" style="padding-left: 30px;"><span style="color: #ff0000;"># Ã‚Â readlink /proc/self/fd/0 | grep -q -e /dev/vc -e ‘/dev/tty[^p]’ -e /dev/console</span></div><div id="_mcePaste" style="padding-left: 30px;"><span style="color: #ff0000;"># if [ $? -eq 0 ] ; then</span></div><div id="_mcePaste" style="padding-left: 30px;"><span style="color: #ff0000;"># Ã‚Â  Ã‚Â  Ã‚Â  Ã‚Â  Ã‚Â VT=”yes”</span></div><div id="_mcePaste" style="padding-left: 30px;"><span style="color: #ff0000;"># Ã‚Â  Ã‚Â  Ã‚Â  Ã‚Â  Ã‚Â reset_vga_palette</span></div><div id="_mcePaste" style="padding-left: 30px;"><span style="color: #ff0000;">#fi</span></div></div><div># A~NADIDO PARA EL BUG</div><div style="padding-left: 30px;"><span style="color: #008000;"> if readlink Ã‚Â /proc/self/fd/0 | grep -q -e /dev/vc -e ‘/dev/tty[^p]’ -e /dev/console; then</span></div><div style="padding-left: 60px;"><span style="color: #008000;"> VT=”yes”</span></div><div style="padding-left: 60px;"><span style="color: #008000;"> reset_vga_palette</span></div><div style="padding-left: 30px;"><span style="color: #008000;"> fi</span></div><div># FIN A~NADIDO</div><div>fi</div>

</div><div>Luego realizamos nuevamenteÃ‚Â ***apt-get -f install*** y listo, si todo saliÃƒÂ³ bien, terminarÃƒÂ¡ la configuraciÃƒÂ³n deÃ‚Â ***console-tools*** y ya tendremos corregido el Bug.</div><div>> <div>#apt-get -f install</div><div>Leyendo lista de paquetes… Hecho</div><div>Creando ÃƒÂ¡rbol de dependencias</div><div>Leyendo la informaciÃƒÂ³n de estado… Hecho</div><div>Se instalaron de forma automÃƒÂ¡tica los siguientes paquetes y ya no son necesarios.</div><div>…blablabla…</div><div>Utilice Ã‚Â«apt-get autoremoveÃ‚Â» para eliminarlos.</div><div>0 actualizados, 0 se instalarÃƒÂ¡n, 0 para eliminar y 31 no actualizados.</div><div>1 no instalados del todo o eliminados.</div><div>Se utilizarÃƒÂ¡n 0B de espacio de disco adicional despuÃƒÂ©s de esta operaciÃƒÂ³n.</div><div>Configurando console-tools (1:0.2.3dbs-67) …</div><div>Setting console screen modes and fonts.</div><div>Setting console screen modes and fonts.  
>  Done!</div>

</div><div>Y ya saben, si le sirviÃƒÂ³, comente.</div><div></div><div>***UPDATE [14/01/2010]: Acabo hacer un upgrade y el bug ya estÃƒÂ¡ corregido.***</div>
