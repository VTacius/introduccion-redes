---
layout: doc
category: doc
title: Introducción al Firewall
orden: 4
---
El firewall es un dispositivo de red que se encarga de administrar el acceso que los equipos bajo su tutela administrativa tienen hacia otros equipos.

Nos referimos a él como dispositivo porque los firewall pueden configurarse en distintos tipos de hardware. Nosotros usamos un servidor, pero la misma configuración podría aplicarse a una computadora de escritorio y funcionaría como tal. Por eso, para abreviar, la forma correcta de referirse a él es como firewall. En general, cualquier otro nombre causará confusión en una conversación para nosotros.

Los aspectos de la red que el firewall administra varían de acuerdo al firewall en específico: Nuestros firewall se encarga de lo siguiente:
* Permisos de red
* Permisos de navegación web
* Rutas 

Los equipos bajo su tutela administrativa conforman las redes LAN y DMZ que se encuentran en su establecimiento. La idea más básica para nuestros firewall es que cada uno se corresponda con un establecimiento. 

## Sobre los permisos
La idea más básica que debe comprender sobre nuestros firewall es que esté es restrictivo por defecto. Sin permisos, el firewall negaría cualquier comunicación de los equipos de su red hacia otras redes. Los permisos son todas aquellas reglas que permiten (Lo contrario, negar, es la opción por defecto) a los equipos usar la red tal como se espera que la usen.
En su primera configuración, nuestros firewall se han configurado con unas cuentas reglas que específican tráfico válido que consideramos estándar para las redes. 
