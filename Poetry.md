#### 🧰 `poetry`
`
Este guia apresenta as melhores práticas para configurar ambientes virtuais isolados usando o `Poetry` (versão ≥ 2.1) em conjunto com o `pyenv`. Essa combinação garante controle total sobre a versão do Python utilizada no projeto, além de proporcionar ambientes previsíveis, portáteis e rastreáveis.

[Documentação Oficial do Poetry](https://python-poetry.org/docs)

> [!✅ Benefícios da Abordagem]
> 
> - Ambientes virtuais isolados e rastreáveis
>     
> - Controle total da versão do Python
>     
> - Maior previsibilidade e portabilidade
>     
> - Facilita o versionamento e o deploy
>     
> - Evita conflitos entre dependências de projetos distintos


---

##### 📁 Navegação e Diagnóstico Inicial

```bash
# (Opcional) Navegue até a pasta do projeto (geralmente já é feito ao abrir o projeto no VS Code)
pwd                      # Verifica o diretório atual
                         # Exemplo: /c/Users/anton/lab/video_downloader_and_ia_transcription
echo $HOME               # Verifica a variável de ambiente HOME (útil para localização de pyenv)
```

---

##### 🐍 Gerenciamento de Versão com pyenv

> 💡 **Recomendação:** Configure o ambiente global do Python com uma versão diferente da que será usada no projeto com `pyenv global <versao.do.python>`. Isso ajuda a identificar rapidamente se o `pyenv` está aplicando corretamente a versão local definida em `.python-version`, pois conflitos ou esquecimentos serão mais evidentes se a versão global não corresponder.

```bash
pyenv local 3.10.0      # Define a versão do Python para o projeto
pyenv version           # Confirma a versão ativa (e origem)
python --version        # Verifica se o interpretador em uso está correto
```

> ⚠️ Se o `python` não refletir a versão do `pyenv`, pode haver conflito com variáveis de ambiente. Priorize a confirmação dessa etapa antes de seguir.

---

##### ⚙️ Configurações Locais do Poetry

a documentação pode ser consultada em: [Configurações](https://python-poetry.org/docs/configuration/)

```bash
poetry config virtualenvs.in-project true --local   # Garante que o ambiente virtual seja criado na pasta do projeto
```

---

##### 📦 Inicialização do Projeto com Poetry
Recomendo a leitura desses conteúdos complementares para maior entendimento do `poetry init` e as configurações do projeto:
- [pyproject.toml](https://python-poetry.org/docs/pyproject#the-pyprojecttoml-file)
- [[Licenças]]
- [[Versionamento]]

```bash
poetry init --no-interaction               # Cria o pyproject.toml sem interação
pyenv which python                         # Exemplo de saída: C:\Users\anton\.pyenv\pyenv-win\versions\3.10.0\python.exe
poetry env use $(pyenv which python)       # Cria o ambiente virtual usando o interpretador fornecido pelo pyenv
poetry env info                            # Mostra detalhes do ambiente, incluindo a origem do Python e o path do ambiente virtual
```

> 🎯 Verifique a saída da `poetry env info` para garantir que:
> 
> - `Python` aponta para o diretório do `pyenv`
>     
> - `Path` do ambiente virtual foi corretamente criado (em `.venv` ou conforme configuração local)
>     

OBS_1: Falar sobre as configurações extras do`pyproject.toml` como por exemplo a configuração `package-mode = false` na seção `[tool.poetry]`. 
OBS_2: Falar sobre o poetry env remove, principalmente para casos onde aconteçam problemas durante a criação da venv.

---

###### 📥 Comandos Situacionais

```bash
poetry lock      # Gera (ou atualiza) o arquivo poetry.lock com versões exatas das dependências
poetry install   # Instala todas as dependências listadas no poetry.lock
$ poetry install --no-root # Instala todas as dependências. O poetry é utilizado apenas com um gerenciador de dependencias
```

- 🔐 **poetry lock:**  
    Use este comando após definir ou atualizar dependências via `poetry add`. Ele registra as versões exatas das bibliotecas para garantir reprodutibilidade. Ideal para versionar e manter ambientes consistentes entre desenvolvedores e ambientes de produção.
    
- 🔄 **poetry install:**  
    Esse comando é usado quando você clona um projeto ou compartilha com outra pessoa. Ele lê o `poetry.lock` (se existir) e instala exatamente as mesmas versões de dependências, garantindo que o ambiente replicado seja idêntico ao original. Se não houver ambiente virtual ainda criado para o projeto, o `poetry install` cria um novo ambiente automaticamente, com base na versão do Python configurada.
    

> 💡 **Dica:** Não é necessário rodar `poetry install` após `poetry add`, pois o `add` já instala e atualiza o lock automaticamente.

---

##### 🧪 Ativação do Ambiente Virtual

**PRECISAMOS COLOCAR MAIS DETALHES SOBRE O AMBIENTE VIRTUAL** 
(ex: a ativação do ambiente pode ser opcional, pois os comandos podem ser executados com o `poetry run`)
(ex: como remover um ambiente virtual com `poetry env remove`, como recriar um ambiente e etc)

Veja abaixo três formas de ativar o ambiente:

 ✅ Opção 1: Mais recomendada (ativa direto do `.venv`)

```bash
source .venv/Scripts/activate
```

 **🔁 Opção 2: Ativação baseada no path resolvido**

```bash
source $(poetry env info --path)/Scripts/activate
```

 **🧙‍♂️ Opção 3: Usando comando do Poetry**

```bash
eval source $(poetry env activate)
```

> 💡 Dica: Em sistemas Unix-like (Linux/WSL/macOS), substitua `Scripts` por `bin` no caminho.
---
##### 🧩 Gerenciamento de Pacotes com Poetry

Este guia explica como adicionar, remover e organizar pacotes em grupos utilizando o Poetry. Ele cobre práticas recomendadas para separar dependências por contexto (produção, desenvolvimento, testes, documentação etc.) e como trabalhar com grupos opcionais para manter o ambiente limpo e flexível.

**AQUI PRECISAMOS INCLUIR [COMO CONFIGURAR REPOSITORIOS](https://python-poetry.org/docs/repositories/)** (ex: `poetry source add --priority=supplemental foo https://pypi.example.org/simple/`)

###### ➕ Adicionando Pacotes

```bash
poetry add requests                    # Adiciona ao grupo principal (produção)
poetry add black --group dev           # Adiciona ao grupo de desenvolvimento
poetry add pytest --group test         # Adiciona ao grupo de testes
poetry add -G dev flake8               # Abreviação para adicionar ao grupo dev
poetry add pandas --source foo         # Pacote de repositório Personalizado
```

###### ➖ Removendo Pacotes

```bash
poetry remove requests                 # Remove o pacote de qualquer grupo
```

---

###### 📂 Separação por Grupos

AQUI PRECISAMOS DETALHAR MELHOR  `poetry add --group <nome-do_grupo> <pacote>`
A partir do Poetry 1.2+, é possível usar **grupos nomeados** para separar dependências conforme seu contexto:

- `main` (implícito): dependências de runtime/produção
    
- `dev`: ferramentas para desenvolvimento (linters, formatadores, etc.)
    
- `test`: dependências para testes
    
- `docs`, `ci`, `build`, etc.: grupos personalizados conforme a necessidade
    

Isso melhora a organização e evita a instalação de dependências desnecessárias em ambientes críticos.

---

###### 🎯 Grupos Opcionais

Grupos opcionais não são instalados por padrão e precisam ser requisitados manualmente.

```bash
poetry add mkdocs --group docs --optional
```

No `pyproject.toml`:

```toml
[tool.poetry.group.docs]
optional = true

[tool.poetry.group.docs.dependencies]
mkdocs = "^1.5"
```

---

###### 🔁 Instalar Grupos Específicos

```bash
poetry install --with dev,test       # Instala produção + dev + test
poetry install --only main           # Instala somente dependências principais
poetry install --with all            # Instala todos os grupos definidos
```

###### 📊 Inspeção de Dependências

Esses comandos são úteis para investigar pacotes principais (diretamente adicionados) e suas dependências transitivas.
```
poetry show            # Lista todas as dependências instaladas no projeto
poetry show --tree     # Mostra a árvore de dependências (quem depende de quem)
```

---

###### 💡 Boas Práticas

- Use `--group` para separar bem responsabilidades
    
- Utilize `--optional` para dependências que não são essenciais
    
- Mantenha o `pyproject.toml` limpo e bem documentado
    
- Use `poetry show --tree` para visualizar dependências com suas relações

---
tree

---

##### 🔐 Dicas para Ambientes Restritos (Ex: Corporativos)

- Evite instalar ambientes em diretórios protegidos, como `C:/Program Files`
    
- Prefira utilizar pastas com permissão total, como `%USERPROFILE%` no Windows ou `~/` no Linux/macOS
    
- Configure o proxy da rede, se necessário:
    
    ```bash
    export HTTP_PROXY=http://proxy.exemplo.com:8080
    export HTTPS_PROXY=http://proxy.exemplo.com:8080
    export NO_PROXY=localhost,127.0.0.1
    ```
    
- Ferramentas de segurança podem bloquear scripts ou ambientes: solicite liberação caso ocorram erros
    
- Se houver bloqueios para o PyPI, utilize repositórios internos (mirrors)
