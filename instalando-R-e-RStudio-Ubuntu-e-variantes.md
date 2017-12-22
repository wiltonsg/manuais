---
title: Instalando R e RStudio em Ubuntu e variantes
autor: Wilton Gonçalves
versão: 1.0
---

# Passos para fazer a instalação do Projeto R:

```
sudo add-apt-repository 'deb http://cran.r-project.org/bin/linux/ubuntu xenial/'
```

```
sudo add-apt-repository 'deb http://cran.rstudio.com/bin/linux/ubuntu xenial/'
```

```
sudo apt-get update
```

```
sudo apt-get install r-base
```

## Despois de instalado execute o camando abaixo para acessar e verificar a versão do R

```
sudo -i R
```

## Para instala uma interface gráfica básica para o R execute o comando já dentro do ambiente R (R commander):

```
install.packages('Rcmdr')
library(Rcmdr) 
```

## Este pacote gera gráficos ASCII em arquivo txt:

```
install.packages('txtplot')
```

# Para fazer a instalação do RStudio:

Acesse a página: https://www.rstudio.com/products/rstudio/download/
Baixe o arquivo .deb referente ao seu sistema e execute a instalção usando o Gdebi.

Ou basta estar na pasta onde o arquivo foi salvo e executar o comando:
	
```
sudo dpkg -i rstudio_versão_do_arquivo.deb
```

### Opcionais:

sudo add-apt-repository 'deb http://cran-r.c3sl.ufpr.br/bin/linux/ubuntu xenial/'

sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E084DAB9

sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9
