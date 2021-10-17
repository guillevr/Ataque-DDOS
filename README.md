# Ataque-DDOS
**¿Qué es un ataque DoS?**

DoS (Denial of Service) conocido como ataque de denegacion de servicios, es un ataque a un sistema de computadoras o red que causa que un servicio o recurso sea inaccesible para los usuarios. Normalmente provoca la perdida de la conectividad con la red por el consumo del ancho de banda de la red de la victima o sobrecarga de los recursos de los que dispone el sistema atacado.

Los ataques DoS se generan mediante la saturación de los puertos con múltiples flujos de información, haciendo que el servidor se sobrecargue y no pueda seguir prestando su servicio. Por eso se le denomina denegación, pues hace que el servidor no pueda atender la cantidad enorme de solicitudes.

Esta técnica es usada por los crackers o piratas informáticos para dejar fuera de servicio servidores objetivo.

Una ampliación del ataque DoS es el llamado ataque de denegación de servicio distribuido, también llamado **DDoS (Distributed Denial of Service)** el cual se lleva a cabo generando un gran flujo de información desde varios puntos de conexión hacia un mismo punto de destino.
La forma más común de realizar un DDoS es a través de una red de bots, siendo esta técnica el ciberataque más usual y eficaz por su sencillez tecnológica.

En ocasiones, esta herramienta ha sido utilizada como un buen método para comprobar la capacidad de tráfico que un ordenador puede soportar sin volverse inestable y afectar los servicios que presta. Un administrador de redes puede así conocer la capacidad real de cada máquina.

**Métodos de ataque**
* Consumo de recursos computacionales, tales como ancho de banda, espacio de disco, o tiempo de procesador.
* Alteración de información de configuración, tales como información de rutas de encaminamiento.
* Alteración de información de estado, tales como interrupción de sesiones TCP (TCP reset).
* Interrupción de componentes físicos de red.
* Obstrucción de medios de comunicación entre usuarios de un servicio y la víctima, de manera que ya no puedan comunicarse adecuadamente.

**Requisitos**

Para realizar dicho ataque necesitaremos al menos dos máquinas con Ubuntu. Una de ellas tendrá un servidor web (apache) y la segunda maquina, será el cliente que utilizaremos para atacar al servidor.

Los requisitos básicos/mínimos para poder instalar ubuntu son:
* Procesador de doble nucleo de 2 GHz o superior.
* 4 GB de RAM.
* 25 GB de espacio libre en el disco duro.

## Realizar un ataque DDOS

Como he comentado anteriormente, para realizar dicho ataque necesitaremos dos maquinas ubuntu (en mi caso son maquinas virtuales conectadas entre si a traves de una red interna), una de ella será nuestro servidor web y la otra será el cliente con el que intentaremos tumbar el servidor.

Para realizar el ataque, deberemos tener en el cliente instalado Hping3.

**¿Que es Hping3?**

Hping3 es una aplicación de terminal para Linux que nos va a permitir analizar y ensamblar fácilmente paquetes TCP/IP. A diferencia de un Ping convencional que se utiliza para enviar paquetes ICMP, esta aplicación permite el envío de paquetes TCP, UDP y RAW-IP. Junto al análisis de los paquetes, esta aplicación puede ser utilizada también con otros fines de seguridad, por ejemplo, para probar la eficacia de un firewall a través de diferentes protocolos, la detección de paquetes sospechosos o modificados, e incluso la protección frente a ataques DoS de un sistema o de un Firewall.

En el pasado, esta herramienta se utiliza para temas de ciberseguridad, pero también podemos usarla para probar redes y hosts. Algunas de las principales aplicaciones que podemos hacer con esta herramienta son las siguientes:

* Comprobar la seguridad y el funcionamiento de los firewalls.
* Usarla como un escaneo avanzado de puertos, aunque es mejor usar Nmap para esta tarea.
* Pruebas de red usando diferentes protocolos, ToS, fragmentación etc.
* Descubrir el MTU en la ruta de forma manual.
* Traceroute avanzado usando todos los protocolos admitidos
* Huella digital remota del sistema operativo
* Comprobar el tiempo de distancia
* Auditoría de pilas TCP/IP

## Configuración del equipo SERVIDOR

Lo primero que debemos de hacer es comprobar que el equipo está actualizado.
>guillevr@servidor:~$ sudo apt-get update

>[sudo] contraseña para guillevr:

>Obj:1 http://es.archive.ubuntu.com/ubuntu hirsute InRelease

>Obj:2 http://es.archive.ubuntu.com/ubuntu hirsute-updates InRelease

>Obj:3 http://es.archive.ubuntu.com/ubuntu hirsute-backports InRelease

>Obj:4 http://security.ubuntu.com/ubuntu hirsute-security InRelease

>Leyendo lista de paquetes... Hecho

>guillevr@servidor:~$

>guillevr@servidor:~$ sudo apt-get upgrade

>Leyendo lista de paquetes... Hecho

>Creando árbol de dependencias... Hecho

>Leyendo la información de estado... Hecho

>Calculando la actualización... Hecho

>Los siguientes paquetes se han retenido:

>  linux-generic-hwe-20.04 linux-headers-generic-hwe-20.04

>  linux-image-generic-hwe-20.04

>0 actualizados, 0 nuevos se instalarán, 0 para eliminar y 3 no actualizados.

>guillevr@servidor:~$

Como observamos, el equipo está actualizado. El siguiente paso será instalar apache2.

> guillevr@servidor:~$ sudo apt-get install apache2
>
> [sudo] contraseña para guillevr:
>
> Leyendo lista de paquetes... Hecho
>
> Creando árbol de dependencias... Hecho
>
> Leyendo la información de estado... Hecho
>
> Se instalarán los siguientes paquetes adicionales:
>
>   apache2-bin apache2-data apache2-utils libapr1 libaprutil1
>
>   libaprutil1-dbd-sqlite3 libaprutil1-ldap
>
> Paquetes sugeridos:
>
>   apache2-doc apache2-suexec-pristine | apache2-suexec-custom
>
> Se instalarán los siguientes paquetes NUEVOS:
>
>   apache2 apache2-bin apache2-data apache2-utils libapr1 libaprutil1
>
>   libaprutil1-dbd-sqlite3 libaprutil1-ldap
>
> 0 actualizados, 8 nuevos se instalarán, 0 para eliminar y 3 no actualizados.
>
> Se necesita descargar 1.741 kB de archivos.
>
> Se utilizarán 7.550 kB de espacio de disco adicional después de esta operación.
>
> ¿Desea continuar? [S/n] s

Una vez haya terminado la instalacion, comprobamos el estado de apache y a traves del navegador, comprobamos que el sitio web funciona perfectamente.
>guillevr@servidor:~$ service apache2 status
>
>● apache2.service - The Apache HTTP Server
>
>Loaded: loaded (/lib/systemd/system/apache2.service; enabled; vendor prese>
>Active: active (running) since Sun 2021-10-17 22:35:57 CEST; 20min ago
>Docs: https://httpd.apache.org/docs/2.4/
>Main PID: 3551 (apache2)
>Tasks: 55 (limit: 5478)
>Memory: 5.2M
>CGroup: /system.slice/apache2.service
>        ├─3551 /usr/sbin/apache2 -k start
>        ├─3553 /usr/sbin/apache2 -k start
>        └─3554 /usr/sbin/apache2 -k start
>
>oct 17 22:35:57 servidor systemd[1]: Starting The Apache HTTP Server...
>
>oct 17 22:35:57 servidor apachectl[3550]: AH00558: apache2: Could not reliably >
>
>oct 17 22:35:57 servidor systemd[1]: Started The Apache HTTP Server.
>
>guillevr@servidor:~$



##FALTA AÑADIR LA FOTO.


Ahora editaremos la pagina un poco para darle un toque personal.
>guillevr@servidor:~$ sudo gedit /var/www/html/index.html
>
>
>
>(gedit:4710): GtkSourceView-CRITICAL **: 22:50:31.266: El resaltado de una linea llevó mucho tiempo, se desactivará el resaltado de sintaxis
>
>guillevr@servidor:~$
>
>guillevr@servidor:~$ cat /var/www/html/index.html
>
>
>
><!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
>
><html xmlns="http://www.w3.org/1999/xhtml">
>
><body>
>
><h2 align="center">Pagina para el proyecto de seguridad.</h2>
>
></body>
>
></html>
>
>guillevr@servidor:~$
>
