---
layout: post
title: Actualización tzdata, tzdata-java para Debian 7 (Wheezy)
date: '2019-04-02 12:27:31'
tags: [tzdata-java, tzdata, debian wheezy, update, actualizacion]
---

Debido a que Debian 7 Wheezy ya no recibe actualizaciones de seguridad, es necesario actualizar a mano los paquetes tzdata y tztada-java
correspondientes al cambio de hora 2019 en Chile.

Para validar si es necesaria la actualización ejecutar

```bash
$ zdump -v America/Santiago | grep 2019
```
Debe arrojar información que no corresponde al cambio de hora 2019, por ejemplo:

```bash
America/Santiago Sun May 12 02:59:59 2019 UTC = Sat May 11 23:59:59 2019-03 isdst=1 gmtoff=-
America/Santiago Sun May 12 03:00:00 2019 UTC = Sat May 11 23:00:00 2019-04 isdst=0 gmtoff=-
America/Santiago Sun Aug 11 03:59:59 2019 UTC = Sat Aug 10 23:59:59 2019-04 isdst=0 gmtoff=-
America/Santiago Sun Aug 11 04:00:00 2019 UTC = Sun Aug 11 01:00:00 2019-03 isdst=1 gmtoff=-
```

## Instrucciones de actualización

Los últimos paquetes tzdata y tztada-java correspondientes a la versión estable de Debian 10 (Buster) ya no son compatibles con versiones
antiguas del OS provocando el siguiente error al intentar instalar.

```bash
$ dpkg -i tzdata_2019a-1_all.deb
dpkg-deb: error: archive 'tzdata_2019a-1_all.deb' contains not
understood data member control.tar.xz, giving up
dpkg: error processing tzdata_2019a-1_all.deb (--install):
subprocess dpkg-deb --control returned error exit status 2
Errors were encountered while processing:
tzdata_2019a-1_all.deb
```
Los paquetes necesarios y compatibles correspondientes a las actualizaciones de seguridad de Debian 8 (Jessie) son los siguientes:

[http://security-cdn.debian.org/debian-security/pool/updates/main/t/tzdata/tzdata-java_2019a-0+deb8u1_all.deb](http://security-cdn.debian.org/debian-security/pool/updates/main/t/tzdata/tzdata-java_2019a-0+deb8u1_all.deb)
[http://security-cdn.debian.org/debian-security/pool/updates/main/t/tzdata/tzdata_2019a-0+deb8u1_all.deb](http://security-cdn.debian.org/debian-security/pool/updates/main/t/tzdata/tzdata_2019a-0+deb8u1_all.deb)

### Instalación
Para instalar realizar los siguientes pasos:

#### Descargar paquetes:

```bash
$ wget -q http://security-cdn.debian.org/debian-security/pool/updates/main/t/tzdata/tzdata-java_2019a-0+deb8u1_all.deb -O /tmp/tzdata-java_2019a-0+deb8u1_all.deb
$ wget -q http://security-cdn.debian.org/debian-security/pool/updates/main/t/tzdata/tzdata_2019a-0+deb8u1_all.deb -O /tmp/tzdata_2019a-0+deb8u1_all.deb
```
#### Instalar los paquetes:

```bash
$ dpkg -i /tmp/tzdata_2019a-0+deb8u1_all.deb
(Reading database ... 93341 files and directories currently installed.)
Preparing to replace tzdata 2018e-0+deb7u1 (using
tzdata_2019a-0+deb8u1_all.deb) ...
Unpacking replacement tzdata ...
Setting up tzdata (2019a-0+deb8u1) ...

$ dpkg -i /tmp/tzdata-java_2019a-0+deb8u1_all.deb
(Reading database ... 93345 files and directories currently installed.)
Preparing to replace tzdata-java 2018e-0+deb7u1 (using
tzdata-java_2019a-0+deb8u1_all.deb) ...
Unpacking replacement tzdata-java ...
Setting up tzdata-java (2019a-0+deb8u1) ...
```
#### Reconfigurar tzdata:

```bash
$ dpkg-reconfigure tzdata
```
#### Seleccionar en las opciones:

America -> Santiago

La salida de la configuración realizada es la siguiente por ejemplo:

```bash
Current default time zone: 'America/Santiago'
Local time is now: Tue Apr 2 11:39:38 -03 2019.
Universal Time is now: Tue Apr 2 14:39:38 UTC 2019.
```
#### Para validar la correcta configuración, nuevamente ejecutamos zdump:

```bash
$ zdump -v America/Santiago | grep 2019
America/Santiago Sun Apr 7 02:59:59 2019 UTC = Sat Apr 6 23:59:2019 -03 isdst=1 gmtoff=-
America/Santiago Sun Apr 7 03:00:00 2019 UTC = Sat Apr 6 23:00:2019 -04 isdst=0 gmtoff=-
America/Santiago Sun Sep 8 03:59:59 2019 UTC = Sat Sep 7 23:59:2019 -04 isdst=0 gmtoff=-
America/Santiago Sun Sep 8 04:00:00 2019 UTC = Sun Sep 8 01:00:2019 -03 isdst=1 gmtoff=-
```

Por último, reiniciar los servicios que correspondan.

## Enlaces Relacionados

[https://packages.debian.org/jessie/all/tzdata-java/download](https://packages.debian.org/jessie/all/tzdata-java/download)
[https://packages.debian.org/jessie/all/tzdata/download](https://packages.debian.org/jessie/all/tzdata/download)
[http://security-cdn.debian.org/debian-security/pool/updates/main/t/tzdata/](http://security-cdn.debian.org/debian-security/pool/updates/main/t/tzdata/)
[http://www.horaoficial.cl/aviso/informacion.html](http://www.horaoficial.cl/aviso/informacion.html)
[https://www.leychile.cl/Navegar?idNorma=1125760](https://www.leychile.cl/Navegar?idNorma=1125760)
