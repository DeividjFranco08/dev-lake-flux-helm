# Instalación

## Instalación de Helm
Ejecute los comando a continuación para instalar Helm, herramienta que nos permitira crear un chart para la aplicación de devlake, para mas información consulte la documentación: https://helm.sh/docs/intro/install/

```bash
curl https://baltocdn.com/helm/signing.asc | gpg --dearmor | sudo tee /usr/share/keyrings/helm.gpg > /dev/null
sudo apt-get install apt-transport-https --yes
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/helm.gpg] https://baltocdn.com/helm/stable/debian/ all main" | sudo tee /etc/apt/sources.list.d/helm-stable-debian.list
sudo apt-get update
sudo apt-get install helm
```

## Instalación de ingress
Ejecute los siguientes comandos para añadir el repositorio de nombre "ingress-ngnix" que va apubntar a la url: https://kubernetes.github.io/ingress-nginx la cual contiene el ingress-nginx. Luego se actualiza el repositorio para sincronizar los repositorios locales con el nuevo: 

```bash
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm repo update
```
Ahora instale el chart ejecutando el comando a continuación, donde se le indica que va instalar una aplicación llamada "ingress-nginx" que nace del repositorio ingress-nginx, utilizando el chart llamado "ingress-nginx" indicando la versión, el archivo de values para la configuración del chart y la creación de un namespace: helm install [NAME] [CHART] [flags]

```bash
helm install -f ./ingress_nginx/values.yaml ingress-nginx ingress-nginx/ingress-nginx --version "4.9.1" --create-namespace --namespace "ingress-nginx"
```

### Upgrade if required
comando para actualizar o re despliegue el servicio que ya se instalo 
```bash
helm upgrade -f ./ingress_nginx/values.yaml ingress-nginx ingress-nginx/ingress-nginx --version "4.9.1" --create-namespace --namespace "ingress-nginx"
```

### Get temnplates
```bash
helm template ingress-nginx ingress-nginx/ingress-nginx --version "4.9.1" -f ./ingress_nginx/values.yaml > mysql-manifest.yaml
```


## Install grafana

```bash
helm repo add ingress-nginx https://grafana.github.io/helm-charts
helm repo update
```
```bash
helm install -f ./grafana/values.yaml grafana/grafana --version "7.3.0" --create-namespace --namespace "grafana"
```
