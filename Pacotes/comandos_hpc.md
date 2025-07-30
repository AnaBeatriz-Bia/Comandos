# Guia de Comandos do Terminal (Linux/HPC)

Este documento serve como uma referência rápida para os comandos de terminal utilizados durante a sessão de trabalho no cluster HPC OGUN.

---

## Conexão Remota

### `ssh`
Conecta a um servidor remoto de forma segura.
* **Uso:** `ssh usuario@host -p porta -v`
* `usuario@host`: Suas credenciais e o endereço do servidor.
* `-p 5001`: Especifica uma porta de conexão diferente da padrão (22).
* `-v`: Modo "verboso" (verbose), que exibe detalhes do processo de conexão. Muito útil para depurar problemas.

---

## Navegação e Gerenciamento de Arquivos

### `cd` (Change Directory)
Muda o diretório atual.
* **Uso:** `cd caminho/para/o/diretorio`
* `cd ..`: Volta um diretório (para o diretório pai).
* `cd ~` ou apenas `cd`: Volta para o diretório `home` do usuário.

### `ls` (List)
Lista os arquivos e pastas no diretório atual.
* **Uso:** `ls`

### `cp` (Copy)
Copia arquivos ou diretórios.
* **Uso:** `cp arquivo_original novo_arquivo_copia`

### `mv` (Move)
Move ou renomeia arquivos e diretórios.
* **Para renomear:** `mv nome_antigo.txt nome_novo.txt`
* **Para mover:** `mv arquivo.txt diretorio_destino/`

### `rm` (Remove)
Remove (apaga) arquivos. **Cuidado: esta ação não pode ser desfeita!**
* **Uso:** `rm nome_do_arquivo.txt`

### `mkdir` (Make Directory)
Cria um novo diretório.
* **Uso:** `mkdir nome_do_novo_diretorio`
* `mkdir -p`: Cria diretórios aninhados (ex: `mkdir -p pasta/subpasta`) sem gerar erro se a pasta pai não existir.

### `touch`
Cria um arquivo vazio ou atualiza a data de modificação de um arquivo existente.
* **Uso:** `touch novo_arquivo.py`

---

## Edição de Arquivos

### `nano`
Um editor de texto simples e fácil de usar diretamente no terminal.
* **Uso:** `nano nome_do_arquivo.txt`
* **Comandos principais:**
    * `Ctrl + O`: Salvar ("Write Out").
    * `Ctrl + X`: Sair do editor.

---

## Gerenciamento de Ambiente e Software (HPC)

### `module load`
Carrega módulos de software pré-instalados no ambiente do cluster. Essencial para acessar compiladores, bibliotecas e programas como o Anaconda.
* **Uso:** `module load anaconda3/2023.07`

### `source activate`
Ativa um ambiente virtual Conda. Isso isola as dependências do seu projeto.
* **Uso:** `source activate nome_do_ambiente`

---

## Execução e Pacotes Python

### `python`
Executa um script Python.
* **Uso:** `python meu_script.py`

### `pip install`
Gerenciador de pacotes do Python, usado para instalar ou atualizar bibliotecas.
* **Uso:** `pip install nome_do_pacote`
* `--upgrade`: Força a atualização de um pacote já instalado para a versão mais recente.
    * **Exemplo:** `pip install --upgrade matplotlib`
 
## Como contar a quantidade de imagens dos datasets

Opção 1
```
ls *.jpg *.PNG *.jpeg *.PNG 2> /dev/null | wc -l
```
Opção 2
```
find . -maxdepth 1 -type f \( -iname '*.jpg' -o -iname '*.jpeg' -o -iname '*.png' \) | wc -l
```
