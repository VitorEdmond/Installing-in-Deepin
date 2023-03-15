# Installing-in-Deepin
Passo a Passo de Instalação, para inicio de um novo projeto no Sistema Linux Deepin
#
### - Init PHP

#### - Updating System
```sh
sudo apt update
sudo apt -y upgrade
sudo reboot
```

#### - Install Repository 
```sh
sudo apt update
sudo apt install -y lsb-release ca-certificates apt-transport-https software-properties-common
echo "deb https://packages.sury.org/php/  buster main" | sudo tee /etc/apt/sources.list.d/sury-php.list
sudo wget -qO - https://packages.sury.org/php/apt.gpg | sudo apt-key add -
```

#### Install PHP
```sh
sudo apt update
sudo apt install php8.1
```

### Check installed version
```sh
php -v
```

### Install extension
```sh
sudo apt install php8.1-{mysql,intl,ldap,gd,cli,bz2,curl,mbstring,pgsql,opcache,soap,cgi,xml,fpm,zip}
```

### - Init Composer
#### - Install packge composer
```sh
sudo php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
sudo php -r "if (hash_file('sha384', 'composer-setup.php') === '55ce33d7678c5a611085589f1f3ddf8b3c52d662cd01d4ba75c0ee0459970c2200a51f492d557530c71c15d8dba01eae') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
sudo php composer-setup.php
sudo php -r "unlink('composer-setup.php');"
sudo mv composer.phar /usr/local/bin/composer
```


### - Init PHPStorm
#### - Doing Download

<a href="https://www.jetbrains.com/toolbox-app/download/download-thanks.html?platform=linux" target="_blank">Download TootlBox</a>

#### - Unzipping

```sh
sudo tar -xvzf jetbrains-toolbox-{version} -C /opt
cd /opt/jetbrains-toolbox-{version}
./jetbrains-toolbox
```

#### - Creating shortcut
```sh
Na tela avance até chegar no instalador do PHP Storm
```
#
### - Init NVM

#### - Install NVM
```sh
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
```
#### - In another Terminal, run
```sh
nvm install node
nvm install-latest-npm
```
#
### - Init NGINX
#### - Install NGINX(Lembre de parar o Apache primeiro : systemctl stop apache2.service)
```sh
sudo apt install nginx-full
```
### - Configure NGINX
##### - Acesse o arquivo default em sites enable
```sh
sudo nano /etc/nginx/sites-enable/default
```
##### - Configuring Default NGINX File:
WARNING: {php_version}, {server_domain_or_IP}, {project_name}
```sh
server {
    listen 80;
    server_name {server_domain_or_IP};
    root /var/www/{project_name}/public;

    add_header X-Frame-Options "SAMEORIGIN";
    add_header X-XSS-Protection "1; mode=block";
    add_header X-Content-Type-Options "nosniff";

    index index.html index.htm index.php;

    charset utf-8;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location = /favicon.ico { access_log off; log_not_found off; }
    location = /robots.txt  { access_log off; log_not_found off; }

    error_page 404 /index.php;

    location ~ \.php$ {
        fastcgi_pass unix:/var/run/php/php{php_version}-fpm.sock;
        fastcgi_index index.php;
        fastcgi_param SCRIPT_FILENAME $realpath_root$fastcgi_script_name;
        include fastcgi_params;
    }

    location ~ /\.(?!well-known).* {
        deny all;
    }
}
```
##### - Validating default NGINX file
```sh
sudo nginx -t
```
##### - Command Exit
```sh
Outputnginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful
```
##### - Restart NGINX
```sh
sudo systemctl reload nginx
```
#### - Config Hosts
```sh
sudo nano /etc/hosts
```
#### - Change to first lines
```sh
127.0.0.1           localhost
127.0.0.1           *.localhost

etc......
```

#
### - Init Git
##### - Install Git
```sh
sudo apt install git
```
#### - Configure Git
```sh
git config --global user.name "Fulano de Tal"
git config --global user.email fulanodetal@exemplo.pt
```
#### - Generating a new SSH key
