---
title: Instalação do Node.JS
autor: Wilton Gonçalves
---
# Instalação do Node.JS via binários

1. Acessar o endereço: https://nodejs.org/en/
2. Baixar o arquivo compactado (node-v-linux-x64.tar.xz)
3. Descompactar o na pasta /opt:
4. Renomear a pasta "node-v10.16.3-linux-x64" para "nodejs"
5. Insira as seguintes informações abaixo nos arquivos .profile, .bashrc e no .zshrc que estão na Home do usuário.

```
# NodeJS
export NODEJS_HOME=/opt/nodejs/bin
export PATH=$NODEJS_HOME:$PATH
```
6. Crie links simbólicos para os arquivos abaixo:

sudo ln -s /opt/nodejs/bin/node /usr/bin/node

sudo ln -s /opt/nodejs/bin/npm /usr/bin/npm

sudo ln -s /opt/nodejs/bin/npx /usr/bin/npx

7. Feche e abra o terminal novamente e digite o comando:

```
node -v
npm -v
npx -v
```