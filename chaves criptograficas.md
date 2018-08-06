# Como criar e usar um par de chaves SSH key

Neste exemplo usaremos um Sistema Operacional Linux Ubuntu, mas isso pode ser feito em qualquer baseado em Unix, já no Windows procure por algum programa para fazer o procedimento, uma dica procure por Puttygen.


Abra o terminal e acesse a pasta SSH

```
cd ~/.ssh
```

Digite o seguinte comando para gerar um par de chaves RSA de 2048 bits:

```
ssh-keygen -t rsa
```
ou
```
ssh-keygen -t rsa -b 2048
```

Digite o seguinte comando para gerar um par de chaves RSA de 4096 bits:

```
ssh-keygen -t rsa -b 4096
```

O exemplo abaixo mostra como gerar um par de chaves para ser utilizado no GitHub.
```
ssh-keygen -t rsa -b 4096 -C " your_email@example.com "
```

Enter a file in which to save the key (/home/you/.ssh/id_rsa): [Press enter]
Digite um arquivo no qual salvar a chave

Enter passphrase (empty for no passphrase): [Type a passphrase]
Insira a frase secreta (vazia para nenhuma frase secreta): [Digite uma frase secreta]

Enter same passphrase again: [Type passphrase again]
Digite a mesma frase secreta novamente: [Digite a senha novamente]
