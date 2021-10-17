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

** Requisitos **

Para realizar dicho ataque necesitaremos al menos dos máquinas con Ubuntu. Una de ellas tendrá un servidor web (apache) y la segunda maquina, será el cliente que utilizaremos para atacar al servidor.

Los requisitos básicos/mínimos para poder instalar ubuntu son:
* Procesador de doble nucleo de 2 GHz o superior.
* 4 GB de RAM.
* 25 GB de espacio libre en el disco duro.

## Realizar un ataque DDOS

Como he comentado anteriormente, para realizar dicho ataque necesitaremos dos maquinas ubuntu (en mi caso son maquinas virtuales conectadas entre si a traves de una red interna), una de ella será nuestro servidor web y la otra será el cliente con el que intentaremos tumbar el servidor.

Para realizar el ataque, deberemos tener en el cliente instalado Hping3.

** ¿Que es Hping3? **
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
