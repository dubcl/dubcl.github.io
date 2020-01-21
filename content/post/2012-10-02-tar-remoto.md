---
layout: post
title: Tar Remoto
date: '2012-10-02 20:14:23'
---


Ahora vamos a ver como hacer el famoso “Tarzan Al Vuelo”, muy util para ahorrar algo de tiempo en nuestros que haceres sysadministicos

<div class="codecolorer-container bash default" style="overflow:auto;white-space:nowrap;width:435px;"><table cellpadding="0" cellspacing="0"><tbody><tr><td class="line-numbers"><div>1  
</div></td><td><div class="bash codecolorer"><span class="co4"># </span><span class="kw2">tar</span> zcvf - <span class="sy0">/</span>path-a-comprimir <span class="sy0">|</span><span class="kw2">ssh</span> user<span class="sy0">@</span>foo.bar.com <span class="st0">"cat > /reapaldo/path-comprimida.tar.gz"</span></div></td></tr></tbody></table></div>

Obviamente pueden cambiar el dominio con la dirección IP de destino

<div class="codecolorer-container bash default" style="overflow:auto;white-space:nowrap;width:435px;"><table cellpadding="0" cellspacing="0"><tbody><tr><td class="line-numbers"><div>1  
</div></td><td><div class="bash codecolorer"><span class="co4"># </span><span class="kw2">tar</span> zcvf - <span class="sy0">/</span>path-a-comprimir <span class="sy0">|</span><span class="kw2">ssh</span> user<span class="sy0">@</span>192.168.0.10 <span class="st0">"cat > /reapaldo/path-comprimida.tar.gz"</span></div></td></tr></tbody></table></div>

Esto tambien es aplicable para usar el comando dd

<div class="codecolorer-container bash default" style="overflow:auto;white-space:nowrap;width:435px;"><table cellpadding="0" cellspacing="0"><tbody><tr><td class="line-numbers"><div>1  
</div></td><td><div class="bash codecolorer"><span class="co4"># </span><span class="kw2">tar</span> cvzf - <span class="sy0">/</span>path-a-comprimir <span class="sy0">|</span><span class="kw2">ssh</span> user<span class="sy0">@</span>192.168.0.10 <span class="st0">"dd of= /reapaldo/path-comprimida.tar.gz"</span></div></td></tr></tbody></table></div>

O hacer algún respaldo directo a un dispositivo de cinta

<div class="codecolorer-container bash default" style="overflow:auto;white-space:nowrap;width:435px;"><table cellpadding="0" cellspacing="0"><tbody><tr><td class="line-numbers"><div>1  
</div></td><td><div class="bash codecolorer"><span class="co4"># </span><span class="kw2">tar</span> cvzf - <span class="sy0">/</span>path-a-comprimir <span class="sy0">|</span><span class="kw2">ssh</span> root<span class="sy0">@</span>192.168.0.10 <span class="st0">"cat > /dev/nst0"</span></div></td></tr></tbody></table></div>

Saludines


