# Aplicación de las Herramientas

![](/ParteEnGrupo/img/inicio.png)


## Servidor
En este escenario he usado una máquina `Kali Linux` como servidor web con apache y mysql con MariaDB y he creado algunos usuarios de prueba. Y por otro lado los clientes, un equipo Debian y otro Windows. Con respecto a las herramientas:

- He configurado `Snort` para que me avise si alguien intenta hacer ping, si intenta escanear la red,ademas de intentar inyecciones sql y algunas reglas mas de la comunidad de snort entre otras asi como las que el mismo trae por defecto para protegerlo de varios ataques adicionales . Si queremos que snort también proteja a nuestros clientes tendremos que configurar el switch  para que envié el trafico de estos al servidor , para que pueda avisarnos en caso de trafico malicioso .  

- Con `Openvas`, crearemos una tarea programada indicando un escaneo completo de la red para que se ejecute una vez a la semana y nos mande el reporte por correo electrónico en el caso de que haya una alerta que supere el nivel 5 .
  
- `Rkhunter` de forma automatizada para que verifique la integridad del sistema de ficheros y que no haya puertas traseras, rootkits, malware, etc en el sistema, avisando también por correo para los dos clientes Linux.

- `John the Ripper e Hydra` para comprobar la fortaleza de las contraseñas de los usuarios crearemos una tarea programada para que en horas de inactividad compruebe si hay contraseñas vulnerables.

Desde ambos clientes se tiene acceso al servidor web y a la base de datos de MariaDB por tener activado el `acceso remoto` que ya expliqué en [la parte individual sobre mysql](../Herramientas_de_Fortalezas_de_Contraseñas/mysql.md).



### Openvas
Como he dicho antes, con Openvas lo he configurado para que haga un escaneo completo de la red como explica Jose [con monitorización continua](../Escaneres%20de%20vulnerabilidades/Monitorización%20continua.%20Demostración.md). 

Originalmente iba a configurar las tareas con `escaneos diarios`,pero en un escenario real es posible que en la empresa haya servicios o personas trabajando 24h y esto generaría mucho trafico en la red ,aunque para un escenario pequeño o con intervalos de tiempo de inactividad como por ejemplo en un instituto por las tardes y noches , haría escaneo diarios  para que el el sistema este preparado ante `cualquier vulnerabilidad` que pueda tener alguna herramienta o actualización. 

Ademas esto se hace forma desatendida ya que estaría programado y solo nos tendríamos qe preocupar cunado recibamos un aviso por correo , para realizar la configuración de [avisos por correo](../Escaneres%20de%20vulnerabilidades/Configuración%20de%20alertas%20de%20correo.%20Demostración.md), puedes seguir este articulo .


En nuestro escenario OpenVas ha quedado configurado para realizar un escaneo completo a la red cada semana :

![](/ParteEnGrupo/img/ConfEscaneo.png)

He puesto que se inicie automáticamente los sábados a las 00:00 para evitar problemas de trafico en la red en un escenario real :

![](/ParteEnGrupo/img/EscaneoProgramado.png)

Ademas me mandara un correo informándome que ha encontrado una vulnerabilidad mayor a 5 y en ese caso me adjuntara el reporte en formato pdf del escaneo .

![](/ParteEnGrupo/img/conf_alertapng.png)



### Rkhunter
Con respecto a `Rkhunter`, es similar a Openvas, la mejor opción es guardar en su base de datos el `estado actual` de los ficheros del sistema habiendo comprobado que el sistema esta limpio, y por otra parte [automatizarlo para uso desatendido](../Integridad%20de%20ficheros/Automatizacion.md), y que se encargue constantemente de revisar el sistema. 

Como permite el uso desatendido se puede dejar trabajando constantemente protegiendo el servidor, aunque es imprescindible también [configurarlo para que alerte por correo](../Integridad%20de%20ficheros/Alertmail.md), de forma que, avisa inmediatamente de que ha surgido cualquier problema y poder reaccionar a tiempo.

Si lo dejamos programados tendremos una entrada de cron similar a esta tanto en el cliente como en el servidor en el directorio  **/etc/cron.daily/rkhunter**:

```bash
#!/bin/sh

RKHUNTER=/usr/bin/rkhunter

test -x $RKHUNTER || exit 0

# source our config
. /etc/default/rkhunter

if [ -z "$NICE" ]; then
    NICE=0
fi

if [ -z "$RUN_CHECK_ON_BATTERY" ]; then
    RUN_CHECK_ON_BATTERY="false"
fi

# Do not run daily check if running on battery except if explicitely allowed
case "$RUN_CHECK_ON_BATTERY" in
    [NnFf]*)
        if [ -x /usr/bin/on_ac_power ]; then
            on_ac_power >/dev/null 2>&1
            [ $? -eq 1 ] && exit 0
        fi
esac

case "$CRON_DAILY_RUN" in
    [YyTt]*)
        OUTFILE=`mktemp` || exit 1
        /usr/bin/nice -n $NICE $RKHUNTER --cronjob --report-warnings-only --appendlog > $OUTFILE
        if [ -s "$OUTFILE" -a -n "$REPORT_EMAIL" ]; then
          (
            echo "Subject: [rkhunter] $(hostname) - Daily report"
            echo "To: $REPORT_EMAIL"
            echo ""
            cat $OUTFILE
          ) | /usr/sbin/sendmail $REPORT_EMAIL
        fi
        rm -f $OUTFILE
        ;;
      *)
       exit 0
       ;;
esac
```

### Hydra y John The Ripper

Estas herramientas  sirven para `defenderse y atacar` al propio sistema, por ejemplo, con `John` para comprobar la seguridad de las contraseñas del servidor en local como [explico aquí](../Herramientas_de_Fortalezas_de_Contraseñas/linux.md) y ver a que usuarios notificar para que realicen un cambio de contraseña por alguna más segura con caracteres, dígitos, símbolos y con cierta longitud para evitar que alguien no autorizado entre en alguna cuenta. 
 
Por otro lado, con `Hydra` haciendo el mismo proceso pero en remoto desde los clientes evitando incluso [el ataque sobre mysql](../Herramientas_de_Fortalezas_de_Contraseñas/mysql.md) desde el cliente que si puede conectarse al servidor. 

Si implementas una política de seguridad de contraseñas efectiva, puedes reducir la necesidad de utilizar herramientas como John the Ripper y Hydra para verificar y fortalecer las contraseñas de manera regular. Una política de seguridad de contraseñas sólida es fundamental para mantener tus sistemas y datos seguros.

Vamos a configurar 2 tipos de tarea :
- En todas las maquinas se comprobara mensualmente la fortaleza de las contraseñas de los usuarios locales 
- Solo en el servidor se comprobara la fortaleza de las contraseñas de los usuarios de MySQL

Para la primera crearemos un pequeño script , aunque podemos afinarlo si tenemos una política de seguridad , por ejemplo la longitud minima de las contraseñas es 8 caracteres :
```bash
#!/bin/bash

# Ejecutar John the Ripper para comprobar contraseñas locales
sudo john --incremental "/etc/shadow"
```

A este script se le puede añadir un segundo para que nos avise por correo si en 24h no ha finalizado , que mate el proceso ya que esto consume muchos recursos en el servidor , si esto es asi significara que nuestras contraseñas son "seguras":


```bash
#!/bin/bash

# Ruta al script principal
SCRIPT_PATH="/ruta/del/script.sh"

# Iniciar el script principal en segundo plano
$SCRIPT_PATH &

# Obtener el ID del proceso del script principal
PID=$!

# Esperar hasta 24 horas
sleep 86400  # 24 horas en segundos

# Verificar si el proceso todavía se está ejecutando
if ps -p $PID > /dev/null; then
    # Si el proceso todavía está en ejecución, matarlo
    kill $PID

    # Enviar un correo con los resultados (reemplaza con tu propio comando de correo)
    echo "El script se ejecutó durante más de 24 horas y se ha detenido." | mail -s "Alerta: Script excedió el tiempo" javierasping@gmail.com
fi

```

Ahora vamos a crear una tarea con cron para ello ejecutamos **crontab -e** y añadimos la siguiente linea para ejecutarlo una vez al mes , añadiremos el segundo script  :

```bash
0 0 * * 0 /ruta/del/script.sh
```

Esto mismo lo haremos con hydra para automatizar la comprobación de contraseñas del mysql

### Snort

Este lo dejaremos corriendo como demonio una vez configurada las reglas por defecto de la comunidad y las que el mismo trae configuradas por defecto . Ademas dejaremos configuradas las [alertas por correo](/SistemaDeteccionDeIntrusos/ConfiguracionAlertasMail.md).

Para conseguir esto ejecutaremos snort :

```bash
sudo snort -A console -q -s -c /etc/snort/snort.conf -i enp1s0 --daemon
```



## Clientes
Desde el cliente `Debian`, he probado a hacer ping, un escaneo de puertos con nmap, y un ataque DDos usando hping3 e inmediatamente el servidor me ha notificado las acciones gracias a Openvas, por lo que queda registrado que al servidor se le ha intentado atacar y obtener información de diferentes maneras, y posteriormente bloquearlas todas estas acciones como explica javi [por el modo IDS](../SistemaDeteccionDeIntrusos/ModosDeOperacion.md), por lo que el sistema queda protegido ante estos ataques cortando el tráfico y de paso dando tiempo para corregir y tomar medidas suponiendo que fuera un escenario real. 

![](/ParteEnGrupo/img/alerta_snort.png)

Desde el cliente `Windows` he repetido el proceso para comprobar que las herramientas funcionan también no sólo desde Debian.

## Conclusión de Utilidad de las Herramientas

La implementación de `Snort, rkhunter, OpenVAS , John y Hydra` para proteger el sistema ya que garantizan por ejemplo que el servidor esta seguro de `agujeros de seguridad` por culpa de vulnerabilidades de herramientas o del propio sistema y que un atacante pueda aprovecharse de ello (como hacer escalada de privilegios o una shell reversa), pero incluso si llega a conseguirlo, rkhunter se encarga de prevenir y avisar que en el sistema hay actividad maliciosa o cambios en algunos archivos que podrían usarse como otra brecha más de seguridad. 

Complementándolo con `Snort` para la detección de amenazas en el tráfico de red detectando cualquier tipo de amenaza que le llegue al sistema avisando al administrador inmediatamente por correo , haciendome llegar la información en el momento del ataque para poder reaccionar a tiempo y realizar las acciones necesarias que deba usar dependiendo del ataque que sufra el  servidor, gracias a que también no solo es una forma pasiva sino activa de protección, porque también toma medidas bloqueando el tráfico si snort esta ubicado en el cortafuegos o en la misma maquina que queremos proteger , si esta en la red en otra ubicación solo sera capaz de avisarnos .

En cambio `John The Ripper e Hydra` lo he usado para poner a prueba las contraseñas de los usuarios y evitar tener  una `contraseña débil`, puede poner en riesgo todo el sistema. Podemos complementar esto con una medida preventiva que es usar politicas de contraseñas tanto en Windows como en Linux asi nos aseguramos de que un usuario no pueda poner una contraseña débil. 

Por último y no menos importante, si este fuera un escenario real, `concienciar a los usuarios` sobre los peligros de internet y evitar practicas como las de tener las contraseñas pegadas en un `posit` en la propia pantalla a la vista de todos o compartirlas con otras personas , cosa que ocurre con demasiada frecuencia. 

No abrir ni muchos menos descargar archivos en los que no sabemos quien es el remitente para asegurarnos descargar malware , para ello tambien podemos complementarlo con antivirus locales en las maquinas del usuario.

De nada sirve tener el `sistema más protegido del mundo`, si los usuarios no tienen noción de que las malas practicas ponen en riesgo todos los sistemas de una empresa, ya que en esta la seguridad es fuerte como su eslabón mas debil, por eso es tan importante concienciar a los usuarios, para que no ocurra lo que le pasó en septiembre al Ayuntamiento de Sevilla por ejemplo. 
