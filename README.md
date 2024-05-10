# Installation

## Install Helm

```bash
curl https://baltocdn.com/helm/signing.asc | gpg --dearmor | sudo tee /usr/share/keyrings/helm.gpg > /dev/null
sudo apt-get install apt-transport-https --yes
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/helm.gpg] https://baltocdn.com/helm/stable/debian/ all main" | sudo tee /etc/apt/sources.list.d/helm-stable-debian.list
sudo apt-get update
sudo apt-get install helm
```

## Install ingress

```bash
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm repo update
```

```bash
helm install -f ./ingress_nginx/values.yaml ingress-nginx ingress-nginx/ingress-nginx --version "4.9.1" --create-namespace --namespace "ingress-nginx"
```
### Upgrade if required
```bash
helm upgrade -f ./ingress_nginx/values.yaml ingress-nginx ingress-nginx/ingress-nginx --version "4.9.1" --create-namespace --namespace "ingress-nginx"
```

## Install grafana