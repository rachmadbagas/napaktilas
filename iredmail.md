# Iredmail Ubuntu 18.04
1. `sudo hostnamectl set-hostname mx.bagas.com`
2. `sudo nano /etc/hostname`
   ```
   mx
   ```
3. `sudo nano /etc/hosts`
   ```
   127.0.0.1 mx.bagas.com mx localhost localhost.localdomain
   ```
4. `hostname -f`
5. `sudo apt install gzip`
6. `wget https://github.com/iredmail/iRedMail/archive/1.0.tar.gz`
7. `tar xf 1.0.tar.gz`
8. `cd iRedMail-1.0/`
9.  `sudo bash iRedMail.sh`
10. `sudo reboot`
