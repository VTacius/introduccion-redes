---
layout: doc
category: doc
title: Introducción a Redes de Área Local
orden: 1
---
Red de Area Local se refiere a todas las computadoras que tiene a su cargo, siempre y cuando estén conectadas por medio de un switch y con una configuración de red adecuada. Cada término en esta frase va a ser explicada en el resto de todo este manual, así que tengalo en mente para que se de cuenta lo simple que puede ser.

{% include concepto.html contenido="LAN es la abreviatura de ***Local Network Address***, y aunque es una abreviatura en inglés, es la forma más frecuente en que nos vamos a referir a su Red de Área Local" %}

Una LAN ni siquiera tiene porque tener acceso a Internet para ser funcional, ni siquiera debe tener acceso a los servidores en La Central. Sin embargo, el acceso a estos últimos es la razón por la que han conectado todos sus equipos en red. Tiene que aprender a ver su LAN como una unidad independiente del toda la red institucional. Eso significa, entre otras cosas, que muchos de sus problemas podrían tener un origen local.

### Conexiones Fisicas y Conexiones Lógicas
La conexión LAN ocurre a dos niveles: uno físico y otro lógico. Entender esta separación es útil para comprender mejor como debe solucionar los problemas en su LAN.

#### Conexiones Físicas: Cables de red y switch
La conexión física de su LAN se basa en conectar su computadora a un switch mediante un cable de red. En realidad, la conexión podría presentar varios puntos de conexión (Un conector en la pared, un rack, otro switch) y todos ellos podrían causar problemas en la conexión. Para ser sinceros, en condiciones normales es el cable UTP que va de su computadora al punto de red en la pared lo que puede causar problemas, debido a que esta más disponible a jalones, golpes y otro tipo de daño.

Para verificar como el sistema reconoce el estado actual del enlace, use el comando `ip link`, cuya salida debe ser parecida a la siguiente:

```bash
ip link
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN mode DEFAULT group default 
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP mode DEFAULT group default qlen 1000
    link/ether 00:16:3e:4c:10:61 brd ff:ff:ff:ff:ff:ff
```

Los puntos importantes acá son `state UP`. Significa que se considera que el link esta arriba y funcional

#### Conexiones Lógicas: Entendiendo que es una IP
Haga un esfuerzo por dominar todos los conceptos de este apartado. Si algo sigue sin quedarle claro, busque ayuda hasta que comprenda y domine todo lo que va a continuación. Tome en cuenta que todo lo que sigue es un poco de teoría, necesaria para que más adelante pueda usarla para configurar un equipo y que así sea parte de su LAN

Una ***Dirección IP***  consiste en cuatro número a los que llamamos octetos, unidos mediante tres puntos entre ellos. A continuación, un ejemplo de `IP` bastante común en nuestras redes.

![Dirección IP]({{site.baseurl}}/contenido/01 - Direccion IP.png)

Por costumbre y comodidas, solemos referirnos a la ***dirección IP*** simplemente como **IP** 

Una IP por si misma no basta para configurar la red en un equipo. Una configuración de red completa requiere al menos de una **Máscara de Red** y **Puerta de Enlace**

#### Máscara de Red ####

La `mascara de red` puede expresarse de dos formas. Por un lado, la `máscara de red`, al igual que la `dirección IP`, esta compuesta por cuatro octetos separados por un punto. **Esta es la forma en que la máscara de red suele ser configurada en los archivos u otras partes**. En este caso, lo común es que los primeros tres octetos sean `255` y el último sea cero. No es común que la máscara tenga otra forma en nuestras redes.

![Máscara de Red]({{site.baseurl}}/contenido/02 - Mascara de Red.png)

Por otra parte, es común encontrar la máscara de red acompañando a la dirección IP de la siguiente forma.

![Dirección IP]({{site.baseurl}}/contenido/03 - IP completa.png)

En este caso, la máscara es el número que sigue después de la barra inclinada. Se lee ***pleca 24***, y es la forma más usual con la que alguien le podría hablar de una IP.

#### Puerta de enlace (Gateway) ####
{% include concepto.html contenido="***Gateway*** es una forma bastante común para referirse a la **Puerta de enlace** " %}
El gateway de la configuración es común a todos los equipos. Es una IP que identifica a un firewall o dispositivo que el proveedor le ha dado. Lo más común es que sea la primera IP disponible, al menos, la segunda. No es común que sea una IP al azar.

Por ejemplo, las siguientes dos IP son gateway válidos y comunes para nuestra configuración de red.

![Gateway]({{site.baseurl}}/contenido/04 - Gateway.png)

Es decir, si alguién le dice que la IP es **192.168.2.5/24**, la IP es **192.168.2.5** y su máscara de red es **255.255.255.0**

Para conocer la configuración de red de un equipos (Que como ya vimos, consta al menos de una dirección IP, de una máscara de red y de un gateway), debe usar el comando `ip addr`. El resultado en consola debería ser igual al siguiente:

```bash
ip addr show
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default 
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever3
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000
    link/ether 00:16:3e:4c:10:61 brd ff:ff:ff:ff:ff:ff
    inet 192.168.2.5/27 brd 192.168.2.31 scope global eth0
       valid_lft forever preferred_lft forever
    inet6 fe80::216:3eff:fe4c:1061/64 scope link 
       valid_lft forever preferred_lft forever
```

Según el comando anterior, la interfaz eth0 esta arriba (Según lo que dice `state UP`) y su ip es `192.168.2.5/27` (Según lo que dice `inet 192.168.2.5/27`)
