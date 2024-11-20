## Herramienta de integridad en Windows

Para este apartado, vamos a ver una herramienta para la integridad de archivos pero del sistema `Windows`. Como veremos en este apartado, es bastante más simple que la que hemos usado para `Linux`, tampoco tiene tantas opciones o nos permite configurar avisos de correo, etc.

### System File Checker (SFC)

Esta es una utilidad diseñada por `Microsoft`, por lo que podríamos considerarla una herramienta "oficial". Esta herramienta tiene un funcionamiento que podríamos resumir en los siguientes pasos:

1. **Verificación de Firma Digital**:
   - Los archivos del sistema de Windows están firmados digitalmente por Microsoft para garantizar su integridad. SFC verifica la firma digital de los archivos para asegurarse de que no hayan sido modificados desde que fueron instalados.

2. **Comparación de Hash**:
   - SFC calcula y compara el hash (por ejemplo, SHA-1, SHA-256, o MD5) de los archivos del sistema con el hash conocido de la versión correcta del archivo. Si los hashes no coinciden, el archivo se considera corrupto.

3. **Referencia a la Caché de Archivos**:
   - SFC utiliza una caché de archivos local que contiene copias limpias y conocidas de los archivos del sistema. Esta caché se encuentra en el directorio `WinSxS` (Side by Side). Si se detecta una discrepancia durante la verificación, SFC reemplaza el archivo corrupto con una copia limpia de la caché de archivos.

4. **Registro de Eventos**:
   - SFC registra sus acciones y resultados en el Registro de Eventos de Windows. Los usuarios pueden revisar este registro para obtener más información sobre qué archivos estaban corruptos y qué acciones se tomaron.

5. **Ejecución**:
   - Cuando ejecutas el comando `sfc /scannow`, SFC inicia un escaneo completo de los archivos del sistema protegidos. Revisa cada archivo contra la versión almacenada en la caché de archivos para identificar y reemplazar los archivos corruptos o faltantes.

6. **Reparación**:
   - Si se encuentran archivos corruptos o modificados, SFC intentará reemplazar estos archivos con las versiones correctas y sin modificar almacenadas en la caché de archivos en el directorio `WinSxS`.

A primera vista, podemos ver que tiene menos funciones o capacidades de análisis respecto a `rkhunter`, así como menos opciones de configuración.

#### Opciones de configuración

El Comando `sfc` (System File Checker) es una utilidad muy útil en Windows que permite a los usuarios escanear y restaurar corrupciones en los archivos del sistema operativo. A continuación, se describen algunas opciones importantes del comando `sfc` junto con ejemplos de cómo usarlas:

1. **Scannow**:
   - **Descripción**: Escanea la integridad de todos los archivos del sistema protegidos y repara los archivos que están dañados.
   - **Ejemplo de uso**: 
     ```shell
     sfc /scannow
     ```

2. **Verifyonly**:
   - **Descripción**: Escanea la integridad de todos los archivos del sistema protegidos, pero no repara los archivos.
   - **Ejemplo de uso**: 
     ```shell
     sfc /verifyonly
     ```

3. **Scanfile**:
   - **Descripción**: Escanea la integridad de un archivo específico y lo repara si encuentra alguna corrupción.
   - **Ejemplo de uso**: 
     ```shell
     sfc /scanfile=c:\windows\system32\kernel32.dll
     ```

4. **Verifyfile**:
   - **Descripción**: Verifica la integridad de un archivo específico, pero no lo repara.
   - **Ejemplo de uso**: 
     ```shell
     sfc /verifyfile=c:\windows\system32\kernel32.dll
     ```

5. **Offwindir y Offbootdir**:
   - **Descripción**: Estas opciones son útiles si necesitas escanear y/o reparar un sistema operativo Windows que no está en ejecución actualmente.
   - **Ejemplo de uso**: 
     ```shell
     sfc /scannow /offbootdir=c:\ /offwindir=d:\windows
     ```
