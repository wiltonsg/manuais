---
title: Instalando Microsoft VS Code
autor: Wilton Gonçalves
---

# Instalando Microsoft Visual Studio Code no Debian e derivados

## Adicionando o repositório

```
sudo sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main" > /etc/apt/sources.list.d/vscode.list'
```

## Baixe e instale a chave do repositório do programa, usando os comandos abaixo;

```
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg

sudo mv microsoft.gpg /etc/apt/trusted.gpg.d/microsoft.gpg
```

## Atualize o gerenciador de pacotes com o comando:

```
sudo apt-get update
```

## Agora use o comando abaixo para instalar o programa:

```
sudo apt-get install code
```
