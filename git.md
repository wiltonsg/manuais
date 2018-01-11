---
title: Instalação, cofiguração e comandos do Git
autor: Wilton Gonçalves
---

# Instalação, cofiguração e comandos do Git

Este manual tem a finalidade de ensinar o básico da ferramenta Git desde a instalação ao uso.
O Git é um sistema de controle de versão distribuído e um sistema de gerenciamento de código fonte, com ênfase em velocidade. O Git foi inicialmente projetado e desenvolvido por Linus Torvalds para o desenvolvimento do kernel Linux, mas foi adotado por muitos outros projetos. Cada diretório de trabalho do Git é um repositório com um histórico completo e funciona independente de acesso a uma rede, internet ou a um servidor central.

Aqui iremos focar na instalação utilizando uma distribuição Linux que é o Ubuntu 16.04 LTS e utilizando linhas de comando no terminal.

Para utilizar a versão mais recente do Git no Ubuntu e derivados utilize os camandos abaixo:

Este comando irá adicionar o repositório PPA:
```
add-apt-repository ppa:git-core/ppa
```

Atualize a lista do repositório:
```
sudo apt-get update
```

Agora faça a instalação:
```
sudo apt-get install git git-core
```

# Configurando o Git pela primeira vez:

A primeira coisa que devemos fazer definir o seu nome de usuário e endereço de e-mail. Isso é importante porque todos os commits no Git utilizam essas informações para anexar aos commits que efetuará:


## Configurando a identidade:
```
git config --global user.name "Wilton Gonçalves"
```

```
git config --global user.email "wiltong@example.com"
```

## Configurando seu editor:
```
git config --global core.editor nano
```

## Sua ferramenta de Diff

Outra opção útil que você pode querer configurar é a ferramente padrão de diff utilizada para resolver conflitos de merge (fusão). Digamos que você queira utilizar o vimdiff:

```
git config --global merge.tool vimdiff
```

## Verificando suas configurações

```
git config --list
```

## Altere o tempo para 1 "uma" hora evitando digitar o tempo todo a senha:

```
git config --global credential.help 'cache --timeout=3600'
```

## Inicializando um Repositório
Caso você esteja iniciando o monitoramento de um projeto existente com Git, você precisa estar no diretório do projeto e digitar:

```
git init
```
## Verificando a situação dos arquivos dentro do projeto:

```
git status
```
## Adicionar os arquivos para uma área de monitoramento do Git:

### Adiciona todos os arquivos
```
git add .
```

### Adicionar somente um arquivo
```
git add tcc.docx
```

### Adicionar todos os arquivos de mesma extenção
```
git add *.xlsx
```

## Gravando o commit de suas alterações no repositório local do Git:

A partir daqui qualquer alterações feitas nos arquivos que foram inclusas com o git add passará ser monitorada.

```
git commit -m "mensagem"
```
