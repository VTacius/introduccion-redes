---
layout: doc
category: doc
title: "Configuración de Red en GNU/Linux: El caso de Debian"
orden: 4
---

Ahora que ya esta familiarizado con los términos más básicos, es hora de ver como los va a usar para realizar una `configuración de red`. 

{% include concepto.html contenido="***Configuración de red*** suele referirse al conjunto `dirección IP`, `máscara de red` y  `gateway` que estando configurados en un equipo permiten que este sea parte de su LAN. Un equipo sin configuración de red no es parte de su LAN, aún cuando este físicamente conectado." %}

Para configurar la red en Debian, es necesario configurar (Es decir, escribiendo en un formato especial) los valores correspondientes a la configuración de red de un equipo en el fichero `/etc/network/interfaces`

No basta con aprenderse de memoria este fichero (Algo que es lo deseable, después de todo, es una de las cosas más importante a realizar en su trabajo). Debe comprenderlo bien. Debe entender que hace cada cosa. A larga, debería ser capaz de reconocer posibles errores en este fichero de un solo vistazo.

Esta es la configuración mínima y funcional para este fichero. Lo que hace es configurar la interfaz `eth0` con la IP `192.168.2.5/24`. Note como `/24` se convierte en `255.255.255.0` en la siguiente configuración.
Note también que se ha configurado una interfaz `lo` que apunta hacia el loopback

```bash
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
 address 192.168.2.5
 netmask 255.255.255.0
 gateway 192.168.2.1

```

{% include concepto.html contenido="***interfaz*** es la forma con que se denomina a nivel de sistema operativo al puerto, ethernet en este caso, donde conecta el cable UTP. Es decir, el puerto de red se refiere a la parte física, mientras que interfaz se refiere al nombre que tiene dentro del sistema Debian" %}

{% include concepto.html contenido="***loopback*** es la forma en que nos referimos a una interfaz especial del sistema cuya IP suele ser la `127.0.0.1/8`. Importante a tomar en cuenta es que no suele tener una utilidad evidente en equipos de escritorio, pero no debería eliminarla de los archivos donde la vea. No se preocupe por ella, ignorela" %}

Las opciones del fichero tienen se explican de la siguiente forma: 
 
address
: Dirección IP asignada al equipo

netmask
: Mascára de red. Lo más común es que sea 255.255.255.0

gateway
: Es el gateway, o puerta de enlace 

Después de eso, es común que se le pida configurar `broadcast` e incluso `network`. Estos son aditamentos innecesarios cuando no se necesita cambiarlos de sus valores por defecto, pero es válido

```bash
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
 address 192.168.2.5
 gateway 192.168.2.1
 netmask 255.255.255.0
 network 192.168.2.0
 broadcast 192.168.2.255

```

A continuación, tiene la forma por defecto que el fichero de configuración tiene actualmente en Debian Jessie. Note como lo único que se ha agregado son los comentarios, que empiezan por `#`

```bash
# This file describes the network interfaces available on your system
# and how to activate them. For more information, see interfaces(5).

# The loopback network interface
auto lo
iface lo inet loopback

# The primary network interface
auto eth0
iface eth0 inet static
 address 192.168.2.5
 gateway 192.168.2.1
 netmask 255.255.255.0
 network 192.168.2.0
 broadcast 192.168.2.255

 # post-up  ethtool -K eth0 tx off

#
# The commented out line above will disable TCP checksumming which
# might resolve problems for some users.  It is disabled by default
#

```

### La interfaz de red ###
La interfaz de red suele llamarse `eth0` hasta Debian Jessie. Desde Debian Stretch  en adelante, el nombre será diferente. La más probable es que se llame `enp1s0`, pero la convención que usa el sistema para asignar el nombre se basa en el hardware, así que tendrá que enterarse de su nombre, la forma más sencilla es hacer uso del comando `ip addr show`  

```bash
ip addr show
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default 
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: enp1s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000
    link/ether 00:16:3e:4c:10:61 brd ff:ff:ff:ff:ff:ff
    inet 10.20.20.5/27 brd 192.168.2.31 scope global enp1s0
       valid_lft forever preferred_lft forever
    inet6 fe80::216:3eff:fe4c:1061/64 scope link 
       valid_lft forever preferred_lft forever
```

El fichero de configuración quedará de la siguiente forma:

```bash
# This file describes the network interfaces available on your system
# and how to activate them. For more information, see interfaces(5).

# The loopback network interface
auto lo
iface lo inet loopback

# The primary network interface
auto enp1s0
iface enp1s0 inet static
 address 192.168.2.5
 gateway 192.168.2.1
 netmask 255.255.255.0
 network 192.168.2.0
 broadcast 192.168.2.255

 # post-up  ethtool -K eth0 tx off

#
# The commented out line above will disable TCP checksumming which
# might resolve problems for some users.  It is disabled by default
#

```

Una vez configurada la interfaz de red en el fichero `/etc/network/interfaces`, es necesario aplicar la configuración. La opción más fácil es reiniciar el equipo. Sin embargo, es posible que no quiera perder el tiempo reiniciando cada equipo que configure. La forma más sencilla es entonces reiniciar el servicio de red con `systemctl restart networking.service`

```bash
systemctl restart networking.service
```
