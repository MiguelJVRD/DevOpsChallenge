# DevOps Challenge
## First Challenge
#### 1.- Se indica que no ha de ser necesario instalar nada, asi que o lo vemos desde el interfaz web del portal de amazon, que ya no seria un # script, o necesitamos al menos tener instalado el cliente "AWS CLI" y configurarlo para nuestra cuenta.

#### Para instalar el cliente de linea de comandos "AWS CLI":

#### Actualizamos el repositorio:
```
sudo apt-get update
sudo apt-get -y upgrade
```
# Instalamos las dependencias y el propio cliente:
sudo apt-get install python-pip
pip install --upgrade pip
sudo pip install awscli

# 2.-Es necesario crearnos una cuenta de tipo Crear un usuario de AWS IAM con rol "Programmatic access" (Acceso mediante programación)
# Con dicha cuenta necesitamos obtener un fichero .CSV con nuestras credenciales para acceso mediante programación:
# Download Credentials (Descargar credenciales)

# Abrimos nuestra consola y ejecutamos:

 aws configure

#  y pulse Intro. Cuando se le pida, introduzca lo siguiente:

# AWS Access Key ID [None]: Introduzca la ID de clave de acceso del archivo credentials.csv que ha descargado en el apartado d del paso 1.

# Nota: Debería tener un aspecto similar a AKIAPWINCOKAO3U4FWTN.

# AWS Secret Access Key [None]: Introduzca la clave de acceso secreta del archivo credentials.csv que ha descargado en el apartado d del paso 1.

# Nota: Debería tener un aspecto similar a 5dqQFBaGuPNf5z7NhFrgou4V5JJNaWPy1XFzBfX3.

# Default region name [None]: Introduzca la region de nuestras maquinas ejemplo: us-east-1.

# Default output format [None]: Introduzca json.

# Despues utilizaremos nuestro script llamado

bucket_data.sh.txt


lo invocamos con:
sh ./bucket_data.sh.txt
