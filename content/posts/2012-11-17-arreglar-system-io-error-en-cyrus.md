---
layout: post
title: Arreglar "System I/O error" en Cyrus.
date: '2012-11-17 18:07:15'
---


Si en el log del correo encuentran esto:

<div class="codecolorer-container bash default" style="overflow:auto;white-space:nowrap;width:435px;"><table cellpadding="0" cellspacing="0"><tbody><tr><td class="line-numbers"><div>1  
</div></td><td><div class="bash codecolorer">said: <span class="nu0">451</span> 4.3.0 System I<span class="sy0">/</span>O error <span class="br0">(</span><span class="kw1">in</span> reply to RCPT TO <span class="kw3">command</span><span class="br0">)</span><span class="br0">)</span></div></td></tr></tbody></table></div>

Esto pasa cuando borrar los correos haciendo rm dentro del directorio /var/spool/cyrus/mail/foo/mail/bar, para arreglarlo debes logearte como  el usuario cyrus

<div class="codecolorer-container bash default" style="overflow:auto;white-space:nowrap;width:435px;"><table cellpadding="0" cellspacing="0"><tbody><tr><td class="line-numbers"><div>1  
</div></td><td><div class="bash codecolorer"><span class="kw2">su</span> - cyrus</div></td></tr></tbody></table></div>

Luego ejecutar el comando *reconstruct* de cyrus.

<div class="codecolorer-container bash default" style="overflow:auto;white-space:nowrap;width:435px;"><table cellpadding="0" cellspacing="0"><tbody><tr><td class="line-numbers"><div>1  
</div></td><td><div class="bash codecolorer"><span class="co4">cyrus@server:~$ </span><span class="sy0">/</span>usr<span class="sy0">/</span>lib<span class="sy0">/</span>cyrus<span class="sy0">/</span>bin<span class="sy0">/</span>reconstruct <span class="re5">-r</span><span class="re5">-f</span> user.foobar</div></td></tr></tbody></table></div>

La salida del comando seria mas o menos así:

<div class="codecolorer-container bash default" style="overflow:auto;white-space:nowrap;width:435px;"><table cellpadding="0" cellspacing="0"><tbody><tr><td class="line-numbers"><div>1  
2  
3  
4  
5  
6  
</div></td><td><div class="bash codecolorer">user.foobar  
 user.foobar.Drafts  
 user.foobar.Sent  
 user.foobar.Custom  
 user.foobar.OtherCustom  
 user.foobar.Trash</div></td></tr></tbody></table></div>

Y luego

<div class="codecolorer-container bash default" style="overflow:auto;white-space:nowrap;width:435px;"><table cellpadding="0" cellspacing="0"><tbody><tr><td class="line-numbers"><div>1  
</div></td><td><div class="bash codecolorer"><span class="co4">cyrus@server:~$</span> <span class="sy0">/</span>usr<span class="sy0">/</span>lib<span class="sy0">/</span>cyrus<span class="sy0">/</span>bin<span class="sy0">/</span>quota <span class="re5">-f</span></div></td></tr></tbody></table></div>

Con esto reconstruimos las estructuras que tenga el usuario, en su cuenta de correo.


