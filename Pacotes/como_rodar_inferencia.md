# Guia para Execução da Inferência YOLOv8 no HPC

Este guia descreve os passos para configurar o ambiente e executar o script de inferência do modelo YOLOv8 no cluster HPC OGUN.

---

## 1. 📂 Pré-requisitos

Antes de começar, garanta que você tenha:
* Acesso SSH ao cluster HPC (`ogun-login0.senaicimatec.com.br`).
* Um ambiente Conda (`ccad`) já criado com as dependências básicas (Python, PyTorch, etc.).

---

## 2. 🚀 Passo a Passo para Execução

Siga os passos abaixo no terminal para rodar a inferência.

### Passo 1: Conectar ao Cluster HPC

Abra seu terminal (PowerShell, bash, etc.) e conecte-se ao nó de login do cluster.

```bash
# Conecta ao servidor na porta 5001 com seu usuário
ssh ana.hougaz@ogun-login0.senaicimatec.com.br -p 5001 -v
```
Você precisará inserir sua senha ou frase-secreta da chave SSH e o código de verificação.

### Passo 2: Preparar o Ambiente

Uma vez conectado, navegue até o diretório do projeto e ative o ambiente Conda.

```bash
# Navega para o diretório principal do projeto
cd /scratch/academico-cimatec/ccad

# Carrega o módulo Anaconda
module load anaconda3/2023.07

# Ativa o ambiente conda específico do projeto
source activate ccad
```

### Passo 3: Preparar Arquivos de Configuração e Modelo

Antes de rodar, precisamos garantir que o script de inferência, o arquivo de configuração do dataset e o modelo pré-treinado estejam corretos.

**a) Configuração do Dataset (`.yaml`):**

Navegue até o diretório de datasets e crie um arquivo de configuração `.yaml` para o seu dataset (neste exemplo, `dataafo.yaml`). 
Ele deve conter os caminhos CERTOS para as imagens de treino/validação e os nomes das classes.

```bash
# Navega para o diretório de datasets
cd vision_model_cimatec/datasets/

# (Opcional) Copia um arquivo existente como template
cp datamob.yaml dataafo.yaml

# Edita o arquivo para ajustar os caminhos e classes
nano dataafo.yaml
```
OBS.: Para salvar e sair do arquivo que usou nano use: **Ctrl + O e depois Ctrl + X**

**b) Script de Inferência:**

Vá para a pasta de modelos/scripts e certifique-se de que seu script de inferência (ex: `inferenciaYolov8Afo.py`) está apontando para o arquivo `.yaml` **correto** e para o caminho do modelo.

```bash
# Retorna ao diretório principal e vai para a pasta de modelos
cd ../../modelos/

# Edita o script de inferência para ajustar os parâmetros
nano inferenciaYolov8Afo.py
```

**c) Download do Modelo Pré-treinado:**

O script de inferência precisa do arquivo de pesos do modelo (`yolov8n.pt`). Para evitar problemas de permissão no diretório `/tmp` do cluster, baixe o modelo manualmente com um script auxiliar.

Crie um arquivo chamado `modelo.py`:
```bash
touch modelo.py
nano modelo.py
```
O comando touch modelo.py teve um propósito simples e direto: criar um arquivo completamente vazio chamado modelo.py

Cole o seguinte código Python dentro dele e salve:
```python
from ultralytics import YOLO

# Esta linha irá baixar o modelo 'yolov8n.pt' para o diretório atual
model = YOLO('yolov8n.pt')

print("Modelo yolov8n.pt baixado com sucesso!")
```

Execute o script para baixar o modelo:
```bash
(ccad) [ana.hougaz@login0 modelos]$ python modelo.py
```

### Passo 4: Executar a Inferência

Com tudo preparado, execute o script de inferência principal.

```bash
# Executa o script de inferência principal
(ccad) [ana.hougaz@login0 modelos]$ python inferenciaYolov8Afo.py
```

O script irá:
1.  Carregar o modelo `yolov8n.pt` local.
2.  Validar o modelo com o dataset configurado no `.yaml`.
3.  Processar todas as imagens.
4.  Salvar as métricas e resultados em um arquivo `.csv`.

### Passo 5: Verificar os Resultados

Após a conclusão, os resultados estarão disponíveis.
* **Métricas Consolidadas:** Verifique o arquivo `resultados_modelos.csv` (ou o nome que você definiu no script).

```bash
# Lista os arquivos para confirmar a criação dos resultados
ls

# Visualiza o arquivo de resultados
nano resultados_modelos.csv
```

---

## 3. 🧹 Organização dos Arquivos (Boa Prática)

Para manter o projeto organizado, mova os scripts e resultados para pastas específicas.

```bash
# Cria um diretório para os resultados
mkdir resultados_inferencia

# Renomeia e move o arquivo de resultados
mv resultados_modelos.csv resultados_inferencia/resultados_afo.csv

# Cria um diretório para os scripts de inferência
mkdir -p inferencias/yolov8

# Move os scripts para o novo diretório
mv inferenciaYolov8Afo.py inferencias/yolov8/
```

# Registro de Erros e Soluções na Execução de Inferência

Aqui registro os principais erros encontrados durante a execução de inferência no cluster HPC OGUN, detalhando as causas e os passos tomados para solucioná-los.

---

## Erro 1: Falha na Importação de Módulos (NumPy e Matplotlib)

### 🚨 O Erro

Ao executar o script da inferência pela primeira vez, o seguinte erro de importação ocorreu:

```
ImportError: numpy.core.multiarray failed to import
...
AttributeError: _ARRAY_API not found
```

### 🤔 O Que Significa

Este erro indica uma **incompatibilidade de versão entre bibliotecas**. Especificamente, a versão do `matplotlib` instalada no ambiente Conda não era compatível com a versão mais recente do `numpy` (v2.0 ou superior). Módulos mais antigos não conseguem "conversar" com as novas estruturas do NumPy.

### ✅ Passo a Passo da Solução

A solução foi forçar a atualização da biblioteca incompatível (`matplotlib`) para uma versão mais nova que fosse compatível com o NumPy 2.0.

1.  **Comando Executado:**

    ```bash
    # Usando o pip do ambiente 'ccad', atualizamos o matplotlib
    pip install --upgrade matplotlib
    ```

2.  **Resultado:** O `pip` baixou e instalou a versão mais recente do `matplotlib` e suas dependências, resolvendo o conflito de versões e permitindo que o script prosseguisse para o próximo estágio.

---

## Erro 2: Permissão Negada e Falha no Download

### 🚨 O Erro

Após corrigir o primeiro problema, o script falhou novamente com dois erros relacionados:

```
ERROR ❌ Error writing to /tmp/Ultralytics/settings.json: [Errno 13] Permission denied
...
❌ Erro na validação: ❌  Download failure for [https://ultralytics.com/assets/Arial.ttf](https://ultralytics.com/assets/Arial.ttf).
```

### 🤔 O Que Significa

Este erro é comum em ambientes compartilhados como clusters HPC. Ele significa que o script **não tinha permissão para escrever arquivos em um diretório temporário do sistema (`/tmp`)**. A biblioteca `ultralytics` tentou criar arquivos de configuração e baixar fontes nesse local, mas foi bloqueada pelas permissões do sistema.

Essa mesma restrição também impedia o download automático do modelo (`yolov8n.pt`).

### ✅ Passo a Passo da Solução

A solução foi contornar a necessidade de escrever no diretório `/tmp`, realizando manualmente o download do modelo para um diretório local onde tínhamos permissão de escrita.

1.  **Diagnóstico:** Identificamos que o problema era de permissão e que o arquivo do modelo (`yolov8n.pt`) não estava sendo baixado corretamente. Por isso, removemos qualquer versão corrompida ou incompleta dele.
    ```bash
    rm yolov8n.pt
    ```

2.  **Criação de um Script Auxiliar:** Criamos um script Python (`modelo.py`) com o único objetivo de baixar o modelo no diretório atual.
    ```bash
    # 1. Cria o arquivo vazio
    touch modelo.py

    # 2. Abre o arquivo para edição
    nano modelo.py
    ```

3.  **Código do Script Auxiliar:** Inserimos o seguinte código em `modelo.py`, que usa a própria biblioteca `ultralytics` para fazer o download.
    ```python
    from ultralytics import YOLO

    # Baixa 'yolov8n.pt' para o diretório local
    model = YOLO('yolov8n.pt')

    print("Modelo baixado com sucesso!")
    ```

4.  **Execução do Download:** Executamos o script auxiliar para baixar o modelo.
    ```bash
    python modelo.py
    ```
    Isso salvou o arquivo `yolov8n.pt` diretamente na pasta `/scratch/academico-cimatec/ccad/modelos/`.

5.  **Execução Final:** Com o arquivo `yolov8n.pt` já presente localmente, executamos o script de inferência principal novamente.
    ```bash
    python inferenciaYolov8Afo.py
    ```
    Desta vez, a biblioteca `ultralytics`:
    * Encontrou o modelo localmente e não tentou baixá-lo.
    * Detectou que `/tmp` não era gravável e, como alternativa, salvou seus arquivos de configuração no diretório `home` do usuário (`/home/ana.hougaz/.config/Ultralytics/`), onde a permissão de escrita é garantida.

O processo foi concluído com sucesso.
