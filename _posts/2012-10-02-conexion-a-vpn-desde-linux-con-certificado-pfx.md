---
layout: post
title: Conexión a VPN desde Linux con certificado PFX
date: '2012-10-02 20:07:10'
---


Bueh!… hace tiempo que no postéo nada, así que nos vamos con algo de utilidad…

Primero instalamos OpenVPN

<div class="codecolorer-container bash default" style="overflow:auto;white-space:nowrap;width:435px;"><table cellpadding="0" cellspacing="0"><tbody><tr><td class="line-numbers"><div>1  
</div></td><td><div class="bash codecolorer"><span class="co4"># </span><span class="kw2">apt-get install</span> openvpn</div></td></tr></tbody></table></div>Luego tenemos que convertir el certificado simple .pfx en p12 con openssl para ello hacemos lo siguiente:

<div class="codecolorer-container bash default" style="overflow:auto;white-space:nowrap;width:435px;"><table cellpadding="0" cellspacing="0"><tbody><tr><td class="line-numbers"><div>1  
2  
3  
</div></td><td><div class="bash codecolorer">$ openssl pkcs12 <span class="re5">-in</span> cert-original.pfx <span class="re5">-nocerts</span><span class="re5">-out</span> privatekey.pem  
 $ openssl pkcs12 <span class="re5">-in</span> cert-original.pfx <span class="re5">-clcerts</span><span class="re5">-nokeys</span><span class="re5">-out</span> publiccert.pem  
 $ openssl pkcs12 <span class="re5">-export</span><span class="re5">-in</span> publiccert.pem <span class="re5">-inkey</span> privatekey.pem <span class="re5">-out</span> cert.p12</div></td></tr></tbody></table></div>Ahora que tenemos listo nuestro certificado creamos archivo de configuración para openvpn.

<div class="codecolorer-container bash default" style="overflow:auto;white-space:nowrap;width:435px;"><table cellpadding="0" cellspacing="0"><tbody><tr><td class="line-numbers"><div>1  
</div></td><td><div class="bash codecolorer"><span class="co4">$ </span><span class="kw2">nano</span> foo-bar.ovpn</div></td></tr></tbody></table></div><div class="codecolorer-container ini default" style="overflow:auto;white-space:nowrap;width:435px;"><table cellpadding="0" cellspacing="0"><tbody><tr><td class="line-numbers"><div>1  
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
</div></td><td><div class="ini codecolorer">client  
 dev tun  
 proto udp  
 remote vpn.foo-bar.com <span class="nu0">1194</span>  
 resolv-retry infinite  
 nobind  
 persist-key  
 persist-tun  
 ca /ruta/de/la/ca/ca.crt  
 pkcs12 /ruta/del/certificado/cert.p12  
 comp-lzo  
 verb <span class="nu0">3</span></div></td></tr></tbody></table></div>Y por último para conectarse , ejecutar como root lo siguente:

<div class="codecolorer-container bash default" style="overflow:auto;white-space:nowrap;width:435px;"><table cellpadding="0" cellspacing="0"><tbody><tr><td class="line-numbers"><div>1  
</div></td><td><div class="bash codecolorer"><span class="co4"># </span>openvpn config_acepta.ovpn</div></td></tr></tbody></table></div>Pueden ejecutar el comando anterior dentro de una consola virtual con screen por si cierran por error la ventana de la consola.

Eso es todo 😉


