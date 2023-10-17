# frappe-setup on ubuntu

### create new user on ubuntu :

    sudo adduser masoud
    sudo usermod -aG sudo masoud
    su - masoud
    sudo whoami


### Version 15/Nightly:
#### Python 3.10 or Python 3.11
    sudo apt install git  python-pip redis-server -y


### MariaDB 10.6.6+
    sudo apt install software-properties-common -y
    sudo apt autoremove -y
    sudo apt-get update
    sudo apt-get install mariadb-server -y
    sudo mysql_secure_installation
    sudo apt install mariadb-client-10.6
    sudo nano /etc/mysql/my.cnf

### add thses texts :
    [mysqld]
    character-set-client-handshake = FALSE
    character-set-server = utf8mb4
    collation-server = utf8mb4_unicode_ci
    
    [mysql]
    default-character-set = utf8mb4

#### then
    service mysql restart


### Install Node.js 18

    curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
    source ~/.bashrc
    nvm install 18
    node -v


#### Redis 6                                       (caching and realtime updates)


### yarn 1.12+                                    (js dependency manager)
    npm install -g yarn

### pip 20+                                       (py dependency manager)
    sudo apt update
    sudo apt install python3-pip -y
    pip3 --version
    sudo apt install python3.10-venv -y

### wkhtmltopdf (version 0.12.5 with patched qt)  (for pdf generation)
    sudo apt-get install xvfb libfontconfig wkhtmltopdf -y

### cron                                          (bench's scheduled jobs: automated certificate renewal, scheduled backups)

### NGINX                                         (proxying multitenant sites in production)

### Frappe bench:
    sudo -H pip3 install frappe-bench

#### close terminal and reopen it

    bench --version

### initial frappe :
    cd ~
    bench init frappe-bench
    cd frappe-bench

### add new site :
    bench new-site mydomain.com
    bench --site mydomain.com add-to-hosts


#### then 
    add 'vm.overcommit_memory = 1' to /etc/sysctl.conf and then reboot or run the command 'sysctl vm.overcommit_memory=1' for this to take effect.

## on development
    bench start


now its accessable on mydomain.com:8000

##  setup production:

    sudo bench setup production masoud
    sudo bench use mydomain.com

    sudo bench restart

#### (masoud is the user that we are working with right now)

    sudo chmod o+x /home/masoud

### again

    sudo bench setup production masoud
    sudo bench use mydomain.com

    sudo bench restart

### how to set ssl

    bench config dns_multitenant on
    sudo apt install certbot -y
    sudo -H bench setup lets-encrypt [site-name]



#### to get backup
    bench backup

#### to restore
    bench restore


## to see frappe services and jobs :
    supervisorctl status
