# Guia Prático para Acesso ao OGUN HPC

## 📌 Pré-requisitos
- Windows PowerShell instalado
- Acesso à internet
- Credenciais de usuário no OGUN HPC

## 🔑 Passo 1: Gerar Chaves SSH
Abra o PowerShell e execute:

```powershell
ssh-keygen -t ed25519
```

Quando solicitado:
1. Pressione Enter para aceitar o local padrão
2. Digite uma senha segura (ou deixe em branco)
3. Confirme a senha

## 🔍 Passo 2: Verificar Chave Pública
Execute no PowerShell:

```powershell
type "$env:USERPROFILE\.ssh\id_ed25519.pub"
```

Saída esperada (exemplo):
```
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIOA6yfZfM3gXu+TzVGohprfpJgLqkcb1QOAAO/wv4d2P anabe@AsusBook
```

## 📤 Passo 3: Enviar Chave Pública
Envie a chave pública (todo o conteúdo exibido) junto com:
1. [Termo de Responsabilidade](https://sesibahia-my.sharepoint.com/:b:/g/personal/vitor_fraga_fieb_org_br/EeiPitiLcZRPncZNKUzEOG0BwJitEcyW7C0CKa2JfI_UqA?e=xeQswc)
2. [Documento de Requisição](https://sesibahia-my.sharepoint.com/:b:/g/personal/vitor_fraga_fieb_org_br/EWYzXHT1uDtHkyJOIEm6l9EBGzLE4UTm3rpIOe22t21RRw?e=HEWXbv)

Destinatário: Vitor Gramacho

## 🔌 Passo 4: Conectar ao OGUN HPC
Após aprovação da chave, execute:

```powershell
ssh ana.hougaz@ogun-login0.senaicimatec.com.br -p 5001 -v
```

## ⚠️ Fluxo de Autenticação Esperado
1. Será solicitada a passphrase da chave (se configurada)
2. Código de verificação pelo Google Authenticator (baixar na App Store) e escanear Qr-Code do e-mail: [E-mail](https://outlook.office365.com/mail/inbox/id/AAQkADY3NDRhOGE3LTdhY2UtNDM5Yi05NTg0LTgwZTY2MmM5YzUwOAAQAMaIrmdX3UlNpvoLBl1B2H4%3D) 
3. Após autenticação, você terá acesso ao terminal remoto

PS.: O código no Google Authenticator fica durante 30 segundos. Coloque antes do tempo acabar.

## 💡 Dicas Importantes
- O modo `-v` mostra detalhes úteis para diagnóstico
- Mantenha sua chave privada em local seguro
- Caso tenha problemas, verifique:
  - Conexão com a internet
  - Porta 5001 liberada no firewall
  - Nome de usuário exatamente como fornecido

## 🛠️ Comandos Úteis no HPC
```bash
ls       # Listar arquivos
pwd      # Mostrar diretório atual
cd       # Navegar entre pastas
exit     # Encerrar sessão
mkdir <nome>	#Cria uma pasta
cp <origem> <destino>	#Copia arquivos
mv <origem> <destino>	#Move/renomeia arquivos
rm <arquivo>	#Remove arquivo (cuidado!)
cat <arquivo>	#Exibe conteúdo de um arquivo
nano <arquivo>	#Edita arquivo (editor simples)
scp <arquivo> user@cluster:/path	#Copia arquivos do/local para o cluster

#Comandos de Gerenciamento de Jobs (Slurm)
sinfo	#Mostra o status das partições (nós de computação)
squeue	#Lista jobs na fila
squeue -u <seu_user>	#Mostra seus jobs
sbatch <script.sh>	#Submete um job (ex.: sbatch meu_job.sh)
scancel <job_id>	#Cancela um job
sacct	#Mostra histórico de jobs
scontrol show job <job_id>	#Detalhes de um job específico
```
