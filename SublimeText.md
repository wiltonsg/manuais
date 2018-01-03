---
title: Instalando o Sublime Text em Debian e variantes
autor: Wilton Gonçalves
versão: 1.0
---
# Instalando o Sublime Text em Debian e variantes

Instale a chave:
```shell
wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg | sudo apt-key add -
```
Certifique-se de que o apt esteja configurado para funcionar com as fontes https:

```shell
sudo apt-get install apt-transport-https
```
Comando para instalação da versão estável:

```shell
echo "deb https://download.sublimetext.com/ apt/stable/" | sudo tee /etc/apt/sources.list.d/sublime-text.list
```
```shell
sudo apt-get update
```
```shell
sudo apt-get install sublime-text
```

Fonte:
http://www.edivaldobrito.com.br/editor-sublime-text-no-ubuntu/

# Instalando o Package Control:

1. Abra o Sublime Text, vá até o menu View > Show Console;
2. Acesse o site https://packagecontrol.io/installation
3. Copie todo o código referente a versão do seu Sublime Text e cole no console do programa e pressione Enter do seu teclado.


# Plugin para executar códigos-fontes dentro do Sublime Text sem abrir o terminal

Instale o plugin **Terminality**

# Sublime Text como IDE para Python

Uma das perguntas mais comuns dos iniciantes na linguagem é “Qual a melhor IDE para Python?”. A resposta curta é que depende muito das preferências pessoais do programador, já que as IDEs para Python possuem funcionalidades bastante parecidas.
A grande questão, no entanto, é que Python foi projetada para ser intuitiva e fácil de usar. Essa característica da linguagem faz com que, na prática, uma IDE pesada seja praticamente desnecessária. Com um bom editor de textos e o interpretador interativo a postos, já é possível obter excelentes níveis de produtividade.
Mesmo o Sublime Text “puro”, ou seja, sem quaisquer plugins, já traz facilidades como o realce de sintaxe, as configurações de identação e os snippets que ficam disponíveis quando o arquivo que está sendo editado é código-fonte Python. Também vale considerar o melhor desempenho e leveza da execução do Sublime em comparação com uma IDE rodando em máquina com a mesma configuração.

## Navegação de código

Talvez uma das principais funções de uma IDE, aquela que na prática é a que usamos mais vezes, seja a facilidade de navegar pelo código de um projeto. Em projetos maiores, a capacidade de se mover com rapidez entre trechos de códigos dos diversos arquivos é absolutamente essencial.
Uma das principais finalidades do Sublime Text é justamente tornar essa navegação tão rápida e intuitiva quanto possível. Para isso, existem as funcionalidades:

**Goto Anything (Ctrl+P)**: abre uma lista de seleção que possui um campo de busca por arquivos abertos ou que pertencem a um projeto. O campo serve para filtrar o conteúdo da lista à medida em que digitamos o nome do arquivo que queremos abrir.

**Goto Symbol (Ctrl+R)**: abre uma lista de seleção na qual podemos escolher um dos símbolos (identificadores) contidos no arquivo atual e leva o cursor para a linha em que ele está definido.

**Goto Definition (F12)**: ao ser acionado, o comando leva você para a posição da definição do símbolo que está sob o cursor. (ST3)

**Goto Symbol in Project (Ctrl+Shift+R)**: abre uma caixa de pesquisa para que você escolha um símbolo dentre os que existem no projeto e leva o cursor para a definição do símbolo selecionado. (ST3)

## Barra lateral

Uma outra facilidade para navegação de que as IDEs proporcionam é a barra lateral para a visualização e navegação entre arquivos do projeto. O Sublime Text também possui recurso semelhante, que pode ser ativado e desativado pelo menu View > Sidebar. No entanto, as opções que o menu de contexto da barra lateral (aquele que aparece quando clicamos com o botão direito do mouse) são um tanto limitadas. Para contornar essas limitações, é possível instalar o plugin **SidebarEnhancements** (ST3).

Este plugin adiciona ao menu de contexto algumas opções como “Abrir com…”, copiar caminho do arquivo como texto, copiar conteúdo do arquivo em outras codificações (UTF-8, base64 etc.), pesquisa de texto (no arquivo, na pasta ou no projeto) entre outras.

## Padronizando seu código

Se você programa em Python, já deve ter ouvido falar da famosa PEP-8, que estabelece um guia de estilo para o código escrito na linguagem.
O Sublime Text conta com alguns plugins que sinalizam quando o código que você está escrevendo contém algum trecho que não está de acordo com a PEP-8. Alguns deles permitem até mesmo reformatar o código para que fique em conformidade com a convenção de código recomendada.

1. Python PEP 8 Autoformat
2. AutoPEP8
3. Flake8 Lint
4. SublimeLinter-pep8
5. Pylinter

Vale ressaltar que alguns desses plugins dependem de ferramentas externas para funcionar, enquanto outros já trazem as dependências incluídas na instalação. Por isso, é sempre bom ler as instruções de cada plugin com atenção.

## Como autocompletar código Python no Sublime Text

O recurso de autocompletar padrão do Sublime Text funciona apenas para palavras que já existem no arquivo que está sendo editado. Embora isso já seja bastante útil, normalmente precisamos que o autocompletar seja um pouco mais inteligente e “adivinhe” que queremos usar algum método, função, classe ou variável que esteja disponível em algum dos módulos Python que estamos importando para o nosso projeto.
Para isso, o ideal é instalar um dos seguintes plugins:

1. SublimeCodeIntel
2. SublimeJedi

## Plugins específicos para Python

Os plugins a seguir têm como proposta fornecer uma um conjunto de funcionalidades específicas para Python que vão além do recurso de autocompletar, tais como refatoração de código, assistente de importação de módulos, entre outros recursos típicos de uma IDE completa.

1. Anaconda
2. SublimeRope (ST2)
3. SublimePythonIDE (ST3)

## Controle de versões

Outra facilidade proporcionada por IDEs é a integração com sistemas de controle de versão. Com os plugins a seguir, é possível obter um nível de integração suficiente para realizar as tarefas mais comuns.

1. Sublimerge
2. GitGutter
3. SidebarGit
3. Mercurial
4. Sublime SVN

## Conclusão

Estas foram algumas dicas e opções de pluigns para quem deseja ter os principais recursos de uma IDE para Python completa no Sublime Text. É claro que existem muitas outras alternativas de plugins que podem ser incorporados à sua instalação do Sublime para proporcionar uma experiência personalizada. O grande segredo é testar cada uma delas para descobrir a que mais combina com seu estilo.
Conhece alguma outra dica, snippet, configuração ou plugin que seja útil para quem programa em Python? Compartilhe com a gente nos comentários!

Fonte:
http://sublimetextdicas.com.br/sublime-text-como-ide-para-python/

# Plugins que utilizo atualmente no Sublime Text

1. AutoPEP8
2. Markdown Preview
3. Terminality
4. SublimePythonIDE
5. Python PEP8 Autoformat
6. Colorsublime
7. A File Icon

# Temas para o Sublime Text

1. Soda
2. Flatland
3. Spacegray
4. Tomorrow Color Schemes
5. Theme - Phoenix
6. Dayle Rees Color Schemes
7. 3024 Color Scheme
8. Theme - Nexus
9. Aqua
10. Nil
11. Boxy
12. Material Theme
13. Agila Theme
14. Lanzhou
15. Sunrise
16. Kronuz
17. Autumn
18. Ayu
19. Theme - Dark Material
20. Theme - Dark Eight
21. Theme - Bamboo
22. ayu
23. Boxy Theme
24. DA UI
25. Guna

# Adicionar o parâmentro para o Python 3

Vá até o Menu: Tools > Build System > New Build System

Cole o código abaixo no novo arquivo que se abrir:

```
{
 "cmd": ["/usr/bin/python3", "$file"],
 "selector": "source.python",
 "file_regex": "file \"(...*?)\", line([0-9]+)"
}
```

E salve como Python3.sublime-build
