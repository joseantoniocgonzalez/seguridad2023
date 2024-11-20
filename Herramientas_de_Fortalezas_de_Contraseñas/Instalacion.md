# *Herramientas de fortaleza de contraseñas: John The Ripper e Hydra*

![](img/john.png)

## **John The Ripper.**

Destaca como uno de los **programas más conocidos** y ampliamente utilizados para **descifrar contraseñas** en sistemas operativos como Windows, Linux y MacOS. Este software de **código abierto**, se especializa en **descifrar contraseñas** mediante dos enfoques principales: **fuerza bruta y diccionario**. La eficiencia de este programa para descifrar los hashes de contraseñas es notablemente rápida, siendo su velocidad dependiente de la potencia del procesador del dispositivo. 

John the Ripper, una herramienta de descifrado de contraseñas **escrita en C**, teniendo como propósito principal a **evaluar la resistencia de las contraseñas** ante ataques de fuerza bruta. Con la capacidad de descifrar hashes como MD5, SHA-1 y otros ampliamente utilizados.

Una característica distintiva es su **capacidad automática para identificar el tipo de hash,** simplificando el proceso de descifrado para el usuario, eliminando la preocupación por el tipo específico de hash que se está intentando romper.

John the Ripper **destaca por su adaptabilidad**, optimizado para diversos modelos de procesadores y compatible con varias arquitecturas de PC y sistemas operativos. Aunque es funcional en diversos entornos, encuentra su principal aplicación en sistemas operativos basados en Linux, siendo incorporado de forma predeterminada en las principales distribuciones orientadas a pruebas de penetración y seguridad informática como “**Kali Linux**”.

Permite definir la longitud a probar de una contraseña, generando todas las combinaciones posibles para alcanzar el objetivo de descifrar el hash. Asimismo, ofrece la configuración de rangos de letras, números o símbolos para probar la contraseña, junto con la posibilidad de incluir reglas para guiar las variaciones.

John the Ripper brinda flexibilidad al permitir pausar y reanudar el proceso de descifrado, para situaciones en las que es necesario apagar el equipo o servidor. Además, **puede automatizarse** para iniciar el descifrado de contraseñas específicas al arrancar el ordenador, sin requerir intervención del administrador de sistemas.

Entre sus usos, destaca su aplicación en la **administración de contraseñas**, donde se emplea para evitar que los usuarios establezcan contraseñas con bajos niveles de seguridad. 

En la actualidad, **existen tres variantes** de este software. En primer lugar, **la versión gratuita**, ampliamente utilizada, seguida por **John the Ripper Pro** y la versión **John The Ripper Jumbo**. Este software es de código abierto y se distribuye bajo la licencia GPL, lo que permite el uso de algunas partes con otras licencias, mientras que otras están en el dominio público. Aunque inicialmente fue diseñado para sistemas Unix, en la actualidad es compatible con alrededor de 15 sistemas operativos diferentes, incluyendo once tipos de Unix, MS-DOS, Windows, BeOS y OpenVMS. Sin embargo, su presencia más común se encuentra en las distribuciones de Linux.

En cuanto a la **versión Pro**, ofrece ventajas como detectar automáticamente cualquier mejora en la tecnología compatible con el procesador de la máquina en la que está instalado. Además, proporciona un diccionario con más de 4 millones de entradas, donde las mejoras se detectan de forma automática, ahorrando tiempo al evitar la necesidad de realizar actualizaciones manuales.

Por último, **John the Ripper Jumbo** es un parche que amplía la capacidad para trabajar con una mayor variedad de algoritmos. Al ser una versión en desarrollo, algunas de sus funciones pueden no estar completamente optimizadas, lo que podría llevar a inconvenientes ocasionales.

Esta herramienta realiza pruebas de fortaleza de contraseñas en un sistema, siguiendo un proceso estructurado para llevar a cabo estas tareas:

1. **Recopilación de Contraseñas:** El primer paso implica recopilar las contraseñas cifradas o en formato hash dentro del sistema. Este proceso puede involucrar la obtención de archivos de contraseñas, bases de datos, registros, entre otros métodos.
1. **Selección del Ataque:** Con la base de datos de contraseñas disponible, se elige el modo de ataque más adecuado según el caso. Esta elección se basa en la información disponible sobre las contraseñas y el tiempo disponible para descifrarlas.
1. **Diccionario de Contraseñas:** Se utiliza un diccionario de contraseñas para el descifrado. Este diccionario puede obtenerse de diversas formas, siendo común incluir palabras clave, nombres propios y términos ampliamente utilizados.
1. **Fuerza Bruta:** Si el método de ataque seleccionado no tiene éxito, se recurre a la fuerza bruta para descifrar las contraseñas, es decir, probar y probar hasta encontrar la contraseña correcta. En este paso, se realizan pruebas con diferentes combinaciones de caracteres hasta lograr una coincidencia exacta con la contraseña.
1. **Hashcat:** En caso de que las contraseñas estén protegidas por funciones hash muy fuertes, la herramienta utiliza hashcat para intentar descifrarlas. Esta herramienta aprovecha la potencia de procesamiento de la GPU para acelerar el proceso.
1. **Descifrado:** Una vez localizada la coincidencia de la contraseña, se procede al descifrado y se muestra al usuario.

Este proceso demuestra la metodología utilizada por la herramienta para evaluar y, en última instancia, descifrar contraseñas dentro de un sistema.

## **Instalación y datos varios**

Para poder instalar la versión gratuita de esta herramienta, hay diferentes formas, como descargarla desde su web, compilandolo para otras distribuciones o simplemente desde la terminal que es el caso que se va a realizar a continuación:

```bash
Sudo apt install john
```
Con la herramienta instalada, uno de los primeros pasos a comprobar es que rendimiento tiene en mi ordenador, por lo que, para hacer una prueba es con el comando `john --test` con el cual se mide  la potencia de procesamiento del micro, lo que a su vez significa la velocidad que tardará en hacer determinadas tareas. Al introducir el comando “john” devuelve los parámetros que se pueden usar, que van variando dependiendo de la versión que tengamos de la herramienta.


| Opción               | Descripción                                                   |
|-----------------------|---------------------------------------------------------------|
| --single              | Modo "single crack"                                           |
| --wordlist=FILE       | Modo "wordlist", leer palabras desde FILE o stdin              |
| --rules               | Habilitar reglas de manipulación de palabras para el modo wordlist |
| --incremental[=MODE]  | Modo "incremental" [usando la sección MODE]                    |
| --external=MODE       | Modo externo o filtro de palabras                              |
| --stdout[=LENGTH]     | Solo mostrar contraseñas candidatas [cortar en LENGTH]         |
| --restore[=NAME]      | Restaurar una sesión interrumpida [llamada NAME]               |
| --session=NAME        | Darle un nombre a una nueva sesión                              |
| --status[=NAME]       | Imprimir el estado de una sesión [llamada NAME]                |
| --make-charset=FILE   | Crear un conjunto de caracteres, FILE será sobrescrito         |
| --show                | Mostrar contraseñas crackeadas                                 |
| --test[=TIME]         | Ejecutar pruebas y benchmarks durante TIME segundos            |
| --users               | [No] cargar solo este (estos) usuario(s)                       |
| --groups              | Cargar [no] usuarios de este (estos) grupo(s)                  |
| --shells              | Cargar usuarios con [sin] esta (estas) shell(s)                |
| --salts               | Cargar sales con [sin] al menos N contraseñas                  |
| --save-memory=LEVEL   | Habilitar ahorro de memoria, en Niveles 1..3                    |
| --node=MIN[-MAX]/TOTAL| Rango del número de este nodo fuera del recuento TOTAL         |
| --fork=N              | Bifurcar N procesos                                            |
| --format=NAME         | Forzar tipo de hash NAME: descrypt/bsdicrypt/md5crypt/bcrypt/LM/AFS/tripcode/dummy/crypt |



## Datos varios
**Otro tema importante es la ubicación de los `archivos de configuración` que son:**

`/etc/john/john.conf` → archivo de configuración.

`/root/.john/john.pot` → archivo donde se almacenan las contraseñas vulneradas.

`John.rec` → archivo donde se almacena el estado, para poder continuar cualquier operación incluso
si se podrucen cortes. (Se actualiza cada 10 minutos)


**Si se ejecuta el comando john sin opciones, este por defecto ejecutará los modos configurados en el primer fichero john.conf que encuentre:**

    ~/.john
    /etc/john
    /usr/share/john

**Esto mismo consiste en lo siguiente:**

- Comienza con el modo single crack, aplicando las reglas especificadas en dicha sección a las palabras que obtiene de la información de /etc/passwd.
- Ejecuta el modo wordlist, aplicando sus reglas a cada una de las palabras del fichero que indique la variable Wordlist. Si dicha variable no contiene ningún valor, usa el fichero /usr/share/john/password.lst.
- Aplica el modo incremental de nombre ASCII, y si no estuviera definido, muestra un mensaje de error.

**Si especificamos opciones:**

- Se tiene en cuenta entre mayúsculas y minúsculas. Por ejemplo: `--single correcto, --Single incorrecto.`
- Se pueden abreviar las opciones tanto como se quiera, siempre que no haya ambigüedad con otra opción. Por ejemplo: `--single y --si es lo mismo y correcto, -s es incorrecto.`
- Pueden ir con un guión o con dos. Por ejemplo: --single y -single es lo mismo y correcto.
- Los argumentos de las opciones se pueden separar con : o con =. Por ejemplo, `-w:palabras.lst y -w=palabras.lst` es lo mismo y correcto.

La opción `--single[=SECCIÓN]` se utiliza para lanzar solo el modo single crack. Si no se especifica ninguna sección se utilizan las reglas de la sección `[List.Rules:Single].`



![](img/hydra.png)

## Hydra


Hydra es una herramienta de prueba de penetración diseñada para realizar ataques de fuerza bruta y diccionario en protocolos de autenticación. Es particularmente conocida por su 
capacidad para realizar ataques a servicios remotos como SSH, FTP, HTTP, entre otros.

Hydra es un cracker de inicio de sesión paralelizado que admite numerosos protocolos para atacar. Es muy rápido y flexible, y los nuevos módulos son fáciles de agregar. Esta herramienta hace posible que los 
investigadores y consultores de seguridad Mostrar lo fácil que sería obtener acceso no autorizado a un sistema remotamente.

Es compatible: Cisco AAA, Cisco auth, Cisco enable, CVS, FTP, HTTP(S)-FORM-GET, HTTP(S)-FORM-POST, HTTP(S)-GET, HTTP(S)-HEAD, HTTP-Proxy, ICQ, IMAP, IRC, LDAP, MS-SQL, MySQL, NNTP, Oracle Listener, Oracle SID, PC-Anywhere, PC-NFS, POP3, PostgreSQL, RDP, Rexec, Rlogin, Rsh, SIP, SMB(NT), SMTP, Enumeración SMTP, SNMP v1+v2+v3, SOCKS5, SSH (v1 y v2), SSHKEY, Subversion, Teamspeak (TS2), Telnet, VMware-Auth, VNC y XMPP.

Para instalar `hydra` en equipos como Debian, que no lo trae de serie como Kali, es:

``` bash
sudo apt install hydra
```

Y algunas de sus opciones son:

| Opción | Descripción |
|--------|-------------|
| -l LOGIN or -L FILE | Login con el nombre LOGIN, o cargar varios logins desde un archivo |
| -p PASS or -P FILE | Intentar contraseña PASS, o cargar varias contraseñas desde archivo |
| -C FILE | Formato "login:pass" separado por dos puntos, en lugar de -L/-P opciones |
| -M FILE | Lista de servidores a atacar, una entrada por línea, ':' para especificar el puerto |
| -t TASKS | Ejecutar TASKS número de conexiones en paralelo por objetivo (predeterminado: 16) |
| -U | Detalles de uso del módulo de servicio |
| -m OPT | Opciones específicas para un módulo, ver salida de -U para obtener información |
| -h | Más opciones de línea de comandos (AYUDA COMPLETA) |
| server | El objetivo: DNS, IP o 192.168.0.0/24 (esto O la opción -M) |
| service | El servicio a crackear (ver abajo para los protocolos soportados) |
| OPT | Algunos módulos de servicio admiten entrada adicional (-U para obtener ayuda del módulo) |

Pero con lo que hay que quedarse de todo más es con los parámetros de `usuario (l de login) y contraseña (-p de password)`, Si `conozco el login o la contraseña` de un usuario, entonces ese parámetro va con `minúsculas`, y `si no lo conozco es con mayúsculas`, es decir, si conozco el usuario pero no la contraseña, seria -l usuario -P método de ataque.


## John o Hydra, ¿cual voy a necesitar?

**Hydra:**

- Tipo de Ataque: Hydra se especializa en ataques de fuerza bruta y diccionario. Puede realizar ataques contra servicios que utilizan diversos protocolos de autenticación, como SSH, FTP, HTTP, etc.

- Objetivo: Su enfoque principal es encontrar combinaciones de nombres de usuario y contraseñas correctas mediante la prueba de múltiples combinaciones sobretodo en escenarios remotos.

**John the Ripper:**

- Tipo de Ataque: John the Ripper se centra en ataques de fuerza bruta, diccionario y ataques basados en rainbow tables. Puede realizar ataques contra archivos de contraseñas cifradas localmente.

- Objetivo: Se utiliza principalmente para romper contraseñas almacenadas localmente, como las que se encuentran en archivos de contraseñas cifradas.


**Conclusión:**

Hydra se centra en ataques a servicios remotos y mientras que John the Ripper se utiliza para romper contraseñas almacenadas localmente.
