# Instalação do Odoo 11 no Ubuntu 18.04 LTS e variantes

## Passo a passo para instalação

A instalação será feita via terminal de comandos baixando o **Odoo** diretamente do **GitHub.**

### Passo 1

Atualize lista de fontes do sistema

```shell
sudo apt update
```

### Passo 2

Atualize o sistema

```shell
sudo apt full-upgrade -y
```

### Passo 3

Instale as dependências do Python para Odoo

```shell
sudo apt install -y python3-pip
```

Instale as dependências PIP3

```
pip3 install Babel decorator docutils ebaysdk feedparser gevent greenlet html2text Jinja2 lxml Mako MarkupSafe mock num2words ofxparse passlib Pillow psutil psycogreen psycopg2 pydot pyparsing PyPDF2 pyserial python-dateutil python-openid pytz pyusb PyYAML qrcode reportlab requests six suds-jurko vatnumber vobject Werkzeug XlsxWriter xlwt xlrd
```

### Passo 4

Dependências do Odoo Web

```shell
sudo apt install -y npm
```

```shell
sudo ln -s /usr/bin/nodejs /usr/bin/node
```

```shell
sudo npm install -g less less-plugin-clean-css
```

```shell
sudo apt install -y node-less
```

### Passo 5

Instalando o PostgreSQL e criando usuário do banco de dados para Odoo

```sh
sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt/ `lsb_release -cs`-pgdg main" >> /etc/apt/sources.list.d/pgdg.list'

wget -q https://www.postgresql.org/media/keys/ACCC4CF8.asc -O - | sudo apt-key add -

sudo apt update && apt upgrade -y

sudo apt install postgresql-9.6

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

### Passo 6

Criando usuário e grupo Odoo

```shell
sudo adduser --system --home=/opt/odoo --group odoo
```

### Passo 7

Instalando o GData

Biblioteca de clientes Python para API de dados do Google responsável pela leitura, escrita e modificação de informações na web.

```shell
cd /opt/odoo
```

Vá para o link "https://pypi.python.org/pypi/gdata" e baixe o gdata-2.0.18 e transfira o arquivo para o servidor.
Caso contrário, através do terminal, siga o passo abaixo:

```shell
sudo wget -c https://pypi.python.org/packages/a8/70/bd554151443fe9e89d9a934a7891aaffc63b9cb5c7d608972919a002c03c/gdata-2.0.18.tar.gz
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

### Passo 8

Download do Odoo via GitHub

Obtenha o último Odoo 11 do repositório github. Baixe o arquivo Zip do URL: "https://github.com/odoo/odoo/tree/10.0". Transfira o mesmo arquivo para o diretório /opt /odoo no servidor através do ftp. Caso contrário, siga a etapa abaixo

```shell
cd /opt/odoo
```

```shell
sudo wget -c https://github.com/odoo/odoo/archive/11.0.zip
```

```shell
sudo unzip 11.0.zip
```

```shell
sudo chown -R odoo: odoo-11.0
```

Ou clonar o Odoo via GitHub

```shell
git clone --depth=1 --branch=11.0 https://github.com/odoo/odoo.git /opt/odoo/odoo
```

```shell
sudo mv odoo/ odoo-11.0/
```

```shell
sudo chown -R odoo: odoo-11.0
```

### Passo 9

Criar arquivo de registro Odoo

```shell
sudo mkdir /var/log/odoo
```

```shell
sudo chown -R odoo:root /var/log/odoo
```

### Passo 10

Edite o arquivo de configuração de Odoo

```shell
sudo cp /opt/odoo/odoo-11.0/debian/odoo.conf /etc/odoo.conf
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
addons_path = /opt/odoo/odoo-11.0/addons
;Log Settings
logfile = /var/log/odoo/odoo.log
log_level = error
```

### Passo 11

WKHTMLTOPDF é ferramenta de código aberto (LGPLv3) para renderizar HTML em PDF e vários formatos de imagem usando o mecanismo de renderização Qt WebKit.

Siga as etapas mencionadas abaixo para fazer a instalação.

#### Passo 11.1

Baixe a versão wkhtmltopdf de https://wkhtmltopdf.org/downloads.html obedecendo da versão do seu Sistema Operacional.

Ou baixe através do GitHub.

```shell
sudo wget -c https://github.com/wkhtmltopdf/wkhtmltopdf/releases/download/0.12.4/wkhtmltox-0.12.4_linux-generic-amd64.tar.xz
```
#### Passo 11.2

Descompacte o arquivo

```shell
sudo tar -Jxf wkhtmltox-0.12.4_linux-generic-amd64.tar.xz
```

#### Passo 11.3

Copie wkhtmltoimage para /usr/bin localizado em /usr/local/bin usando o comando abaixo

```shell
sudo cp /opt/odoo/wkhtmltox/bin/wkhtmltoimage /usr/bin/wkhtmltoimage
sudo cp /opt/odoo/wkhtmltox/bin/wkhtmltopdf /usr/bin/wkhtmltopdf
```

### Passo 12

Agora, inicie o servidor Odoo

```shell
cd /opt/odoo/odoo-11.0
```

```shell
./odoo-bin
```

### Passo 13

Abra um navegador Web de sua preferência para acessar o Odoo 10

```
http://localhost:8069
```

# Removendo o Odoo
Os comandos abaixo sevem para fazer a remoção completa do Odoo do seu Sistema junto com suas configurações.

```
sudo rm -R /opt/odoo
sudo rm -f /etc/odoo-server.conf
sudo rm -f /etc/odoo.conf
sudo rm -R /var/log/odoo
sudo rm -f /usr/bin/wkhtmltoimage
sudo rm -f /usr/bin/wkhtmltopdf
sudo userdel -r odoo
sudo groupdel odoo
sudo apt-get purge postgresql-9.6* -y
sudo rm -r -f /etc/postgresql/
sudo rm -r -f /etc/postgresql-common/
sudo rm -r -f /var/lib/postgresql/
sudo userdel -r postgres
sudo groupdel postgres
sudo rm -R ~/.local/share/Odoo
sudo rm -f ~/.odoorc
sudo rm -f /etc/apt/sources.list.d/pgdg.list
sudo rm -f /etc/apt/sources.list.d/pgdg.list.save
sudo apt-get purge npm* -y
sudo apt-get autoremove -y
sudo rm -R ~/.npm
sudo apt-get remove $(deborphan) -y
```

Traduzido de GETOPENERP

Fonte:

https://www.getopenerp.com/install-odoo-10-on-ubuntu-16-04/

https://odoobrasil.wordpress.com/2016/10/31/instalando-odoo-erp-localizacao-brasileira-linux/

http://www.codebind.com/linux-tutorials/install-postgresql-9-6-ubuntu-18-04-lts-linux/

https://askubuntu.com/questions/1052079/unable-to-install-postgresql-9-6-in-ubuntu-18-04