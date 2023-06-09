# ArgoCd 
This is a condensed summary from [argocd - getting started](https://argo-cd.readthedocs.io/en/stable/getting_started/)

##Installation

Create a namespace _argocd_ and install argocd into this namespace

```sh
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```


##Download with Curl
```sh
curl -sSL -o argocd-linux-amd64 https://github.com/argoproj/argo-cd/releases/latest/download/argocd-linux-amd64
sudo install -m 555 argocd-linux-amd64 /usr/local/bin/argocd
rm argocd-linux-amd64
```

###Download for Windows
You can view the latest version of Argo CD at the link above or run the following command to grab the version:
```ps1
$version = (Invoke-RestMethod https://api.github.com/repos/argoproj/argo-cd/releases/latest).tag_name
```
Download ArgoCd
```ps1
$url = "https://github.com/argoproj/argo-cd/releases/download/" + $version + "/argocd-windows-amd64.exe"
$output = "argocd.exe"

Invoke-WebRequest -Uri $url -OutFile $output
```

##Access ArgoCd API Server
Change argocd-server service type to LoadBalancer

```sh
kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'
```

###Restarting  ArgoCd Pods
```sh
kubectl -n argocd delete pods --selector app.kubernetes.io/name=argocd-server
```

##Helm Charts
```sh
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo add grafana https://grafana.github.io/helm-charts
helm repo add loki https://grafana.github.io/loki/charts
helm repo update
```
