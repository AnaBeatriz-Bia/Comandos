## Como Fazer o 1º Acesso ao Cluster HPC

Este guia explica como gerar uma chave SSH e configurar o acesso ao cluster HPC pela primeira vez no Windows.

## Passo 1: Gerar a Chave SSH

1. Abra o **Prompt de Comando** do Windows.

2. Execute o seguinte comando para gerar uma chave SSH do tipo **ed25519**. **Certifique-se de que o comando está correto**:

    ```bash
    ssh-keygen -t ed25519
    ```

3. O sistema pedirá para você escolher um local para salvar a chave. O caminho padrão é `C:\Users\<seu-usuario>\.ssh\id_ed25519`. Pressione **Enter** para salvar no local padrão.

4. Em seguida, será solicitado para você inserir uma **senha**. Se preferir, você pode deixar em branco e pressionar **Enter**. Se quiser adicionar uma senha, digite-a e pressione **Enter**. Após isso, você será solicitado a confirmar a senha.

5. O sistema irá gerar a chave privada e pública no diretório `.ssh` do seu perfil de usuário.

## Passo 2: Verificar a Chave Pública

Após gerar a chave SSH, você pode verificar a chave pública gerada com o seguinte comando:

```bash
type %userprofile%\.ssh\id_ed25519.pub
```

Esse comando exibirá a chave pública gerada, que será algo semelhante a:

```
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIKuhGM5Wj8zmHhE7B3yS4z1MHDYquZk8b7mKHM7XKxmp fieb\ana.hougaz@N305-SP01671
