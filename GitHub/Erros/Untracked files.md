# Solução para "Untracked files" no Git com exemplo

Se ao rodar `git status` você ver algo como:

```
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        GitHub/Erros/
```

isso significa que há arquivos não rastreados pelo Git. Para corrigir isso, siga os passos abaixo.

## 1️⃣ Navegar até a pasta correta
Antes de adicionar os arquivos ao Git, entre na pasta onde eles estão:
```sh
cd GitHub/Erros/
```

## 2️⃣ Verificar o status novamente
Agora, execute:
```sh
git status
```
Isso confirmará que você está no diretório certo e os arquivos ainda estão não rastreados.

## 3️⃣ Adicionar os arquivos ao Git
Para rastrear os arquivos, use:
```sh
git add .
```

## 4️⃣ Criar um commit
Agora, faça o commit das mudanças:
```sh
git commit -m "Solução do Untracked files"
```

## 5️⃣ Enviar para o repositório remoto
Por fim, envie as mudanças para o GitHub:
```sh
git push
```

Agora seus arquivos estão versionados corretamente! 🚀

