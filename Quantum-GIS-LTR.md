---
title: Instalação o Quantum GIS LTR no Ubuntu e Debian
autor: Wilton Gonçalves
---

# Instalação o Quantum GIS LTR no Ubuntu e Debian

O QGIS é um Sistema de Informação Geográfica (SIG) de Código Aberto licenciado segundo a Licença Pública Geral GNU. O QGIS é um projeto oficial da Open Source Geospatial Foundation (OSGeo). Funciona em Linux, Unix, Mac OSX, Windows e Android e suporta inúmeros formatos de vetores, rasters e bases de dados e funcionalidades.

### Adicionando repositórios

**(Versão 2.14.22 previous LTR)**
```shell
sudo add-apt-repository "deb http://qgis.org/debian-ltr xenial main"

sudo add-apt-repository "deb http://qgis.org/ubuntugis-ltr ubuntu xenial main" (Opcional)
```

**(Versão 2.18.16 new LTR)**

```shell
sudo add-apt-repository "deb http://qgis.org/debian xenial main"

sudo add-apt-repository "deb-src http://qgis.org/debian xenial main" (Opcional)
```

### Adicionando a chave

Versão 2016
```shell
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-key 073D307A618E5811
```

Versão 2017
```shell
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-key CAEB3DC3BDF7FB45
```

### Atualize a lista do repositório

```shell
sudo apt-get update
```

### Instale o QGIS e os adicionais

```shell
sudo apt-get install qgis python-qgis qgis-plugin-grass
```

### Outras formas de fazer a instalação

deb http://ppa.launchpad.net/ubuntugis/ubuntugis-unstable/ubuntu xenial main

Se você usar um dos nossos repositórios baseados em ubuntugis você também precisa adicionar seguinte linha

deb http://ppa.launchpad.net/ubuntugis/ubuntugis-unstable/ubuntu *codename* main

Depois digite:

```shell
sudo apt-get update
sudo apt-get install qgis python-qgis qgis-plugin-grass
```

Em caso de erro do servidor de chaves adicione a chave pública do repositório qgis.org no seu conjunto de chaves, digite:

**Chave versão 2016**

```shell
wget -O - http://qgis.org/downloads/qgis-2016.gpg.key | gpg --import
gpg --fingerprint 073D307A618E5811
```

Deve sair:

pub   2048R/618E5811 2016-08-17 [expires: 2017-08-17]
      Key fingerprint = 942D 6AD5 DF3E 75DE A9AF  72B2 073D 307A 618E 5811
uid                  QGIS Archive Automatic Signing Key (2016) <qgis-developer@lists.osgeo.org>
sub   2048R/D34A963D 2016-08-17

Depois de ter verificado a impressão digital você pode adicionar a chave para o apt com

```shell
gpg --export --armor 073D307A618E5811 | sudo apt-key add -
```

**Chave versão 2017**

```shell
wget -O - https://qgis.org/downloads/qgis-2017.gpg.key | gpg --import
gpg --fingerprint CAEB3DC3BDF7FB45
```

Deve sair:

pub   2048R/BDF7FB45 2017-08-16 [expires: 2019-08-16]
      Key fingerprint = 61E0 A086 749E 463E DE50  2255 CAEB 3DC3 BDF7 FB45
uid                  QGIS Archive Automatic Signing Key (2017) <qgis-developer@lists.osgeo.org>
sub   2048R/E959BBCF 2017-08-16 [expires: 2019-08-16]
Depois de ter verificado a impressão digital você pode adicionar a chave para o apt com

```shell
gpg --export --armor CAEB3DC3BDF7FB45 | sudo apt-key add -
```

Alternativamente, você pode baixar a chave de um keyserver e adicione a chave para o apt de uma só vez (sem verificação manual de impressão digital)

```shell
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-key 073D307A618E5811
```

```shell
deb http://qgis.org/debian-ltr ubuntu xenial main
deb-src http://qgis.org/ubuntugis-ltr ubuntu xenial main
```

#### Via PPA

```shell
sudo add-apt-repository ppa:ubuntugis/ppa
sudo apt-get update

deb http://ppa.launchpad.net/ubuntugis/ppa/ubuntu xenial main
deb-src http://ppa.launchpad.net/ubuntugis/ppa/ubuntu xenial main
```
