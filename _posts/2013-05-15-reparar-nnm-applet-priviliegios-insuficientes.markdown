---
layout: post
title: Reparar nm-applet Priviliegios Insuficientes
date: '2013-05-15 12:36:48'
---


En una máquina recién instalada, me topo con que al editar la configuración de red con nm-applet sale un mensaje “privilegios Insuficientes”.  
 Vale mencionar que no uso gnome, solo instalé nm-applet, por ende no tengo gnome-keyring ni gtksu, etc…

Para resolver el problema debemos hacer lo siguiente

Editar

<div class="codecolorer-container bash default" style="overflow:auto;white-space:nowrap;width:435px;"><table cellpadding="0" cellspacing="0"><tbody><tr><td class="line-numbers"><div>1  
</div></td><td><div class="bash codecolorer"><span class="kw2">nano</span><span class="sy0">/</span>etc<span class="sy0">/</span>polkit-<span class="nu0">1</span><span class="sy0">/</span>localauthority<span class="sy0">/</span><span class="nu0">50</span>-local.d<span class="sy0">/</span>org.freedesktop.NetworkManager.pkla</div></td></tr></tbody></table></div>Si no existe, crearlo y agregar lo siguiente

<div class="codecolorer-container bash default" style="overflow:auto;white-space:nowrap;width:435px;"><table cellpadding="0" cellspacing="0"><tbody><tr><td class="line-numbers"><div>1  
2  
3  
4  
5  
6  
</div></td><td><div class="bash codecolorer"><span class="br0">[</span>nm-applet<span class="br0">]</span>  
<span class="re2">Identity</span>=unix-group:netdev  
<span class="re2">Action</span>=org.freedesktop.NetworkManager.<span class="sy0">*</span>  
<span class="re2">ResultAny</span>=<span class="kw2">yes</span>  
<span class="re2">ResultInactive</span>=no  
<span class="re2">ResultActive</span>=<span class="kw2">yes</span></div></td></tr></tbody></table></div>luego agregar el o los usuarios al grupo netdev

<div class="codecolorer-container bash default" style="overflow:auto;white-space:nowrap;width:435px;"><table cellpadding="0" cellspacing="0"><tbody><tr><td class="line-numbers"><div>1  
</div></td><td><div class="bash codecolorer">adduser usuario netdev</div></td></tr></tbody></table></div>Y listo, ya podemos hacer uso de nm-applet sin problemas.


