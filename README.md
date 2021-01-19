# iaw-practica-15
# 1 Práctica 15: Instalación de WordPress usando contenedores Docker
En esta práctica tendremos que realizar la implantación de un sitio WordPress en Amazon Web Services (AWS) haciendo uso de contenedores Docker.

## 1.1 Tareas a realizar
#### A continuación se describen muy brevemente algunas de las tareas que tendrá que realizar.

#### Crear una máquina virtual Amazon EC2.

#### Instalar y configurar Docker y Docker compose en la máquina virtual.

#### Crear un archivo docker-compose.yml para poder desplegar los servicios de WordPress, MySQL y phpMyAdmin. Deberá utilizar las imágenes oficiales de Docker Hub.

Busque cuál es la dirección IP pública de su instancia y compruebe que puede acceder a los servicios de WordPress y phpMyAdmin desde una navegador web.

sudo apt update

sudo apt install docker 

sudo apt install docker-compose

sudo usermod -aG docker $USER

sudo systemctl enable docker

sudo systemctl start docker

sudo reboot

docker network create wordpress-net

docker run -d \
--rm \
--name mysqlc \
--network wordpress-net \
-p 3306:3306 \
-e MYSQL_ROOT_PASSWORD=root \
-e MYSQL_DATABASE=wp_database \
-e MYSQL_USER=wp_user \
-e MYSQL_PASSWORD=wp_password \
-v wordpress_mysql_data:/var/lib/mysql \
mysql:5.7.28

docker run -d \
--rm \
--network wordpress-net \
-e PMA_ARBITRARY=1 \
-p 8080:80 \
phpmyadmin/phpmyadmin

docker run -d \
--rm \
--name wordpressc \
--network wordpress-net \
-p 80:80 \
-e WORDPRESS_DB_HOST=mysqlc \
-e WORDPRESS_DB_NAME=wp_database \
-e WORDPRESS_DB_USER=wp_user \
-e WORDPRESS_DB_PASSWORD=wp_password \
-v wordpress_data:/var/www/html \
wordpress



