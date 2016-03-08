---
layout: post
title: Instalar Subversion + Trac en Debian Wheezy
date: '2013-01-09 11:38:10'
---


La vamos a hacer cortita… Abstenerse de comentarios del tipo “GIT es mejor”, “Hubieras instalado GIT”, “SVN está deprecado” etc, etc…

Un personaje pidió tener un servidor SVN, así que se le instaló y estos son los pasos a seguir.

En resumen vamos a instalar Apache 2 + DAV + SubVersion + Trac sobre un servidor Debian Wheezy y vamos a asumir que los archivos de SVN y Trac los vamos a dejar en **/mnt/storage**

1.- Instalamos los paquetes necesarios

<div class="codecolorer-container bash default" style="overflow:auto;white-space:nowrap;width:435px;"><table cellpadding="0" cellspacing="0"><tbody><tr><td class="line-numbers"><div>1  
</div></td><td><div class="bash codecolorer"><span class="kw2">apt-get install</span> python-setuptools trac subversion libapache2-svn libapache2-mod-python</div></td></tr></tbody></table></div>2.- Activamos el modulo de apache dav_fs

<div class="codecolorer-container bash default" style="overflow:auto;white-space:nowrap;width:435px;"><table cellpadding="0" cellspacing="0"><tbody><tr><td class="line-numbers"><div>1  
</div></td><td><div class="bash codecolorer">a2enmod dav_fs</div></td></tr></tbody></table></div>Esto activará también los módulos dav y dav_svn por que son dependencias.

3.- Creamos un directorio con la estructura que llevarán nuestros repositorios por defecto.

<div class="codecolorer-container bash default" style="overflow:auto;white-space:nowrap;width:435px;"><table cellpadding="0" cellspacing="0"><tbody><tr><td class="line-numbers"><div>1  
2  
3  
</div></td><td><div class="bash codecolorer"><span class="kw2">mkdir</span><span class="re5">-p</span><span class="sy0">/</span>mnt<span class="sy0">/</span>storage<span class="sy0">/</span>plantilla_repo<span class="sy0">/</span>branches  
<span class="kw2">mkdir</span><span class="re5">-p</span><span class="sy0">/</span>mnt<span class="sy0">/</span>storage<span class="sy0">/</span>plantilla_repo<span class="sy0">/</span>tags  
<span class="kw2">mkdir</span><span class="re5">-p</span><span class="sy0">/</span>mnt<span class="sy0">/</span>storage<span class="sy0">/</span>plantilla_repo<span class="sy0">/</span>trunk</div></td></tr></tbody></table></div>4.- Creamos el archivo que contendrá los usuarios y contraseñas para acceder tanto al repositorio SVN como a la web de Trac.

<div class="codecolorer-container bash default" style="overflow:auto;white-space:nowrap;width:435px;"><table cellpadding="0" cellspacing="0"><tbody><tr><td class="line-numbers"><div>1  
2  
</div></td><td><div class="bash codecolorer">htpasswd <span class="re5">-c</span><span class="sy0">/</span>etc<span class="sy0">/</span>apache2<span class="sy0">/</span>svn.passwd usuariofoo  
 htpasswd <span class="sy0">/</span>etc<span class="sy0">/</span>apache2<span class="sy0">/</span>svn.passwd usuariobar</div></td></tr></tbody></table></div>OJO, primero es con “-c” para crear el archivo y luego SIN “-c” para agregar otro usuario, si usan “-c” nuevamente el archivo se sobrescribirá.

5.- Ahora creamos o editamos el archivo de configuración del sitio web en apache, en este caso editaremos el default site.

<div class="codecolorer-container bash default" style="overflow:auto;white-space:nowrap;width:435px;"><table cellpadding="0" cellspacing="0"><tbody><tr><td class="line-numbers"><div>1  
</div></td><td><div class="bash codecolorer"><span class="kw2">nano</span><span class="sy0">/</span>etc<span class="sy0">/</span>apache2<span class="sy0">/</span>sites-enabled<span class="sy0">/</span>000-default</div></td></tr></tbody></table></div>Y agregamos:

<div class="codecolorer-container text default" style="overflow:auto;white-space:nowrap;width:435px;"><table cellpadding="0" cellspacing="0"><tbody><tr><td class="line-numbers"><div>1  
2  
3  
4  
5  
6  
7  
8  
9  
10  
11  
12  
13  
14  
15  
16  
17  
18  
19  
20  
</div></td><td><div class="text codecolorer"><Location  /svn>  
     DAV svn  
     SVNParentPath /mnt/storage/svn  
     SVNAutoversioning on  
     AuthType Basic  
     AuthName "Subversion Repository"  
     AuthUserFile /etc/apache2/svn.passwd  
     Require valid-user  
 </Location /svn>  
  
 <Location /trac>  
     SetHandler mod_python  
     PythonHandler trac.web.modpython_frontend  
     PythonOption TracEnvParentDir /mnt/storage/trac/  
     PythonOption TracUriRoot /trac  
     AuthType Basic  
     AuthName "Trac"  
     AuthUserFile /etc/apache2/svn.passwd  
     Require valid-user  
 </Location /trac></div></td></tr></tbody></table></div>6.- Creamod el directorio para los proyectos en Trac

<div class="codecolorer-container bash default" style="overflow:auto;white-space:nowrap;width:435px;"><table cellpadding="0" cellspacing="0"><tbody><tr><td class="line-numbers"><div>1  
</div></td><td><div class="bash codecolorer"><span class="kw2">mkdir</span><span class="sy0">/</span>mnt<span class="sy0">/</span>storage<span class="sy0">/</span>trac</div></td></tr></tbody></table></div>Ahora creamos nuestro primer proyecto

7.- Creamos el repocitorio SVN e importamos el directorio que tiene la plantilla con la estructura por defecto.

<div class="codecolorer-container bash default" style="overflow:auto;white-space:nowrap;width:435px;"><table cellpadding="0" cellspacing="0"><tbody><tr><td class="line-numbers"><div>1  
2  
3  
4  
5  
</div></td><td><div class="bash codecolorer"><span class="kw2">svnadmin</span> create <span class="sy0">/</span>mnt<span class="sy0">/</span>storage<span class="sy0">/</span>svn<span class="sy0">/</span>myproject <span class="re5">--fs-type</span> fsfs  
<span class="kw2">svn</span> import<span class="sy0">/</span>mnt<span class="sy0">/</span>storage<span class="sy0">/</span>plantilla_repo file:<span class="sy0">///</span>mnt<span class="sy0">/</span>storage<span class="sy0">/</span>svn<span class="sy0">/</span>Proyecto1 <span class="re5">-m</span><span class="st0">"Importacion inicial"</span>  
<span class="kw2">find</span> <span class="sy0">/</span>mnt<span class="sy0">/</span>storage<span class="sy0">/</span>svn<span class="sy0">/</span>Proyecto1 <span class="re5">-type</span> f <span class="sy0">|</span><span class="kw2">xargs</span><span class="kw2">chmod</span><span class="nu0">600</span>  
<span class="kw2">find</span> <span class="sy0">/</span>mnt<span class="sy0">/</span>storage<span class="sy0">/</span>svn<span class="sy0">/</span>Proyecto1 <span class="re5">-type</span> d <span class="sy0">|</span><span class="kw2">xargs</span><span class="kw2">chmod</span><span class="nu0">2770</span>  
<span class="kw2">chown</span><span class="re5">-Rf</span> root.www-data <span class="sy0">/</span>mnt<span class="sy0">/</span>storage<span class="sy0">/</span>svn<span class="sy0">/</span>Proyecto1</div></td></tr></tbody></table></div>8.- Creamos el proyecto en Trac

<div class="codecolorer-container bash default" style="overflow:auto;white-space:nowrap;width:435px;"><table cellpadding="0" cellspacing="0"><tbody><tr><td class="line-numbers"><div>1  
2  
3  
4  
</div></td><td><div class="bash codecolorer">trac-admin <span class="sy0">/</span>mnt<span class="sy0">/</span>storage<span class="sy0">/</span>trac<span class="sy0">/</span>Proyecto1 initenv  
<span class="kw2">find</span> <span class="sy0">/</span>mnt<span class="sy0">/</span>storage<span class="sy0">/</span>trac<span class="sy0">/</span>Proyecto1 <span class="re5">-type</span> f <span class="sy0">|</span><span class="kw2">xargs</span><span class="kw2">chmod</span><span class="nu0">600</span>  
<span class="kw2">find</span> <span class="sy0">/</span>mnt<span class="sy0">/</span>storage<span class="sy0">/</span>trac<span class="sy0">/</span>Proyecto1 <span class="re5">-type</span> d <span class="sy0">|</span><span class="kw2">xargs</span><span class="kw2">chmod</span><span class="nu0">2770</span>  
<span class="kw2">chown</span><span class="re5">-Rf</span> root.www-data <span class="sy0">/</span>mnt<span class="sy0">/</span>storage<span class="sy0">/</span>trac<span class="sy0">/</span>Proyecto1</div></td></tr></tbody></table></div>9.- Reiniciamos apache

<div class="codecolorer-container bash default" style="overflow:auto;white-space:nowrap;width:435px;"><table cellpadding="0" cellspacing="0"><tbody><tr><td class="line-numbers"><div>1  
</div></td><td><div class="bash codecolorer">service apache2 restart</div></td></tr></tbody></table></div>4. Agregamos un usuario con permisos de administrador al proyecto en Trac, este debe estar en el archivo svn.passwd que creamos anteriormente

<div class="codecolorer-container bash default" style="overflow:auto;white-space:nowrap;width:435px;"><table cellpadding="0" cellspacing="0"><tbody><tr><td class="line-numbers"><div>1  
</div></td><td><div class="bash codecolorer">trac-admin <span class="sy0">/</span>mnt<span class="sy0">/</span>storage<span class="sy0">/</span>trac<span class="sy0">/</span>Proyecto1</div></td></tr></tbody></table></div>Esto abrirá una shell donde se pueden ejecutar los comando para Trac, ejecutamos lo siguiente para asignar al administrador.

<div class="codecolorer-container bash default" style="overflow:auto;white-space:nowrap;width:435px;"><table cellpadding="0" cellspacing="0"><tbody><tr><td class="line-numbers"><div>1  
</div></td><td><div class="bash codecolorer">Trac <span class="br0">[</span><span class="sy0">/</span>mnt<span class="sy0">/</span>storage<span class="sy0">/</span>trac<span class="sy0">/</span>Proyecto1<span class="br0">]</span><span class="sy0">></span> permission add usuariofoo TRAC_ADMIN</div></td></tr></tbody></table></div>Con esto estaríamos listos y ya pueden acceder al proyecto en Trac en la url, por ejemplo, **http://dominio.com/trac/Proyecto1** y para el SVN **http://dominio.com/svn/Proyecto1**, logeandose con los usuarios que agregamos en el svn.passwd


