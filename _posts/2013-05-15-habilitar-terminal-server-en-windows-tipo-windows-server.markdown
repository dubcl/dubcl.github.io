---
layout: post
title: Habilitar Terminal Server en Windows tipo Windows Server
date: '2013-05-15 18:04:39'
---


Tengo algunas máquinas con Windows XP y necesito conectarme vía remota a ellas, el problema es que al no ser servidores no levantan el servicio de Terminal Server automáticamente, asta que el usuario se logee localmente y no permiten mas de 1 conexión simultanea, para solventar este problema le traemos una papita para activar el Servicio de Terminal Server como lo hacen en Windows Server.

Primero nos bajamos un parche para el servicio, el [Universal Termsrv Patch](http://www.mediafire.com/?vp13kl6luizebq1), luego lo descomprimen y ejecutan **UniversalTermsrvPatch-x86.exe** y le dan al boton “**Patch**“.

Luego abren el cuadro de dialogo “**Ejecutar**” y ejecutan “**gpedit.msc**“, se abren paso por el siguiente menú:

**Configuracion del equipo -> Plantillas Administrativas -> Componentes de Windows -> Terminal Services -> Limitar numero de conexiones**

Abren la opción “Limitar numero de conexiones”, la habilitan y seleccionan el numero de conexiones simultaneas que quieren.

Ahora se van a:

**Panel de Control -> Herramientas Administrativas -> Servicios**

Y buscan “**Servicio de Terminal Server**“, le dan click derecho y luego en **propiedades**, en “**Tipo de inicio**” seleccionan “**Automático**” y aceptan el cambio.

Luego de todo esto reinician la maquina y ya tienen su “Servicio de Terminal Server” funcionando como lo hace en servidores Windows.

Este método lo probé en Windows XP, en teoría debería funcionar en Windows 7 también.

 


