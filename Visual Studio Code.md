## Índice
- Introdução ao Vs Code
- Extensões para desenvolvimento Python
- Configurações
	- Terminal
	- LangueServer e Formatter
	- Como forçar o VS Code a usar o `.venv` corretamente
	- Integração com Git e Github
- 

---
## 🧩 Extensões | Desenvolvimento Python

Para um desenvolvedor **Python** voltado para **IA, Machine Learning, Ciência de Dados e DataViz**.

### 🎨 Temas & Interface

🔹 Melhorias visuais para o editor e usabilidade.

#### Temas

- [One Dark Pro](https://marketplace.visualstudio.com/items?itemName=zhuangtongfa.Material-theme) → Tema escuro moderno.
    
- [Night Owl](https://marketplace.visualstudio.com/items?itemName=sdras.night-owl) → Um dos temas escuros mais bem avaliados.
    
- [Dracula Official](https://marketplace.visualstudio.com/items?itemName=dracula-theme.theme-dracula) → Tema escuro vibrante.
    

#### Ícones

- [Material Icon Theme](https://marketplace.visualstudio.com/items?itemName=PKief.material-icon-theme) → Ícones modernos para arquivos.
    

#### Tradução

- [Portuguese (Brazil) Language Pack for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=MS-CEINTL.vscode-language-pack-pt-br) → Tradução para PT-BR.
    

> 🚨 **Possível Conflito**: Vários temas ativos ao mesmo tempo podem gerar inconsistências visuais.  
> ⚠️ **Recomendação**: Escolha um ou dois temas principais e desative os demais para manter uma experiência consistente.

---

### 🐍 Ambiente Python

🔹 Essencial para instalar, gerenciar e rodar Python corretamente no VS Code.

- [Python](https://marketplace.visualstudio.com/items?itemName=ms-python.python) → Indispensável para qualquer projeto Python.
    
- [Pylance](https://marketplace.visualstudio.com/items?itemName=ms-python.vscode-pylance) → IntelliSense + Type Checker avançado.
    
- [Ruff](https://marketplace.visualstudio.com/items?itemName=charliermarsh.ruff) → Linter + Formatador ultra-rápido.
    
- [Python Poetry](https://marketplace.visualstudio.com/items?itemName=python-poetry.poetry-vscode) → Suporte para gerenciador de pacotes Poetry.
    
- [autoDocstring](https://marketplace.visualstudio.com/items?itemName=njpwerner.autodocstring) → Gera docstrings automáticas.
    

> 🚨 **Possível Conflito**: Ruff e Pylance têm sobreposição de funções. Recomenda-se configurar o Ruff para desativar regras duplicadas.

---

### 📓 Ambientes Interativos e Notebooks

🔹 Ferramentas para notebooks e execução interativa.

- [Jupyter](https://marketplace.visualstudio.com/items?itemName=ms-toolsai.jupyter) → Suporte completo a notebooks Jupyter.
    
- Jupyter Keymap → Atalhos no estilo clássico do Jupyter.
    
- Jupyter Cell Tags → Tags úteis para organização de células.
    
- Jupyter Notebook Renderers → Suporte a rich outputs (Plotly, LaTeX, etc.).

---

### 📊 Visualização e Dashboards

🔹 Ferramentas para análise e visualização de dados.

- [Data Preview](https://marketplace.visualstudio.com/items?itemName=RandomFractalsInc.vscode-data-preview) → Visualização tabular de datasets.
    
- [Data Wrangler](https://marketplace.visualstudio.com/items?itemName=ms-toolsai.datawrangler) → Interface visual para manipular dados.
    
- [Geo Data Viewer](https://marketplace.visualstudio.com/items?itemName=RandomFractalsInc.geo-data-viewer) → Visualização de dados geográficos.


---

### 🗃️ SQL & Banco de Dados

🔹 Ferramentas para trabalhar com SQL, formatação e validação.

- [SQL Formatter](https://marketplace.visualstudio.com/items?itemName=adpyke.vscode-sql-formatter) → Formatação de SQL.
    
- [sqlfluff](https://marketplace.visualstudio.com/items?itemName=dorzey.vscode-sqlfluff) → Linter básico e verificação de estilo SQL.
    

---

### 📄 Documentação & Diagramação

🔹 Ferramentas para documentação e geração de diagramas.

- [Markdown All in One](https://marketplace.visualstudio.com/items?itemName=yzhang.markdown-all-in-one) → Aprimora escrita em Markdown.
    
- [PlantUML](https://marketplace.visualstudio.com/items?itemName=jebbs.plantuml) → Diagramas UML com código.
    


---

### 🧹 Formatadores & Estilo de Código

🔹 Ferramentas para formatação de arquivos e padrões de estilo.

- JSON Tools
    
- JSON Formatter
    
- Rainbow CSV
    
- Edit CSV
    
- Even Better TOML
	
- **Copy Path (Unix Style)** Copy absolute and relative Windows paths to clipboard in Unix/Linux/POSIX style


---

### 🛠️ Extras & Ferramentas de Apoio

🔹 Extensões que aumentam a produtividade e suporte ao desenvolvimento.

- [GitLens](https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens) → Ferramenta avançada de Git.
    
- Docker → Suporte a ambientes isolados, deploy e containers.
    


---

### 🌐 Desenvolvimento Web e API

🔹 Ferramentas voltadas para o desenvolvimento de interfaces com foco em ciência de dados.

- [FastAPI](https://marketplace.visualstudio.com/items?itemName=tiangolo.fastapi) → Suporte ao framework FastAPI.
    
- [Django](https://marketplace.visualstudio.com/items?itemName=batisteo.vscode-django) → Suporte ao framework Django.
	
- [Thunder Client](https://marketplace.visualstudio.com/items?itemName=rangav.vscode-thunder-client) → Cliente HTTP leve e visual para testar APIs.
    

---

## CONFIGURAÇÕES INICIAIS

### 🛠️ 1. Definir o Git Bash como terminal padrão

##### Passos:

1. **Abra o VS Code**
    
2. Pressione `Ctrl + Shift + P` → digite e selecione: `Terminal: Select Default Profile`
    
3. Selecione: **Git Bash**
    

> ⚠️ Se não aparecer, você pode configurar manualmente no `settings.json`:

##### Acesse o `settings.json`:

- `Ctrl + Shift + P` → `Preferences: Open Settings (JSON)`
    

##### Adicione ou edite o seguinte bloco:
```json
"terminal.integrated.defaultProfile.windows": "Git Bash",
"terminal.integrated.profiles.windows": {
  "Git Bash": {
    "path": "C:\\Program Files\\Git\\bin\\bash.exe",
    "icon": "terminal-bash"
  }
}
```

---

### 🧠 2. Configurar Ruff + Pylance

#### 💡 Objetivo:
Configurar o Ruff e o Pylance para atuarem de forma complementar sem sobreposição de funcionalidades. Cada um atuando onde tem maior performance.

- Ruff: linter + formatador
    
- Pylance: IntelliSense + type checking (usando `pyright` por baixo dos panos)
    

---

#### 🔧 Etapas:

##### a. Desabilitar o linter interno do Pylance (para que só o Ruff atue como linter)

Adicione ao `settings.json`:

``` json
"python.linting.enabled": true,
"python.linting.ruffEnabled": true,
"python.linting.pylintEnabled": false,
"python.linting.flake8Enabled": false,
"python.linting.mypyEnabled": false,
```

---

##### b. Definir Ruff como **formatador**:

``` json
"python.formatting.provider": "ruff",
"editor.formatOnSave": true,
```
Se preferir, ative o formatador **só para arquivos Python**:

``` json
"[python]": {
  "editor.defaultFormatter": "charliermarsh.ruff",
  "editor.formatOnSave": true
}
```
---

##### c. Habilitar o **Pylance** como o IntelliSense

``` json
"python.languageServer": "Pylance",
"python.analysis.typeCheckingMode": "basic", // ou "strict" se quiser checagem mais agressiva
```

---
#### 🧪 Testando

1. Crie um script `.py` com erros de formatação e digitação
    
2. O Ruff corrigirá formatações ao salvar (`Ctrl + S`)
    
3. O Pylance mostrará erros de tipo com sublinhado


---

## **ANOTAÇÕES**

**Ao Instalar um pacote pelo terminal do VS Code, precisamos reiniciar?**
**Qual a diferença de um terminal para um Terminal Interativo?**
**O que é um Kernel?**
**Como alterar o terminal padrão do VS Code para Git Bash?**
Para utilizar o **Git Bash** como terminal padrão no VS Code, siga estes passos:

1. **Abra as configurações do VS Code**  
   - Atalho: `Ctrl + Shift + P`
   - Digite: `Preferences: Open Settings (JSON)`

2. **Adicione a configuração abaixo** ao arquivo `settings.json`:
   ```json
   {
       "terminal.integrated.defaultProfile.windows": "Git Bash",
       "terminal.integrated.profiles.windows": {
           "Git Bash": {
               "path": "C:\\Program Files\\Git\\bin\\bash.exe"
           }
       }
   }

```

## 🎯 **Objetivo**

Fazer com que o **VS Code adicione automaticamente a raiz do seu projeto (`.`)** no `PYTHONPATH`, para que **os imports relativos à estrutura de pacotes funcionem corretamente**, mesmo que você esteja dentro de subpastas do seu projeto.
```
{
  "python.envFile": "${workspaceFolder}/.env"
}
```