# Bind 9 Ubuntu 18.04
1. `sudo apt-get install bind9 bind9utils bind9-doc`
2. `sudo nano /etc/default/bind9`
    ```
    RESOLVCONF=no
    OPTIONS="-u bind -4"
    ```
1. `sudo nano /etc/bind/named.conf.options`
    ```
    forwarders {
	   8.8.8.8;
	   8.8.4.4;
	};
    ```
2. `sudo nano /etc/bind/named.conf.local`
    ```
    zone "bagas.com" {
        type master;
        file "/etc/bind/zones/db.bagas.com";
    };

    zone "192.168.in-addr.arpa" {
        type master;
        file "/etc/bind/zones/db.192.168";
    };
    ```
3. `mkdir /etc/bind/zones/`
4. `sudo mkdir /etc/bind/zones/`
5. `sudo cp /etc/bind/db.local /etc/bind/zones/db.bagas.com`
6. `nano /etc/bind/zones/db.bagas.com`
    ```
    ;
    ; BIND data file for local loopback interface
    ;
    $TTL	604800
    @	IN	SOA	bagas.com. root.bagas.com. (
                    2		; Serial
                604800		; Refresh
                86400		; Retry
                2419200		; Expire
                604800 )	; Negative Cache TTL
    ;
    @	IN	NS	bagas.com.
    @	IN	A	192.168.56.104
    www IN  A	192.168.56.104
    mail    IN  A	192.168.56.104
    1w  IN  MX  10  mail.bagas.com
    ```
7. `sudo cp /etc/bind/db.127 /etc/bind/zones/db.192.168`
8.  `sudo nano /etc/bind/zones/db.192.168`
    ```
    ;
    ; BIND reverse data file for local loopback interface
    ;
    $TTL	604800
    @	IN	SOA	bagas.com. root.bagas.com. (
                    1		; Serial
                604800		; Refresh
                86400		; Retry
                2419200		; Expire
                604800 )	; Negative Cache TTL
    ;
    @	IN	NS	ns.bagas.com.
    1.0.0	IN	PTR	bagas.com.
    @	IN	A	192.168.56.104
    www	IN	A	192.168.56.104
    ```
9.  `named-checkconf`
10. `named-checkzone bagas.com /etc/bind/zones/db.bagas.com`
11. `named-checkzone 192.168.in-addr.arpa /etc/bind/zones/db.192.168`
12. `sudo systemctl restart bind9`