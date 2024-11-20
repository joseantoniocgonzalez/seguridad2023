## Automatizar rkhunter

En este apartado vamos a ver la forma de automatizar `rkhunter`. Debo decir que hay muchas formas de hacerlo; de hecho, podemos configurarlo usando `cron` de forma manual. Pero en este caso, `rkhunter` incluye la opción de ser configurado haciendo uso de la herramienta `debconf` que incluye `Debian` para sus paquetes. Este método nos hará unas preguntas para generar un fichero de configuración que estará en "`/etc/default/rkhunter`". Para ejecutar esta configuración automática debemos ejecutar:

```bash
dpkg-reconfigure rkhunter
```

Nos hará diferentes preguntas y nos generará un fichero de configuración respecto a eso.

### Fichero /etc/default/rkhunter
```bash
# Defaults for rkhunter automatic tasks
# sourced by /etc/cron.*/rkhunter and /etc/apt/apt.conf.d/90rkhunter
#
# This is a POSIX shell fragment
#

# Set this to yes to enable rkhunter daily runs
# (default: false)
CRON_DAILY_RUN="true"

# Set this to yes to enable rkhunter weekly database updates
# (default: false)
CRON_DB_UPDATE="true"

# Set this to yes to enable reports of weekly database updates
# (default: false)
DB_UPDATE_EMAIL="false"

# Set this to the email address where reports and run output should be sent
# (default: root)
REPORT_EMAIL="root"

# Set this to yes to enable automatic database updates
# (default: false)
APT_AUTOGEN="true"

# Nicenesses range from -20 (most favorable scheduling) to 19 (least favorable)
# (default: 0)
NICE="0"

# Should daily check be run when running on battery
# powermgmt-base is required to detect if running on battery or on AC power
# (default: false)
RUN_CHECK_ON_BATTERY="false"
```

Ahora vamos a ver qué significa cada parámetro de este fichero.

1. **CRON_DAILY_RUN**: Esto indica si se debe realizar un escaneo cada día; en mi caso, al estar en `true`, sí se realizará dicho escaneo.

2. **CRON_DB_UPDATE**: Indica a `rkhunter` si debe ejecutar cada semana el comando `rkhunter --update`, esto hará que actualice su base de datos para detectar nuevas firmas de amenazas. En mi caso, al estar en `true`, se realizará.

3. **DB_UPDATE_EMAIL**: Indica si queremos recibir un email semanal con el informe de la actualización de la base de datos. Por defecto se ha configurado en `false`, pero será una opción interesante para tenerla en `true`.

4. **REPORT_EMAIL**: Esto configura el destino para los avisos de los escaneos diarios, o del informe semanal de actualizaciones. Por defecto está el usuario `root`, pero en nuestro caso lo modificaremos para aprovechar el servidor de base de datos indicando un email de destino.

5. **APT_AUTOGEN**: Esta opción permitirá que cada vez que se instale o actualice los paquetes del sistema con el comando `apt` o similares, se genere un snapshot del estado de los archivos. Esto sería similar a ejecutar `rkhunter --propupd`. Una opción útil, pero peligrosa ya que podríamos dar por válido ficheros infectados o modificados. En mi opinión, siempre deberíamos ejecutar esa copia de estado de forma manual y estando seguros de que el sistema está correcto.

6. **NICE**: Indica la prioridad con la que se ejecuta el escaneo en el sistema. El valor por defecto está bien.

7. **RUN_CHECK_ON_BATTERY**: Indica si queremos que `rkhunter` se ejecute cuando estamos en modo batería en el caso de los portátiles. Al consumir batería por la intensidad de las pruebas que realiza, es mejor dejarlo en `false`.

## Uso automatizado

Como hemos podido ver, este fichero configurará `rkhunter` para que se use de forma desatendida, se actualice y nos envíe avisos en caso de detectar algo. Como dije antes, es un proceso que se podría haber realizado de otras formas más manuales, pero no tiene sentido reinventar la rueda cuando la herramienta ya nos proporciona una forma de configurarlo.

La única opción que deberíamos tener realmente cuidado de usar es la de realizar instantáneas de estado, pues eso marcará que hasta ese punto el sistema está libre de problemas, malware, etc. Si hacemos que se realice en cada uso de `apt`, podríamos de forma errónea marcar ficheros infectados como correctos.

Todas las opciones que configuramos en ese fichero, generan tareas de `cron`. Estas tareas podemos verlas en el propio directorio, por ejemplo `/etc/cron.daily/rkhunter`. Ese fichero es un script escrito en `bash` que se ejecutará de forma diaria porque está dentro del directorio `daily` de `cron`. Podemos modificar dicho fichero para que envíe un mensaje diferente en los reportes de correo, u otras cosas, pues como dije, no deja de ser un script de `bash` hecho a base de estructura condicional `case`.

Para finalizar, dejo un ejemplo del contenido de dicho fichero:

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