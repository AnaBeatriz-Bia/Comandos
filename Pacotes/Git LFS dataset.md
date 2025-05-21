# Guia: Envio de Dataset com Git LFS para o GitHub - exemplo dataset AFO

## Antes de tudo clone o repositório que você quer enviar o dataset pelo VScode usando:
```bash
git clone "https://github.com/gisellyreis/vision_model_cimatec.git"
```
## 1. Copiar o Dataset

Copie manualmente a pasta `AFO` que você baixou e que está em `Downloads`para dentro da pasta no seu computador em `Disco Local`, `Usuários`... `vision_model_cimatec/datasets/` no seu repositório local clonado do GitHub.

**Local:**
```

vision_model_cimatec/
└── datasets/
└── AFO/

````

## 2. Navegar até o Repositório Local pelo VScode

Se ainda não estiver no diretório do repositório:

```powershell
cd caminho/para/vision_model_cimatec
````

Ou abra diretamente no VS Code.

## 3. Rastrear Arquivos com Git LFS

Certifique-se de rastrear os formatos de arquivos grandes com Git LFS:

```bash
git lfs install
git lfs track "*.jpg"
git lfs track "*.png"
git lfs track "*.csv"
git lfs track "*.zip"
git add .gitattributes
```

## 4. Adicionar Arquivos ao Git

Adicione o diretório do dataset:

```bash
git add datasets/AFO
```

Para verificar os arquivos adicionados:

```bash
git status
```

## 5. Fazer Commit

Realize o commit das alterações:

```bash
git commit -m "Added AFO dataset with Git LFS"
```

## 6. Enviar ao GitHub

Envie os dados ao repositório remoto:

```bash
git push
```

## 7. No Cluster (para cada usuário da equipe)

Cada usuário deve clonar o repositório e puxar os arquivos do Git LFS:

```bash
git clone https://github.com/seu-usuario/vision_model_cimatec.git
cd vision_model_cimatec
git lfs pull
```

```

Se desejar, posso salvar esse conteúdo com nome de arquivo sugerido como `upload_dataset_git_lfs.md`. Deseja que eu faça isso?
```
