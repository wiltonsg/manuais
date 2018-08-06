---
title: Como usar o pip
autor: Wilton Gonçalves
---

# O que é o pip?

O pip é um sistema de gerenciamento de pacotes usado para instalar e gerenciar pacotes de software escritos na linguagem de programação Python. Muitos pacotes podem ser encontrados no Python Package Index

# Como instalar o pip para gerenciar pacotes do Python
## Instalação no Debian e derivados
### Para o Python 2

```
sudo apt-get install python-pip
```

### Para o Python 3

```
sudo apt-get install python3-pip
```

# Como usar o pip
Aqui será utilizado o pip3 que usar o Python 3, caso queira usar o Python 2 use o pip no lugar do pip3. Todos os comandos são executados dentro de um Terminal.

## Instalação de um pacote:

```
sudo pip3 install nome-do-pacote
```

## Desinstalação de um pacote:

```
sudo uninstall nome-do-pacote
```

## Procurar um pacote:

```
pip3 search nome-do-pacote
```

## Listar os pacotes instalados:

```
pip3 list
```

## Mostrar informações sobre um pacote:

```
pip3 show nome-do-pacote
```

## Para ver a lista completa de comandos:

```
pip3 help
```
