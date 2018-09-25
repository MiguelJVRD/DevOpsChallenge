# Second Challenge

## Shell script para la instalacion del Kubernetes
```
#!/bin/bash

# Miguel Angel Jover Diaz, Devops Challenge, Second Challenge, 24/9/2019

```

#### Actualizamos los repositorios:
```
sudo apt-get update

sudo apt-get -y upgrade
```


#### Instalamos KOPS y sus dependencias:
```
 wget -O kops https://github.com/kubernetes/kops/releases/download/$(curl -s https://api.github.com/repos/kubernetes/kops/releases/latest | grep tag_name | cut -d '"' -f 4)/kops-linux-amd64

chmod +x kops

sudo mv kops /usr/local/bin/
```


#### Instalamos kubernetes:
```
curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl

chmod +x kubectl

sudo mv kubectl /usr/local/bin/
```


#### instalamos el AWS CLI:
```
sudo apt-get install python-pip

pip install --upgrade pip

sudo pip install awscli
```


#### configuramos el cliente de AWS con nuestras credenciales, region y formato por defecto:
```
aws configure
``` 




#### generamos unas claves de SSH para intercambiar:
```
ssh-keygen
```



#### creamos un bucket para guardar el estado del cluster:
```
aws s3 mb s3://kopsclusterdemo
```


#### Creamos el cluster:
```
kops create cluster --name=k8sclustersetup.tk --state=s3://kopsclusterdemo --zones=eu-west-2a --node-count=2 --node-size=t2.micro --master-size=t2.micro --dns-zone=k8sclustersetup.tk

kops update cluster k8sclustersetup.tk --yes --state=s3://kopsclusterdemo
```


#### creamos un Ingress Controller, elegimos NGINX:
##### https://github.com/nginxinc/kubernetes-ingress/tree/v1.3.0/helm-chart



#### nstalamos los prerequisitos: Helm
``` 
curl https://raw.githubusercontent.com/kubernetes/helm/master/scripts/get > get_helm.sh
chmod 700 get_helm.sh
./get_helm.sh
```

#### Inicializamos Helm
```
helm init
```
