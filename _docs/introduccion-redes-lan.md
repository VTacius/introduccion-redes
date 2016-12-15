---
layout: doc
category: doc
title: Introducción a Redes de Área Local
orden: 2
---
Su Red de Area Local no es más que todas las computadoras que tiene a su cargo, siempre y cuando estén conectadas por medio de un switch.

{% include concepto.html contenido="LAN es la abreviatura de ***Local Network Address***, y aunque es una abreviatura en inglés, es la forma más frecuente en que nos vamos a referir a su Red de Área Local" %}

Una LAN ni siquiera tiene porque tener acceso a Internet para ser funcional, ni siquiera debe tener acceso a los servidores en La Central. Sin embargo, el acceso a estos últimos es la razón por la que han conectado todos sus equipos en red. Tiene que aprender a ver su LAN como una unidad independiente del toda la red institucional. Eso significa, entre otras cosas, que muchos de sus problemas podrían tener un origen local.

### Conexiones Fisicas y Conexiones Lógicas
La conexión LAN ocurre a dos niveles: uno físico y otro lógico. Entender esta separación es útil para comprender mejor como debe solucionar los problemas en su LAN.

#### Conexiones Físicas: Cables de red y switch
La conexión física de su LAN se basa en conectar su computadora a un switch mediante un cable de red. En realidad, la conexión podría presentar varios puntos de conexión (Un conector en la pared, un rack, otro switch) y todos ellos podrían causar problemas en la conexión. Para ser sinceros, en condiciones normales es el cable UTP que va de su computadora al punto de red en la pared lo que puede causar problemas, debido a que esta más disponible a jalones, golpes y otro tipo de daño.

#### Conexiones Lógicas: Entendiendo que es una IP
Este tema *debe* dominarlo. El concepto de IP no debe tener mayores misterio para usted. 

Para ser un poco precisos, la forma correcta es ***Dirección IP***, pero la costumbre y comodidad nos hace referirnos a ella como ***IP***. Dirección IP señala la utilidad que tiene, y es la de identificar a su equipo dentro de su red. De allí la necesidad de asegurarse de que cada una sea única.

Una IP consiste en cuatro número a los que llamamos octetos, unidos mediante tres puntos entre ellos.

![Dirección IP](/contenido/01 - Direccion IP.png)

Una IP por si misma no basta para configurar la red. Una configuración de red completa requiere al menos de una **Máscara de Red** y **Puerta de Enlace**

#### Máscara de Red ####

Debe considerar la mascara de red de dos formas. Por un lado, la máscara de red, al igual que la dirección IP, esta compuesta por cuatro octetos separados por un punto. **Esta es la forma en que la máscara de red suele ser configurada en los archivos u otras partes**

![Máscara de Red](/contenido/02 - Mascara de Red.png)

Por otra parte, es común encontrar la máscara de red acompañando a la dirección IP de la siguiente forma. Esta forma es común cuando se suele hablar de ella. Se lee ***pleca 24***

![Dirección IP](/contenido/03 - IP completa.png)

#### Puerta de enlace (Gateway) ####
{% include concepto.html contenido="***Gateway*** es una forma bastante común para referirse a la **Puerta de enlace** " %}
El gateway de la configuración es común a todos los equipos. Es una IP que identifica a un firewall o dispositivo que el proveedor le ha dado. Lo más común es que sea la primera IP disponible, al menos, la segunda. No es común que sea una IP al azar.

Por ejemplo, las siguientes dos IP son gateway válidos y comunes para nuestra configuración de red.

![Gateway](/contenido/04 - Gateway.png)

Es decir, si alguién le dice que la IP es **192.168.2.5/24**, la IP es **192.168.2.5** y su máscara de red es **255.255.255.0**
Diagrama subjetivo de como funciona la red.
