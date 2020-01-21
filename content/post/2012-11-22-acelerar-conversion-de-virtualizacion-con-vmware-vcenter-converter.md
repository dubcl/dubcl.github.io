---
layout: post
title: Acelerar conversión de virtualización con VMWare VCenter Converter
date: '2012-11-22 09:23:11'
---


Los que trabajamos con virtualización, es común realizar conversiones de máquinas físicas a máquinas virtuales, en el caso de hoy, de Xen Citrix a ESXi 5.x.

Para realizar esta tarea se utiliza VMWare VCenter Converter, pero cuando lo usas te das cuenta que en algunos casos anda como río de [ulpo](http://es.wikipedia.org/wiki/Ulpo).

Ayer mientras hacia una conversión me topé con una interesante truco para mejorar notablemente la taza de transferencia, para ello tenemos que:

Ubicar el fichero **converter-worker.xml**, comúnmente se encuentra en

C:Documents and SettingsAll UsersDatos de programaVMwareVMware vCenter Converter Standalone

instalado en un Windows XP (En Windows 7 ni idea donde queda, no tengo win7 XD)

Luego buscamos el atributo

<useSsl>true</useSsl>

En la línea 303 aproximadamente y cambiamos **true** por **false**

Eso es todo, con esto las conversiones se realizará aproximadamente un 50% mas rápidas 😉


