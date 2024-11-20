# Usad el comando `whois` para averiguar información de un dominio.

El comando `whois` se utiliza para obtener información detallada sobre un dominio en Internet. Su funcionamiento básico implica proporcionar el nombre de dominio como argumento para la consulta. A continuación, se explican los pasos típicos de su funcionamiento:

1. **Ejecución del Comando**: El usuario ejecuta el comando `whois` seguido del nombre de dominio que desea consultar. Por ejemplo: whois wru.wales.

![](/ParteEnGrupo/img/Captura%20desde%202023-10-19%2017-21-03.png)

2. **Solicitud al Servidor Whois**: El comando envía una solicitud a un servidor Whois. Dependiendo del dominio que se esté consultando (por ejemplo, dominios genéricos como .com, .org o dominios de nivel superior geográfico como .uk para Reino Unido), se dirigirá a un servidor Whois específico que mantenga la información de ese dominio.

3. **Respuesta del Servidor Whois**: El servidor Whois responde con información detallada sobre el dominio. Esto incluye datos como el nombre del titular del dominio, la organización, la dirección, los contactos administrativos y técnicos, la fecha de registro, la fecha de vencimiento, el estado del dominio y otros detalles relevantes.

4. **Visualización de la Información**: El comando `whois` mostrará en la pantalla del usuario la información proporcionada por el servidor Whois. Esta información varía según la disponibilidad y la política de privacidad de la entidad que registró el dominio.

5. **Interpretación de la Información**: El usuario interpreta la información para comprender quién es el propietario del dominio, cuándo se registró, cuándo vence y quiénes son los contactos relacionados.



### Información de WHOIS para el dominio "wru.wales"

- **Nombre de Dominio**: wru.wales
- **ID de Registro de Dominio**: wru-WALES
- **Servidor WHOIS del Registrador**: No disponible
- **Registrador**: Gandi SAS
- **Fecha de Creación**: 26 de septiembre de 2014
- **Fecha de Actualización**: 19 de septiembre de 2023
- **Fecha de Vencimiento del Registro**: 26 de septiembre de 2024
- **Estado del Dominio**: clientTransferProhibited (Prohibida la transferencia del cliente)

### Información del Registrante (Ocultada por razones de privacidad):

- **Nombre**: REDACTED FOR PRIVACY
- **Organización**: REDACTED FOR PRIVACY
- **Dirección**: REDACTED FOR PRIVACY
- **Ciudad**: REDACTED FOR PRIVACY
- **Código Postal**: REDACTED FOR PRIVACY
- **País**: GB
- **Teléfono**: REDACTED FOR PRIVACY
- **Correo Electrónico**: Consulte el servicio RDDS del Registrador de Registro identificado en esta salida para obtener información sobre cómo contactar al Registrante, Administrador, o Contacto Técnico del dominio consultado.

### Información del Administrador, Técnico y Facturación (Ocultada por razones de privacidad):

- La información de contacto es la misma que la del Registrante.

### Servidores de Nombres (DNS):

- ns-81-c.gandi.net
- ns-41-b.gandi.net
- ns-161-a.gandi.net

### DNSSEC: Sin firmar

[Formulario de queja de inexactitudes del WHOIS de ICANN](https://www.icann.org/wicf)

**Última actualización de la base de datos WHOIS**: 19 de octubre de 2023

Esta información WHOIS proporciona detalles sobre el dominio "wru.wales," incluyendo información sobre su registro, fechas clave, estado, y servidores de nombres asociados. Ten en cuenta que algunos detalles, como la información de contacto, se ocultan por motivos de privacidad y seguridad.


# Usad `nslookup` y `dig` para obtener toda la información posible de un dominio.

`nslookup` es un comando que se utiliza para realizar búsquedas de DNS (Sistema de Nombres de Dominio). Con este comando, puedes consultar información sobre nombres de dominio, como las direcciones IP asociadas o la resolución inversa (obtener un nombre de dominio a partir de una dirección IP).

*Pros:*
- Fácil de usar.
- Para principiantes.

*Contras:*
- Capacidad limitada en comparación con `dig`.
- Menos control y detalles.

**dig**


`dig` (abreviatura de "domain information groper") es una herramienta de línea de comandos más avanzada que `nslookup`. Se utiliza para realizar consultas más detalladas en servidores DNS. Puede proporcionar información detallada sobre registros DNS, servidores autorizados y más.

*Pros:*
- Mayor control.
- Amplia funcionalidad.

*Contras:*
- Curva de aprendizaje.
- Requiere comandos específicos para obtener información detallada.

En resumen, si solo necesitas realizar consultas de DNS básicas, `nslookup` es una opción más simple y accesible. Sin embargo, si deseas un mayor control y detalles específicos sobre registros DNS, servidores y otros aspectos más avanzados, `dig` es la herramienta más adecuada. El uso de uno u otro dependerá de tus necesidades y tu nivel de experiencia técnica.




La salida de la consulta DNS usando `dig` para el dominio "hermandaddelaestrella.org" muestra la información de resolución de nombres (registros A) para ese dominio. Aquí está la explicación de la salida:


![](/ParteEnGrupo/img/Captura%20desde%202023-10-19%2017-33-50.png)



- `; <<>> DiG 9.18.19-1~deb12u1-Debian <<>> hermandaddelaestrella.org`: Esta línea muestra la versión de `dig` que estás utilizando y la consulta que realizaste para el dominio "hermandaddelaestrella.org".

- `;; global options: +cmd`: Esto indica que estás utilizando las opciones globales de `dig` con el comando.

- `;; Got answer:`: Indica que has recibido una respuesta del servidor DNS.

- `;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 61230`: En esta sección, se proporciona información sobre la consulta DNS. `opcode` muestra que es una consulta, `status` muestra que la consulta fue exitosa (NOERROR), e `id` es el identificador de la consulta.

- `;; flags: qr rd ra; QUERY: 1, ANSWER: 3, AUTHORITY: 0, ADDITIONAL: 1`: Aquí se indican varias banderas y detalles sobre la respuesta:
   - `qr`: Indica que esta es una respuesta.
   - `rd`: Indica que se realizó una consulta recursiva.
   - `ra`: Indica que se aceptan consultas recursivas.
   - `QUERY: 1`: Hubo una pregunta en la consulta.
   - `ANSWER: 3`: La respuesta incluye 3 registros de dirección IP (registros A).
   - `AUTHORITY: 0`: No se proporciona información de autoridad en la respuesta.
   - `ADDITIONAL: 1`: Se incluye una sección adicional con información de autoridad.

- `;; OPT PSEUDOSECTION:`: Esta sección muestra información adicional relacionada con DNS.

- `; EDNS: version: 0, flags:; udp: 512`: Aquí se especifica la versión de EDNS utilizada, junto con algunas banderas y el límite UDP (User Datagram Protocol) utilizado para la respuesta.

- `;; QUESTION SECTION:`: Esta sección muestra la pregunta en la consulta DNS. En este caso, la consulta es sobre la dirección IP (A record) de "hermandaddelaestrella.org".

- `;hermandaddelaestrella.org. IN A`: Esta línea muestra la pregunta DNS que se realizó, buscando la dirección IP (registro A) de "hermandaddelaestrella.org".

- `;; ANSWER SECTION:`: Aquí se muestra la sección de respuestas, que proporciona información sobre los registros de dirección IP (registros A) para el dominio "hermandaddelaestrella.org". Se muestran tres direcciones IP diferentes asociadas con este dominio.

- `;; Query time: 500 msec`: Indica el tiempo que tardó en responder la consulta DNS, en este caso, 500 milisegundos.

- `;; SERVER: 192.168.1.1#53(192.168.1.1) (UDP)`: Muestra la dirección IP del servidor DNS utilizado para realizar la consulta y el número de puerto UDP.

- `;; WHEN: Thu Oct 19 17:31:15 CEST 2023`: Muestra la fecha y hora en la que se realizó la consulta.

- `;; MSG SIZE rcvd: 102`: Indica el tamaño del mensaje de respuesta recibido, que en este caso es de 102 bytes.

La respuesta muestra que el dominio "hermandaddelaestrella.org" tiene tres registros de dirección IP asociados a él, lo que significa que tiene múltiples direcciones IP. Esto puede ser útil en situaciones de redundancia o equilibrio de carga.



La salida de la consulta DNS utilizando `nslookup` para el dominio "hermandaddelaestrella.org" muestra la información de resolución de nombres (registros A) para ese dominio. Aquí está la explicación de la salida:

![](/ParteEnGrupo/img/Captura%20desde%202023-10-19%2017-37-24.png)


- `Server: 192.168.1.1`: Indica la dirección IP del servidor DNS utilizado para realizar la consulta.

- `Address: 192.168.1.1#53`: Muestra la dirección IP del servidor DNS y el número de puerto utilizado para la consulta DNS.

- `Non-authoritative answer`: Esto significa que la respuesta no proviene de una fuente autoritativa (no es la fuente original de los registros DNS).

A continuación, se enumeran las direcciones IP asociadas al dominio "hermandaddelaestrella.org":

- `Name: hermandaddelaestrella.org` indica el nombre de dominio consultado.

- `Address: 185.230.63.186`, `Address: 185.230.63.107` y `Address: 185.230.63.171` son las direcciones IP asociadas al dominio. Se muestran tres direcciones IP diferentes asociadas con este dominio.

La respuesta muestra que el dominio "hermandaddelaestrella.org" tiene tres registros de dirección IP asociados a él, lo que significa que tiene múltiples direcciones IP. Esto puede ser útil en situaciones de redundancia o equilibrio de carga.


## Usad DNSDumpster para obtener un esquema de los departamentos de una empresa.

DNSDumpster es una herramienta en línea que proporciona información detallada sobre un dominio y sus registros DNS asociados. Esta herramienta es útil para realizar análisis de infraestructura de Internet y obtener una visión general de la presencia en línea de una organización o entidad. DNSDumpster ofrece características como:

- **Búsqueda de DNS:** Permite buscar y enumerar todos los registros DNS asociados con un dominio específico, incluidos los registros A, registros MX (para servidores de correo), registros NS (servidores de nombres) y otros tipos de registros.

- **Descubrimiento de subdominios:** Puede ayudar a identificar subdominios asociados con un dominio principal, lo que es útil para conocer la estructura de un sitio web o una red.

- **Mapeo de direcciones IP:** Proporciona información sobre las direcciones IP que están asociadas con el dominio, lo que puede ayudar a identificar la ubicación geográfica de los servidores.

- **Información del propietario del dominio:** Ofrece detalles sobre la entidad o individuo que registró el dominio, incluido el nombre del titular del dominio, la dirección de correo electrónico de contacto y la información del registrador.

- **Geolocalización de servidores:** Puede mostrar la ubicación geográfica de los servidores relacionados con el dominio.

En resumen, DNSDumpster es una herramienta de recopilación de información que permite a los usuarios obtener una comprensión más profunda de la infraestructura de dominios y sitios web. Puede ser útil para investigaciones de seguridad, auditorías de dominios y análisis de activos en línea. 




La información proporcionada  es una lista de registros relacionados con el dominio "fifa.com". Estos registros contienen información sobre la infraestructura técnica  del sitio web "fifa.com". Aquí hay una descripción general de lo que cada sección parece contener:



![](/ParteEnGrupo/img/Captura%20desde%202023-10-19%2017-43-04.png)

- **DNS Servers**: Enumera los servidores de nombres (DNS) utilizados por el dominio "fifa.com". Esto es crucial para la resolución de nombres de dominio en Internet.

- **MX Records**: Estos registros especifican servidores de correo que son responsables de recibir correos electrónicos destinados a "fifa.com". Son esenciales para la gestión del correo electrónico de la organización.

- **TXT Records**: Estos registros a menudo contienen información adicional, como políticas de seguridad de correo electrónico (SPF) o verificación de dominio para servicios de terceros (como Google o Facebook).

- **Host Records (A)**: Estos registros enumeran los nombres de host y las direcciones IP asociadas con esos nombres de host. Esto es fundamental para la resolución de direcciones IP y la gestión de servicios web.

- **HTTP**: Proporciona información sobre los servidores web utilizados, como software y direcciones IP. También puede revelar detalles sobre la tecnología utilizada.

- **HTTP TECH**: Detalla la tecnología utilizada en los servidores web, como el sistema operativo y otros componentes.

- **FTP**: Indica la presencia de servidores FTP y detalles sobre ellos.

- **SSH**: Muestra información sobre servidores SSH, que se utilizan para acceder a sistemas de forma segura.

- **GeoIP of Host Locations**: Proporciona información sobre la ubicación geográfica de los servidores.

- **Hosting (IP block owners)**: Revela detalles sobre la propiedad de los bloques de direcciones IP utilizados por la fifa .

Ademas la herramienta es capaz de hacernos un mapa con la información recopiladas del servidor DNS :

![](/ParteEnGrupo/img/Captura%20desde%202023-10-19%2017-47-41.png)


## Intentad localizar con Shodan las máquinas expuestas por una empresa. Reconocimiento Activo.

**Shodan** es un motor de búsqueda especializado que se centra en la identificación y análisis de dispositivos conectados a Internet. A diferencia de los motores de búsqueda convencionales, Shodan no busca información en sitios web, sino que rastrea la red en busca de dispositivos y sistemas en línea, como servidores, enrutadores, cámaras web, dispositivos IoT (Internet de las cosas), sistemas de control industrial y más. Shodan permite a los usuarios buscar y acceder a información detallada sobre estos dispositivos y sistemas en todo el mundo.

Algunas de las características y capacidades de Shodan incluyen:

1. **Búsqueda de dispositivos**: Los usuarios pueden buscar dispositivos por tipo, ubicación geográfica, dirección IP, nombre de host y otros parámetros.

2. **Información detallada**: Shodan proporciona información detallada sobre los dispositivos encontrados, incluyendo detalles técnicos, versiones de software, puertos abiertos y otros datos relevantes.

3. **Visualización de mapas**: Los resultados de búsqueda se pueden visualizar en un mapa geográfico, lo que permite ver la distribución de dispositivos en diferentes ubicaciones.

4. **Exploración de servicios y vulnerabilidades**: Shodan puede ayudar a identificar servicios y protocolos en ejecución en dispositivos, lo que puede ser útil para detectar posibles vulnerabilidades de seguridad.

5. **Monitorización de cambios**: Los usuarios pueden configurar alertas para monitorizar dispositivos específicos o cambios en la configuración de los dispositivos.

6. **Análisis de dispositivos IoT**: Shodan es especialmente útil para rastrear dispositivos IoT, como cámaras web, sistemas de automatización del hogar, dispositivos médicos y más.

7. **Uso ético**: Shodan se utiliza en auditorías de seguridad, investigaciones de ciberseguridad y para evaluar la exposición de dispositivos en línea. Es importante utilizar Shodan de manera ética y legal.

En resumen, Shodan es una herramienta que proporciona visibilidad y conocimiento sobre dispositivos y sistemas en Internet. Es ampliamente utilizado por profesionales de la ciberseguridad, investigadores de seguridad y administradores de red para identificar y abordar problemas de seguridad en la infraestructura de Internet. 

https://www.shodan.io/


![](/ParteEnGrupo/img/Captura%20desde%202023-10-19%2018-15-38.png)

**Información General:**
- **Hostnames (Nombres de Host):** Muestra el nombre de host asociado con la dirección IP. En este caso, es "c-73-102-41-133.hsd1.in.comcast.net."
- **Domains (Dominios):** Indica el dominio principal al que pertenece el host. En este caso, es "comcast.net."
- **Country (País):** Muestra el país en el que se encuentra el host, que es "United States" (Estados Unidos).
- **City (Ciudad):** Especifica la ciudad en la que se encuentra el host, en este caso, "Noblesville."
- **Organization (Organización):** Indica la entidad u organización a la que está asociado el host. En este caso, es "Comcast IP Services, L.L.C."
- **ISP (Proveedor de Servicios de Internet):** Muestra el proveedor de servicios de Internet que atiende a este host, que es "Comcast Cable Communications, LLC."
- **ASN (Número de Sistema Autónomo):** El número de sistema autónomo al que está asignado el host, que es "AS33491."
- **Operating System (Sistema Operativo):** Indica el sistema operativo detectado en el host, que es "Windows."

## Tecnologías Web:
- **JavaScript Frameworks (Frameworks de JavaScript):** Muestra que el sitio web utiliza el framework MooTools para la programación en JavaScript.

## Puertos Abiertos:
- **8080 / tcp:** Indica que el puerto 8080 de protocolo TCP está abierto en el host.
- **webcam 7 httpd:** Informa que el servicio web que se está ejecutando en el puerto 8080 es un servidor web relacionado con "webcam 7."

## Respuesta HTTP:
- Se muestra una respuesta HTTP recibida al intentar acceder al servidor web en el puerto 8080.
- El estado de la respuesta es "200 OK", lo que significa que la solicitud fue exitosa.
- La respuesta incluye información sobre el servidor, el tipo de contenido, la longitud del contenido, la configuración de caché y la fecha de la respuesta.

En resumen, esta información proporciona detalles sobre un host en Estados Unidos, con nombre de host y dominio asociados, y ofrece información sobre su sistema operativo, tecnologías web utilizadas, puertos abiertos y detalles de una respuesta HTTP en el puerto 8080, que parece estar relacionada con una cámara web ("webcam 7").





## Utilizad Wappalyzer para obtener información del Gonzalo Nazareno.

**Wappalyzer** es una herramienta que se utiliza para identificar las tecnologías y software que se ejecutan en un sitio web. Ofrece información detallada sobre las tecnologías utilizadas en la creación y funcionamiento de un sitio web. A continuación, se explican las características clave de Wappalyzer:

- **Detección de Tecnologías:** Wappalyzer escanea un sitio web y detecta las tecnologías utilizadas en él. Esto incluye sistemas de gestión de contenidos (CMS), frameworks, lenguajes de programación, servicios de alojamiento, servidores web y más.

- **Interfaz de Usuario Amigable:** Wappalyzer presenta la información de manera clara y sencilla en una interfaz de usuario amigable. Los resultados son fáciles de interpretar, incluso para personas no técnicas.

- **Información Detallada:** Proporciona detalles específicos sobre las tecnologías detectadas. Por ejemplo, si identifica un CMS, mostrará el nombre y la versión del CMS. Esto es útil para comprender la tecnología subyacente de un sitio web.

- **Extensiones para Navegadores:** Wappalyzer está disponible como una extensión para varios navegadores web populares, como Google Chrome y Mozilla Firefox. Esto permite a los usuarios escanear sitios web con facilidad mientras navegan por Internet.

- **Uso en Auditorías de Seguridad:** Los profesionales de seguridad web y los auditores de seguridad utilizan Wappalyzer para identificar las vulnerabilidades relacionadas con las tecnologías utilizadas en un sitio web.

- **Investigación Competitiva:** Wappalyzer se utiliza en la investigación competitiva para conocer las tecnologías utilizadas por otros sitios web y comprender las tendencias tecnológicas en línea.



### Informe sobre la Infraestructura Técnica

![](/ParteEnGrupo/img/Captura%20desde%202023-10-21%2012-31-46.png)

- **Gestor de Incidencias:**
  - Redmine es una plataforma de gestión de proyectos y seguimiento de incidencias de código abierto. Se utiliza para administrar proyectos, hacer un seguimiento de tareas, resolver problemas y colaborar en equipos. Es especialmente valioso para equipos de desarrollo de software.

- **Seguridad:** 
  - HSTS (HTTP Strict Transport Security)
    - HSTS es un mecanismo de seguridad que ayuda a garantizar conexiones seguras entre el navegador del usuario y el servidor web. Obliga a que las conexiones se realicen a través de HTTPS en lugar de HTTP, lo que mejora la privacidad y la seguridad de los datos transmitidos.

- **Frameworks Web:**
  - **Django**
    - Django es un framework web de alto nivel escrito en Python. Facilita el desarrollo rápido de aplicaciones web seguras y escalables. Se utiliza ampliamente en el desarrollo de aplicaciones web.
  - **Ruby on Rails**
    - Ruby on Rails (también conocido como Rails) es un framework web de código abierto escrito en Ruby. Es conocido por su simplicidad y facilidad de uso, lo que lo hace popular entre los desarrolladores web.

- **Miscelánea:**
  - **RSS (Really Simple Syndication)**
    - RSS es un formato que permite a los usuarios suscribirse y recibir actualizaciones de contenido web, como noticias o blogs, de manera conveniente.
  - **Gravatar (Globally Recognized Avatar)**
    - Gravatar es un servicio que permite a los usuarios asociar una imagen de perfil a su dirección de correo electrónico. Esta imagen se muestra en sitios web compatibles cuando los usuarios comentan o interactúan.

- **Servidor Web:**
  - **Nginx 1.14.2**
    - Nginx es un servidor web de alto rendimiento y proxy reverso. Se utiliza para servir sitios web y aplicaciones web de manera eficiente. Es conocido por su escalabilidad y velocidad.
  - **Phusion Passenger 5.0.30**
    - Phusion Passenger es un módulo de aplicación para servidores web, como Nginx. Facilita la implementación de aplicaciones web Ruby y Python. Es especialmente útil para aplicaciones Ruby on Rails.

- **Lenguajes de Programación:**
  - **Python**
    - Python es un lenguaje de programación versátil que se utiliza en el desarrollo web, análisis de datos, automatización y más.
  - **Ruby**
    - Ruby es el lenguaje de programación en el que se basa Ruby on Rails. Es conocido por su sintaxis sencilla y elegante.

- **CDN (Content Delivery Network):** Google Hosted Libraries
  - Una CDN es una red de servidores distribuidos globalmente que almacena y entrega contenido web, como librerías de JavaScript y CSS, de manera eficiente a los usuarios. Google Hosted Libraries es un servicio de CDN de Google que aloja librerías comunes utilizadas en desarrollo web.

- **Librerías JavaScript:**
  - **jQuery 1.11.1**
    - jQuery es una librería de JavaScript ampliamente utilizada para simplificar la manipulación del DOM, la gestión de eventos y la interacción del lado del cliente en aplicaciones web.
  - **jQuery UI 1.11.0**
    - jQuery UI es una extensión de jQuery que proporciona componentes de interfaz de usuario y widgets personalizables para mejorar la experiencia del usuario en aplicaciones web.

- **Proxy Reverso:**
  - **Nginx 1.14.2**
    - Nginx también se utiliza como un proxy reverso. Actúa como intermediario entre los clientes y los servidores, gestionando las solicitudes y distribuyendo el tráfico de manera eficiente.

- **UI Framework:** Bootstrap 3.3.7
  - Bootstrap es un marco de diseño web que proporciona un conjunto de componentes y estilos predefinidos para crear interfaces de usuario modernas y responsivas. La versión 3.3.7 es una versión específica de Bootstrap utilizada en la interfaz de usuario.








## Buscad la utilidad del comando `nc`

El comando `nc` (netcat) es una herramienta versátil en el campo de la ciberseguridad y se utiliza para varios propósitos. Aquí hay algunas formas en que se puede utilizar en ciberseguridad:

- **Análisis de puertos y servicios**: `nc` se puede utilizar para escanear puertos y servicios en un sistema. Por ejemplo, puedes verificar si un puerto específico está abierto en un servidor, lo que es útil para identificar posibles vulnerabilidades.
  
  nc -vz target_host target_port

  - **Transferencia segura de archivos**: Puedes utilizar nc para transferir archivos de manera segura entre sistemas. Por ejemplo, puedes cifrar los datos durante la transferencia con SSH y nc.

nc -l -p 1234 < file.txt | ssh user@target_host "cat > received_file.txt"

- **Shell inversa o shell persistente**: En ciberseguridad, los atacantes pueden utilizar nc para establecer una conexión de shell inversa en un sistema comprometido y obtener acceso al sistema objetivo. Por otro lado, los profesionales de la ciberseguridad también pueden utilizarlo para conectarse de forma segura a sistemas remotos.
- 
  - Atacante: En el sistema comprometido, ejecutar:
  
  nc -lvp 1234 -e /bin/bash

**Defensor: En el sistema desde el que te conectas al atacante**
nc target_host 1234


- **Pruebas de seguridad y penetración**: nc es una herramienta útil para realizar pruebas de seguridad y penetración. Puedes usarlo para probar la respuesta de una aplicación o un servidor a solicitudes específicas y evaluar la seguridad de un sistema.

- **Auditorías de seguridad**: En auditorías de seguridad, puedes utilizar nc para verificar la disponibilidad y accesibilidad de servicios en la red. Esto te ayuda a identificar áreas de vulnerabilidad potenciales.

- **Análisis de tráfico y red**: Puedes usar nc para capturar y analizar tráfico de red en tiempo real. Esto es útil para monitorear la red y detectar actividades sospechosas.

- **Evaluación de cortafuegos y reglas de filtrado**: nc te permite verificar la efectividad de las reglas del cortafuegos al intentar conectarse a través de diferentes puertos y protocolos.

- **Conexiones de red seguras**: Los profesionales de la ciberseguridad pueden utilizar nc para establecer conexiones seguras a través de túneles SSH y realizar tareas de administración de sistemas en sistemas remotos.



## Buscad la forma de utilizar el comando nmap para conocer las máquinas de una red usando ARP Scan y explica en qué se basa su funcionamiento capturando el tráfico generado con Wireshark.

El comando nmap se puede utilizar para escanear una red en busca de máquinas utilizando ARP (Protocolo de Resolución de Direcciones) Scan. Este tipo de escaneo se basa en el uso del protocolo ARP para descubrir las máquinas activas en una red local.

```
sudo nmap -sn 192.168.122.0/24 -PR
```

Si vemos la salida del comando hemos recibido 3 respuestas , esto significa que en nuestra red hay 3 dispositivos :

![](/ParteEnGrupo/img/cli_arp_scan.png)

Si analizamos la captura de wireshark este le manda un arp request a todas las direcciones IP de nuestra red , si el cliente existe este recibirá un ARP reply del cliente y conocerá si hay un dispositivo con esa IP en la red . Si no se recibe una respuesta se da por hecho de que no hay un dispositivo con esa dirección .

![](/ParteEnGrupo/img/wireshark_arp_scan.png)

## Buscad la forma de utilizar el comando nmap para conocer las máquinas de una red usando ICMP Scan y explica en qué se basa su funcionamiento capturando el tráfico generado con Wireshark.

La opción -sP en Nmap se utiliza para realizar un sondeo ping en una red o rango de direcciones IP con el propósito de descubrir sistemas activos en la red. Esta opción no realiza sondeos de puertos ni detecta sistemas operativos, simplemente envía solicitudes de ping a las direcciones IP objetivo y enumera los sistemas que responden al ping.

El sondeo ping es una técnica de reconocimiento de red ligera y no intrusiva que permite al usuario obtener una lista de sistemas activos en la red sin realizar un análisis de puertos o detectar el sistema operativo. Es especialmente útil para conocer cuántos equipos están en línea y pueden ser un punto de partida para análisis y escaneos más profundos.

```
sudo nmap -sP 192.168.122.0/24 
```

Vemos la respuesta que nos da :
![](/ParteEnGrupo/img/nmap_ping.png)


Pese a que en la documentación indica que va a usar ICMP si analizamos el parámetro con una sola dirección para que sea mas legible , podemos ver que se  realizaron intentos de conexión TCP a los puertos 80 y 443 una vez el host ha contentado a la petición ARP .

![](/ParteEnGrupo/img/wireshark_icmp_scan.png)

## Buscad la forma de identificar los servicios que ofrece una máquina usando en nmap la técnica TCP SYN Ping y haz una pequeña prueba sobre una MV con Apache2 accesible desde la tuya. Explica en qué se basa su funcionamiento usando Wireshark.

La opción -PS en Nmap se utiliza para realizar un "Ping TCP SYN" a una máquina o dispositivo en una red. Esto implica el envío de paquetes TCP SYN (solicitud de conexión) a puertos específicos en el objetivo para determinar si el puerto está abierto (escuchando) o cerrado.

```
sudo nmap -PS -sV 192.168.122.83
```
El escaneo sigue la siguiente lógica : 

Envío de paquetes TCP SYN: Nmap envía paquetes TCP con la bandera SYN establecida. El paquete es "vacío" porque no contiene datos adicionales. La bandera SYN (Synchronize) se utiliza en el protocolo TCP (Transmission Control Protocol) para iniciar una conexión.

Selección de puertos: Por defecto, Nmap usa el puerto 80 (HTTP) como puerto de destino. Sin embargo, puedes especificar puertos personalizados con la opción -PS. Por ejemplo, -PS22,80,443 enviará paquetes de ping SYN a los puertos 22 (SSH), 80 (HTTP) y 443 (HTTPS) en las máquinas objetivo.

Respuestas esperadas: Cuando se envía un paquete de ping TCP SYN a un puerto de una máquina objetivo, hay dos posibles respuestas:

Si el puerto está cerrado, la máquina destino enviará un paquete de respuesta RST (Reset) para indicar que la conexión no se estableció.
Si el puerto está abierto, la máquina destino responderá con el segundo paso del saludo en tres pasos TCP, enviando un paquete TCP SYN/ACK (Synchronize/Acknowledge).
Interpretación de las respuestas: Nmap no está interesado en si el puerto está abierto o cerrado. Lo que busca son respuestas SYN/ACK o RST. Si recibe cualquiera de estas respuestas, considera que la máquina está viva y responde. Esto significa que la máquina objetivo está en línea y es accesible.

Privilegios y la llamada al sistema connect(): En sistemas UNIX, generalmente solo los usuarios con privilegios de root pueden enviar paquetes TCP crudos. Sin embargo, los usuarios no privilegiados pueden sortear esta restricción utilizando la llamada al sistema connect() para enviar el paquete SYN al puerto destino. Si la llamada connect() devuelve un resultado de éxito rápido o un error ECONNREFUSED, Nmap puede deducir que la pila TCP ha respondido con un SYN/ACK o un RST, lo que indica que la máquina está disponible.



Si este sobre una maquina veremos lo siguiente :

![](/ParteEnGrupo/img/nmapTCPSYCPING.png)


Aquí podemos ver la secuencia de mensajes para el puerto 80 de este escaneo :

![](/ParteEnGrupo/img/wireshar_apache.png)


1. Paquete de Solicitud de Conexión (SYN):

- El escaneo comienza con un paquete enviado desde la dirección IP de origen 192.168.122.1 al destino 192.168.122.83.
- Este paquete utiliza el protocolo TCP y contiene la bandera SYN (Synchronize), que indica la intención de establecer una conexión.
- Este paquete se envía desde el puerto origen 49896 al puerto destino 80, que es el puerto estándar para HTTP (el protocolo web).

2. Respuesta de Aceptación de Conexión (SYN, ACK):

- La máquina 192.168.122.83, que es el destino, responde rápidamente con un paquete SYN/ACK (Synchronize/Acknowledge).
- En este paquete, se establece la bandera SYN y la bandera ACK para indicar que está dispuesta a establecer una conexión y que ha recibido la solicitud anterior.
- Esto significa que la máquina objetivo está lista para recibir datos y reconoce que ha recibido el paquete de solicitud.

3. Respuesta de Restablecimiento de Conexión (RST):

- El tercer paquete proviene nuevamente de la dirección IP de origen 192.168.122.1 y se envía a la dirección IP de destino 192.168.122.83.
- Este paquete TCP contiene la bandera RST (Reset), que se utiliza para restablecer la conexión.

