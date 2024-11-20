# Introducción
SNORT es un sistema de detección de intrusiones (IDS) y un sistema de prevención de intrusiones (IPS) de código abierto y potente. Proporciona análisis en tiempo real del tráfico de red y registra paquetes de datos. Utiliza un lenguaje basado en reglas que combina métodos de inspección de firmas, protocolos y anomalías para detectar actividades potencialmente maliciosas.

Con SNORT, los administradores de red pueden detectar una amplia gama de amenazas, incluyendo ataques de denegación de servicio (DoS), ataques distribuidos de denegación de servicio (DDoS), ataques Common Gateway Interface (CGI), desbordamientos de búfer y escaneos de puertos sigilosos. SNORT crea reglas que definen el comportamiento malicioso en la red, identifica paquetes maliciosos y envía alertas a los usuarios.

Este software de código abierto es de uso gratuito y puede ser implementado por individuos y organizaciones. El lenguaje de reglas de SNORT permite definir qué tráfico de red debe ser analizado y qué acciones tomar cuando se detectan paquetes maliciosos.

SNORT se utiliza tanto para descubrir paquetes maliciosos como para proporcionar una solución completa de prevención de intrusiones en la red, monitoreando la actividad de la red y bloqueando posibles vectores de ataque.

Lanzado en 1998 por Martin Roesch, SNORT fue inicialmente considerado una tecnología de detección de intrusiones "ligera". Sin embargo, rápidamente se convirtió en una herramienta esencial en la seguridad de redes, capaz de monitorear redes TCP/IP y detectar una amplia variedad de tráfico sospechoso y ataques conocidos. Con el tiempo, SNORT ha evolucionado para convertirse en un estándar global en la prevención y detección de intrusiones, siendo ampliamente desplegado en todo el mundo.

## Elementos del sistema

SNORT consta de varios componentes esenciales para su funcionamiento:
- **Módulo de Captura de Tráfico**: Este componente utiliza la librería libpcap para capturar todos los paquetes de la red.
- **Decodificador**: El decodificador procesa los paquetes capturados y crea estructuras de datos a partir de ellos. También identifica los protocolos de enlace y red utilizados en la comunicación.
- **Preprocesadores**: Los preprocesadores son herramientas que preparan los datos para su posterior detección. Existen varios tipos de preprocesadores, cada uno diseñado para analizar tipos específicos de tráfico.
- **Motor de Detección**: Este componente es el corazón de SNORT y analiza los paquetes en función de las reglas definidas para detectar actividades sospechosas o ataques.
- **Plugins de Detección**: Los plugins de detección son partes del software que se compilan junto con SNORT y se utilizan para ajustar y modificar el comportamiento del motor de detección según las necesidades específicas.
- **Plugins de Salida**: Estos plugins permiten definir cómo, dónde y de qué manera se guardan las alertas y los paquetes de red correspondientes que generan esas alertas.

## Modos de Operación

SNORT ofrece tres modos de operación para adaptarse a diferentes necesidades , podemos resumirlos en 3 :

- **Analizador de Paquetes**: En este modo, SNORT muestra en tiempo real la actividad de la red en la que está desplegado, proporcionando visibilidad instantánea de lo que está sucediendo en la red.

- **Registrador de Paquetes**: Cuando se utiliza como registrador de paquetes, SNORT guarda registros (logs) de toda la actividad de la red. Estos registros son útiles para un análisis posterior y la identificación de patrones o tendencias.

- **Sistema de Prevención de Intrusos en la Red (NIDS)**: En este modo, SNORT opera en toda la red, especificando un archivo de configuración de reglas y patrones a procesar. Su objetivo principal es detectar y prevenir intrusiones y ataques en la red en tiempo real.


## ¿Dónde colocar Snort?

Snort debe ubicarse cerca del 'punto de estrangulamiento' (el punto por el cual todo el tráfico fluye al entrar o salir de su red). Esto generalmente implica estar en el interior del enrutador o cortafuegos de borde, por ejemplo. Puede ejecutar Snort de varias maneras:

Como un dispositivo 'en línea' detrás o después del cortafuegos/enrutador.

Esto implica que Snort está directamente en la ruta del tráfico y puede detectar amenazas en tiempo real. Sin embargo, también agrega un elemento que puede fallar en su conectividad.
Utilizando un puerto SPAN (Switched Port Analyzer) o puerto de espejeo para enviar tráfico a Snort.

Con esta configuración, el tráfico se copia y se envía a Snort para su análisis. Esto es útil para evitar posibles problemas de rendimiento en el tráfico en vivo, pero aún así permite la detección de amenazas.