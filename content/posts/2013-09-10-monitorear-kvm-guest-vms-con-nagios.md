---
layout: post
title: Monitorear KVM Guest VMs con Nagios
date: '2013-09-10 17:01:15'
---


Super fácil, copiamos el siguiente script

 #!/bin/bash # check_virt - Check that a virtual machine is running. # Written by Richard W.M. Jones <rjones@redhat.com> # # Derived from check_xenvm (see below for copyright of check_xenvm) #---------------------------------------------------------------------- # COPYRIGHT : (c) 2006 SUSE Linux GmbH. All rights reserved. # # AUTHOR : Axel Schmidt # # BELONGS TO : NLPOS/SLEPOS/Xen Nagios Integration # # DESCRIPTION : Runs "xm list" and returns the available xen vms # # $Revision: 1.1 $ # # Permission to use, copy, modify, distribute, and sell this software # and its documentation for any purpose is hereby granted without fee, # provided that the above copyright notice appear in all copies and that # both that copyright notice and this permission notice appear in # supporting documentation. # # The above copyright notice and this permission notice shall be # included in all copies or substantial portions of the Software. # # THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, # EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF # MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. # IN NO EVENT SHALL THE AUTHOR OR SUSE BE LIABLE FOR ANY CLAIM, DAMAGES # OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR # OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR # THE USE OR OTHER DEALINGS IN THE SOFTWARE. #---------------------------------------------------------------------- HOSTNAME=$1 if [ -z $HOSTNAME ]; then echo "Usage: $0 hostname" exit 3 ;# Status 3 = UNKNOWN (orange) fi if [ -f /usr/bin/sudo ]; then STATE="$(sudo /usr/bin/virsh domstate $HOSTNAME | head -1)" else STATE="$(/usr/bin/virsh domstate $HOSTNAME | head -1)" fi case "$STATE" in running) echo "$HOSTNAME Running - status 0" exit 0 ;# Status 0 = OK (green) ;; blocked) echo "$HOSTNAME Bloqued - status 0" exit 0 ;# Status 0 = OK (green) ;; paused) echo "$HOSTNAME Paused - status 1" exit 1 ;# Status 1 = WARNING (yellow) ;; shutdown) echo "$HOSTNAME Shutdown - status 2" exit 2 ;# Status 2 = CRITICAL (red) ;; shut\ off) echo "$HOSTNAME ShutOff - status 2" exit 2 ;# Status 2 = CRITICAL (red) ;; crashed) echo "$HOSTNAME Creashed - status 2" exit 2 ;# Status 2 = CRITICAL (red) ;; *) echo "$HOSTNAME Critical - status 3" exit 3 ;# Status 2 = CRITICAL (red) esac

Sinseramente no recuerdo de donde lo saqué, le hice un par de modificaciones.

También hay que agregar a la configuración de sudo lo siguiente al final del archivo en el KVM Host:

 nagios ALL=(root) NOPASSWD:/usr/bin/virsh

Luego agregar a su nrpe.cfg, por ejemplo:

 command[check_vm01]=/ruta/hacia/check_virt vm01

Y ya lo pueden probar desde su servidor nagios:

 nagios-server$ /usr/lib/nagios/plugins/check_nrpe -H 99.99.99.99 -c check_vm01 cge-almacen1 Running - status 0


