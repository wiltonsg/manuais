---
title: Instalando o PyCharm no Ubuntu e derivados
autor: Wilton Gonçalves
---

# Instalando o PyCharm no Ubuntu e derivados

## Parte 1 - instalar o Java

As aplicações da JetBrains não são exatamente compatíveis com a versão do Java que vem por padrão no Ubuntu. Por isso, precisamos atualizar.
Abra o terminal e execute os comandos abaixo:

```shell
sudo add-apt-repository ppa:webupd8team/java
```

```shell
sudo apt-get update
```

```shell
echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | sudo /usr/bin/debconf-set-selections
```

```shell
sudo apt-get install oracle-java8-installer -y
```

```shell
sudo apt-get install oracle-java8-set-default -y
```

Após os comandos acima, veja se a instalação está correta, executando no console:

```shell
java -version
```

A saída esperada é algo como:

```shell
java version "1.8.0_45"
Java(TM) SE Runtime Environment (build 1.8.0_45-b14)
Java HotSpot(TM) 64-Bit Server VM (build 25.45-b02, mixed mode)
```

## Parte 2 - pip e virtualenv

O PyCharm usa o **pip** para baixar módulos/bibliotecas/extensões (como quiser chamar) do python, e o **virtualenv** para criar os queridos ambientes virtuais que mantém a sanidade dos programadores python. Então, para tirar proveito dessas funcionalidades, é bom garantir que estejam instalados também.
Para isto, abra o console e digite:

```shell
cd ~/Downloads
wget -c https://bootstrap.pypa.io/get-pip.py
```

```shell
sudo -H python2 get-pip.py
sudo -H python3 get-pip.py
sudo -H pip2 install virtualenv
```

## Parte 3 - copiar o PyCharm

1. Clique no link ao lado para ir à página de Download do PyCharm (https://www.jetbrains.com/pycharm/download/#section=linux)
2. Clique em "Download Community"
3. Grave o arquivo no diretório que quiser

## Parte 4 - Instalar o PyCharm

Com os pré-requisitos prontos e instalados, vamos ao prato principal:

```shell
sudo tar -C /opt/ -xzf <diretorio_onde_gravou_o_download>/pycharm-community-2017.3.2.tar.gz
cd /opt/pycharm-community-2017.3.2/bin
./pycharm.sh
```
Ou
1. Abra o navegador de arquivos e vá ao diretório /opt/pycharm-community-4.5.1
2. Entre no diretório 'bin' e, com dois cliques sobre, execute o script 'pycharm.sh'
3. Se aparecer uma janela perguntando como rodar o programa, clique no último botão ('Executar' ou 'Run')
4. Dê "OK" na janela que abrir
5. E na próxima janela, deixe todas as últimas opções selecionadas. Ao clicar em 'OK' o PyCharm vai pedir a senha de 'root' para criar as entradas no menu.

Pronto, é isso. O software está instalado, e pronto para uso.

Fonte:
http://pythonclub.com.br/instalando-pycharm-ubuntu.html
