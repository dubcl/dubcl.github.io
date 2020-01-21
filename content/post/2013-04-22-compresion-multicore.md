---
layout: post
title: Compresión Multicore
date: '2013-04-22 16:31:21'
---


Para que tener un procesador con varios cores si no los usas? Pues puedes usarlos comprimiendo tus directorios favoritos, la papita es [pigz](http://zlib.net/pigz/), veamos como funciona.

<span style="font-size: 13px; line-height: 19px;"></span>

<div class="codecolorer-container bash default" style="overflow:auto;white-space:nowrap;width:435px;"><table cellpadding="0" cellspacing="0"><tbody><tr><td class="line-numbers"><div>1  
</div></td><td><div class="bash codecolorer"><span class="kw2">tar</span> cvf - foo<span class="sy0">/</span><span class="sy0">|</span> pigz <span class="re5">-9</span><span class="re5">-p</span><span class="nu0">6</span><span class="sy0">></span><span class="sy0">/</span>path<span class="sy0">/</span>bar.tar.gz</div></td></tr></tbody></table></div>Donde foo/ es el directorio a comprimir -9 es el nivel de compresión (0-9) -p es la cantidad de cores a usar

Obviamente esto se puede usar al vuelo 😉

<div class="codecolorer-container bash default" style="overflow:auto;white-space:nowrap;width:435px;"><table cellpadding="0" cellspacing="0"><tbody><tr><td class="line-numbers"><div>1  
</div></td><td><div class="bash codecolorer"><span class="kw2">tar</span> cvf - foo<span class="sy0">/</span><span class="sy0">|</span> pigz <span class="re5">-9</span><span class="re5">-p</span><span class="nu0">6</span><span class="sy0">|</span><span class="kw2">ssh</span> usuario<span class="sy0">@</span>192.168.0.1 <span class="st0">"cat > /backup/path/bar.tar.gz"</span></div></td></tr></tbody></table></div>
