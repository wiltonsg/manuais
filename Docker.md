---
title: Instalação do Docker no Ubuntu 16.04
autor: Wilton Gonçalves
---
# Instalação do Docker nu Ubuntu 16.04 LTS

O Docker é uma plataforma de software que permite a criação, o teste e a implantação de aplicações rapidamente. O Docker cria pacotes de software em unidades padronizadas chamadas de contêineres que têm tudo o que o software precisa para ser executado, inclusive bibliotecas, ferramentas de sistema, código e runtime. Ao usar o Docker, é possível implantar e escalar rapidamente aplicações em qualquer ambiente e ter a certeza de que o seu código será executado.

Aqui será utilizado a versão Community Edition (CE)

## Instalação de depedências

```
sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common
```

## Adicionando a chave do Docker

```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

```
sudo apt-key fingerprint 0EBFCD88
```

A saida deste comando acima deverá sair algo assim:

```
pub   4096R/0EBFCD88 2017-02-22
      Key fingerprint = 9DC8 5822 9FC7 DD38 854A  E2D8 8D81 803C 0EBF CD88
uid                  Docker Release (CE deb) <docker@docker.com>
sub   4096R/F273FCD8 2017-02-22
```

## Adicione o repositório do Docker

```
sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
```

## Atualize a lista do repositório

```
sudo apt-get update
```

## Comando para instalação do Docker CE

```
sudo apt-get install docker-ce
```

## Verifique se o Docker foi instalado corretamente

```
sudo docker run hello-world
```

## Executando o Docker sem a necessidade de digitar "sudo"

```
sudo usermod -aG docker $(whoami)
```
Encerre a seção e faça o login novamente para que as alterações sejam confirmadas

## Executando o Docker sem o "sudo"

```
docker images
```
