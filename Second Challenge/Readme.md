# Second Challenge

## Shell script para la instalación del Kubernetes
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

kubeadm init

sudo kubectl apply -f https://docs.projectcalico.org/v2.6/getting-started/kubernetes/installation/hosted/kubeadm/1.6/calico.yaml
```


#### Instalamos el AWS CLI:
```
sudo apt-get install python-pip

pip install --upgrade pip

sudo pip install awscli
```


#### Configuramos el cliente de AWS con nuestras credenciales, region y formato por defecto:
```
aws configure
``` 




#### Generamos unas claves de SSH para intercambiar:
```
ssh-keygen
```



#### Creamos un bucket para guardar el estado del cluster:
```
aws s3 mb s3://kopsclusterdemo
```


#### Creamos el cluster:
```
kops create cluster --name=k8sclustersetup.tk --state=s3://kopsclusterdemo --zones=eu-west-2a --node-count=2 --node-size=t2.micro --master-size=t2.micro --dns-zone=k8sclustersetup.tk

kops update cluster k8sclustersetup.tk --yes --state=s3://kopsclusterdemo
```


## Creamos un Ingress Controller, elegimos NGINX:




#### Instalamos los prerequisitos: Helm
``` 
curl https://raw.githubusercontent.com/kubernetes/helm/master/scripts/get > get_helm.sh
chmod 700 get_helm.sh
./get_helm.sh
```

#### Inicializamos Helm
```
helm init
```
#### Instalamos los prerequisitos: Git

```
apt-get install git
```

#### Instalamos el Chart del NGINX, para ello clonamos el repositorio del Ingress Controller

```
git clone git@github.com:nginxinc/kubernetes-ingress.git
```

#### Cambiamos al directorio de trabajo /helm-chart:

```
cd kubernetes-ingress/helm-chart
```

#### Ponemos un nombre a la versión

```
helm install --name Mi-Version .
```

#### Desplegamos un servidor web
```
kubectl create deployment nginx --image=nginx
```
#### Lo ponemos accesible desde internet por el puerto 80
```
kubectl create service nodeport nginx --tcp=80:80
```

