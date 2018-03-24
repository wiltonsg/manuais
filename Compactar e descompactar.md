# Compactar e descompactar arquivos via terminal

## Para COMPACTAR:
### zip:

```
zip nome_do_arquivo.zip arquivo_a_ser_compactado
```

### rar:

```
rar a nome_do_arquivo.rar arquivo_a_ser_compactado
```

### tar:

```
tar -cf nome_arquivo.tar arquivo_a_ser_compactado
```

### tar.gz:

```
tar -cf nome_arquivo.tar arquivo_a_ser_compactado
gzip -9 nome_arquivo.tar
```

### bz2:

```
bzip2 nome_do_arquivo.bz2
```

### tar.bz2:

```
tar -jxvf nome_do_arquivo.tar.bz2
```

 Para se compactar mais de um arquivo por vez, basta acrescentar a lista mais arquivos. EX:  tar -cf nome_arquivo.tar arquivo_a_ser_compactado1 arquivo_a_ser_compactado2 arquivo_a_ser_compactado3

## Para DESCOMPACTAR:

### zip:

```
unzip nome_do_arquivo.zip
```

### rar:

```
unrar x nome_do_arquivo.rar
```

### tar:

```
tar -xvf nome_do_arquivo.tar
```

### tar.gz:

```
tar -vzxf nome_do_arquivo.tar.gz
```

### bz2:

```
bunzip nome_do_arquivo.bz2
```

### tar.bz2:

```
tar -jxvf nome_do_arquivo.tar.bz2
```

## Lista de parâmetros que podem ser usados:

```
-c – cria um novo arquivo tar;
-M – cria, lista ou extrai um arquivo multivolume;
-p – mantém as permissões originais do(s) arquivo(s);
-r – acrescenta arquivos a um arquivo tar;
-t – exibe o conteúdo de um arquivo tar;
-v – exibe detalhes da operação;
-w – pede confirmação antes de cada ação;
-x – extrai arquivos de um arquivo tar;
-z – comprime ou extrai arquivos tar resultante com o gzip;
-j – comprime ou extrai arquivos tar resultante com o bz2;
-f – especifica o arquivo tar a ser usado;
-C – especifica o diretório dos arquivos a serem armazenados.
```

Fonte: http://blog.kolaborativa.com/2011/10/compactar-e-descompactar-arquivos-zip-rar-tar-gz-bz2-tar-tar-bz2-pelo-terminal/
