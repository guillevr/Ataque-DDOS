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

Para realizar dicho ataque necesitaremos al menos tres máquinas con Ubuntu 21.04 (puedes elegir la versión que quieras). La primera máquina tendrá un servidor web (apache), la segunda, será el cliente que utilizaremos para intentar conectar el servidor y la tercera maquina, será la que utilizaremos para atacar el servidor.

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
* Huella digital remota ºdel sistema operativo
* Comprobar el tiempo de distancia
* Auditoría de pilas TCP/IP

## Comprobamos la IP del equipo CLIENTE y SERVIDOR y realizamos pruebas de conectividad entre ellos.
IP equipo CLIENTE:

>guillevr@cliente:~$ ifconfig
>
>enp0s3: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
>
>        inet 10.0.2.4  netmask 255.255.255.0  broadcast 10.0.2.255
>
>        inet6 fe80::5202:97b9:3faf:ecce  prefixlen 64  scopeid 0x20<link>
>
>        ether 08:00:27:60:93:c3  txqueuelen 1000  (Ethernet)
>
>        RX packets 18034  bytes 21898656 (21.8 MB)
>
>        RX errors 0  dropped 0  overruns 0  frame 0
>
>        TX packets 12939  bytes 2304910 (2.3 MB)
>
>        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
>
>
>
>lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
>
>        inet 127.0.0.1  netmask 255.0.0.0
>
>        inet6 ::1  prefixlen 128  scopeid 0x10<host>
>
>        loop  txqueuelen 1000  (Bucle local)
>
>        RX packets 879  bytes 98837 (98.8 KB)
>
>        RX errors 0  dropped 0  overruns 0  frame 0
>
>        TX packets 879  bytes 98837 (98.8 KB)
>
>        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0


IP equipo SERVIDOR:

>guillevr@servidor:~$ ifconfig
>
>enp0s3: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
>
>        inet 10.0.2.5  netmask 255.255.255.0  broadcast 10.0.2.255
>
>        inet6 fe80::5202:97b9:3faf:ecce  prefixlen 64  scopeid 0x20<link>
>
>        ether 08:00:27:60:93:c3  txqueuelen 1000  (Ethernet)
>
>        RX packets 18034  bytes 21898656 (21.8 MB)
>
>        RX errors 0  dropped 0  overruns 0  frame 0
>
>        TX packets 12939  bytes 2304910 (2.3 MB)
>
>        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
>
>
>
>lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
>
>        inet 127.0.0.1  netmask 255.0.0.0
>
>        inet6 ::1  prefixlen 128  scopeid 0x10<host>
>
>        loop  txqueuelen 1000  (Bucle local)
>
>        RX packets 879  bytes 98837 (98.8 KB)
>
>        RX errors 0  dropped 0  overruns 0  frame 0
>
>        TX packets 879  bytes 98837 (98.8 KB)
>
>        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

Realizamos prueba de conexion desde el ATACANTE hacia el SERVIDOR y el CLIENTE con un ping.
> guillevr@atacante:~$ ping 10.0.2.4
>
> PING 10.0.2.4 (10.0.2.4) 56(84) bytes of data.
>
> 64 bytes from 10.0.2.4: icmp_seq=1 ttl=64 time=1.87 ms
>
> 64 bytes from 10.0.2.4: icmp_seq=2 ttl=64 time=0.774 ms
>
> 64 bytes from 10.0.2.4: icmp_seq=3 ttl=64 time=0.628 ms
>
> 64 bytes from 10.0.2.4: icmp_seq=4 ttl=64 time=0.621 ms
>
> ^C
>
> --- 10.0.2.4 ping statistics ---
>
> 4 packets transmitted, 4 received, 0% packet loss, time 3024ms
>
> rtt min/avg/max/mdev = 0.621/0.972/1.868/0.520 ms
>
> guillevr@atacante:~$
>
> guillevr@atacante:~$ ping 10.0.2.5
>
> PING 10.0.2.5 (10.0.2.5) 56(84) bytes of data.
>
> 64 bytes from 10.0.2.5: icmp_seq=1 ttl=64 time=1.08 ms
>
> 64 bytes from 10.0.2.5: icmp_seq=2 ttl=64 time=0.753 ms
>
> 64 bytes from 10.0.2.5: icmp_seq=3 ttl=64 time=0.681 ms
>
> 64 bytes from 10.0.2.5: icmp_seq=4 ttl=64 time=0.976 ms
>
> ^C
>
> --- 10.0.2.5 ping statistics ---
>
> 4 packets transmitted, 4 received, 0% packet loss, time 3033ms
>
> rtt min/avg/max/mdev = 0.681/0.872/1.081/0.162 ms
>
> guillevr@atacante:~$


## Configuración del equipo SERVIDOR

Lo primero que debemos de hacer es comprobar que el equipo está actualizado.
>guillevr@servidor:~$ sudo apt-get update
>
>[sudo] contraseña para guillevr:
>
>Obj:1 http://es.archive.ubuntu.com/ubuntu hirsute InRelease
>
>Des:2 http://security.ubuntu.com/ubuntu hirsute-security InRelease [110 kB]
>
>Des:3 http://es.archive.ubuntu.com/ubuntu hirsute-updates InRelease [115 kB]
>
>Des:4 http://es.archive.ubuntu.com/ubuntu hirsute-backports InRelease [101 kB]
>
>Des:5 http://security.ubuntu.com/ubuntu hirsute-security/main amd64 DEP-11 Metadata [9.696 B]
>
>Des:6 http://security.ubuntu.com/ubuntu hirsute-security/universe amd64 DEP-11 Metadata [5.672 B]
>
>Des:7 http://es.archive.ubuntu.com/ubuntu hirsute-updates/main amd64 DEP-11 Metadata [95,1 kB]
>
>Des:8 http://es.archive.ubuntu.com/ubuntu hirsute-updates/universe amd64 DEP-11 Metadata [57,8 kB]
>
>Des:9 http://es.archive.ubuntu.com/ubuntu hirsute-updates/multiverse amd64 DEP-11 Metadata [944 B]
>
>Des:10 http://es.archive.ubuntu.com/ubuntu hirsute-backports/universe amd64 DEP-11 Metadata [9.352 B]
>
>Descargados 505 kB en 2s (226 kB/s)                                         
>
>Leyendo lista de paquetes... Hecho
>
>guillevr@servidor:~$
>
>guillevr@servidor:~$ sudo apt-get grade
>
>E: Operación inválida: grade
>
>guillevr@servidor:~$ sudo apt-get upgrade
>
>Leyendo lista de paquetes... Hecho
>
>Creando árbol de dependencias... Hecho
>
>Leyendo la información de estado... Hecho
>
>Calculando la actualización... Hecho
>
>Los siguientes paquetes se han retenido:
>
>  linux-generic-hwe-20.04 linux-headers-generic-hwe-20.04
>
>  linux-image-generic-hwe-20.04
>
>0 actualizados, 0 nuevos se instalarán, 0 para eliminar y 3 no actualizados.
>
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
>     Loaded: loaded (/lib/systemd/system/apache2.service; enabled; vendor prese>
>
>     Active: active (running) since Sun 2021-10-17 22:35:57 CEST; 20min ago
>
>       Docs: https://httpd.apache.org/docs/2.4/
>
>   Main PID: 3551 (apache2)
>
>      Tasks: 55 (limit: 5478)
>
>     Memory: 5.2M
>
>     CGroup: /system.slice/apache2.service
>
>             ├─3551 /usr/sbin/apache2 -k start
>
>             ├─3553 /usr/sbin/apache2 -k start
>
>             └─3554 /usr/sbin/apache2 -k start
>
>
>
>oct 17 22:35:57 servidor systemd[1]: Starting The Apache HTTP Server...
>
>oct 17 22:35:57 servidor apachectl[3550]: AH00558: apache2: Could not reliably >
>
>oct 17 22:35:57 servidor systemd[1]: Started The Apache HTTP Server.
>
>guillevr@servidor:~$


Ahora editaremos la pagina un poco para darle un toque personal.
>guillevr@servidor:~$ sudo gedit /var/www/html/index.html
>
>
>
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
>	<body>
>
>		<h2 align="center">Pagina para el proyecto de seguridad.</h2>
>
>	</body>
>
></html>
>
>
>
>guillevr@servidor:~$


![](pag_por_defecto_apache.png)

Lo mas importante es, irnos al CLIENTE y comprobar que buscando en el navegador la IP del SERVIDOR nos aparece la página web que hemos creado.
![](acceso_a_web_cliente_servidor.png)


## Configuración del equipo ATACANTE.

> Lo primero que debemos de hacer es comprobar que el equipo está actualizado.
> guillevr@atacante:~$ sudo apt-get update
>
> [sudo] contraseña para guillevr:
>
> Obj:1 http://security.ubuntu.com/ubuntu hirsute-security InRelease
>
> Obj:2 http://es.archive.ubuntu.com/ubuntu hirsute InRelease
>
> Obj:3 http://es.archive.ubuntu.com/ubuntu hirsute-updates InRelease
>
> Obj:4 http://es.archive.ubuntu.com/ubuntu hirsute-backports InRelease
>
> Leyendo lista de paquetes... Hecho
>
> guillevr@atacante:~$
>
> guillevr@atacante:~$ sudo apt-get upgrade
>
> Leyendo lista de paquetes... Hecho
>
> Creando árbol de dependencias... Hecho
>
> Leyendo la información de estado... Hecho
>
> Calculando la actualización... Hecho
>
> Los siguientes paquetes se han retenido:
>
>   linux-generic-hwe-20.04 linux-headers-generic-hwe-20.04
>
>   linux-image-generic-hwe-20.04
>
> 0 actualizados, 0 nuevos se instalarán, 0 para eliminar y 3 no actualizados.
>
> guillevr@atacante:~$

Ahora instalaremos la herramienta que necesitamos para dicho ataque (hping3) y una herramienta que necesitaremos para ver las peticiones que se realizan hacia el servidor (wireshark).
> guillevr@atacante:~$ sudo apt-get install hping3
>
> Leyendo lista de paquetes... Hecho
>
> Creando árbol de dependencias... Hecho
>
> Leyendo la información de estado... Hecho
>
> Se instalarán los siguientes paquetes NUEVOS:
>
>   hping3
>
> 0 actualizados, 1 nuevos se instalarán, 0 para eliminar y 3 no actualizados.
>
> Se necesita descargar 106 kB de archivos.
>
> Se utilizarán 263 kB de espacio de disco adicional después de esta operación.
>
> Des:1 http://es.archive.ubuntu.com/ubuntu hirsute/universe amd64 hping3 amd64 3.a2.ds2-10 [106 kB]
>
> Descargados 106 kB en 0s (282 kB/s)
>
> Seleccionando el paquete hping3 previamente no seleccionado.
>
> (Leyendo la base de datos ... 192380 ficheros o directorios instalados actualmente.)
>
> Preparando para desempaquetar .../hping3_3.a2.ds2-10_amd64.deb ...
>
> Desempaquetando hping3 (3.a2.ds2-10) ...
>
> Configurando hping3 (3.a2.ds2-10) ...
>
> Procesando disparadores para man-db (2.9.4-2) ...
>
> guillevr@atacante:~$


## Uso básico de Hping3.

Uso básico de la herramienta:
El uso de esta herramienta es muy sencillo, pero disponemos de una gran cantidad de argumentos con el objetivo de aumentar sus funcionalidades, como lanzar un determinado número de paquetes, enviar paquetes con un determinado intervalo de espera, enviar paquetes para «floodear» a un objetivo y realizarle una denegación de servicio, posibilidad de contar los paquetes enviados y recibidos por los diferenes hosts, e incluso un modo de depuración para ver a bajo nivel qué está ocurriendo en la red.

* v –version muestra la versión actual de hping3
* -c –count contador de paquetes
* -i –interval tiempo de espera (uX para X microsegundos, por ejemplo -i u1000)
* –fast alias para -i u10000 (10 paquetes por segundo)
* –faster alias para -i u1000 (100 paquetes por segundo)
* –flood envía paquetes lo más rápido posible, no muestra las respuestas.
* -n –numeric salida con números
* -q –quiet comando silencioso sin que lo muestre por pantalla
* -I –interface nombre de la interfaz, si no se pone nada, por defecto es la interfaz de la puerta de encima predeterminada.
* -V –verbose modo verbose para depuración
* -D –debug información de debugging
* -z –bind enlaza ctrl+z a ttl (por defecto al puerto de destino)
* -Z –unbind desenlaza ctrl+z
* –beep beep por cada paquete recibido que coincida
