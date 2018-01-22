---
title: Instalação do GRAV CMS
autor: Wilton Gonçalves
---
# Instalação do GRAV CMS

## Primeiro instale a ferrameta GIT e outras dependências:

```shell
sudo apt-get install git software-properties-common curl build-essential libyaml-dev
```

## Instale agora o servidor Apache:

```shell
sudo apt-get install apache2 apache2-utils
```

## Instale agora o PHP e os módulos:

```shell
sudo apt-get install php7.0 php7.0-fpm php7.0-cli php7.0-gd php7.0-mbstring php-pear php7.0-curl php7.0-dev php7.0-opcache php7.0-xml php7.0-json php7.0-zip php7.0-common libapache2-mod-php7.0 php-memcached php7.0-mcrypt
```

### Instale a dependência apcu do PHP:

```shell
sudo pecl install apcu
```
### Crie um arquivo chamado **apcu.ini** (Pode ser usado qualquer editor de texto de sua preferência)

```shell
sudo nano /etc/php/7.0/mods-available/apcu.ini
```
### Insira no arquivo recem criado a seguinte informação:

extension=apcu.so

### Instale agora o YAML

```shell
sudo pecl install yaml-2.0.0
```
### Crie um arquivo chamado **yaml.ini** (Pode ser usado qualquer editor de texto de sua prefeência)

```shell
sudo nano /etc/php/7.0/mods-available/yaml.ini
```
### Insira no arquivo recém criado a seguinte informação:

extension=yaml.so

## Execute os comandos abaixo:

```shell
sudo sh -c "echo extension=apcu.so > /etc/php/7.0/mods-available/apcu.ini"
sudo ln -s /etc/php/7.0/mods-available/apcu.ini /etc/php/7.0/fpm/conf.d/20-apcu.ini
sudo ln -s /etc/php/7.0/mods-available/apcu.ini /etc/php/7.0/cli/conf.d/20-apcu.ini
```

```shell
sudo service php7.0-fpm restart
```

```shell
sudo sh -c "echo extension=yaml.so > /etc/php/7.0/mods-available/yaml.ini"
sudo ln -s /etc/php/7.0/mods-available/yaml.ini /etc/php/7.0/fpm/conf.d/20-yaml.ini
sudo ln -s /etc/php/7.0/mods-available/yaml.ini /etc/php/7.0/cli/conf.d/20-yaml.ini
```

```shell
sudo service php7.0-fpm restart
```

## Instale o Composer:

```shell
sudo apt-get install composer
```

```shell
curl -sS https://getcomposer.org/installer | php
```
### Mova o Composer para o seguinte diretório:

```shell
sudo mv composer.phar /usr/local/bin/composer
```

### Crie um arquivo chamado de www-data.conf

```shell
sudo nano /etc/php/7.0/fpm/pool.d/www-data.conf
```

#### Salve as seguintes informações nele:

[www-data]
user = www-data
group = www-data
listen = /var/run/php-fpm-www-data.sock
listen.owner = www-data
listen.group = www-data
listen.mode = 0666
pm = ondemand
pm.max_children = 5
pm.process_idle_timeout = 10s
pm.max_requests = 200
chdir = /

## Habilitando o módulo rewrite.load no Apache:

```shell
sudo a2enmod rewrite
```

```shell
sudo systemctl restart apache2
```

## Altere o arquivo de configuração do Apache, para consolidar o uso da "URL amigável".

```shell
sudo nano /etc/apache2/apache2.conf
```
Encontre o seguinte código:

<Directory /var/www/>
   Options Indexes FollowSymLinks
   AllowOverride None
   Require all granted
</Directory>

Atere para:

<Directory /var/www/>
   Options Indexes FollowSymLinks
   AllowOverride All
   Require all granted
</Directory>

## Reinicie o serviço do Apache:

```shell
sudo systemctl restart apache2
```

## Altere a permição do diretório:

```shell
sudo chmod 777 /var/www/html
```
## Execute os comandos abaixo:

```shell
sudo a2enmod proxy proxy_fcgi rewrite
sudo a2enconf php7.0-fpm
sudo systemctl restart apache2
```
## Agora copie e descompacte o Grav + Admin no diretório

/var/www/html

Execute o comando:

```shell
sudo chown -R www-data: /var/www/html/grav/
```

Abra seu navegador e digite na barra de endereço:

localhost/grav

E siga os passos para cofiguração do CMS.
