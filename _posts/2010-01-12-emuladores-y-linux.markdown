---
layout: post
title: Emuladores y Linux
date: '2010-01-12 03:13:55'
---


Estando en casa de mis padres, aburrido por cierto, he estado en busca de alguna entretenciÃƒÂ³n para matar el tiempo y me he acordado de algunos juegos de antaÃƒÂ±o, de los que, o nosÃ‚Â juntÃƒÂ¡bamosÃ‚Â todos los amigos en casa de alguno que tenia una consola, o nosÃ‚Â ÃƒÂ­bamos a gastar algunas monedas a los arcades, asÃƒÂ­ que me puse a buscar emuladores para las distintas plataformas que tanta entretenciÃƒÂ³n nos proporcionaban por aquellos aÃƒÂ±os.

**XMame + GXMame (GMameUI)**

[![](http://carlos.debianchile.cl/wp-content/uploads/2010/01/xmame01-300x199.png "xmame01")](http://carlos.debianchile.cl/wp-content/uploads/2010/01/xmame01.png)

xmame.x11

El clÃƒÂ¡sico de los emuladores arcade, como olvidar esas partidas de TMNT de cuatro player, Street Fighter, Mortal Kombat, Los Simpsons, el “Monito de Nieve” (Snow Bross), Tumblepop y tantos otros, con este emulador los puedes disfrutar desde la comodidad de tu PC. En Debian Sid la versiÃƒÂ³n existente es la 0.106, lo pueden instalar con

> #apt-get install xmame

Su versiÃƒÂ³n natural es para se usada en consola pero existen algunos Front-End’s, como el [GXMame](http://gxmame.sourceforge.net) y el nuevo [GMameUI](http://gmameui.sourceforge.net), basado en el anterior, pero no funciona tan bien como GXMame, aunque este es mucho mas viejo, cave mencionar que GXMame hay que instalarlo a mano, ya que como verÃƒÂ¡n en su sitio web, la ultima versiÃƒÂ³n es del 2003.

> #apt-get install gmameui

GXMame y GMameUI cuentan con una interfaz de selecciÃƒÂ³n de ROM y opciones de configuraciÃƒÂ³n similares a las del Mame32 o MameUI de windows, asÃƒÂ­ que no tiene como perderse.

[![](http://carlos.debianchile.cl/wp-content/uploads/2010/01/gxmame01-300x201.png "gxmame01")](http://carlos.debianchile.cl/wp-content/uploads/2010/01/gxmame01.png)GXMame

[![](http://carlos.debianchile.cl/wp-content/uploads/2010/01/main_window.png "gmameui")](http://carlos.debianchile.cl/wp-content/uploads/2010/01/main_window.png)GMameUI

**ZSNES**

Emulador por excelencia de Super Nintendo, Super Famicom para los demÃƒÂ¡s. Emula el 99.9% de las ROM’s de SNES, aunque tambiÃƒÂ©n existe snes9x, ZSNES destaca por ser igual tanto en la versiÃƒÂ³n de windows como en la de Linux, no asÃƒÂ­ snes9x. Super Mario World, Mortal Kombat II, Killer Instinct, Zombies – Ate My Neighbors, Chorno Cross, Super Mario Kart, por nombrar algunos, harÃƒÂ¡n las delicias de ese gamepad que tienen lleno de polvo en el armario.

> #apt-get install zsnes

[![](http://carlos.debianchile.cl/wp-content/uploads/2010/01/zsnes01.png "zsnes01")](http://carlos.debianchile.cl/wp-content/uploads/2010/01/zsnes01.png)zsnes – selecciÃƒÂ³n de ROM

[![](http://carlos.debianchile.cl/wp-content/uploads/2010/01/zsnes02-300x235.png "zsnes02")](http://carlos.debianchile.cl/wp-content/uploads/2010/01/zsnes02.png)zsnes, emulando Super Mario Kart

**Mupen64Plus**

Ya pueden ir imaginando los que significa el 64, si, asÃƒÂ­ es, este es el emulador de Nintendo 64, la que nos permitiÃƒÂ³ ver a Mario en 3D, todavia recuerdo cuando pasaba frente a la tienda donde en la vitrina tenÃƒÂ­an una de estas con el Mario 64, y ahÃƒÂ­ quedaba, mirando un buen rato como se movÃƒÂ­a esa gran cabezota de Mario delante de ese fondo azul. Cabe mencionar, que al igual que ZSNES, Mupen64Plus es idÃƒÂ©ntico al de windows.

> #apt-get install mupen64plus

[![](http://carlos.debianchile.cl/wp-content/uploads/2010/01/mupen01-300x209.png "mupen01")](http://carlos.debianchile.cl/wp-content/uploads/2010/01/mupen01.png) Mupen64Plus

[![](http://carlos.debianchile.cl/wp-content/uploads/2010/01/mupen02-300x236.png "mupen02")](http://carlos.debianchile.cl/wp-content/uploads/2010/01/mupen02.png)Mupen64Plus, ejecutando Mario Kart 64

**FCEU, Nestra**

Ambos emuladores de Nintendo, si, el del mÃƒÂ­tico Mario Bross + Duck Hunt, Kirby Adventure, Zelda, etc… los dos son excelentes emuladores, lo lamentable es que solo son usables desde la consola. TambiÃƒÂ©n existe [FCEUX](http://fceux.com), el cual si trae una interfaz GTK, pero al parecer (lo digo asÃƒÂ­, por que no lo he usado) no tienen todas las caracterÃƒÂ­sticas de FCEU.

> #apt-get install fceu

[![](http://carlos.debianchile.cl/wp-content/uploads/2010/01/fecu01.png "fecu01")](http://carlos.debianchile.cl/wp-content/uploads/2010/01/fecu01.png)FCEU

> #apt-get install nestra

[![](http://carlos.debianchile.cl/wp-content/uploads/2010/01/nestra011.png "nestra")](http://carlos.debianchile.cl/wp-content/uploads/2010/01/nestra011.png)  
 Nestra

**pSX**

Este es EL emulador definitivo de PlayStation para Linux, aunque algunos digan que el EPCSX es el mejor, pues yo les digo NO!, la verdad no le tenÃƒÂ­a ninguna fe a este emulador, pero al probarlo me a dejado sin palabras, hace lo que tiene que hacer y nada mas, es liviano, funciona tanto con el teclado como con gamepad, soporta Memory Card’s, corre juegos en CD e imÃƒÂ¡genes ISO, pueden descargar el binario desde [aquÃƒÂ­](http://psxemulator.gazaxian.com) tanto para windows como para Linux. Como TIPs mencionar que no viene con los archivos de las MemCards, la soluciÃƒÂ³n, ir al directorio en donde quieren guardar los archivos MemCards, generalmente /ruta/a/pSX/mem/, y crear 2 archivos vacios, luego ejecutar pSX, que al ejecutarse corre la BIOS de PSX (que por cierto deben descargarla a parte), e ir al menu de la Memory Card, esto hara que detecte los archivos y formatee estos como si fueran de verdad.

[![](http://carlos.debianchile.cl/wp-content/uploads/2010/01/psx01-300x248.png "psx01")](http://carlos.debianchile.cl/wp-content/uploads/2010/01/psx01.png)pSX, PlayStation BIOS

[![](http://carlos.debianchile.cl/wp-content/uploads/2010/01/psx02-300x248.png "psx02")](http://carlos.debianchile.cl/wp-content/uploads/2010/01/psx02.png)pSX, corriendo Bust a Move en ISO

Bueno amigos (si es que alguien lee este blog 😛 ), estos son **algunos** de los emuladores disponibles para Linux, asÃƒÂ­ que no tienen escusa para relajarse un rato disfrutando de esos juegos de antaÃƒÂ±o que tantas horas y horas de entretenciÃƒÂ³n nos proporcionaban.

Y recuerde… si le gustÃƒÂ³ o leÃ‚Â sirviÃƒÂ³, comente :D.


