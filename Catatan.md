# **Catatan Penting Q**


1. Netplan Ip Config
   Location ``` /etc/netplan/[tab_key] ```
   1. DHCP
      ```
      network:
        version: 2
        renderer: networkd
        ethernets:
            enp3s0:
            dhcp4: true
      ```
   2. Static
      ```
      network:
        version: 2
        renderer: networkd
        ethernets:
            enp3s0:
            addresses:
                - 10.10.10.2/24
            gateway4: 10.10.10.1
            nameservers:
                search: [mydomain, otherdomain]
                addresses: [10.10.10.1, 1.1.1.1]
      ```
   3. Multiple Gateway 
      ```
      network:
        version: 2
        renderer: networkd
        ethernets:
            enp3s0:
            addresses:
            - 9.0.0.9/24
            - 10.0.0.10/24
            - 11.0.0.11/24
            #gateway4:    # unset, since we configure routes below
            routes:
            - to: 0.0.0.0/0
                via: 9.0.0.1
                metric: 100
            - to: 0.0.0.0/0
                via: 10.0.0.1
                metric: 100
            - to: 0.0.0.0/0
                via: 11.0.0.1
                metric: 100
      ```
   4. Command 
      ```
      sudo netplan apply //apply changes
      sudo netplan try //test config
      ```
2. Apache Site Setting
   1. Config file
      ```
      <VirtualHost *:80>
           ServerAdmin webmaster@localhost
           ServerName example.com
           ServerAlias www.example.com
           
           DocumentRoot /var/www
           <Directory />
                   Options FollowSymLinks
                   AllowOverride None
           </Directory>
      <VirtualHost *:80>
      ```
   2. Apply Change
      ```
      sudo a2ensite virtual_host_file_name
      ```
3. Nginx Site Setting
4. Apache2 Laravel Htaccess 
   ```
   Options +FollowSymLinks -Indexes
   RewriteEngine On

   RewriteCond %{HTTP:Authorization} .
   RewriteRule .* - [E=HTTP_AUTHORIZATION:%{HTTP:Authorization}]

   RewriteCond %{REQUEST_FILENAME} !-d
   RewriteCond %{REQUEST_FILENAME} !-f
   RewriteRule ^ index.php [L]
   ```
5. Full Download Template
   ```
   wget \
    --recursive \
    --no-clobber \
    --page-requisites \
    --html-extension \
    --convert-links \
    --restrict-file-names=windows \
    --no-parent \
        site
   ```