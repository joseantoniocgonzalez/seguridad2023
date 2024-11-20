
### Escaneo Rápido de una Red

Para escanear  una red completa, vamos a  utilizar el modo de escaneo rápido, que es igual  de  eficiente y pero mas  rápido. Sigue estos pasos:

Un escaneo de red es una técnica en la que se envían mensajes a diferentes direcciones en una red de equipos para descubrir qué equipos están activos, qué servicios están disponibles en esos equipos y cómo están conectados en esa red en su conjunto. Esto es útil para administrar la red, identificar posibles problemas o vulnerabilidades, y mapear la estructura de la red en su totalidad.
al contrario que en  un escaneo de una sola IP se enfoca en una dirección de equipo específica en la red. El propósito principal de escanear una sola IP es obtener información detallada sobre esa dirección IP en particular, como los puertos abiertos, los servicios en funcionamiento y cualquier posible problema de seguridad o configuración en esa IP en particular. Se utiliza típicamente para diagnosticar o evaluar una dirección IP específica.


Para escanear  una red completa, vamos a  utilizar el modo de escaneo rápido, que es igual  de  eficiente y pero mas  rápido. Sigue estos pasos:


1. Accede a la herramienta de escaneo de seguridad.
2. En la interfaz, ve a la sección "Scan" o "Escaneo".
3. En la sección "Task" o "Tarea", busca un icono que se asemeje a una varita mágica y haz clic en él.
4. Se abrirá una nueva tarjeta o ventana para configurar un escaneo rápido.

Esto te permitirá escanear toda la red de manera eficiente y obtener resultados de seguridad rápidamente.


<img src="img/Captura desde 2023-10-07 16-55-05.png" width="1200">



# Descripción de Vulnerabilidades

A continuación se presenta una descripción de las vulnerabilidades detectadas, junto con detalles relevantes:

1. **Greenbone Security Assistant (GSA) Default Credentials (HTTP)**
   - Severidad: 10.0 (Alta)
   - Calidad de Detección (QoD): 100%
   - Host: 192.168.1.210
   - Ubicación: Puerto 443/tcp
   - Descripción: Esta vulnerabilidad indica el uso de credenciales predeterminadas en el Greenbone Security Assistant (GSA), una interfaz web para administrar sistemas de seguridad. El uso de credenciales predeterminadas es un riesgo de seguridad significativo.

2. **Check if Mailserver answer to VRFY and EXPN requests**
   - Severidad: 5.0 (Media)
   - Calidad de Detección (QoD): 99%
   - Host: 192.168.1.222
   - Ubicación: Puerto 25/tcp
   - Descripción: Esta vulnerabilidad sugiere verificar si el servidor de correo responde a solicitudes VRFY y EXPN. Estas solicitudes son comprobaciones típicas de seguridad en los servidores de correo para evitar la verificación de usuarios válidos.

3. **SSL/TLS: Deprecated TLSv1.0 and TLSv1.1 Protocol Detection**
   - Severidad: 4.3 (Media)
   - Calidad de Detección (QoD): 98%
   - Host: 192.168.1.222
   - Ubicación: Puerto 25/tcp
   - Descripción: Esta vulnerabilidad indica la detección de protocolos obsoletos TLSv1.0 y TLSv1.1 en el tráfico SSL/TLS. Se recomienda no utilizar estos protocolos obsoletos debido a sus riesgos de seguridad.

4. **TCP Timestamps Information Disclosure**
   - Severidad: 2.6 (Baja)
   - Calidad de Detección (QoD): 80%
   - Host: 192.168.1.222
   - Ubicación: Puerto general/tcp
   - Descripción: Esta vulnerabilidad se refiere a la divulgación de información de marcas de tiempo TCP en el tráfico de red, lo que puede revelar detalles sobre la actividad de la red.

5. **ICMP Timestamp Reply Information Disclosure (192.168.1.222)**
   - Severidad: 2.1 (Baja)
   - Calidad de Detección (QoD): 80%
   - Host: 192.168.1.222
   - Ubicación: Tipo de tráfico ICMP
   - Descripción: Esta vulnerabilidad se refiere a la divulgación de información de respuesta a marcas de tiempo ICMP en el host 192.168.1.222, lo que puede proporcionar detalles sobre la actividad de la red.

6. **ICMP Timestamp Reply Information Disclosure (192.168.1.229)**
   - Severidad: 2.1 (Baja)
   - Calidad de Detección (QoD): 80%
   - Host: 192.168.1.229 (tab-a8-de-dolores)
   - Ubicación: Tipo de tráfico ICMP
   - Descripción: Similar a la vulnerabilidad anterior, esta se refiere a la divulgación de información de respuesta a marcas de tiempo ICMP en el host 192.168.1.229 (tab-a8-de-dolores).



<img src="img/Captura desde 2023-10-21 10-25-15.png" width="1200">



Y tambien podemos comprobar los equipos que estan ahora mismo conectados a dicha red.

<img src="img/Captura desde 2023-10-21 10-28-45.png" width="1200">





