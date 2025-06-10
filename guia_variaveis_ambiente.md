# Correção de Variáveis de Ambiente VS Code + Git Bash

## Abstract 📋
Este guia resolve problemas de má formação de variáveis de ambiente no VS Code com Git Bash integrado.
Aborda configurações específicas para Windows 11 com Python gerenciado via pyenv e Poetry.
Inclui soluções para caracteres cortados em paths e configurações de terminal integrado.
Fornece verificações e testes para garantir funcionamento correto do ambiente de desenvolvimento.

## Índice Temático 📚
- Diagnóstico do Problema
- Configuração do Git Bash
- Configuração do VS Code
- Configuração do Python/Pyenv
- Verificações e Testes
- Troubleshooting Avançado

## Diagnóstico do Problema 📖

### Sintomas Identificados
- `$HOME` retorna `C:\Usersnton` ao invés de `C:\Users\anton`
- `$PYTHONPATH` aparece truncado: `C:\Usersnton\lab` com quebra de linha
- Caracteres sendo "cortados" nas variáveis de ambiente

### Causas Prováveis
1. **Codificação de caracteres**: Conflito entre UTF-8 e Windows-1252
2. **Configuração de terminal**: Args incorretos no VS Code
3. **Variáveis do sistema**: Conflito entre variáveis do Windows e Git Bash
4. **Escape de caracteres**: Problemas com barras e caracteres especiais

## Configurações Recomendadas
### Configuração do Git Bash 📖

#### Arquivo ~/.bashrc (Versão Corrigida)
```bash
# Force correct encoding
export LANG=en_US.UTF-8
export LC_ALL=en_US.UTF-8

# Fix HOME path - use Windows format but ensure proper escaping
export HOME="$(cygpath -w "$USERPROFILE" | sed 's/\\/\//g')"

# Alternative HOME fix (choose one)
# export HOME="/c/Users/anton"

# Fix Python paths
export PYTHONIOENCODING=utf-8

# Custom prompt with proper escaping
PS1='\[\033]0;$TITLEPREFIX:$PWD\007\]'
PS1="$PS1"'\n'
PS1="$PS1"'\[\033[32m\]\u@\h '
PS1="$PS1"'\[\033[35m\]\w'
PS1="$PS1"'\[\033[0m\]'
PS1="$PS1"'\n$ '

# Aliases
alias ll='ls -lah --color'
alias gs='git status'
alias gp='git pull'
alias gc='git commit'
alias gb='git branch'

# Git completion
if [ -f "/mingw64/share/git/completion/git-completion.bash" ]; then
    . "/mingw64/share/git/completion/git-completion.bash"
fi

# Poetry completion
if command -v poetry &> /dev/null; then
    source ~/.bash_completion
fi
```

#### Arquivo ~/.bash_profile (Simplificado)
```bash
# Load bashrc
if [ -f ~/.bashrc ]; then
    source ~/.bashrc
fi

# Ensure proper PATH for Python/Poetry
export PATH="$HOME/.pyenv/pyenv-win/bin:$HOME/.pyenv/pyenv-win/shims:$PATH"
export PATH="$HOME/.local/bin:$PATH"
```

### Configuração do VS Code 📖

#### settings.json (Versão Corrigida)
```json
{
    "security.allowedUNCHosts": [
        "192.168.0.89"
    ],
    "workbench.iconTheme": "material-icon-theme",
    "terminal.integrated.defaultProfile.windows": "Git Bash",
    "terminal.integrated.profiles.windows": {
        "Git Bash": {
            "path": "C:\\Program Files\\Git\\usr\\bin\\bash.exe",
            "args": [
                "--login",
                "-i"
            ],
            "env": {
                "LANG": "en_US.UTF-8",
                "LC_ALL": "en_US.UTF-8",
                "PYTHONIOENCODING": "utf-8"
            }
        }
    },
    "terminal.integrated.env.windows": {
        "LANG": "en_US.UTF-8",
        "LC_ALL": "en_US.UTF-8",
        "PYTHONIOENCODING": "utf-8"
    },
    "jupyter.interactiveWindow.creationMode": "perFile",
    "workbench.editorAssociations": {
        "*.csv": "default",
        "*.pdf": "default"
    },
    "python.defaultInterpreterPath": "C:\\Users\\anton\\.pyenv\\pyenv-win\\versions\\3.13.2\\python.exe",
    "git.enableSmartCommit": true,
    "workbench.editor.empty.hint": "hidden",
    "terminal.integrated.inheritEnv": false
}
```

#### Configuração do Python/Pyenv 📖

#### Variáveis de Sistema Windows
Adicione via **Sistema > Propriedades > Variáveis de Ambiente > Variáveis do Sistema**:

```
PYENV=%USERPROFILE%\.pyenv\pyenv-win
PYENV_ROOT=%USERPROFILE%\.pyenv\pyenv-win
PYENV_HOME=%USERPROFILE%\.pyenv\pyenv-win
PYTHONIOENCODING=utf-8
LANG=en_US.UTF-8
```

#### PATH System (adicionar no início)
```
%USERPROFILE%\.pyenv\pyenv-win\bin
%USERPROFILE%\.pyenv\pyenv-win\shims
%USERPROFILE%\.local\bin
```

#### Teste de Python
```bash
# Verificar versão do Python
python --version

# Verificar localização
which python

# Verificar encoding
python -c "import sys; print(sys.getdefaultencoding())"
```

## Verificações e Testes 📖

### Script de Diagnóstico
Crie um arquivo `test_env.sh`:

```bash
#!/bin/bash
echo "=== DIAGNÓSTICO DE AMBIENTE ==="
echo
echo "1. HOME: '$HOME'"
echo "2. USERPROFILE: '$USERPROFILE'"
echo "3. PATH: '$PATH'"
echo "4. LANG: '$LANG'"
echo "5. LC_ALL: '$LC_ALL'"
echo "6. PYTHONPATH: '$PYTHONPATH'"
echo "7. PYTHONIOENCODING: '$PYTHONIOENCODING'"
echo
echo "=== TESTES DE COMANDO ==="
echo "pwd: $(pwd)"
echo "whoami: $(whoami)"
echo "python --version: $(python --version 2>&1)"
echo "poetry --version: $(poetry --version 2>&1)"
echo
echo "=== VERIFICAÇÃO DE CARACTERES ==="
echo "Comprimento de HOME: ${#HOME}"
echo "HOME em hexdump:"
echo "$HOME" | hexdump -C | head -5
```

### Comandos de Verificação
```bash
# Teste básico de variáveis
echo "HOME: '$HOME'"
echo "Tamanho: ${#HOME}"

# Verificar codificação
locale
echo $LANG

# Testar caminhos Python
python -c "import os; print(f'HOME: {os.environ.get(\"HOME\")}'); print(f'USERPROFILE: {os.environ.get(\"USERPROFILE\")}')"

# Verificar Poetry
poetry env info
```

## Troubleshooting Avançado 📖

### Problema: Caracteres Cortados
**Solução 1: Forçar UTF-8**
```bash
# No início do ~/.bashrc
export LANG=C.UTF-8
export LC_ALL=C.UTF-8
```

**Solução 2: Usar cygpath**
```bash
# Converter path do Windows para formato Unix
export HOME="$(cygpath -u "$USERPROFILE")"
```

**Solução 3: Definir manualmente**
```bash
# Hardcode temporário para teste
export HOME="/c/Users/anton"
```

### Problema: VS Code não carrega configurações
1. Feche completamente o VS Code
2. Delete cache: `%APPDATA%\Code\User\workspaceStorage`
3. Reinicie o VS Code
4. Abra novo terminal

### Problema: Poetry não funciona
```bash
# Reinstalar Poetry no ambiente correto
curl -sSL https://install.python-poetry.org | python3 -

# Ou via pip
pip install --user poetry

# Adicionar ao PATH
export PATH="$HOME/.local/bin:$PATH"
```

### Verificação Final
Após aplicar as correções, execute:

```bash
# 1. Verificar HOME
echo "HOME correto: $HOME"

# 2. Verificar Python
python -c "import os; print('Python HOME:', os.path.expanduser('~'))"

# 3. Verificar Poetry
poetry --version

# 4. Testar projeto
cd seu_projeto
poetry env info
poetry install --dry-run
```

## Índice de Consulta Rápida ⏱️

| Seção | Tópico | Descrição |
|-------|--------|-----------|
| Diagnóstico | Identificação | Sintomas e causas dos problemas |
| Git Bash | ~/.bashrc | Configuração principal do terminal |
| Git Bash | ~/.bash_profile | Carregamento de configurações |
| VS Code | settings.json | Configuração do terminal integrado |
| Python | Variáveis Sistema | Configuração do Windows |
| Python | PATH | Ordem correta dos caminhos |
| Testes | Diagnóstico | Script para verificar ambiente |
| Testes | Verificação | Comandos de teste manual |
| Troubleshooting | Caracteres | Soluções para encoding |
| Troubleshooting | Cache | Limpeza de configurações |
| Troubleshooting | Poetry | Reinstalação e configuração |


## Conclusão