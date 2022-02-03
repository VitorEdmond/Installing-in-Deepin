# Installing-in-Deepin
Passo a Passo de Instala;'ao, para inicio de um novo projeto no Sistema Linux Deepin
Te
### 01 - Init PHP
#### 1.1 - Updating System
```sh
sudo apt update
sudo apt -y upgrade
sudo reboot
```
#### 1.2 - Install Repository 
```sh
sudo apt install -y software-properties-common
echo "deb https://packages.sury.org/php/ buster main" | sudo tee /etc/apt/sources.list.d/sury-php.list
wget -qO - https://packages.sury.org/php/apt.gpg | sudo apt-key add -
```
#### 1.3 - Install PHP and extension
```sh
sudo apt install php8.1
sudo apt install php8.1-{mysql,intl,ldap,gd,cli,bz2,curl,mbstring,pgsql,opcache,soap,cgi,xml}
```
#
### 02 - Init Composer
#### 2.1 - Install packge composer
```sh
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
php -r "if (hash_file('sha384', 'composer-setup.php') === '906a84df04cea2aa72f40b5f787e49f22d4c2f19492ac310e8cba5b96ac8b64115ac402c8cd292b8a03482574915d1a8') { echo 'Installer verified'; }else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
php composer-setup.php
php -r "unlink('composer-setup.php');"
sudo mv composer.phar /usr/local/bin/composer
```
#
### 03 - Init PostgreSQL
#### 3.1 - Instalando PostgreSQL
```sh
sudo apt update
sudo apt install postgresql postgresql-contrib
```
#### 3.2 - Create User
```sh
sudo -i -u postgres
CREATE USER nomedousuario SUPERUSER INHERIT CREATEDB CREATEROLE; 
ALTER USER nomedousuario PASSWORD 'senha';
```
#
### 04 - Init PHPStorm
#### 4.1 - Doing Download
<a href="https://download.jetbrains.com/webide/PhpStorm-2021.3.2.tar.gz?_gl=1*1t4ryre*_ga*MTMwMTA3OTIzMy4xNjQzNjYwNzQy*_ga_V0XZL7QHEB*MTY0MzY2MDc0MS4xLjEuMTY0MzY2MDc2OC4w&_ga=2.90021019.165695
8173.1643660742-1301079233.1643660742" target="_blank">Download PHPStorm</a>
#### 4.2 - Unzipping
```sh
sudo tar -xvzf PhpStorm-2021.3.2.tar.gz -C /opt
cd /opt/PhpStorm/bin 
./phpstorm.sh
```
#### 4.3 - Creating shortcut
```sh
Na tela de boas-vindas, clique em Configurar | Criar entrada na área de trabalho
```
#
### 05 - Init NVM
#### 5.1 - Install NVM
```sh
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
```
#### 5.2 - In another Terminal, run
```sh
nvm install node
nvm install-latest-npm
```
### Install Git
```sh
sudo apt install git
```
### Install Git Desktop
#### To setup the package repository, run these commands:
```sh
wget -qO - https://packagecloud.io/shiftkey/desktop/gpgkey | sudo tee /etc/apt/trusted.gpg.d/shiftkey-desktop.asc > /dev/null
sudo sh -c 'echo "deb [arch=amd64] https://packagecloud.io/shiftkey/desktop/any/ any main" > /etc/apt/sources.list.d/packagecloud-shiftkey-desktop.list'
sudo apt-get update
```
#### Then install GitHub Desktop:
```sh
sudo apt install github-desktop
```
# Iniciando um Projeto
### 01 - Init Project Laravel
#### Local
```sh
composer create-project laravel/laravel {nome_projeto}
```
dfsfdfdsf
#
### 02 - Init Tailwind
```sh
npm install -D tailwindcss
npx tailwindcss init
```
#### 2.1 Install packge for tailwind
```sh
npm install @tailwindcss/line-clamp
npm install @tailwindcss/aspect-ratio
npm install @tailwindcss/forms
npm install -D @tailwindcss/typography
```
#### 2.2 - Configure archive tailwind.config.js
```sh
module.exports = {
  content: [
    './src/**/*.{html,js}',
    './vendor/wireui/wireui/resources/**/*.blade.php',
    './vendor/wireui/wireui/ts/**/*.ts',
    './vendor/wireui/wireui/src/View/**/*.php'
  ],
  theme: {
    // ...
  },
  plugins: [
    require('@tailwindcss/typography'),
    require('@tailwindcss/forms')
    require('@tailwindcss/line-clamp')
    require('@tailwindcss/aspect-ratio')
  ],
}
```
#### 2.3 - Configure archive app.css in resource
```sh
@tailwind base;
@tailwind components;
@tailwind utilities;
```
#
### 03 - Configure WireUI
#### 3.1 - Install packge WireUI
```sh
composer require wireui/wireui
```
#### 3.2 - Configure archive blade
```sh
<body>
  ...
  
  @wireUiScripts
  <script src="//unpkg.com/alpinejs"></script>
</body>
</html>
```
#
### 04 - Configure Livewire
#### Install packge Livewire
```sh
composer require livewire/livewire
```
#### Include the JavaScript
```sh
...
    @livewireStyles
</head>
<body>
    ...
 
    @livewireScripts
</body>
</html>
```
