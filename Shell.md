---
title: Alterando e Personalizando o Shell
autor: Wilton Gonçalves
---

# Alterando e personalizando a Shell

## Como instalar o Powerline e usar no Bash

```
sudo apt-get install powerline
```

### Altere o arquivo de configuração do Bash.

```
nano ~/.bashrc
```

Vá até o final do arquivo a acrescente as seguintes informações, salve o arquivo e feche:

```
# Configuration Powerline
powerline-daemon -q
POWERLINE_BASH_CONTINUATION=1
POWERLINE_BASH_SELECT=1
. /usr/share/powerline/bindings/bash/powerline.sh
```

### Caso utilize o ZSH, abra o arquivo **.zshrc** e acrescente as informações abaixo:

```
# Configuration Powerline
. /usr/share/powerline/bindings/zsh/powerline.zsh
```

Feche e abra o terminal e pronto.

## Como instalar o ZSH ou Z shell, uma alternativa ao Bash

```
sudo apt-get install zsh
```

Dentro do terminal digite **zsh** que isso irá mudar para o ZSH e para sair digite **exit** e você retornará para o Bash.

Para abrir o terminal diretamente no ZSH altere o arquivo **passwd**

```
sudo nano /etc/passwd
```

Procure pela linha que contem a seguinte informação:

user:x:1000:1000:User,,,:/home/user:/bin/bash

No lugar do **user** irá aparecer o seu nome de usuário. Depois altere o **bash** por **zsh**.

### Personalizando o ZSH

#### Instale o **Oh My Zsh**

Caso não tenha o **GIT** instalado faça a instalação, pois será necessário para fazer a instalação do **Oh My Zsh**.

```
sudo apt-get install git
```

via wget

```
sh -c "$(wget https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"
```

via curl

```
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

### Altere o tema do seu ZSH.

Abra o arquivo **.zshrc**

```
nano ~/.zshrc
```

Altere a linha que contem **ZSH_THEME="robbyrussell"** por **ZSH_THEME="agnoster"**
