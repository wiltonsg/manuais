---
title: Instalação, cofiguração e comandos do Git
autor: Wilton Gonçalves
---

# Instalação, cofiguração e comandos do Git

Este manual tem a finalidade de ensinar o básico da ferramenta Git desde a instalação ao uso.
O Git é um sistema de controle de versão distribuído e um sistema de gerenciamento de código fonte, com ênfase em velocidade. O Git foi inicialmente projetado e desenvolvido por Linus Torvalds para o desenvolvimento do kernel Linux, mas pode ser utilizado para controlar arquivos de texto como do Microsoft Word ou do LibreOffice e planilhas também.

Aqui iremos focar na instalação utilizando uma distribuição Linux que é o Ubuntu 16.04 LTS e utilizando linhas de comando no terminal.

Quem utiliza o Microsoft Windows basta acessar a página https://git-scm.com/ ir na opação download e escolher a versão correspondente ao seu sistema.

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
git config --global user.name "Nome Sobrenome"
```

```
git config --global user.email "fulano@example.com"
```

## Verificando suas configurações

```
git config --list
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

## Visualizando o Histórico de Commits

Depois que você tiver criado vários commits, ou se clonou um repositório com um histórico de commits existente, você provavelmente vai querer ver o que aconteceu. A ferramenta mais básica e poderosa para fazer isso é o comando:

```
git log
```

### Usando Interface Gráfica para Visualizar o Histórico

```
gitk
```

## Modificando Seu Último Commit

Uma das situações mais comuns para desfazer algo, acontece quando você faz o commit muito cedo e possivelmente esqueceu de adicionar alguns arquivos, ou você bagunçou sua mensagem de commit. Se você quiser tentar fazer novamente esse commit, você pode executá-lo com a opção --amend:

```
git commit --amend
```

## Tirando um arquivo da área de seleção

As duas próximas seções mostram como trabalhar nas suas modificações na área de seleção e diretório de trabalho. A parte boa é que o comando que você usa para ver a situação nessas duas áreas também lembra como desfazer suas alterações. Por exemplo, vamos dizer que você alterou dois arquivos e quer fazer o commit deles como duas modificações separadas, mas você acidentalmente digitou git add * e colocou os dois na área de seleção. Como você pode retirar um deles? O comando git status lembra você:

```
git reset HEAD tcc.odt
```

## Desfazendo um Arquivo Modificado

```
git checkout -- tcc.odt
```

Para saber mais sobre os comandos do Git basta acessar a página de documentação do mesmo que está no fontes abaixo. Para quem utiliza o Microsoft Windows pode usar uma interface gráfica para a ferramenta, recomendo o GitHub Desktop que está disponível no seguinte endereço: https://desktop.github.com/

## Criando Branch
Para criar um branch e mudar para ele ao mesmo tempo, você pode executar o comando git checkout com a opção -b:

```
git checkout -b develop
```
Isso é um atalho para:

```
git branch develop
git checkout develop
```


## Mudando de Branch

```
git checkout master
```
## Efetuando o Merge

```
git checkout master
git merge hotfix
```
## Apagando um Branch

```
git branch -d hotfix
```

# Extras

Preenchimento Automático
Se você usa um shell Bash, você pode habilitar um script de preenchimento automático que vem com o Git. Faça download do código fonte, e olhe no diretório contrib/completion; lá deve existir um arquivo chamado git-completion.bash. Copie este arquivo para o seu diretório home, e adicione a linha abaixo ao seu arquivo .bashrc:

```
source ~/.git-completion.bash
```

Fontes:
https://git-scm.com/
https://git-scm.com/book/pt-br/v1/Primeiros-passos-No%C3%A7%C3%B5es-B%C3%A1sicas-de-Git
https://pt.wikipedia.org/wiki/Git
