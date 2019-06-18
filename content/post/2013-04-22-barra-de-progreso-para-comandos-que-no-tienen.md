---
layout: post
title: Barra de progreso para comandos que no tienen
date: '2013-04-22 15:52:27'
---


Ésta es una papita para cuando usamos comandos que no nos entrega información de tranferencia.

La mágia la hace el comando [bar](http://clpbar.sourceforge.net/), por ejemplo, su uso sería:

<div class="codecolorer-container bash default" style="overflow:auto;white-space:nowrap;width:435px;"><table cellpadding="0" cellspacing="0"><tbody><tr><td class="line-numbers"><div>1  
</div></td><td><div class="bash codecolorer"><span class="kw2">dd</span><span class="re2">if</span>=<span class="sy0">/</span>path<span class="sy0">/</span>foo.img <span class="sy0">|</span> bar <span class="re5">-s</span> 99G <span class="sy0">|</span><span class="kw2">dd</span><span class="re2">of</span>=<span class="sy0">/</span>path<span class="sy0">/</span>bar.img</div></td></tr></tbody></table></div>Donde -s 99G es el tamaño del archivo a transferir.

Esto también funciona al tranferir al vuelo, por ejemplo:

<div class="codecolorer-container bash default" style="overflow:auto;white-space:nowrap;width:435px;"><table cellpadding="0" cellspacing="0"><tbody><tr><td class="line-numbers"><div>1  
</div></td><td><div class="bash codecolorer"><span class="kw2">dd</span><span class="re2">if</span>=<span class="sy0">/</span>path<span class="sy0">/</span>foo.img <span class="sy0">|</span> bar <span class="re5">-s</span> 99G <span class="sy0">|</span><span class="kw2">ssh</span> root<span class="sy0">@</span>192.168.0.1 <span class="st0">"dd of=/path/bar.img"</span></div></td></tr></tbody></table></div>bar nos entregaría información como ésta:

<div class="codecolorer-container bash default" style="overflow:auto;white-space:nowrap;width:435px;"><table cellpadding="0" cellspacing="0"><tbody><tr><td class="line-numbers"><div>1  
</div></td><td><div class="bash codecolorer">13.0GB    at    11.0MB<span class="sy0">/</span>s    eta: <span class="nu0">2</span>:<span class="nu0">15</span>:<span class="nu0">18</span>    <span class="nu0">12</span><span class="sy0">%</span><span class="br0">[</span>=         <span class="br0">]</span></div></td></tr></tbody></table></div>
