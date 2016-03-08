---
layout: post
title: Eliminar archivos anterior a una fecha
date: '2013-01-16 16:04:25'
---


Cortito, necesitamos eliminar los ficheros de un directorio anterior a una fecha determinada.

<div class="codecolorer-container text default" style="overflow:auto;white-space:nowrap;width:435px;"><table cellpadding="0" cellspacing="0"><tbody><tr><td class="line-numbers"><div>1  
</div></td><td><div class="text codecolorer">find . -type f ! -newer foo.bar -delete</div></td></tr></tbody></table></div>Esto saca el timestamp del archivo foo.bar, y borra todo lo que tenga fecha anterior a este, incluido el archivo foo.bar.

Si nececitamos crear un archivo con una fecha determinada usamos

<div class="codecolorer-container text default" style="overflow:auto;white-space:nowrap;width:435px;"><table cellpadding="0" cellspacing="0"><tbody><tr><td class="line-numbers"><div>1  
</div></td><td><div class="text codecolorer">touch -t fechahora timestamp.foo</div></td></tr></tbody></table></div>Donde fechahora es en formato YYYYMMDDHHSS, esto crea un fichero con el timestamp determinado, para luego usarlo en el comando anterior.


