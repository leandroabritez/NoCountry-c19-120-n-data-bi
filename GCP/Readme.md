# Configuración de una VM en Google Cloud Platform y Ejecución de Jupyter Notebook

Este documento proporciona los pasos detallados para configurar una Máquina Virtual (VM) en Google Cloud Platform (GCP) y ejecutar Jupyter Notebook en ella para realizar el procesamiento de un archivo y verificar fraudes mediante Machine Learning (ML).

## Paso 1: Crear una VM en Google Cloud Platform

1. **Accede a la consola de Google Cloud**:
   - Visita [Google Cloud Console](https://console.cloud.google.com/).

2. **Navega a Compute Engine**:
   - En el menú de navegación, selecciona `Compute Engine` > `Instancias de VM`.

3. **Crea una nueva instancia**:
   - Haz clic en `Crear instancia`.
   - Configura los detalles de la instancia:
     - **Nombre**: `instance-20240722-225950` (o cualquier nombre descriptivo).
     - **Región y zona**: Elige una región y zona adecuadas para ti.
     - **Tipo de máquina**: Selecciona una que se ajuste a tus necesidades (e.g., `e2-medium`).
     - **Disco de arranque**: Usa una imagen estándar de Ubuntu (e.g., `Ubuntu 20.04 LTS`).

   > **Necesidad**: Crear una instancia de VM nos proporciona un entorno de computación en la nube donde podemos ejecutar Jupyter Notebook y realizar análisis de datos de manera escalable y segura.

4. **Configura el firewall**:
   - En la sección `Firewall`, selecciona las opciones `Permitir tráfico HTTP` y `Permitir tráfico HTTPS`.

   > **Necesidad**: Permitir el tráfico HTTP/HTTPS asegura que podamos acceder a la VM y a cualquier servicio web que ejecutemos en ella, como Jupyter Notebook.

5. **Crear la instancia**:
   - Haz clic en `Crear` para lanzar la VM.

## Paso 2: Conectar a la VM y Configurar el Entorno

1. **Conéctate a la VM mediante SSH**:
   - En la consola de Google Cloud, ve a `Compute Engine` > `Instancias de VM`.
   - Haz clic en el botón `SSH` junto a tu instancia para abrir una ventana de terminal.

   > **Necesidad**: Conectar a la VM a través de SSH nos permite administrar y configurar el entorno desde la línea de comandos.

2. **Actualizar los paquetes del sistema**:
   sh
   sudo apt update
   sudo apt install -y python3-pip
   pip3 install jupyter

   > **Necesidad**: Jupyter Notebook es una herramienta esencial para el análisis interactivo de datos y el desarrollo de algoritmos de machine learning.

### 4. Configurar Google Cloud SDK (gsutil)

Para transferir archivos entre Google Cloud Storage y tu VM, necesitas tener Google Cloud SDK instalado y configurado. Si aún no lo has hecho, sigue estos pasos:

1. **Instalar Google Cloud SDK**:
   - Ejecuta el siguiente comando para descargar e instalar el SDK:
     ```sh
     sudo apt-get install google-cloud-sdk
     ```

2. **Autenticarse en Google Cloud**:
   - Ejecuta el siguiente comando para autenticarse con tu cuenta de Google:
     ```sh
     gcloud auth login
     ```
   - Sigue las instrucciones en pantalla para completar la autenticación.

   > **Necesidad**: Configurar Google Cloud SDK y autenticarse permite interactuar con Google Cloud Storage para transferir archivos desde y hacia tu VM.

### 5. Copiar el archivo desde Google Cloud Storage a la VM

Para realizar el análisis de datos, primero debes transferir tu archivo desde Google Cloud Storage a la VM. Usa el siguiente comando para copiar el archivo:


gsutil cp gs://bucket_nocountry/EDA.ipynb .

 > **Necesidad**: Copiar el archivo de análisis de datos (EDA.ipynb) a la VM es esencial para que puedas acceder y trabajar en el notebook dentro del entorno de tu máquina virtual.

## Paso 3: Ejecutar Jupyter Notebook en la VM

### 1. Instalar Jupyter Notebook

Si Jupyter Notebook no está instalado en la VM, sigue estos pasos para instalarlo:

1. **Actualizar los repositorios y el sistema**:
   ```sh
   sudo apt-get update
   sudo apt-get upgrade


2. Instalar pip y Jupyter Notebook:
  sudo apt-get install python3-pip
  pip3 install jupyter


**Necesidad**: Instalar Jupyter Notebook es esencial para ejecutar y trabajar con notebooks en la VM, permitiendo el desarrollo y análisis de datos directamente desde el entorno en la nube.

### 2. Iniciar Jupyter Notebook

Para ejecutar Jupyter Notebook y hacerlo accesible a través de tu navegador, utiliza el siguiente comando:

jupyter notebook --ip=0.0.0.0 --no-browser


   **Necesidad**: Ejecutar Jupyter Notebook con estas opciones permite el acceso remoto desde tu navegador local, sin abrir automáticamente una ventana en la VM.

### 3. Copiar el Token de Acceso

Después de ejecutar el comando anterior, verás una salida en la consola que incluye un enlace con un token de acceso. Copia este token, ya que lo necesitarás para acceder a Jupyter Notebook.

   **Necesidad**: El token de acceso es necesario para autenticarte y acceder a Jupyter Notebook desde tu navegador local.

## Paso 4: Crear un Túnel SSH para Acceder a Jupyter Notebook

### 1. Obtener el Nombre de tu Instancia de VM

Accede a la consola de Google Cloud y navega a `Compute Engine` > `Instancias de VM`. Localiza el nombre de tu instancia.

   **Necesidad**: Conocer el nombre de tu instancia es esencial para establecer una conexión SSH y redirigir el tráfico desde la VM a tu máquina local.

### 2. Crear el Túnel SSH

Desde tu máquina local, ejecuta el siguiente comando para crear un túnel SSH que redirija el tráfico del puerto de Jupyter Notebook:

gcloud compute ssh your-vm-instance-name --zone your-zone -- -L 8888:localhost:8888


Reemplaza `your-vm-instance-name` con el nombre de tu instancia y `your-zone` con la zona correspondiente.

   **Necesidad**: Crear un túnel SSH permite acceder de forma segura a Jupyter Notebook a través de tu navegador local.

### 3. Acceder a Jupyter Notebook desde tu Navegador Local

Con el túnel SSH en funcionamiento, abre tu navegador y navega a:
http://localhost:8888


Introduce el token de acceso cuando se te solicite para acceder a Jupyter Notebook.

   **Necesidad**: Acceder a Jupyter Notebook desde tu navegador local facilita el desarrollo y la ejecución de tus notebooks en un entorno de nube.

## Consideraciones Adicionales

- **Permisos de Bucket de Google Cloud Storage**: Asegúrate de que la cuenta de servicio tenga los permisos necesarios para acceder al bucket y al archivo en Google Cloud Storage.
- **Seguridad**: Cierra el túnel SSH y detén Jupyter Notebook cuando no lo estés utilizando para evitar accesos no autorizados.

## Conclusión

Estos pasos te permiten configurar y ejecutar Jupyter Notebook en una VM de Google Cloud Platform, facilitando el análisis de datos y el desarrollo de modelos de machine learning en un entorno de nube seguro y accesible.
