# Installing CMS Ubuntu 18.04 
1.  ```sudo apt install apache2 mysql-server php libapache2-mod-php php-mysql```

2.  ```sudo mysql_secure_installation```
3.  ```sudo mysql```
    ```
    mysql> SELECT user,authentication_string,plugin,host FROM mysql.user;
    mysql> ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'passwordmu';
    mysql> FLUSH PRIVILEGES;
    ```
4.  ```mysql -u root -p```

5.  `sudo nano /etc/apache2/mods-enabled/dir.conf`

    ``` 
    <IfModule mod_dir.c>
        DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm
    </IfModule>
    ```
6.  `sudo systemctl restart apache2`
#### WORDPRESS
>7.  `wget https://wordpress.org/latest.zip`
>8.  `sudo apt install unzip`
>9.  `unzip latest.zip`
>10.  `sudo mv wordpress/ /var/www/html/`
#### DRUPAL
>7. `wget https://www.drupal.org/download-latest/zip`
>8. `unzip zip`
>9. `mv drupal-8.8.0/ drupal/`
>10. `mv drupal/ /var/www/html/`
#### Joomla
>7. `wget https://downloads.joomla.org/cms/joomla3/3-9-13/Joomla_3-9-13-Stable-Full_Package.zip\?format\=zip`
>8. `unzip Joomla_3-9-13-Stable-Full_Package.zip\?format=zip -d joomla`
>9. `mv joomla/ /var/www/html/`
11.   `sudo chmod 777 -R /var/www/`
12.   `sudo nano /etc/apache2/sites-available/bagas.com.conf`
        ```
        <VirtualHost *:80>
            ServerAdmin webmaster@localhost
            ServerName your_domain
            ServerAlias www.your_domain
            DocumentRoot /var/www/html/wordpress
            ErrorLog ${APACHE_LOG_DIR}/error.log
            CustomLog ${APACHE_LOG_DIR}/access.log combined
        </VirtualHost>
        ```
13.   `sudo a2ensite bagas.com.conf` 
14.   `systemctl reload apache2`
15.   `systemctl restart apache2`