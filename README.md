# dev-lake-flux-helm
Repositorio para desplegar componentes en kubernetes por medio de flux


# INSTALACIÓN DE DEVLAKE PASO A PASO
1. Instale la última versión estable con el nombre de la versión devlake

helm repo add devlake https://apache.github.io/incubator-devlake-helm-chart
helm repo update
ENCRYPTION_SECRET=$(openssl rand -base64 2000 | tr -dc 'A-Z' | fold -w 128 | head -n 1)
helm install devlake devlake/devlake --set lake.encryptionSecret.secret=$ENCRYPTION_SECRET

2. Instale la última versión de desarrollo con el nombre de la versión:devlake

helm repo add devlake https://apache.github.io/incubator-devlake-helm-chart
helm repo update
ENCRYPTION_SECRET=$(openssl rand -base64 2000 | tr -dc 'A-Z' | fold -w 128 | head -n 1)
helm install devlake devlake/devlake --version=1.0.0-beta6 --set lake.encryptionSecret.secret=$ENCRYPTION_SECRET

Si está utilizando minikube dentro de su Mac, use el siguiente comando para reenviar el puerto:
kubectl port-forward service/devlake-ui  30090:4000

y abrir otra terminal:
kubectl port-forward service/devlake-grafana  30091:3000

A continuación, puedes visitar: config-ui por url grafana por url http://YOUR-NODE-IP:30090http://YOUR-NODE-IP:30091

# AGREGAR REPOSITORIOS HELM PASO A PASO

1. Agregar el repositorio de Helm:
helm repo add <nombre-repositorio> <url-repositorio>

2. Crear un Helm release:

flux create helm release <nombre-release> \
  --chart <nombre-chart> \
  --namespace <nombre-namespace> \
  --values <ruta-archivo-values> \
  --repository <nombre-repositorio>

3. Aplicar los cambios:

flux reconcile workspaces

# EXPLICACION DE COMANDOS

helm repo add: Este comando se utiliza para agregar el repositorio de Helm que contiene el chart que desea instalar. Reemplace <nombre-repositorio> con un nombre único para el repositorio y <url-repositorio> con la URL del repositorio.

flux create helm release: Este comando se utiliza para crear un Helm release en su clúster de Kubernetes. Reemplace <nombre-release> con el nombre que desea dar al release, <nombre-chart> con el nombre del chart que desea instalar, <nombre-namespace> con el namespace en el que desea instalar el chart, <ruta-archivo-values> con la ruta del archivo helm_values que contiene los valores personalizados para la instalación, y <nombre-repositorio> con el nombre del repositorio que agregó en el paso 1.

flux reconcile workspaces: Este comando se utiliza para aplicar los cambios a su clúster de Kubernetes. Flux reconciliará el estado actual de su clúster con el estado deseado que se define en sus manifests.

# EJEMPLO

Supongamos que tiene un chart de Helm llamado my-chart en un repositorio llamado my-repo ubicado en la URL https://my-repo.example.com. También tiene un archivo helm_values llamado values.yaml que contiene los valores personalizados para la instalación. Para instalar este chart en un namespace llamado default, puede usar los siguientes comandos:

helm repo add my-repo https://my-repo.example.com
flux create helm release my-release --chart my-chart --namespace default --values values.yaml --repository my-repo
flux reconcile workspaces

Estos comandos agregarán el repositorio my-repo a su clúster de Kubernetes, crearán un Helm release llamado my-release en el namespace default utilizando el chart my-chart y los valores personalizados en el archivo values.yaml, y luego aplicarán los cambios a su clúster.

Consideraciones adicionales:

Asegúrese de tener Flux instalado y configurado en su clúster de Kubernetes antes de ejecutar estos comandos.
Si desea instalar un chart de Helm que no está en un repositorio público, deberá agregar el chart a su clúster de Kubernetes antes de poder crear un Helm release.
Puede encontrar más información sobre Flux en la documentación oficial: https://fluxcd.io/
