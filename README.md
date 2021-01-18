# iaw-practica-15

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



