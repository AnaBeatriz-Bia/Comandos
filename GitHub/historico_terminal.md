# Comando PowerShell - Visualizando Histórico de Comandos no VScode

O comando abaixo permite que você visualize o histórico de comandos usados no **PowerShell**:

```powershell
Get-Content "$env:USERPROFILE\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadLine\ConsoleHost_history.txt"
