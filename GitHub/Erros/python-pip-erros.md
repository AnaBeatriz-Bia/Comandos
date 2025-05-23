# Como corrigir erros comuns de Python/PIP no Windows + VSCode

## ❌ ERRO: Python não foi encontrado

```bash
python --version
````

### Mensagem:

> Python não foi encontrado; executar sem argumentos para instalar do Microsoft Store ou desabilitar este atalho...

### ✅ Solução:

Use o comando alternativo do Windows para verificar a versão do Python:

```bash
py --version
```

Se o comando `py` funcionar, o Python está instalado. Use `py` em vez de `python` para todos os comandos.

---

## ❌ ERRO: pip não reconhecido

```bash
pip install matplotlib
```

### Mensagem:

> pip : O termo 'pip' não é reconhecido como nome de cmdlet...

### ✅ Solução:

Use `py -m pip` em vez de `pip` diretamente:

```bash
py -m pip install matplotlib pillow
```

---

## ❌ ERRO: instalação de PIL

```bash
pip install PIL
```

### Mensagem:

> pip : O termo 'pip' não é reconhecido...

### ✅ Solução:

`PIL` está obsoleto. O nome correto do pacote é `Pillow`. Use:

```bash
py -m pip install pillow
```

---

## ✅ Recomendações

* Sempre teste se `py` funciona:

  ```bash
  py --version
  ```
* Para instalar pacotes, prefira:

  ```bash
  py -m pip install <nome_do_pacote>
  ```

---

## ✅ Criação de ambiente virtual (opcional e recomendado)

```bash
py -m venv venv
.\venv\Scripts\Activate
py -m pip install pillow matplotlib
```

---

## 📌 Resumo prático

```bash
py --version
py -m pip install pillow matplotlib
```

Se for usar ambiente virtual:

```bash
py -m venv venv
.\venv\Scripts\Activate
py -m pip install pillow matplotlib
```

