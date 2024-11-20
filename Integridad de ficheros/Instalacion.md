## Instalación

Después de la breve introducción, procederemos a instalarlo. El programa `rkhunter` está disponible generalmente en los repositorios de cualquier distro estándar. En mi caso, haciendo uso de una distro derivada de `Ubuntu`, voy a instalarlo con el comando:

```bash
apt install rkhunter
```

Una vez instalada, la herramienta estará lista para ser usada. El uso más básico consiste en dos comandos diferentes que serían `rkhunter --propupd` y `rkhunter -c`. El primero permite guardar en la base de datos de `rkhunter` el estado actual de los ficheros del sistema, y el segundo realizar un escaneo.
El estado del sistema es una de las partes principales del funcionamiento de esta herramienta. De forma resumida, guarda la suma de comprobación, permisos, tamaño de los ficheros en su base de datos, de forma que si algún programa modifica de forma ilegítima algún fichero cambiando sus permisos, suma de comprobación, etc., lo detectaría en el escaneo.

Vamos a poner un ejemplo sobre lo anterior. En el directorio `/usr/bin` tenemos los ejecutables de los programas del sistema, lo que de forma resumida se podría decir los comandos que usamos en terminal. Al ejecutar el comando `rkhunter --propupd`, registrará la suma de cada fichero, en mi caso en formato `SHA256`, así como otros datos que le permitan identificar el fichero. Esto es lo que se conoce como propiedades de los archivos. Si modificásemos algún fichero o añadiésemos uno, al realizar el escaneo lo detectaría, indicándonos que ha sido modificado, provocando así una advertencia.

Por ese mismo motivo, el uso del comando `rkhunter --propupd` debe hacerse con la certeza de que el estado actual del sistema es correcto y no está afectado por virus o modificaciones ilegítimas. Ya que si realizamos esa instantánea del sistema, será marcado el estado de ese momento de ejecución como seguro o válido en cada escaneo.

## Fichero de configuración

Todas las configuraciones de `rkhunter` se hacen mayormente en dos ficheros, aunque se pueden crear otros ficheros complementarios.

El principal estaría en `/etc/rkhunter.conf`, que contiene toda la configuración del programa, desde los avisos hasta el comportamiento de su escaneo. Es un fichero bastante extenso y puede llegar a ser realmente complejo, por lo que no llegaremos a ver todas sus opciones, pero sí algunas de las más importantes.
El segundo fichero sería `/etc/default/rkhunter`. Este contiene la configuración sobre la automatización de escaneos, actualizaciones, etc. Lo veremos más adelante en el apartado de automatización.

### Opciones del fichero **rkhunter.conf**

Debido a que el propio fichero tiene descrito con detalle cada opción posible que podemos configurar, haré una lista de forma resumida de las opciones más importantes.

Se recomienda ejecutar el comando `rkhunter -C` después de hacer cualquier cambio en este archivo para verificar la configuración.

1. **Mirrors y Actualizaciones**:
   - `ROTATE_MIRRORS=1`: Si está configurado a '1', rota los mirrors (servidores espejo) para balancear la carga entre ellos durante las actualizaciones. Si está configurado a '0', los mirrors se usan en el orden en que aparecen en el archivo `mirrors.dat`.
   - `UPDATE_MIRRORS=0`: Si está configurado a '1', el archivo de mirrors se actualiza también durante la ejecución de `--update`. Si está configurado a '0', el archivo de mirrors debe ser actualizado manualmente.
   - `MIRRORS_MODE=1`: Define qué mirrors usar durante las actualizaciones: '0' para cualquier mirror, '1' para solo mirrors locales, '2' para solo mirrors remotos.
   - `WEB_CMD="/bin/false"`: Especifica el comando a usar para descargar archivos de Internet cuando se usan las opciones `--update` o `--versioncheck`.

2. **Notificación por Correo**:
   - `MAIL-ON-WARNING=root`: Envía un correo electrónico a la dirección especificada si se encuentra una advertencia durante el chequeo del sistema. Puedes especificar múltiples direcciones separándolas con un espacio.
   - `MAIL_CMD=...`: Define el comando de correo a usar si se ha establecido `MAIL-ON-WARNING`.

3. **Directorios Temporales**:
   - `TMPDIR`, `DBDIR`, y `SCRIPTDIR`: definen los directorios para archivos temporales, bases de datos y scripts, respectivamente.

4. **Configuraciones de Ruta y Directorio**:
   - `BINDIR=...`: Modifica la ruta de búsqueda de comandos de rkhunter.

5. **Opciones de Idioma**:
   - `LANGUAGE` y `UPDATE_LANG` configuran el idioma predeterminado y los idiomas a actualizar durante la ejecución de `--update`.

6. **Opciones de Registro**:
   - `LOGFILE`, `APPEND_LOG`, y `COPY_LOG_ON_ERROR` configuran el archivo de registro, si se debe agregar al archivo de registro existente o crear uno nuevo cada vez, y si se debe copiar el archivo de registro en caso de errores o advertencias.

7. **Opciones de Syslog y Visualización**:
   - `USE_SYSLOG`, `COLOR_SET2`, `AUTO_X_DETECT`, y `WHITELISTED_IS_WHITE` configuran el uso de syslog, los conjuntos de colores y cómo se muestran los resultados "Whitelisted".

8. **Configuraciones de SSH**:
   - `ALLOW_SSH_ROOT_USER`, `ALLOW_SSH_PROT_V1`, y `SSH_CONFIG_DIR` configuran los ajustes de SSH y dónde encontrar el archivo de configuración de SSH.

9. **Tests**:
    - `ENABLE_TESTS` y `DISABLE_TESTS` permiten al usuario especificar qué tests realizará el software. Por ejemplo, `ENABLE_TESTS=ALL` indica que se deben ejecutar todos los tests, mientras que `DISABLE_TESTS` lista los tests que deben ser ignorados.

10. **Opciones de Hash**:
    - `HASH_CMD` y `HASH_FLD_IDX` configuran cómo se deberían realizar los checks de hash en los archivos. Por ejemplo, `HASH_CMD=SHA256` indica que se debe usar SHA256 para los checks de hash.

11. **Opción de Gestor de Paquetes**:
    - `PKGMGR` le dice a rkhunter cómo obtener información de las propiedades de los archivos. Si está configurado como 'NONE', no se usará ningún gestor de paquetes, pero si se configura como 'RPM' o 'DPKG', entonces rkhunter obtendrá la información de los archivos desde los gestores de paquetes correspondientes.

12. **Whitelisting**:
    - Hay varias opciones de whitelisting (lista blanca) como `SCRIPTWHITELIST`, `ALLOWHIDDENDIR`, `ALLOWHIDDENFILE`, etc., que permiten especificar archivos, directorios o scripts que no deben ser considerados sospechosos por rkhunter.
    - `APP_WHITELIST` permite especificar aplicaciones o versiones de aplicaciones específicas que deben ser incluidas en una lista blanca, lo que significa que no serán consideradas sospechosas por rkhunter.
    - `SHARED_LIB_WHITELIST=/lib/snoopy.so`: Permite especificar bibliotecas compartidas que deben ser excluidas de la comprobación de bibliotecas precargadas.
    - `RTKT_DIR_WHITELIST=""` y `RTKT_FILE_WHITELIST=""`: Permiten especificar archivos y directorios que deben ser excluidos de las comprobaciones de rootkits y malware.
    - `PORT_WHITELIST=""` y `PORT_PATH_WHITELIST=""`: Estas opciones permiten especificar puertos o rutas a ejecutables conocidos que deberían ser excluidos de ciertas comprobaciones de malware. 

13. **Configuración de Memoria Compartida y Red**:
    - Opciones como `ALLOWIPCPROC`, `ALLOWPROCLISTEN`, y `ALLOWPROMISCIF` permiten controlar cómo rkhunter debería manejar los procesos que utilizan memoria compartida o escuchan en interfaces de red.

14. **Opciones de Escaneo**:
    - `SCAN_MODE_DEV` le dice a rkhunter cómo debe escanear el directorio `/dev`. `THOROUGH` es el valor recomendado, aunque puede aumentar el tiempo de escaneo.

15. **Configuraciones para `suspscan`**::
    - La opción `SUSPSCAN_DIRS` permite especificar directorios que deben ser escaneados en busca de archivos sospechosos. Esta opción es importante, pero se advierte que puede ser intensiva en términos de CPU y E/S, y puede generar falsos positivos.
    - `SUSPSCAN_TEMP=/dev/shm`: Esta opción especifica el directorio para archivos temporales usados por el test `suspscan`. Se sugiere usar un directorio basado en memoria como un sistema de archivos `tempfs` para mayor rapidez. El valor predeterminado es `/dev/shm`. En sistemas `Linux` todo lo guardado en el directorio `/dev/shm` es almacenado en la memoria RAM o swap.
    - `SUSPSCAN_MAXSIZE=1024000`: Esta opción especifica el tamaño máximo de archivo (en bytes) que el test `suspscan` inspeccionará. Si un archivo es más grande que este valor, no será inspeccionado.
    - `SUSPSCAN_THRESH=200`: Especifica el umbral de puntuación para el test `suspscan`. Ningún resultado será reportado si está por debajo de este valor.
    - `SUSPSCAN_WHITELIST=""`: Puedes especificar rutas de archivos para ser excluidos del test `suspscan`. Se pueden especificar más de una ruta.

16. **Opciones de Servicio de Red**:
    - Las opciones `INETD_ALLOWED_SVC` y `XINETD_ALLOWED_SVC` permiten especificar servicios de red permitidos, o que consideramos seguros.

17. **Opciones de Ruta**:
    - Opciones como `STARTUP_PATHS`, `PASSWORD_FILE`, y `SYSLOG_CONFIG_FILE` permiten especificar las ubicaciones de varios archivos y directorios importantes. En la primera opción, a su vez, el fichero password te permite indicar a **`rkhunter`** que revise el fichero `shadow` o el `syslog` en el último caso.

18. **Información del sistema operativo**:
    - `OS_VERSION_FILE=/etc/debian_version`: Especifica dónde se encuentra el archivo que contiene la versión del sistema operativo. Si cambia entre ejecuciones, rkhunter emitirá una advertencia.
    - `WARN_ON_OS_CHANGE=1`: Si se cambia información del sistema operativo desde la última ejecución de `rkhunter --propupd`, se emitirá una advertencia.
    - `UPDT_ON_OS_CHANGE=0`: Si el sistema operativo cambia, rkhunter puede realizar automáticamente una actualización de propiedades (`--propupd`) si esta opción está habilitada.

19. **Uso de bloqueo**:
    - `USE_LOCKING=0`: Si se habilita, se usará un mecanismo de bloqueo para evitar la corrupción de ciertos archivos si rkhunter se está ejecutando más de una vez.

20. **Modo de escaneo de rootkit**:
    - `SCANROOTKITMODE=THOROUGH`: Permite un escaneo más exhaustivo para rootkits, pero se advierte que solo debe ser habilitado por usuarios avanzados que pueden interpretar correctamente los resultados.

21. **Pruebas de `unhide` y opciones de `unhide-tcp`**:
    - `UNHIDE_TESTS=sys` y `UNHIDETCP_OPTS=""` configuran cómo se ejecutan las pruebas `unhide` y `unhide-tcp`, respectivamente.

22. **Mostrar el número de advertencias en el resumen**:
    - `SHOW_SUMMARY_WARNINGS_NUMBER=0`: Controla cómo se muestra el número de advertencias en el resumen.