ASSIGNMENT 2

TASK 1 :- Setup a lamp server and host a wordpress site on your local system Note: Don't install php directly using yum or apt-get
compile it from source using PREFIX with /usr/local/php directory :-
1) Install Apache2
```
# sudo apt-get update
# sudo apt-get install apache2
```

2) Configure Apach2
```
# sudo apache2ctl configtest
# sudo nano /etc/apache2/apache2.conf
```

Append -  ServerName 192.168.33.16
```
# sudo apache2ctl configtest
# sudo systemctl restart apache2
```

Check - http://192.168.33.16

3) Install mysql
```
# sudo apt-get install mysql-server
# sudo apt-get install php libapache2-mod-php php-mcrypt php-# mysql
```

4) Configure the file
```
# sudo nano /etc/apache2/mods-enabled/dir.conf
```

Append -  
<IfModule mod_dir.c>
     DirectoryIndex index.html index.cgi index.pl index.php # index.xhtml index.htm
</IfModule>
<IfModule mod_dir.c>
    DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm
</IfModule>
```
# sudo systemctl restart apache2
# sudo systemctl status apache2
```




5) Configure this file

```
# sudo nano /var/www/html/info.php
```

<?php
phpinfo();
?>
6) Check on your local host
http://192.168.33.16/info.php

7) Create database and Grant the local host
```
# mysql -u root -p
```

mysql> CREATE DATABASE wordpress DEFAULT CHARACTER SET utf8 COLLATE utf8_unicode_ci;
mysql> GRANT ALL ON wordpress.* TO 'root'@'localhost' IDENTIFIED BY 'Love@1234';
mysql> FLUSH PRIVILEGES;
mysql> EXIT;

8) Install Additional PHP Extensions
```
# sudo apt-get update
# sudo apt-get install php-curl php-gd php-mbstring php-mcrypt php-xml php-xmlrpc
# sudo systemctl restart apache2
```

9) Adjust Apache's Configuration to Allow for .htaccess Overrides and Rewrites
```
# sudo nano /etc/apache2/apache2.conf
```

<Directory /var/www/html/>
    AllowOverride All
</Directory>
Enable the Rewrite Module
```
# sudo a2enmod rewrite
```

Enable the Changes
```
# sudo apache2ctl configtest
# sudo systemctl restart apache2
```


10) Download WordPress
```
# cd /tmp
# curl -O https://wordpress.org/latest.tar.gz
# tar xzvf latest.tar.gz
# touch /tmp/wordpress/.htaccess
# chmod 660 /tmp/wordpress/.htaccess
# cp /tmp/wordpress/wp-config-sample.php /tmp/wordpress/wp-# config.php
# mkdir /tmp/wordpress/wp-content/upgrade
# sudo cp -a /tmp/wordpress/. /var/www/html
```

11) Configure the WordPress Directory
```
# sudo chown -R root:www-data /var/www/html
# sudo find /var/www/html -type d -exec chmod g+s {} \;
# sudo chmod g+w /var/www/html/wp-content
# sudo chmod -R g+w /var/www/html/wp-content/themes
# sudo chmod -R g+w /var/www/html/wp-content/plugins
```

12) Setting up the WordPress Configuration File
```
# curl -s https://api.wordpress.org/secret-key/1.1/salt/
```

paste the output in:-
```
# nano /var/www/html/wp-config.php
```

13) Configure the changes
```
# sudo vi /var/www/html/wp-config.php
```

define('DB_NAME', 'wordpress');

/** MySQL database username */
define('DB_USER', 'localhost');

/** MySQL database password */
define('DB_PASSWORD', 'LOve@1234');

. . .

define('FS_METHOD', 'direct');

14) Complete the Installation Through the Web Interface
http://192.168.33.16
