# Como Extrair um Dataset Zipado em um Cluster

Este guia documenta o processo de extração de arquivos `.zip` em um ambiente de cluster, abordando problemas comuns como detecção de "zip bomb" e prompts de substituição de arquivos.

-----

## 1\. Iniciando a Extração

Primeiro, certifique-se de estar no diretório que contém seu arquivo `.zip`.

```bash
# Exemplo de listagem do diretório para confirmar a presença do arquivo
[ana.hougaz@login0 datasets]$ ls
afo.zip  data1.yaml  dataset_yolo_organized  data.yaml  seadronessee  seadronessee.zip
```

Para iniciar a extração, use o comando `unzip`:

```bash
[ana.hougaz@login0 datasets]$ unzip afo.zip
```

-----

## 2\. Lidando com o Erro "possible zip bomb"

É comum encontrar a seguinte mensagem de erro ao descompactar arquivos grandes ou com estruturas de diretório complexas:

```
error: invalid zip file with overlapped components (possible zip bomb)
To unzip the file anyway, rerun the command with UNZIP_DISABLE_ZIPBOMB_DETECTION=TRUE environmnent variable
```

Esta mensagem indica que o `unzip` interpretou a estrutura do arquivo como potencialmente maliciosa (uma "zip bomb"). Para prosseguir com a extração, você precisa desabilitar essa detecção temporariamente, definindo a variável de ambiente `UNZIP_DISABLE_ZIPBOMB_DETECTION` como `TRUE`:

```bash
[ana.hougaz@login0 datasets]$ UNZIP_DISABLE_ZIPBOMB_DETECTION=TRUE unzip afo.zip
```

-----

## 3\. Resolvendo Conflitos de Substituição de Arquivos

Após desabilitar a detecção de "zip bomb", o `unzip` pode perguntar se você deseja substituir arquivos existentes, especialmente se o diretório de destino já contiver arquivos com os mesmos nomes.

Você verá um prompt semelhante a este:

```
replace dataset_yolo_organized/data.yaml? [y]es, [n]o, [A]ll, [N]one, [r]ename:
```

Para uma extração completa e sem interrupções, **recomendamos usar a opção `A` (All)**. Isso garantirá que todos os arquivos sejam descompactados, substituindo quaisquer versões existentes sem mais prompts.

```bash
replace dataset_yolo_organized/images/test/a_1026.jpg? [y]es, [n]o, [A]ll, [N]one, [r]ename: A
```

Ao pressionar `A` e Enter, a extração continuará automaticamente para todos os arquivos restantes.

-----

## 4\. Verificando a Integridade da Extração

Após a conclusão da descompactação, é uma boa prática verificar se todos os arquivos foram extraídos corretamente. Você pode navegar até o diretório de destino e listar seu conteúdo.

Neste exemplo, o diretório extraído é `dataset_yolo_organized`:

```bash
# Navegue para o diretório extraído
[ana.hougaz@login0 datasets]$ cd dataset_yolo_organized

# Liste o conteúdo do diretório principal do dataset
[ana.hougaz@login0 dataset_yolo_organized]$ ls
data.yaml  images

# Navegue para um subdiretório e liste seu conteúdo (exemplo)
[ana.hougaz@login0 dataset_yolo_organized]$ cd images/test
[ana.hougaz@login0 test]$ ls
a_1013.jpg  a_324.jpg   b1_195.jpg  c_71.jpg    e_85.jpg    k1_22.jpg   r2_13.jpg   r3_279.jpg  r4_70.jpg   s2_16.jpg   s5_461.jpg
# ... (e assim por diante com o restante dos arquivos)
```

-----

## 5\. Limpeza (Opcional)

Se precisar remover o diretório extraído por qualquer motivo (por exemplo, para refazer a extração ou limpar o espaço), use o comando `rm -r`.

**Atenção:** O comando `rm -r` remove recursivamente o diretório e todo o seu conteúdo. Use com cuidado.

```bash
# Certifique-se de estar no diretório pai do dataset_yolo_organized (e.g., 'datasets')
[ana.hougaz@login0 datasets]$ rm -r dataset_yolo_organized
```

-----
