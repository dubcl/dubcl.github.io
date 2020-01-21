---
layout: post
title: Unión de sistemas de archivos en linux
date: '2012-10-02 20:22:55'
---


Hay veces que es necesario ir incrementando el espacio de un directorio a medida que se necesita, una forma es sencillamente añadir otro disco mas grande al original y copiar la data al nuevo destino, pero esto es muy engorroso y requiere de mucho tiempo.

Otra forma es usar [unionfs](http://es.wikipedia.org/wiki/UnionFS) o [aufs](http://en.wikipedia.org/wiki/Aufs), pero está más que obsoleto, además de que no es lo suficientemente inteligente para darse cuenta cuando un disco está lleno y comenzar el gusrdado de data en el siguiente disco.

Para solver esta problematica esta mdhhfs, cumple la misma función que union fs, pero este si se da cuenta cuando un disco se llena y automaticamente sigue en el disco siguiente, su forma de uso es:

Montaje en consola

<div class="codecolorer-container bash default" style="overflow:auto;white-space:nowrap;width:435px;"><table cellpadding="0" cellspacing="0"><tbody><tr><td class="line-numbers"><div>1  
</div></td><td><div class="bash codecolorer"><span class="co4"># </span>mhddfs <span class="sy0">/</span>mnt<span class="sy0">/</span>hdd1,<span class="sy0">/</span>mnt<span class="sy0">/</span>hdd2,<span class="sy0">/</span>mnt<span class="sy0">/</span>hdd3 <span class="sy0">/</span>mnt<span class="sy0">/</span>virtual <span class="re5">-o</span> allow_other</div></td></tr></tbody></table></div>

Montaje en fstab

<div class="codecolorer-container bash default" style="overflow:auto;white-space:nowrap;width:435px;"><table cellpadding="0" cellspacing="0"><tbody><tr><td class="line-numbers"><div>1  
</div></td><td><div class="bash codecolorer"><span class="co4">mhddfs#</span><span class="sy0">/</span>mnt<span class="sy0">/</span>hdd1,<span class="sy0">/</span>mnt<span class="sy0">/</span>hdd2,<span class="sy0">/</span>mnt<span class="sy0">/</span>hdd3 <span class="sy0">/</span>mnt<span class="sy0">/</span>virtual fuse defaults,allow_other <span class="nu0">0</span><span class="nu0">0</span></div></td></tr></tbody></table></div>

El parámetro (-o) allow_other permite que otros usuarios puedan acceder al directorio final.

Link’s

[http://romanrm.ru/en/mhddfs](http://romanrm.ru/en/mhddfs)


