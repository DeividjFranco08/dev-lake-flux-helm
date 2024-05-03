# dev-lake-flux-helm
Repositorio para desplegar componentes en kubernetes por medio de flux

# Despliegue de aplicaciones con Helm Chart: Paso a paso
Helm es un administrador de paquetes para Kubernetes que simplifica el proceso de empaquetado, instalación y gestión de aplicaciones en clusters de Kubernetes.

# Paso 1: Crear un Helm Chart
Un Helm Chart es un paquete que contiene los recursos de Kubernetes necesarios para desplegar una aplicación. Para crear un Helm Chart, se suele usar la herramienta helm create.
--helm create <nombre-chart>
Por ejemplo, para crear un Helm Chart llamado mi-aplicacion, use el siguiente comando:
--helm create mi-aplicacion
Esto creará una estructura de directorios para su Helm Chart, incluyendo un archivo Chart.yaml que define la información meta del chart, un directorio templates que contiene los templates para los recursos de Kubernetes, y un archivo values.yaml que contiene los valores por defecto para los templates.

# Paso 2: Definir los Recursos de Kubernetes
En el directorio templates de su Helm Chart, cree los archivos YAML que definan los recursos de Kubernetes necesarios para su aplicación. Por ejemplo, si su aplicación necesita un Deployment, cree un archivo deployment.yaml con la siguiente estructura:

YAML
apiVersion: apps/v1
kind: Deployment
metadata:
  name: <nombre-deployment>
spec:
  replicas: <numero-replicas>
  selector:
    matchLabels:
      app: <nombre-aplicacion>
  template:
    metadata:
      labels:
        app: <nombre-aplicacion>
    spec:
      containers:
      - name: <nombre-contenedor>
        image: <imagen-docker>
        ports:
        - containerPort: <puerto-contenedor>


# Paso 3: Definir los Valores por Defecto
En el archivo values.yaml, defina los valores por defecto para los templates. Estos valores pueden ser sobrescritos durante la instalación del Helm Chart. Por ejemplo, para el template deployment.yaml, puede definir los siguientes valores por defecto en values.yaml:

YAML
nombre-aplicacion: mi-aplicacion
nombre-deployment: mi-aplicacion-deployment
numero-replicas: 3
imagen-docker: nginx:latest
puerto-contenedor: 80

# Paso 4: Empaquetar el Helm Chart
Una vez que haya definido los recursos de Kubernetes y los valores por defecto, puede empaquetar el Helm Chart usando el comando helm package:
--helm package <nombre-chart>
Esto creará un archivo .tgz que contiene todos los archivos necesarios para su Helm Chart.

# Paso 5: Instalar el Helm Chart en un Cluster de Kubernetes
Para instalar el Helm Chart en un cluster de Kubernetes, use el comando helm install:
--helm install <nombre-release> <nombre-chart> [options]
Por ejemplo, para instalar el Helm Chart que empaquetó en el paso anterior, use el siguiente comando:
--helm install mi-release mi-aplicacion.tgz
Esto creará los recursos de Kubernetes definidos en el Helm Chart en su cluster de Kubernetes.

# Paso 6: Actualizar el Helm Chart
Si necesita realizar cambios en su aplicación, puede actualizar el Helm Chart siguiendo estos pasos:
Edite los archivos en el directorio templates y/o values.yaml de su Helm Chart.
Empaquete el Helm Chart actualizado usando el comando helm package.
Actualice el Helm Chart en su cluster de Kubernetes usando el comando helm upgrade:
-- helm upgrade <nombre-release> <nombre-chart> [options]
Esto actualizará los recursos de Kubernetes en su cluster de Kubernetes para que coincidan con la versión actualizada del Helm Chart.

# Paso 7: Desinstalar el Helm Chart
Para desinstalar el Helm Chart de su cluster de Kubernetes, use el comando helm uninstall:
-- helm uninstall <nombre-release>
Esto eliminará los recursos de Kubernetes creados por el Helm Chart.