---
title: Instalando o Apache 2.4 + PHP 7 + MariaDB
autor: Wilton Gonçalves
---
# Instalando o Apache 2.4 + PHP 7 + MariaDB (LAMP)

## Atualizando o sistema

```shell
sudo apt-get update && sudo apt-get -y upgrade && sudo apt-get -y dist-upgrade
```

## Instalando o MariaDB

MariaDB que é a versão Open Source do MySQL.
No terminal rode o comando abaixo, e informe sua senha, você pode deixá-la em branco no ambiente de desenvolvimento, mas lembre-se de utilizar uma senha segura no ambiente de produção.

```shell
sudo apt-get install mariadb-server
```

A dica abaixo é opcional no ambiente de desenvolvimento, mas é altamente recomendável que você execute o comando abaixo no servidor de produção.
O comando **mysql_secure_installation** é muito importante e deve ser usado no servidor de produção, o assistente irá nos guiar através de algumas opções que vem configuradas por padrão, mas são perigosas de se usar em no servidor de produção.

```shell
sudo mysql_secure_installation
```

Informe sua senha, se você deixou sua senha em branco, apenas tecle enter.
Esta é uma oportunidade para você mudar sua senha para algo seguro se você não tiver feito isso.
Você deve responder “Y” (Sim) para todas as questões restantes.
Pronto, agora nosso MySQL está pronto para uso.

## Instalando o Apache 2.4

```shell
sudo apt-get install apache2
```

Abra o navegador e acesse http://localhost ou http://seu.ip, a página padrão do Apache deve ser exibida.

## Rewrite Module

Para podermos utilizar URLs amigáveis devemos ativar o módulo rewrite do apache, a maioria dos frameworks PHP pedem que ele esteja ativo, após a ativação reinicie o apache.

```shell
sudo a2enmod rewrite
sudo systemctl restart apache2
```

## Instalando o PHP 7 e os módulos adicionais

```shell
sudo apt-get install libapache2-mod-php7.0 php7.0-mysql php7.0-curl php7.0-json php-memcached php7.0-dev php7.0-mcrypt php7.0-sqlite3 php7.0-mbstring
```

**Deixando o PHP mais seguro**

Vamos fazer uma pequena alteração na configuração do PHP para tornar nossa configuração mais segura.

Abra o arquivo /etc/php/7.0/apache2/php.ini com o nano e procure pela linha (ctrl + w) **cgi.fix_pathinfo**, ela está comentada por ";" e com valor setado para 1, descomente a linha e defina o valor para zero (0).

```shell
sudo nano /etc/php/7.0/apache2/php.ini
```

Deve ficar conforme abaixo

```
cgi.fix_pathinfo=0
```

Reinicie o Apache com o comando abaixo

```shell
sudo systemctl restart apache2
```

Seguindo a diante, agora crie um arquivo chamado **info.php**, execute o comando abaixo.

```shell
sudo nano /var/www/html/info.php
```

Copie e cole o código abaixo.

```php
<?php phpinfo();
```

Volte ao navegador e acesse http://localhost/info.php, muito feliz vendo uma página com informações do PHP7.

## Mcrypt

Outro requisito dos frameworks PHP é que a extensão mcrypt do PHP também esteja ativa, rode o comando abaixo e reinicie o apache novamente.

```shell
sudo phpenmod mcrypt
sudo systemctl restart apache2
```

### Dica

Para facilitar sua vida mude a permissão da pasta html, isso pode ser feito facilmente rodando o comando abaixo.

```shell
sudo chmod 777 /var/www/html
```

## Bônus 1: Instalar o XDebug

O XDebug é uma ferramenta indispensável para quem programa em PHP, o processo é um pouco diferente da instalação no LAMP.

Facilitei sua vida e resumi de forma simples e fácil a instalação do XDebug, basta rodar os comandos abaixo.

```shell
cd
wget http://xdebug.org/files/xdebug-2.5.0.tgz
tar -xvzf xdebug-2.5.0.tgz
cd xdebug-2.5.0
phpize
./configure
make
cp modules/xdebug.so /usr/lib/php/20151012
sudo echo 'zend_extension = /usr/lib/php/20151012/xdebug.so' >> /etc/php/7.0/apache2/php.ini
```

Reinice o Apache e voilá.

```shell
sudo systemctl restart apache2
```

Volte a pagina de informações, ctrl+f e procure por **xdebug support** e veja o XDebug está **enabled**

## Bônus 2: Instalar o Composer

Novamente, se você esta configurando um ambiente de desenvolvimento este passo é segundo presentinho para você.
Acho que nem preciso explicar o que é o Composer, se você programa em PHP certamente já sabe o que ele é, vamos instalá-lo globalmente para utilizarmos em qualquer lugar do nosso sistema.
Rode este comando gigante abaixo e Voilà.

```shell
curl -sS https://getcomposer.org/installer | php
sudo mv composer.phar /usr/local/bin/composer
```

Execute composer no terminal e veja que agora você pode utilizá-lo onde quiser.

## Conclusão

Finalizamos mais uma instalação, dessa vez configuramos nosso ambiente LAMP, instalamos tudo manualmente e deixamos tudo funcionando perfeitamente.

Essa dica é muito boa para quem não se sente a vontade com o nginx ou prefere o bom e velho LAMP.

Fontes:

https://matheuslima.com.br/instalando-o-apache-2-4-php-7-mysql-lamp/

http://www.edivaldobrito.com.br/como-instalar-o-xampp-no-linux/
