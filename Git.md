---
create_date: 2025-06-04 00:00
update: 2025-06-04 00:00
autor: AntonioJCS
tags:
  - git
  - git-bash
  - github
  - gitlab
---
# 🖥️ **PARTE I - INTRODUÇÃO**
#### 🧭 **Ecossistema Git**  
- **Git:** O motor do versionamento.
- **GitHub:** Hospedagem, colaboração, CI/CD.
- **GitLab:** Alternativa ao GitHub, com DevOps integrado.
- **Git Bash:** Terminal do Git no Windows.

### 🔗**Aulas e Tutoriais**
[Documentação Oficial do Git](https://git-scm.com/docs)⭐⭐⭐
 [Git - Tutorial Completo do Básico ao Avançado](https://www.atlassian.com/git/tutorials) ⭐
[Tudo que você precisa saber sobre GIT](https://www.youtube.com/watch?v=oi3eqnBcsJE) ⭐⭐
[App Web Para Treinar Git de forma Visual](https://git-school.github.io/visualizing-git/#free-remote)
[Entendendo GIT | (não é um tutorial!)](https://www.youtube.com/watch?v=6Czd1Yetaac)
[Usando Git Direito | Limpando seus Commits!](https://www.youtube.com/watch?v=6OokP-NE49k)
[Protegendo e Recuperando Dados Perdidos - Git, Backup, BTRFS](https://www.youtube.com/watch?v=yfEhz9poqW8)

---
## 💡 **Quando e Por Que Usar Git?**

| Benefício                | Descrição                                    | Exemplo Prático                         |
| ------------------------ | -------------------------------------------- | --------------------------------------- |
| 🛡️ **Segurança**        | Registro criptografado e rastreável          | Saber quem, quando e o que foi alterado |
| 🕰️ **Histórico**        | Você nunca perde nada                        | Recupera qualquer versão anterior       |
| 🧑‍🤝‍🧑 **Colaboração** | Trabalho em equipe sem sobrescrever mudanças | Times trabalhando juntos                |
| ⚡ **Performance**        | Rápido mesmo em projetos grandes             | Milhares de commits em segundos         |
| 🌐 **Portabilidade**     | Funciona em qualquer sistema                 | Linux, Windows, Mac                     |
| 🔄 **Offline**           | Não precisa de internet pra versionar        | Commita no avião, sincroniza depois     |

**Use Git para:**  
- Qualquer projeto de programação
- Documentos importantes (contratos, artigos)
- Trabalhos em equipe

**Evite usar para:**  
- Arquivos muito grandes (vídeos, imagens pesadas)
- Dados sensíveis sem criptografia


---

# 🖥️ **PARTE II - PRIMEIROS PASSOS**

## 🔧 **Setup Git (Windows)**

### 1. Download e Instalação
- Baixe em: [git-scm.com](https://git-scm.com)
	- [Site com Ferramentas Git](https://gitforwindows.org/)
- Execute como administrador.

### 2. Configurações Recomendadas  
Veja o que selecionar (base nas melhores práticas para ambientes Python e Data Science):

| Etapa          | Escolha Recomendada                            | Por quê?                                                   |
| -------------- | ---------------------------------------------- | ---------------------------------------------------------- |
| Diretório      | `C:\Program Files\Git`                         | Padrão do sistema                                          |
| Componentes    | ✅ Git Bash + Git GUI + Explorer Integration    | Prático no dia a dia                                       |
| Editor padrão  | Visual Studio Code                             | Ótima integração                                           |
| Branch inicial | `main`                                         | Padrão moderno, evita conflitos                            |
| PATH           | "Git from command line and 3rd-party software" | Funciona em qualquer terminal                              |
| SSH            | Use bundled OpenSSH                            | Já pronto para usar                                        |
| HTTPS          | Use OpenSSL library                            | Compatibilidade máxima em ambiente misto (Windows e Linux) |
| Line endings   | Checkout Windows-style, commit Unix-style      | Sem bugs de quebra de linha                                |
| Terminal       | Use MinTTY                                     | Experiência de terminal superior                           |
| git pull       | Default (fast-forward or merge)                | Mais seguro p/ iniciantes                                  |
| Credenciais    | Git Credential Manager                         | Segurança epraticidade                                     |

**Após instalar, abra o Git Bash e teste:**
```bash
git --version
```

---

## ⚙️ **Configuração Inicial**

### 👤 **Bash**
~/.bashrc
%USERPROFILE%/.bashrc
o arquivo seguq em anexo e deve ser colado no caminho indicado

### 👤 **Configurar Identidade**
```bash
git config --global user.name "Seu Nome Completo"
git config --global user.email "seu@email.com"
git config --global --list # Verificar configuração
```

### 🔑 **Configuração de Chave SSH**
- Gere sua chave:
```bash
ssh-keygen -t ed25519 -C "seu@email.com"
```
- Copie a chave:
```bash
cat ~/.ssh/id_ed25519.pub | clip
```
- Adicione no GitHub/GitLab ([GitHub Keys](https://github.com/settings/keys))
- Teste:
```bash
ssh -T git@github.com
```

### 💻**Configurando Proxy/HTTPS (se necessário)**

Caso sua rede corporativa ou ambiente exija uso de proxy para acessar a internet, configure o proxy no Git:

**Definindo proxy HTTP:**
```bash
git config --global http.proxy http://usuario:senha@proxy.exemplo.com:porta
```

**Definindo proxy HTTPS:**
```bash
git config --global https.proxy https://usuario:senha@proxy.exemplo.com:porta
```

Se não usar usuário/senha no proxy, basta omitir do endereço.  
Para remover o proxy:
```bash
git config --global --unset http.proxy
git config --global --unset https.proxy
```



---

## 🖱️ **Navegação no Terminal**

### 🖥️ **Comandos Básicos**

| Comando  | Para que serve                             | Exemplo                              |
| -------- | ------------------------------------------ | ------------------------------------ |
| `pwd`    | Mostra o caminho da pasta atual            | `pwd`                                |
| `ls`     | Lista arquivos e pastas                    | `ls -la`                             |
| `cd`     | Navegar entre diretórios                   | `cd projetos`                        |
| `cd ..`  | Subir um nível na hierarquia de pastas     | `cd ..`                              |
| `mkdir`  | Criar nova pasta                           | `mkdir scripts`                      |
| `touch`  | Criar arquivo vazio                        | `touch README.md`                    |
| `cat`    | Ver conteúdo de arquivos                   | `cat README.md`                      |
| `cp`     | Copiar arquivos                            | `cp a.txt b.txt`                     |
| `mv`     | Mover ou renomear arquivos                 | `mv a.txt backup/`                   |
| `rm`     | Remover arquivos ou diretórios             | `rm temp.txt`                        |
| `clear`  | Limpar a tela do terminal                  | `clear`                              |
| `grep`   | Buscar texto dentro de arquivos            | `grep "erro" logs.txt`               |
| `echo`   | Mostrar texto ou escrever em arquivo       | `echo "Oi" > saudacao.txt`           |
| `source` | Executar um script no shell atual          | `source .venv/Scripts/activate`      |
| `eval`   | Avaliar e executar uma string como comando | `eval source $(poetry env activate)` |

---

# 🚀 **Fluxo Git e seus Principais comandos**

## **Fluxo Git**

1. **📂 Diretório de Trabalho (`Working Directory`)**  
    É o ambiente local do desenvolvedor, onde os arquivos do projeto são criados, editados e removidos. Todas as modificações iniciais acontecem aqui, antes de entrarem sob controle do Git.
    
2. **📥 Área de Preparação (`Staging Area`)**  
    Área intermediária onde você adiciona arquivos modificados com o comando `git add`. Aqui você seleciona quais mudanças farão parte do próximo commit, permitindo maior controle sobre o que será registrado no histórico.
    
3. **📦 Repositório Local (`Local Repository`)**  
    Local onde os commits são efetivamente salvos, formando o histórico de versões do projeto. Cada desenvolvedor possui seu próprio repositório local, que armazena os commits de forma independente, utilizando identificadores únicos (hashes).
    
4. **🌐 Repositório Remoto (`Remote Repository`)**  
    Servidor externo (como GitHub, GitLab, Bitbucket, etc.) que armazena uma cópia compartilhada do repositório. Permite colaboração entre múltiplos desenvolvedores, backup centralizado e integração contínua de código.


```plantuml
@startuml
autonumber

' ===== PARTICIPANTES =====
participant "Diretório de Trabalho\n(Working Directory)" as Dir
participant "Área de Preparação\n(Staging Area)" as Staging
participant "Repositório Local\n(Local Repository)" as Local
participant "Repositório Remoto\n(Remote Repository)" as Remote

' ====== FLUXO PRINCIPAL =======
group Commit e Push (Salvar e Compartilhar)
  Dir -[#gray]-> Dir : git status / git log
  Dir -[#00C853]-> Staging : git add <arquivo>
  Staging -[#00C853]-> Local : git commit -m "mensagem"
  Local -[#00C853]-> Remote : git push
end

group Atualizar com mudanças do remoto
  note over Dir, Remote: **git pull** = git fetch + git merge
  Remote -[#D50000]-> Local : git fetch (baixa commits)
  Local -[#D50000]-> Dir : git merge (aplica commits)
end

group Buscar sem aplicar (fetch)
  Remote -[#D50000]-> Local : git fetch
end

group Clonar (primeiro acesso)
  Remote -[#D50000]-> Dir : git clone <repo>
end

group Branching (ramificações)
  Local -[#2962FF]-> Local : git branch <nome> (cria)
  Local -[#2962FF]-> Staging : git switch <nome> (troca)
end

group Stash (guardar alterações)
  Dir -[#2962FF]-> Local : git stash (salva temporário)
  Local -[#FFD600]-> Dir : git stash pop (recupera alterações)
end

group Conflitos de Merge
  note over Dir, Local: Ocorre se há alterações concorrentes
  Local -[#FFD600]-> Dir : git merge <branch>
  Dir -[#FFD600]-> Dir : Resolve conflitos manualmente
  Dir -[#00C853]-> Staging : git add <arquivo> (após resolver)
  Staging -[#00C853]-> Local : git commit -m "Merge resolved"
end
@enduml
```


## **Principais Comandos**
### 🟢 Inicialização e Configuração

| Tipo     | Comando | Função |
|----------|---------|--------|
| Config   | `git init` | Inicializa um repositório Git local |
| Create   | `git clone <url>` | Clona um repositório remoto |
| Config   | `git config` | Define configurações de usuário, editor, etc. |
| Config   | `git config --global user.name "Seu Nome"` | Configura nome global |
| Config   | `git config --global user.email "seu@email.com"` | Configura email global |
| Config   | `git config --global push.autoSetupRemote true` | Push automático da branch atual para remoto |

---

### 📂 Status e Inspeção

| Tipo   | Comando | Função |
|--------|---------|--------|
| Read   | `git status` | Mostra estado atual dos arquivos |
| Read   | `git diff` | Mostra diferenças entre arquivos |
| Read   | `git log` | Histórico de commits |
| Read   | `git log --oneline` | Histórico resumido |
| Read   | `git log --graph` | Histórico visual em árvore |
| Read   | `git show <hash>` | Mostra detalhes de um commit específico |

---

### 📦 Staging e Commit

| Tipo   | Comando | Função |
|--------|---------|--------|
| Update | `git add <arquivo>` | Adiciona à staging area |
| Update | `git add .` | Adiciona tudo ao staging |
| Create | `git commit -m "mensagem"` | Cria um commit |
| Update | `git commit --amend` | Edita o último commit |

---

### 🔁 Branches

| Tipo   | Comando | Função |
|--------|---------|--------|
| Read   | `git branch` | Lista branches locais |
| Create | `git branch <nome>` | Cria uma nova branch |
| Delete | `git branch -d <nome>` | Deleta uma branch local (segura) |
| Delete | `git branch -D <nome>` | Força a deleção da branch |
| Update | `git branch -m novo-nome` | Renomeia a branch atual |
| Update | `git switch <nome>` | Muda de branch |
| Create | `git switch -c <nome>` | Cria e muda para nova branch |

---

### ☁️ Repositórios Remotos

| Tipo     | Comando | Função |
|----------|---------|--------|
| Read     | `git remote -v` | Lista os remotos conectados |
| Create   | `git remote add origin <url>` | Conecta ao repositório remoto |
| Delete   | `git remote remove origin` | Remove o remoto |
| Create   | `git push` | Envia commits para o remoto |
| Create   | `git push --set-upstream origin <branch>` | Push inicial com tracking |
| Update   | `git push --force` | Push forçado (⚠️ cuidado!) |
| Update   | `git pull` | Traz atualizações do remoto |
| Read     | `git fetch` | Busca sem aplicar |

---

### 🔄 Merge e Rebase

| Tipo   | Comando | Função |
|--------|---------|--------|
| Update | `git merge <branch>` | Une branch à atual |
| Update | `git merge --strategy=ours <branch>` | Prioriza atual |
| Update | `git rebase <branch>` | Reaplica commits por cima da outra branch |
| Update | `git rebase -i HEAD~n` | Rebase interativo (editar commits) |

---

### 🧯 Desfazer e Reset

| Tipo     | Comando | Função |
|----------|---------|--------|
| Update   | `git restore <arquivo>` | Restaura arquivo do commit mais recente |
| Update   | `git restore --staged <arquivo>` | Remove do staging area |
| Delete   | `git reset --soft HEAD~1` | Remove commit, mantém staging |
| Delete   | `git reset --mixed HEAD~1` | Remove commit e staging, mantém arquivos |
| Delete   | `git reset --hard HEAD~1` | Remove commit e arquivos (⚠️ irreversível) |
| Update   | `git revert <hash>` | Desfaz commit criando novo commit |

---

### 💾 Stash (Guardar Alterações Temporárias)

| Tipo   | Comando | Função |
|--------|---------|--------|
| Create | `git stash` | Salva temporariamente alterações não commitadas |
| Read   | `git stash list` | Lista stashes salvos |
| Update | `git stash pop` | Recupera e remove stash mais recente |
| Update | `git stash apply` | Aplica stash sem remover |

---

### 🗃️ Tags e Versões

| Tipo   | Comando | Função |
|--------|---------|--------|
| Read   | `git tag` | Lista tags |
| Create | `git tag <nome>` | Cria tag leve |
| Create | `git tag -a <nome> -m "mensagem"` | Cria tag anotada |
| Create | `git push origin <tag>` | Envia tag para o remoto |

---

### 🧹 Limpeza e Ignorar Arquivos

| Tipo     | Comando | Função |
|----------|---------|--------|
| Delete   | `git clean -fd` | Remove arquivos não rastreados (⚠️ cuidado) |
| Config   | `.gitignore` | Arquivos/padrões que o Git deve ignorar |
