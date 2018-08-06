---
title: Ambiente Isolado para Python
autor: Wilton Gonçalves
---

# Ambiente Isolado para programação em Python

O post de hoje não será tão estreitamente relacionado à dicas sobre código Python como foram os anteriores. Ele irá tratar sobre o ambiente usado para o desenvolvimento em sua máquina.

Para quem está envolvido no desenvolvimento de vários projetos em paralelo, é bastante comum que um projeto tenha dependências de bibliotecas diferentes das usadas pelos outros projetos.
Em um ambiente Ubuntu Linux, por exemplo, os módulos Python instalados no sistema são armazenados em /usr/lib/python2.7/dist-packages/ (para Python 2.7). Dessa forma, se tivermos desenvolvendo dois projetos diferentes, eles estarão compartilhando algumas bibliotecas. E se for necessário que o projeto A utilize a versão x de determinado módulo, enquanto que o projeto B deve utilizar a versão y do mesmo módulo? Como os dois projetos, A e B, utilizam os módulos instalados no mesmo local do disco, fica difícil satisfazer esse requisito.

Outra situação muito comum de acontecer é estarmos desenvolvendo ou testando uma aplicação em um ambiente sobre o qual não temos permissões para a instalação de pacotes no sistema. Sabendo que muita gente passa por situações parecidas, foi criado o virtualenv. Se tivermos o virtualenv à disposição, podemos criar um ambiente virtual em nossa pasta pessoal e instalar os pacotes necessários dentro desse ambiente, sem a necessidade de ter privilégios de super-usuário. Quando for necessário lidar com vários projetos ao mesmo tempo, podemos criar um ambiente virtual para cada projeto, ambos na mesma máquina.

Assim, o virtualenv é uma ferramenta que permite que criemos, com o perdão da redundância, ambientes virtuais isolados para projetos Python. Por exemplo, se tivermos dois projetos, A e B, podemos criar dois ambientes virtuais, um para cada um dos projetos. Poderíamos chamá-los de venvA e venvB, por exemplo. Quando criamos esses dois ambientes, é criado um diretório com o nome de cada ambiente, com o seguinte conteúdo cada um:

bin  include  lib  local
Dentro do diretório bin, são criados arquivos binários (executáveis) necessários em um ambiente de desenvolvimento Python:

$ ls bin/
activate          activate.fish     easy_install    get_env_details
pip-2.7           postdeactivate    predeactivate   activate.csh
activate_this.py  easy_install-2.7  pip             postactivate
preactivate       python
Perceba que temos, dentre os arquivos listados, o interpretador Python (python), além de outras ferramentas importantes como o pip, que pode ser usadoo como instalador de pacotes do virtualenv. Existem também arquivos que são relacionados ao próprio ambiente virtual. Assim, cada ambiente virtual terá seus próprios executáveis para interpretar seus programas e gerenciar seus pacotes. Além disso, é criado também um diretório lib/python2.7/site-packages/, onde serão armazenados os pacotes que você instalar para aquele ambiente. Ou seja, ambos os ambientes venvA e venvB possuirão seu próprio interpretador Python, bem como suas próprias bibliotecas de código. Assim, cada projeto poderá ter versões específicas de determinados pacotes, sem a ocorrência de conflitos entre versões.

Como usar o virtualenv?
O virtualenv pode ser instalado de várias formas. A forma mais comum é através do gerenciador de pacotes pip. Tendo o pip instalado, você pode instalar o virtualenv com o seguinte comando:

user@host:~/$ sudo pip install virtualenv
Tendo feito isso, agora podemos começar a criar os ambientes virtuais para projetos Python. Primeiramente, vamos criar um ambiente:

user@host:~/$ virtualenv NomeDoAmbiente
Após executado o comando acima, será criado, no diretório atual, um subdiretório chamado NomeDoAmbiente, contendo aquela mesma estrutura já comentada anteriormente. Após o ambiente ter sido criado, precisamos ativá-lo:

user@host:~/$ source ./NomeDoAmbiente/bin/activate
(NomeDoAmbiente)user@host:~/$
Você irá perceber que o prompt do seu shell é alterado após a execução do comando acima, sendo a partir daí, precedido pelo nome do ambiente virtual ativo entre parênteses (veja acima). Isso faz também com que sua variável de ambiente $PATH passe a apontar, em primeiro lugar, para a pasta bin de dentro do ambiente virtual, de forma que quando você chamar o interpretador Python pela linha de comando, o executável que será aberto será o interpretador que está instalado dentro do ambiente virtual atual, pois será o primeiro encontrado no $PATH.

Instalando pacotes dentro do ambiente virtual
Uma vez que ativamos o ambiente virtual que desejamos usar, podemos então instalar os pacotes que forem necessários para nosso projeto. Por exemplo, considere que estamos trabalhando em nosso ambiente (ativado anteriormente), chamado de NomeDoAmbiente, e desejamos instalar o pacote Django. Podemos utilizar o gerenciador de pacotes pip que está instalado dentro de nosso ambiente virtual NomeDoAmbiente:

(NomeDoAmbiente)user@host:~/$ pip install Django
Downloading/unpacking Django
    Downloading Django-1.4.1.tar.gz (7.7Mb): 7.7Mb downloaded
    Running setup.py egg_info for package Django
Installing collected packages: Django
    Running setup.py install for Django
Successfully installed Django
Cleaning up...
Agora, podemos abrir um shell Python dentro do ambiente NomeDoAmbiente recém criado, e testar se o Django está mesmo instalado:

(NomeDoAmbiente)user@host:~/$ python
Python 2.7.2+ (default, Jul 20 2012, 22:15:08)
[GCC 4.6.1] on linux2
Type "help", "copyright", "credits" or "license" for more information.
>>> import django
>>> django.__file__
'/home/user/NomeDoAmbiente/local/lib/python2.7/site-packages/django/__init__.pyc'
Tudo certo, o Django está instalado corretamente dentro do ambiente NomeDoAmbiente.

Para sair do ambiente virtual ativo, utilize o comando deactivate.

Gerando lista de dependências do projeto
Lembra quando você envia um projeto pronto para o chefe e ele manda um email dizendo que o projeto não funciona? Muitas vezes, o problema é que o computador do chefe não possui instaladas as bibliotecas que o projeto necessita. Nessa situação, a dupla virtualenv + pip nos ajuda novamente.

Uma vez que estejamos utilizando ambientes virtuais para nossos projetos, e que estejamos instalando todos os pacotes necessários via pip, temos facilmente em mãos a lista de pacotes dos quais nosso projeto depende. Para obter essa lista, basta utilizar o comando freeze do pip:

(NomeDoAmbiente)user@host:~/$ pip freeze
Django==1.4.1
Werkzeug==0.8.3
argparse==1.2.1
distribute==0.6.24
django-bootstrap-toolkit==2.5.8
django-extensions==0.9
django-registration==0.8
wsgiref==0.1.2
Tal comando escreve na saída-padrão a lista de pacotes (bem como suas versões), de cada uma das dependências instaladas via pip no projeto ativo. De posse dessa lista, podemos agora facilmente enviar a lista de dependências para o nosso chefe, utilizando as informações fornecidas pelo pip freeze para garantir que a máquina do chefe irá satisfazer todas as dependências do nosso projeto. Primeiro, devemos armazenar em um arquivo as informações geradas pelo pip freeze:

(NomeDoAmbiente)user@host:~/$ pip freeze > requirements.txt
Após isso, podemos enviar o arquivo requirements.txt para o chefão e, usando o pip, ele poderá executar:

(NomeDoAmbiente)anotheruser@anotherhost:~/$ pip install -r requirements.txt
O comando acima irá instalar as versões especificadas dos pacotes listados no arquivo fornecido como entrada. Tendo instalado corretamente os pacotes listados, nosso projeto estará com todas as dependências satisfeitas no computador do chefe, e poderá ser executado sem problemas.

virtualenvwrapper
Existe outro projeto, chamado virtualenvwrapper, que é um wrapper sobre o virtualenv, e que provê uma série de facilidades para a manipulação de ambientes virtuais. Vale muito a pena dar uma conferida nele!

Utilizando o virtualenvwrapper, a ativação de um ambiente fica muito mais simples:

user@host:~/$ workon NomeDoAmbiente
(NomeDoAmbiente)user@host:~/$
Além disso, ele provê vários atalhos para facilitar a nossa vida, como o cdvirtualenv, que troca o diretório atual para o diretório do virtualenv ativo. Alguns outros aliases úteis:

cdsitepackages: troca o diretório atual para o diretório onde os pacotes Python do ambiente virtual ativo estão instalados.
lssitepackages: comando muito útil para listarmos os arquivos/diretórios presentes no diretório de instalação dos módulos do ambiente virtual ativo.
mkvirtualenv NOME: cria um ambiente virtual chamado NOME.
dentre outros 😉
virtualenv embutido no Python 3.3
A versão 3.3 do Python traz consigo a possibilidade de criarmos ambientes virtuais sem a necessidade de instalação do pacote virtualenv separadamente, ou seja, o virtualenv fará parte da distribuição oficial do Python. Mais informações podem ser encontradas na documentação oficial: http://docs.python.org/dev/library/venv.html.

Enfim…
O virtualenv é extremamente útil quando você está trabalhando com vários projetos ao mesmo tempo, ou em um ambiente sobre o qual você não tenha permissões de super-usuário. Mas fique atento, pois o virtualenv irá instalar uma versão de cada biblioteca e dos executáveis para cada um dos seus ambientes virtuais, o que irá consumir mais espaço em disco.

Introdução
Quando desenvolvemos em Python, é comum ficarmos maravilhados com o poder de suas bibliotecas.

Tudo se torna mais fácil ainda quando podemos baixá-las com um simples comando (pip install <pacote> por exemplo).

Dessa forma, se não tomarmos alguns cuidados, podemos deixar nosso ambiente de desenvolvimento lotado de bibliotecas.

Isso quando não as utilizamos algumas vezes e depois nunca mais.

Não apenas isso! Imagine o seguinte cenário: você está desenvolvendo uma aplicação, chamada CoolApp que utiliza a biblioteca powerlib em sua versão 1.0.

Por enquanto tudo ok…

Daí, algum tempo se passa e você acaba largando essa aplicação, pois cansou-se dela e ela nem era tão promissora assim.

Você começa então a desenvolver uma aplicação ultra mega powerfull, chamada TheApp, que por coincidência utiliza a mesma biblioteca (powerlib), mas em sua versão 2.0.

Bom, você inocentemente realiza o upgrade (sudo pip install --upgrade powerlib) dessa biblioteca para sua versão 2.0 para poder continuar seu desenvolvimento.

Então me diga: o que acontecerá caso você tente retomar o desenvolvimento da aplicação CoolApp (juntamente com o desenvolvimento da aplicação TheApp)?

Resposta: Caso você tenha instalado todas as suas bibliotecas no diretório padrão (/usr/lib/pythonX.X/site-packages), apenas uma aplicação irá funcionar… NOOOOOOOOOOOO!!!!

Ou seja, quando desenvolvemos Python “globalmente” e não isolamos cada ambiente de desenvolvimento, podemos ter conflitos entre versões de bibliotecas.

Outro ponto, e se quisermos desenvolver um projeto em Python 2 e outro em Python 3? Como fazer?

E ainda mais: e se você não puder instalar suas dependências no diretório global site-packages (seu programa pode estar sendo executado em um host remoto, por exemplo)?

Mas calma, a solução para todos os seus problemas está aqui, e chama-se virtualenv. Portanto, vamos começar entendendo melhor do que se trata!

Como o Virtualenv Funciona
Funcionamento do virtualenv

O funcionamento do virtualenv é realmente simples. Ele basicamente cria uma cópia de todos os diretórios necessários para que um programa Python seja executado, isto inclui:

As bibliotecas comuns do Python (standard library);
O gerenciador de pacotes pip;
O próprio binário do Python (Python 2.x/3.x);
As dependências que estiverem no diretório site-packages;
Seu código fonte descrevendo sua aplicação.
Assim, ao instalar uma nova dependência dentro do ambiente criado pelo virtualenv, ele será colocado no diretório site-packages relativo à esse ambiente, e não mais globalmente.

Assim, só esse ambiente enxergará essa dependência. Show, né?!

Primeiros Passos
Instalação
Para a instalação do virtualenv vamos precisar do pip.

Caso você ainda não tenha o gerenciador de pacotes pip, instale-o clicando aqui e executando o script baixado com python get-pip.py.

Agora com o pip, precisamos executar apenas um comando para instalar o virtualenv:

1
$ sudo pip install virtualenv
Pronto! virtualenv instalado e funcionando! Agora vamos começar a utilizá-lo!

Inicializando um Ambiente Virtual
virtualenv possui apenas um comando! Olha que simples:

1
$ virtualenv [opções] <nome_da_pasta>
Esse comando cria um novo ambiente de desenvolvimento totalmente isolado!

No nosso caso, vamos chamar nossa pasta de ENV.

Nessa pasta são criados alguns diretórios importantes, como:

ENV/lib e ENV/include: contêm as bibliotecas de suporte ao ambiente virtual. Os pacotes baixados via pip por exemplo serão instalados em ENV/lib/pythonX.X/site-packages/ (não mais globalmente).
ENV/bin: residem os binários necessários para executar o próprio Python, entre outros executáveis (como o pip ou setuptools). Dessa forma, os comandos python script.py e ENV/bin/python script.py produzem exatamente o mesmo resultado.
Script de Ativação do Ambiente Virtual
Após criar o seu novo ambiente, podemos ativá-lo com o comando:

1
$ source ENV/bin/activate
O comando source lê um arquivo e executa os comandos contidos ali.

Ao ativar o virtualenv, o diretório ENV/bin será adicionado como primeiro registro do caminho $PATH do seu sistema operacional.

Ele também altera o padrão do seu prompt, adicionando o prefixo (ENV) para indicar que vocês está em um ambiente controlado pelo virtualenv.

Como Desativar seu Ambiente Virtual
Para desativar um ambiente virtual e remover tudo que foi feito e instalado, retornando ao estado anterior do sistema (sem o virtualenv) basta executar:

1
2
$ deactivate
$ rm -r ENV
Fazendo isso, seu ambiente virtual é desfeito e tudo que foi copiado para este ambiente é apagado (comando rm).

Opção --python
Para criarmos um novo ambiente contendo a versão do Python de sua escolha (Python 2.x ou Python 3.x), devemos informar ao virtualenv, no momento da criação de um novo ambiente, a localização do binário do Python.

Caso você não saiba o caminho do binário do Python que você está procurando, utilize o comando which.

Por exemplo, para saber onde estava o binário do Python 3 em minha máquina, eu executei o comando which python3 que me respondeu com /usr/local/bin/python3.

Com isso, podemos criar nosso novo ambiente utilizando o python3 da seguinte forma:

1
virtualenv --python='/usr/local/bin/python3' ENV
Com seu ambiente ativado, verifique qual versão está sendo utilizada, com o comando python --version.

Pronto! Python 2 e Python 3 no sistema operacional de maneira simples! :snake:

Algumas Opções Interessantes
De acordo com sua documentação, o comando possui algumas opções e é utilizado da seguinte maneira: virtualenv [opções] <nome_da_pasta>.

Para a lista completa de valores possíveis de [opções], acesse sua documentação.

Separei algumas opções interessantes para vocês:

--system-site-packages: Essa opção cria um ambiente com todas as dependências já instaladas globalmente. Ou seja, não será um ambiente limpo.
--python=/path/to/pythonX.X: Usado para definir o diretório de uma versão alternativa do Python que será utilizado nesse ambiente virtual.
--no-pip: Cria o ambiente sem o pip.
--no-setuptools: Cria o ambiente sem o setuptools.
Arquivo de Configuração virtualenv.ini
Ao criar um novo ambiente, o virtualenv busca parâmetros no arquivo virtualenv.ini presente no caminho $HOME/.virtualenv/virtualenv.ini (Mac OS/Linux) ou %APPDATA%\virtualenv\virtualenv.ini (Windows).

Nesse arquivo, podemos adicionar parâmetros do virtualenv que serão utilizados em todos os ambientes criados.

Por exemplo, podemos definir opções da seguinte forma:

1
2
3
4
5
[virtualenv]
no-pip
no-setuptools
system-site-packages
python = /opt/python-3.3/bin/python
Assim, todo ambiente que criarmos terão essas opções por padrão (sem termos que digitar os parâmetros toda vez).

Ambiente Isolado para Python com virtualenv
Foto: Yuko Honda

Boa parte do meu dia-a-dia de desenvolvedor é gasto em proramando em Python. Gosto de estar sempre atualizado com o que há de novo para essa linguagem e para isso saio instalando tudo o que aparece para para experimentar. Além de Python o Linux também faz parte da minha vida e uso ele quase 100% do meu tempo (em vias de mudar para o OS X).

A plataforma Python, de uns tempos pra cá, vêm padronizando os arquivos Eggs para distribuição de aplicações e bibliotecas. Em conjunto com o PyPI (Python Package Index) e o utilitário easy_install (que é parte do framework setuptools) é possível instalar componentes Python com apenas um comando.

A facilidade para instalar esses pacotes é enorme mas removê-los é chato porque envolve a edição de alguns arquivos texto, e ter permissão de escrita no diretório de bibliotecas do Python (permissão que também é necessária para a instalar o pacote).

Cada pacote instalado acrescenta uma entrada ao sys.path do Python fazendo com que o tempo para importar um módulo aumente um pouco mais (cada uma dessas entradas é consultada em busca do módulo e se você der uma olhada na saída do strace verá que a procura por um módulo envolve vários passos).

O Linux que eu uso (Ubuntu) precisa ter um ambiente Python estável, já que grande parte de suas aplicações roda em cima dessa linguagem, ou seja, danificar esse ambiente pode atrapalhar todo o funcionamento do sistema.

Isso tudo junto com o fato de que adoro experimentar as novidades do mundo Python faziam com que meu Python ficasse totalmente poluído com versões bleeding edge de bibliotecas que muitas vezes são incompatíveis com as versões “oficialmente suportadas” pelo pessoal que faz o Ubuntu.

Seria necessário um jeito fácil de se criar ambientes isolados do Python usando como base a própria instalação do sistema para que eu pudesse fazer esses testes e experiências sem danificá-lo. Não ficar replicando cópias de Python pela máquina também seria interessante.

E então surge a solução…

Parece engraçado mas no mesmo dia que perdi horas “arrumando” o Python em meu computador eu li no blog do Ian Bicking que ele tinha desenvolvido um programinha que fazia exatamente o que eu precisava: o virtualenv.

O uso do virtualenv é extremamente simples e direto. Basta instalar, executar e ativar.

Instalação

Se você está usando Ubuntu ou Debian:

sudo apt-get install python-setuptools
sudo easy_install virtualenv
Se não está:

wget http://peak.telecommunity.com/dist/ez_setup.py
sudo python ez_setup.py
Criando o ambiente

Para criar um ambiente basta executar o virtualenv e passar como parâmetro o nome do diretório onde tal ambiente será instalado:

virtualenv meu_python
Esse comando irá criar um diretório chamado meu_python com os diretórios:

bin – executável do interpretador, o script easy_install e o arquivo activate que será usado para “ativar” o ambiente. Quando o ambiente está “ativo” os executáveis dos aplicativos Python são instalados aqui também.
lib – a árvore com links simbólicos e/ou cópias de todos os módulos e bibliotecas do Python. Quando esse ambiente está “ativo” os módulos e pacotes serão sempre instalados dentro desse diretório.
include – dentro desse diretório estão os links simbólicos para todos os headers do Python que são necessários para se compilar extensões escritas em C para ele.
Ativando o ambiente para usar

Para usar esse ambiente recém-criado é necessário ativá-lo. para isso basta executar o seguinte comando:

source meu_python/bin/activate
Esse comando irá adicionar o diretório meu_python/bin no PATH da sua sessão e mudar o prompt para que você possa distinguir visualmente quando este ambiente está ativo.

Atenção: O virtualenv não cria o link simbólico python -> python2.5, portanto, se precisar dele você terá que criá-lo à mão com o seguinte comando

(cd meu_python/bin; ln -s python2.5 python; hash -r)
Depois disso é só sair instalando as coisas sem a menor preocupação.
