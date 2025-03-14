### Como funciona a sincronização:

- **GitHub** é o repositório remoto. Quando você faz alterações no repositório pelo site do GitHub (como editar arquivos diretamente lá), elas são refletidas **somente no repositório remoto**.
- **VScode/Terminal** é o repositório local. Quando você faz alterações na sua área de trabalho, essas mudanças são refletidas **somente no seu computador** até você enviar essas alterações para o GitHub.

#### Como atualizar a sua área de trabalho, VScode e GitHub:

1. **Quando você faz alterações no GitHub (site):**
   - Se você editar algo diretamente no site do GitHub, a alteração será apenas no repositório remoto (no GitHub).
   - Para **sincronizar sua área de trabalho** (local) com o que está no GitHub, você precisa **fazer um pull** do repositório remoto. Isso vai baixar as últimas alterações feitas no GitHub para a sua área de trabalho.

   **Comando:**
   ```bash
   git pull origin master
   ```
   Isso vai trazer as alterações do repositório remoto para a sua cópia local.

2. **Quando você faz alterações na sua área de trabalho (no VScode ou em qualquer editor):**
   - Se você modificar ou adicionar arquivos no seu repositório local, essas mudanças não aparecerão no GitHub até que você faça um **commit** e um **push**.
   
   **Passos para enviar para o GitHub:**
   - **Adicione as alterações** (preparar os arquivos para o commit):
     ```bash
     git add .
     ```
   - **Faça o commit** (salve as alterações no histórico local):
     ```bash
     git commit -m "Descrição da alteração"
     ```
   - **Envie para o GitHub** (atualize o repositório remoto):
     ```bash
     git push origin master
     ```

### Resumo:

- **Alterações no GitHub (site)**: Para que sua área de trabalho tenha essas mudanças, você precisa rodar o comando `git pull origin master` no terminal.
- **Alterações na sua área de trabalho**: Quando fizer alterações na sua área de trabalho e quiser que elas apareçam no GitHub, você precisa fazer `git add`, `git commit` e `git push`.

### Sincronização Automática:

Como o repositório local está na sua área de trabalho (no OneDrive, por exemplo), **qualquer alteração feita localmente será sincronizada automaticamente com o OneDrive**. No entanto, **para que o GitHub saiba dessas alterações e as receba**, é necessário usar o processo de commit e push mencionado acima. A sincronização automática com o OneDrive é para os arquivos em si, mas o GitHub só vai ser atualizado após o `git push`.

Sempre que fizer mudanças, lembre-se de:
1. **Fazer `git pull`** para pegar as mudanças do GitHub.
2. **Fazer `git add`, `git commit` e `git push`** para enviar suas mudanças ao GitHub.

Assim, você vai manter tudo atualizado entre o GitHub, sua área de trabalho local e o OneDrive!
