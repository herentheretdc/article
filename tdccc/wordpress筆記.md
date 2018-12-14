# Wordpress安裝筆記

```
sudo apt-get update
sudo apt-get install apache2
sudo apt-get install mariadb-server
sudo mysql -u root -p #password empty
	CREATE DATABASE wordpress;
	CREATE USER 'user'@'localhost' IDENTIFIED BY 'password';
	GRANT ALL PRIVILEGES ON wordpress . * TO 'user'@'localhost';
	FLUSH PRIVILEGES;
	exit;
sudo apt-get install php libapache2-mod-php php-mcrypt php-mysql

sudo a2enmod ssl rewrite php7.0
sudo echo "<?php phpinfo(); ?>" > /var/www/html/index.php

apache2ctl configtest
> Syntax Ok

service apache2 restart

curl localhost/index.php

curl -O "https://tw.wordpress.org/wordpress-4.9-zh_TW.zip"

unzip wordpress-4.9-zh_TW.zip
#sudo apt-get install unzip

sudo mv wordpress /var/
sudo chown -R www-data:www-data
```
