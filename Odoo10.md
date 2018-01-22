---
title: Instalação do Odoo 10 no Ubuntu 16.04 LTS
autor: Wilton Gonçalves
---
# Instalação do Odoo 10 no Ubuntu 16.04 LTS e variantes

## Passo a passo para instalação

A instalação será feita via terminal de comandos baixando o **Odoo** diretamente do **GitHub.**

### Passo 1

Atualize lista de fontes do sistema

```shell
sudo apt-get update
```

### Passo 2

Atualize o sistema

```shell
sudo apt-get upgrade
```

ou

```shell
sudo apt-get dist-upgrade
```

### Passo 3

Instale as dependências do Python para Odoo

```shell
sudo apt-get install python-dateutil python-docutils python-feedparser python-jinja2 python-ldap python-libxslt1 python-lxml python-mako python-mock python-openid python-psycopg2 python-psutil python-pybabel python-pychart python-pydot python-pyparsing python-reportlab python-simplejson python-tz python-unittest2 python-vatnumber python-vobject python-webdav python-werkzeug python-xlwt python-yaml python-zsi poppler-utils python-pip python-pypdf python-passlib python-decorator gcc python-dev mc bzr python-setuptools python-markupsafe python-reportlab-accel python-zsi python-yaml python-argparse python-openssl python-egenix-mxdatetime python-usb python-serial lptools make python-pydot python-psutil python-paramiko poppler-utils python-pdftools antiword python-requests python-xlsxwriter python-suds python-psycogreen python-ofxparse python-gevent
```

### Passo 4

Dependências do Odoo Web

```shell
sudo apt-get install -y npm
```

```shell
sudo ln -s /usr/bin/nodejs /usr/bin/node
```

```shell
sudo npm install -g less less-plugin-clean-css
```

### Passo 5

Instalando o PostgreSQL

```shell
sudo apt-get install python-software-properties
```
Você pode usar qualquer editor de texto de sua preferência, aqui foi utilizado o Nano

```shell
sudo nano /etc/apt/sources.list.d/pgdg.list
```

Adicione o repositório no arquivo que foi aberto:

```shell
deb http://apt.postgresql.org/pub/repos/apt/ xenial-pgdg main
```

No terminal digite o seguinte comando para adicionar a chave:

```shell
wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
```
Atualizando a lista dos repositórios e instalando

```shell
sudo apt-get update
```

```shell
sudo apt-get install postgresql-9.6
```

### Passo 6

Criando usuário do banco de dados para Odoo

```sh
sudo su postgres
```

```shell
cd
```

```shell
createuser -s odoo
```

```shell
createuser -s ubuntu_user_name
```

```shell
exit
```

### Passo 7

Criando usuário e grupo Odoo

```shell
sudo adduser --system --home=/opt/odoo --group odoo
```

### Passo 8

Instalando o GData

Biblioteca de clientes Python para API de dados do Google responsável pela leitura, escrita e modificação de informações na web.

```shell
cd /opt/odoo
```

Vá para o link "https://pypi.python.org/pypi/gdata" e baixe o gdata-2.0.18 e transfira o arquivo para o servidor.
Caso contrário, através do terminal, siga o passo abaixo:

```shell
wget https://pypi.python.org/packages/a8/70/bd554151443fe9e89d9a934a7891aaffc63b9cb5c7d608972919a002c03c/gdata-2.0.18.tar.gz
```

```shell
sudo tar zxvf gdata-2.0.18.tar.gz
```

```shell
sudo chown -R odoo: gdata-2.0.18
```

```shell
sudo -s
```

```shell
cd gdata-2.0.18/
```

```shell
python setup.py install
```

```shell
exit
```

### Passo 9

Download do Odoo via GitHub

Obtenha o último Odoo 10 do repositório github. Baixe o arquivo Zip do URL: "https://github.com/odoo/odoo/tree/10.0". Transfira o mesmo arquivo para o diretório /opt /odoo no servidor através do ftp. Caso contrário, siga a etapa abaixo

```shell
cd /opt/odoo
```

```shell
sudo wget https://github.com/odoo/odoo/archive/10.0.zip
```

```shell
sudo unzip 10.0.zip
```

```shell
sudo chown -R odoo: odoo-10.0
```

Ou clonar o Odoo via GitHub

```shell
git clone --depth=1 --branch=10.0 https://github.com/odoo/odoo.git /opt/odoo/odoo
```

```shell
sudo mv odoo/ odoo-10.0/
```

```shell
sudo chown -R odoo: odoo-10.0
```

### Passo 10

Criar arquivo de registro Odoo

```shell
sudo mkdir /var/log/odoo
```

```shell
sudo chown -R odoo:root /var/log/odoo
```

### Passo 11

Edite o arquivo de configuração de Odoo

```shell
sudo cp /opt/odoo/odoo-10.0/debian/odoo.conf /etc/odoo.conf
```

```shell
sudo chown odoo: /etc/odoo.conf
```

```shell
sudo nano /etc/odoo.conf
```

Copie e cole abaixo o conteúdo no arquivo de configuração, escreva caminhos de complementos corretos

```
[options]
; This is the password that allows database operations:
; admin_passwd = PASSWORD
db_host = False
db_port = False
db_user = odoo
db_password = False
addons_path = /opt/odoo/odoo-10.0/addons
;Log Settings
logfile = /var/log/odoo/odoo.log
log_level = error
```

### Passo 12

WKHTMLTOPDF é ferramenta de código aberto (LGPLv3) para renderizar HTML em PDF e vários formatos de imagem usando o mecanismo de renderização Qt WebKit.

Siga as etapas mencionadas abaixo para fazer a instalação.

#### Passo 12.1

Baixe a versão wkhtmltopdf de https://wkhtmltopdf.org/downloads.html obedecendo da versão do seu Sistema Operacional.

Ou baixe através do GitHub.

```shell
wget https://github.com/wkhtmltopdf/wkhtmltopdf/releases/download/0.12.4/wkhtmltox-0.12.4_linux-generic-amd64.tar.xz
```

#### Passo 12.2

Descompacte o arquivo

```shell
sudo tar -Jxf wkhtmltox-0.12.4_linux-generic-amd64.tar.xz
```

#### Passo 12.3

Copie wkhtmltoimage para /usr/bin localizado em /usr/local/bin usando o comando abaixo

```shell
sudo cp /opt/odoo/wkhtmltox/bin/wkhtmltoimage /usr/bin/wkhtmltoimage
```

#### Passo 12.4

Copie wkhtmltopdf para /usr/bin localizado em /usr/local/bin usando o comando abaixo

```shell
sudo cp /opt/odoo/wkhtmltox/bin/wkhtmltopdf /usr/bin/wkhtmltopdf
```

### Passo 13

Agora, inicie o servidor Odoo

```shell
cd /opt/odoo/odoo-10.0
```

```shell
./odoo-bin
```

### Passo 14

Abra um navegador Web de sua preferência para acessar o Odoo 10

```
http://localhost:8069
```

Traduzido de GETOPENERP

Fonte:

https://www.getopenerp.com/install-odoo-10-on-ubuntu-16-04/

https://odoobrasil.wordpress.com/2016/10/31/instalando-odoo-erp-localizacao-brasileira-linux/
