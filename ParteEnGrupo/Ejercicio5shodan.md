## Ejercicio 5.1
GHDB (Google Hacking Database) es una herramienta muy útil para averiguar como localizar con Shodan un tipo de dispositivo concreto. Explicad qué son los dorks y emplea GHDB para averiguar cómo localizar cámaras IP que tengan una IP pública con Shodan. ¿Es un producto de Google? ¿Por qué se llama así?

### ¿Qué es Google Dorking?
Google Dorks o Dorking, también conocido como Google Hacking es una técnica que consiste en aplicar la búsqueda avanzada de Google para conseguir encontrar en Internet información concreta a base de ir filtrando los resultados con operadores conocidos como Dorks, que son símbolos que especifican una condición. Por ejemplo, si ponemos en nuestro texto de búsqueda las dobles comillas (“texto”), buscará información que coincida exactamente con el texto. Es decir, si buscamos “OSI”, nos devolverá el contenido que concuerde exactamente con ese término

Dependiendo de los parámetros utilizados para la búsqueda, los resultados cambiarán, pero podría ser posible identificar información de todo tipo:

- Credenciales: usuarios y contraseñas de tus cuentas.
- Contenido audiovisual: fotos y vídeos.
- URLs privadas.
- Documentación sensible: DNI, números de teléfono, otros carnets.
- Información bancaria: números de cuenta o tarjetas.
- Correos electrónicos.
- Acceso a cámaras de seguridad.

### ¿Es legal usar Google Dorks?
Es importante que antes de lanzarte a utilizar Google Dorks, tengas claro que la información que quieres obtener o estás buscando no debes utilizarla para perjudicar a otras personas o que el objetivo de obtener dicha información sea para fines poco éticos.

Teniendo claro el párrafo anterior, la respuesta a la pregunta: ¿es legal usar Google Dorks? La respuesta es sí, ya que toda la información que puedes encontrar cuando realizas las búsquedas, es información pública, es decir, está expuesta y publicada en Internet bien sea consciente o inconscientemente por ti mismo o incluso por terceras partes.

### ¿Cómo utilizar Google Dorks?
Primero necesitas conocer los comandos básicos de las búsquedas avanzadas. Se llaman operadores y son símbolos o palabras específicas con las que puedes encontrar algo en concreto que busques.

Por ejemplo, si quieres comprobar si tu nombre aparece en páginas web, puedes introducir en la barra de navegación de tu buscador: “Tu nombre y apellidos” entre comillas. Del mismo modo, puedes realizar búsquedas entrecomillando lo que quieras encontrar: “número de dni”, “dirección de casa”, “teléfono”, “email”, “matrícula del coche”, etc.

Por otro lado, si te gustaría saber si están expuestas tus credenciales de acceso a algún servicio online que utilices, es decir, si están publicadas en alguna web accesibles para todo el mundo debido algún hakeo o robo de datos, debes utilizar el operador inurl e intext tal que así: inurl: [URL de la web] AND intext: [contraseña]

También, si quieres buscar palabras en concreto que contengan una página web, puedes usar el operador allintext: (palabra deseada). Ejemplo: allientext: noticias coronavirus.


Otra utilidad interesante de esta herramienta es que puedes hacer búsquedas para encontrar documentos e información específica. Por ejemplo, puedes buscar si en una página web está expuesto tu currículum vitae, con el comando site: [página web] y entre comillas los datos que te ayuden a localizarlo: “teléfono” “correo” “dirección”, etc. Por último, buscamos el documento en sí con intitle: “currículum vitae”. Ej. site: paginaweb.com “teléfono” “dirección” "correo electrónico” intitle: curriculum vitae.

Hay otros muchos operadores que puedes utilizar, en la página de soporte de Google encontrarás más información: https://support.google.com/websearch/answer/2466433

### ¿Es un producto de Google?
No es un producto de Google , es una iniciativa de la comunidad de seguridad informática. Google Hacking Database (GHDB) es un proyecto open-source que recopila una inmensa colección de los dorks conocidos. Este proyecto es la eminencia en lo que refiere a esta temática, y es actualizado y mantenido por el grupo Offensive Security (los mismos creadores de Kali Linux, Backtrack y Exploit-DB).

### Buscar camaras usando GHDB
A la hora de realizar una búsqueda en Google, hay ciertas palabras clave y operadores que funcionan como un lenguaje de consulta estructurado y tienen un significado especial para este motor de búsqueda. Los mismos se utilizan para filtrar los resultados. Es decir que los usuarios pueden apoyarse en estos operadores para encontrar resultados relevantes para sus búsquedas de forma más rápida y precisa, aunque, por otra parte, una persona con fines malintencionados podría utilizar estas mismas técnicas para obtener información sensible, y esto es lo que se conoce como “Google Dorks” o “Google Hacking”.

| Operador   | Ejemplo de Búsqueda en Google  | Propósito  | ¿Se Puede Combinar con Otros?  |
|------------|--------------------------------|------------|--------------------------------|
| site       | site:wikipedia.org             | Buscar resultados dentro de un sitio específico | Sí |
| related    | related:wikipedia.org          | Buscar sitios relacionados        | Sí |
| cache      | cache:wikipedia.org            | Buscar la versión del sitio en caché | Sí |
| intitle    | intitle:wikipedia              | Buscar en el título de la página | Sí |
| inurl      | inurl:wikipedia                | Buscar una palabra contenida en una URL | Sí |
| filetype   | filetype:pdf                   | Buscar por tipos de archivo específicos | Sí |
| intext     | intext:wiki                    | Buscar en el texto del sitio web solamente | Sí |
| ""         | "Wikipedia"                    | Buscar palabra por coincidencia exacta | Sí |
| +          | jaguar + car                   | Buscar más de una palabra clave | Sí |
| -          | jaguar speed -car              | Excluir palabras de la búsqueda  | Sí |
| OR         | jaguar OR car                  | Combinar dos palabras           | Sí |
| *          | how to * Wikipedia             | Operador de comodín              | Sí |
| imagesize  | imagesize:320x320              | Búsqueda de imágenes por tamaño  | No |
| @          | @wikipedia                     | Buscar en redes sociales        | Sí |
| #          | #wiki                         | Buscar hashtags                   | Sí |
| $          | camera $400                   | Buscar un precio                 | Sí |
| ..         | camera $50..$100               | Buscar dentro un rango de precios | Sí |

Con este dork se pueden encontrar cámaras web modelo “WebcamXP 5” que están transmitiendo en vivo y que no tienen ningún tipo de restricción de acceso por IP (whitelist) o que no requieren autenticación.

**intitle:"webcamXP 5"**

![](/ParteEnGrupo/img/Ejercicio5Shodan_WebcamXP5.png)

Por ejemplo metiendome en varias camaras publicas , he seleccionado una perrera en la cual sus camaras son accesibles desde el buscador de google :

![](/ParteEnGrupo/img/Ejercicio5Shodan_WebcamXP5_dentro.png)



### Busqueda en shodan 

Para utilizar filtros en el buscador tendremos que estar registrados , una vez esto introducire el siguiente filtro para que busque por el puerto 80 y ademas que tengan capturas de pantalla disponibles :
![](/ParteEnGrupo/img/Ejercicio5Shodan_buscador.png)

Podemos ir navegando y viendo los distintos resultados que nos ofrece :

![](/ParteEnGrupo/img/Ejercicio5Shodan_camara.png)


## Ejercicio 5.2
Una vez localizada, entregad una captura de pantalla donde se vea la localización de la cámara, el país, el proveedor de internet, los puertos abiertos,…Te puede ser útil este artículo.

Si analizamos la siguiente captura de pantalla anterior podemos sacar la siguiente información de esta "cámara":

![](/ParteEnGrupo/img/Ejercicio5Shodan_datos.png)


| Información General      |                  |
|--------------------------|------------------|
| Nombres de Hosts         | 114-33-48-14.hinet-ip.hinet.net |
| Dominios                 | HINET.NET        |
| País                     | Taiwán           |
| Ciudad                   | Tainan           |
| Organización             | Chunghwa Telecom Co., Ltd. |
| ISP                      | Grupo de Negocios de Comunicación de Datos |
| ASN                      | AS3462           |



| Puertos Abiertos |
|-----------------|
| 80              |
| 9530            |


| Vulnerabilidad    | Descripción                                                                                                                      |
|------------------|----------------------------------------------------------------------------------------------------------------------------------|
| CVE-2018-10088   | Desbordamiento de búfer en XiongMai uc-httpd 1.0.0 con impacto y vectores de ataque no especificados, una vulnerabilidad diferente a CVE-2017-16725. |



## Ejercicio 5.3
Comprobad si hay algún sistema con “Windows XP” conectado a internet, ¿en qué país?, ¿qué puerto está exponiendo?. Razona tu respuesta: ¿qué problemas de seguridad puede tener?,¿por qué crees que puede exponerse a ataques una máquina tan vulnerable?

Si nos vamos a shodan y introducimos el filtro de búsqueda *os:"Windows XP"* :

![](/ParteEnGrupo/img/Ejercicio5Shodan_WindowsXP_Busqueda.png)

Como podemos ver hay 5.215 Windows XP accesibles desde internet , aquí te dejo el ranking de los 10 países que tienes mas de estos sistemas accesibles desde internet :

![](/ParteEnGrupo/img/Ejercicio5Shodan_WindowsXP_Paises.png)

Si elegimos uno de España en el buscador y analizamos los puertos que tiene abiertos :

![](/ParteEnGrupo/img//Ejercicio5Shodan_WindowsXP_Telefonica.png)


| Puerto     | Servicio                  |
|------------|---------------------------|
| 1433       | Microsoft SQL Server      |
| 1700       | Enterasys RoamAbout       |
| 1489       | Oracle TNS Listener       |
| 9829       | Nexus Portal              |
| 91         | Protel                   |


Un sistema que ejecuta Windows XP en la actualidad enfrenta una serie de problemas de seguridad significativos. En primer lugar, uno de los mayores desafíos es la falta de actualizaciones de seguridad. Microsoft dejó de proporcionar actualizaciones de seguridad para Windows XP en abril de 2014. Esto significa que cualquier vulnerabilidad que se descubra después de esa fecha no se parcheará oficialmente, dejando el sistema expuesto a riesgos de seguridad.

Además, la exposición a vulnerabilidades conocidas es una preocupación constante. Dado que Windows XP es un sistema operativo obsoleto y no recibe parches de seguridad, los atacantes pueden explotar vulnerabilidades conocidas para comprometer el sistema. Es especialmente preocupante, ya que las técnicas de explotación y las vulnerabilidades se vuelven públicas y accesibles con el tiempo.

Es probable que las empresas que aún utilizan sistemas operativos obsoletos, como Windows XP, lo hagan debido a la necesidad de ejecutar software específico desarrollado para funciones críticas en sus operaciones. Es muy probable que este software no haya sido diseñado para sistemas operativos más recientes y, por lo tanto, no haya recibido actualizaciones de seguridad a lo largo de su ciclo de vida. Esta situación es especialmente común en entornos industriales, como fábricas, donde sistemas legados desempeñan un papel vital en los procesos de producción.


## Ejercicio 5.4
Localizad un servidor de Minecraft vulnerable a CVE-2021-44228. Explica cómo se parchea esta vulnerabilidad. Opcional: Graba un vídeo demostrando cómo podrías atacar un servidor vulnerable a CVE-2021-44228. Recuerda que debe ser un servidor propio para no tener problemas legales.

Log4j es una vulnerabilidad de ejecución remota de código (RCE) que le permite a los actores maliciosos a ejecutar código arbitrario en Java, tomando el control del servidor.

Lo primero que hare sera montarme un servidor vulnerable para ello me descargare la version de Minecraft 1.8.8 y la version de java 1.8.0 :

![](/ParteEnGrupo/img/Descargas_Log4j.png)

![](/ParteEnGrupo/img/Log4j_Java_version.png)

Ahora iniciaremos el servidor de Minecraft , yo para ello lo introduciré en un directorio , para tener los archivos ordenados . 

Haz doble clic en el archivo del servidor (por ejemplo, "server.jar"). Esto iniciará el servidor de Minecraft. Se generara automáticamente un archivo "eula.txt" que debas editar para aceptar los términos del Acuerdo de licencia de usuario final de Minecraft.

Una vez hecho esto , vuelve a ejecutar el  archivo server.jar y el servidor se creara .

El puerto por defecto es el 25565 , en tu cliente para conectarte al mismo crea una conexión en el apartado multijugador con la dirección IP de tu servidor . Si no tienes el launcher premiun recuerda en el fichero server.properties del servidor poner el modo online-mode=false .

Una vez comprobamos que nos podemos conectar al servidor , toca comprobar que es vulnerable . He probado varios escáneres sin embargo ninguno me ha detectado la vulnerabilidad , ademas he lanzado varios scripts que he encontrado en github y tampoco la detectan . Aquí te dejo la salida de OpenVas con cada una de las tareas que te deja lanzar , incluso tiene una especifica para Log4j pero no las detecta . En los reportes ninguna de las vulnerabilidades detectadas hacen referencia ni a esta , ni a ninguna relacionada con java .

![](/ParteEnGrupo/img/Log4j_escaner.png)

Sin embargo el servidor es vulnerable , para llevarlo acabo he seguido este repositorio de git https://github.com/davidbombal/log4jMinecraft .

En nuestra maquina atacante : 
1. Clona el repositorio: git clone https://github.com/davidbombal/log4jMinecraft.git
2. Ejecuta el script log4j.py (por ejemplo, python3 log4j.py <dirección_ip>, es decir, python3 log4j.py 192.168.1.132). Esto instala el software necesario y también inicia el servidor LDAP.
3. Ejecuta el script jcomp_pyserv.py (por ejemplo, python3 jcomp_pyserv.py). Esto compila la carga útil de Java que se ejecutará y también inicia un servidor Python3 http.server.


Aquí te dejo el video donde se demuestra que el servidor es vulnerable -->  https://youtu.be/Z93VnOM8LIM?si=O11VIPOJBnygmLt1


Según la version de Minecraft para parchearlo hay que seguir un procedimiento distinto , puedes encontrarlo en su web oficial --> https://help.Minecraft.net/hc/en-us/articles/4416199399693-Security-Vulnerability-in-Minecraft-Java-Edition .

En mi caso como he utilizado la version 1.8.8 , tendremos que crear un fichero XML que te dan en la misma pagina web en el directorio donde esta el servidor --> https://launcher.mojang.com/v1/objects/4bb89a97a66f350bc9f73b3ca8509632682aea2e/log4j2_17-111.xml .
Ademas tendremos que iniciar el servidor indicando que leea este fichero , asi que para ello creamos un fichero .bat indicando al iniciar el servidor que lea el mismo -->   -Dlog4j.configurationFile=log4j2_17-111.xml


Aquí te dejo en video la demostración de que el parche funciona https://youtu.be/LEB7fcsjdnA , en este te muestro las acciones para parchearlo , una vez aplicado no seremos capaz de ejecutar código en el servidor .
