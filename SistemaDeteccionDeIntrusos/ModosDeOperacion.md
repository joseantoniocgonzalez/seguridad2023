# Modos de operación

## IPS (Intrusion Prevention System) y  IDS (Intrusion Detection System)

En este modo, Snort desempeña tanto el rol de un IPS (Sistema de Prevención de Intrusiones) como el de un IDS (Sistema de Detección de Intrusiones). Esto implica que no solamente detecta intrusiones, sino que también toma medidas activas para bloquear o prevenir el tráfico malicioso. Snort puede bloquear conexiones o paquetes que cumplan con ciertos criterios establecidos en las reglas.

La funcionalidad de Snort depende de la acción definida en las reglas. Si una regla especifica la acción "drop," Snort actuará como un IPS, bloqueando el tráfico que coincida con la regla. Si la acción es "alert," Snort actuará como un IDS, generando alertas sobre la detección de intrusiones sin bloquear el tráfico.

De esta manera, Snort adapta su comportamiento en función de las acciones definidas en las reglas, brindando flexibilidad para cumplir con los objetivos de seguridad específicos de una red o sistema.

Recuerda que si queremos que snort tire el trafico tenemos que decir en la accion de la regla drop :

![](img/Aspose.Words.6990a0ff-8ff7-410b-9b51-99bd2ec2562d.043.png)

Para ejecutar snort en este modo , podemos usar el siguiente comando:

![](img/Aspose.Words.6990a0ff-8ff7-410b-9b51-99bd2ec2562d.044.png)

Ahora si por ejemplo lanzamos un ping , este no llegara a su destino ya que snort ha tirado el paquete  :

![](img/Aspose.Words.6990a0ff-8ff7-410b-9b51-99bd2ec2562d.045.png)

Si mientras tenemos activo snort lanzamos un nmap en lugar de decirnos que los puertos están abiertos nos dirá que están filtered ya que hay un dispositivo de red que los analiza :

![](img/Aspose.Words.6990a0ff-8ff7-410b-9b51-99bd2ec2562d.046.png)

## Modo sniffer 

Si queremos hacer que snort guarde la captura del trafico en un archivo para su posterior visualización o análisis , podemos usar la opción -b  para habilitar la captura de tráfico en un archivo de registro en formato tcpdump (.pcap). Además, puedes usar la opción -L para especificar la ubicación y el nombre del archivo de registro.

![](img/Aspose.Words.6990a0ff-8ff7-410b-9b51-99bd2ec2562d.047.png)

Nuestra captura se guardara en la misma ruta en la que se guardan los logs de snort :

![](img/Aspose.Words.6990a0ff-8ff7-410b-9b51-99bd2ec2562d.048.png)

Si queremos abrirla podemos usar wireshark o tcpdump , los archivos no tendremos permisos para abrirlos asi que una solución facil es moverlo a un directorio sobre el que tengas permisos :

![](img/Aspose.Words.6990a0ff-8ff7-410b-9b51-99bd2ec2562d.049.png)
