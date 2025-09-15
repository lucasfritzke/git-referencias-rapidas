# Mini Dicionário de Git

Este é um guia rápido com os termos e comandos mais comuns do Git.

## Índice

- [Termos Básicos](#termos-básicos)
  - [Repository (Repositório)](#repository-repositório)
  - [Clone](#clone)
  - [Commit](#commit)
  - [Parâmetros do Commit](#parâmetros-do-commit)
  - [Branch (Ramo)](#branch-ramo)
  - [Merge](#merge)
  - [Pull](#pull)
  - [Push](#push)
- [Áreas do Git](#áreas-do-git)
  - [Working Directory](#working-directory)
  - [Staging Area (Área de Preparação)](#staging-area-área-de-preparação)
  - [Repository](#repository)
- [Comandos Úteis](#comandos-úteis)
  - [git status](#git-status)
  - [git log](#git-log)
  - [git diff](#git-diff)
  - [git reset](#git-reset)
  - [git checkout](#git-checkout)
  - [git branch](#git-branch)
  - [git remote](#git-remote)
- [Fluxo de Trabalho Básico](#fluxo-de-trabalho-básico)
- [Boas Práticas para Mensagens de Commit](#boas-práticas-para-mensagens-de-commit)
  - [Formato Recomendado](#formato-recomendado)
  - [Tipos Comuns](#tipos-comuns)
  - [Usando Gitmoji](#usando-gitmoji)
  - [Exemplos](#exemplos)
  - [Dicas](#dicas)
- [Situações Comuns](#situações-comuns)
  - [Ignorar Arquivos](#ignorar-arquivos)
  - [Resolver Conflitos](#resolver-conflitos)
  - [Salvar Alterações Temporárias](#salvar-alterações-temporárias)
  - [Editar o Último Commit](#editar-o-último-commit)
  - [Navegar pelo Histórico e Trabalhar com Commits Antigos](#navegar-pelo-histórico-e-trabalhar-com-commits-antigos)
- [Operações Avançadas](#operações-avançadas)
  - [Rebase](#rebase)
  - [Squash](#squash)
  - [Cherry-pick](#cherry-pick)
  - [Rebase Interativo](#rebase-interativo)
  - [Reflog](#reflog)
  - [Bisect](#bisect)

## Termos Básicos

### Repository (Repositório)
Um repositório Git é um local onde o Git armazena todos os arquivos, histórico e metadados do seu projeto.
- **Exemplo:** `git init` (cria um novo repositório local)

### Clone
Cria uma cópia de um repositório remoto em seu ambiente local.
- **Exemplo:** `git clone https://github.com/usuario/repositorio.git`

### Commit
Um snapshot do seu repositório em um determinado momento. Cada commit tem uma mensagem descritiva.
- **Exemplo:** `git commit -m "Adiciona funcionalidade de login"`

### Parâmetros do Commit
O comando `git commit` possui diversos parâmetros úteis para diferentes situações:

- **`-m "<mensagem>"`**: Especifica a mensagem do commit
  - Exemplo: `git commit -m "Adiciona autenticação por email"`

- **`-a` ou `--all`**: Adiciona automaticamente todas as modificações de arquivos já rastreados (tracked)
  - Exemplo: `git commit -a -m "Atualiza configurações"`

- **`--amend`**: Modifica o último commit em vez de criar um novo
  - Exemplo: `git commit --amend -m "Nova mensagem corrigida"`
  - Exemplo: `git commit --amend --no-edit` (mantém a mesma mensagem)

- **`-S` ou `--gpg-sign`**: Assina o commit usando GPG
  - Exemplo: `git commit -S -m "Commit assinado com GPG"`

- **`--no-verify`**: Ignora os hooks de pre-commit e commit-msg
  - Exemplo: `git commit --no-verify -m "Commit rápido sem verificações"`

- **`--author="Nome <email>"`**: Especifica um autor diferente para o commit
  - Exemplo: `git commit -m "Mensagem" --author="João Silva <joao@exemplo.com>"`

- **`--date="YYYY-MM-DD HH:MM:SS"`**: Define uma data específica para o commit
  - Exemplo: `git commit -m "Mensagem" --date="2023-10-15 14:30:00"`

- **`-p` ou `--patch`**: Permite selecionar quais partes (hunks) de cada arquivo modificado serão incluídas no commit
  - Exemplo: `git commit -p`

- **`--fixup=<commit>`**: Marca o commit como uma correção para ser incorporada em um commit específico durante um rebase interativo
  - Exemplo: `git commit --fixup=abc123 -m "Corrige bug no login"`

- **`--squash=<commit>`**: Similar ao fixup, mas preserva a mensagem do commit para revisão durante o rebase
  - Exemplo: `git commit --squash=abc123 -m "Ajustes adicionais de login"`

- **`--allow-empty`**: Permite criar um commit sem alterações (útil para triggering CI/CD)
  - Exemplo: `git commit --allow-empty -m "Dispara build"`

- **`--dry-run`**: Mostra o que seria commitado sem realmente fazer o commit
  - Exemplo: `git commit --dry-run -m "Teste"`

### Branch (Ramo)
Versões paralelas do repositório que permitem trabalhar em diferentes funcionalidades simultaneamente.
- **Exemplo:** `git branch feature-login` (cria uma nova branch)
- **Exemplo:** `git checkout feature-login` (muda para a branch criada)
- **Exemplo:** `git checkout -b feature-login` (cria e muda para a nova branch)

### Merge
Combina alterações de uma branch em outra.
- **Exemplo:** `git merge feature-login` (integra a branch feature-login à branch atual)

### Pull
Atualiza seu repositório local com as mudanças do repositório remoto.
- **Exemplo:** `git pull origin main`

### Push
Envia commits locais para o repositório remoto.
- **Exemplo:** `git push origin main`

## Áreas do Git

### Working Directory
Área onde você trabalha com seus arquivos, faz alterações e cria novos arquivos.

### Staging Area (Área de Preparação)
Área intermediária onde você coloca arquivos modificados antes de fazer um commit.
- **Exemplo:** `git add arquivo.txt` (adiciona um arquivo à staging area)
- **Exemplo:** `git add .` (adiciona todos os arquivos modificados)

### Repository
Onde todos os commits são armazenados, representando o histórico do projeto.

## Comandos Úteis

### git status
Mostra o estado atual do repositório, incluindo arquivos modificados, adicionados ou removidos.
- **Exemplo:** `git status`

### git log
Exibe o histórico de commits.
- **Exemplo:** `git log` (exibe o histórico completo)
- **Exemplo:** `git log --oneline` (formato resumido, uma linha por commit)
- **Exemplo:** `git log -n 5` (exibe apenas os 5 últimos commits)
- **Exemplo:** `git log --author="nome"` (filtra por autor)
- **Exemplo:** `git log --since="2023-01-01" --until="2023-12-31"` (filtra por período)
- **Exemplo:** `git log --grep="feature"` (busca por palavra-chave nas mensagens)
- **Exemplo:** `git log --graph --oneline --all` (visualização gráfica de todos os branches)

### git diff
Mostra as diferenças entre arquivos, commits ou branches.
- **Exemplo:** `git diff` (diferenças não adicionadas à staging area)
- **Exemplo:** `git diff --staged` (diferenças já adicionadas à staging area)

### git reset
Desfaz alterações ou remove arquivos da staging area.
- **Exemplo:** `git reset HEAD arquivo.txt` (remove um arquivo da staging area)
- **Exemplo:** `git reset --hard HEAD~1` (desfaz o último commit)

### git checkout
Navega entre branches ou commits específicos.
- **Exemplo:** `git checkout feature-branch` (muda para outra branch)
- **Exemplo:** `git checkout -b nova-branch` (cria e muda para uma nova branch)
- **Exemplo:** `git checkout a1b2c3d` (navega para um commit específico, colocando o repositório em estado "detached HEAD")
- **Exemplo:** `git checkout a1b2c3d -- arquivo.txt` (recupera um arquivo específico do commit a1b2c3d)

### git branch
Gerencia branches (ramos) no repositório.
- **Exemplo:** `git branch` (lista todas as branches locais)
- **Exemplo:** `git branch -a` (lista branches locais e remotas)
- **Exemplo:** `git branch nova-branch` (cria uma nova branch)
- **Exemplo:** `git branch -d feature-branch` (deleta uma branch)
- **Exemplo:** `git branch nova-branch a1b2c3d` (cria uma nova branch a partir de um commit específico)

### git remote
Gerencia conexões com repositórios remotos.
- **Exemplo:** `git remote -v` (lista repositórios remotos)
- **Exemplo:** `git remote add origin https://github.com/usuario/repositorio.git`

## Fluxo de Trabalho Básico

1. Faça alterações nos arquivos (`Working Directory`)
2. Adicione as alterações à área de preparação (`git add`)
3. Faça um commit das alterações (`git commit`)
4. Envie as alterações para o repositório remoto (`git push`)

## Boas Práticas para Mensagens de Commit

Uma boa mensagem de commit deve ser clara, concisa e informativa. Seguir um padrão consistente melhora a legibilidade do histórico do projeto.

### Formato Recomendado

```
<tipo>(<escopo>): <assunto>

<corpo>

<rodapé>
```

### Tipos Comuns
- **feat**: Nova funcionalidade
- **fix**: Correção de bug
- **docs**: Alterações na documentação
- **style**: Alterações que não afetam o código (formatação, espaços em branco, etc.)
- **refactor**: Refatoração de código sem alteração de funcionalidade
- **perf**: Melhorias de performance
- **test**: Adição ou correção de testes
- **chore**: Alterações em processos de build, ferramentas, etc.

### Usando Gitmoji

Gitmoji é uma convenção que utiliza emojis no início das mensagens de commit para identificar visualmente o propósito do commit. Você pode combiná-los com o formato Conventional Commits descrito acima.

#### Formato com Gitmoji

```
<emoji> <tipo>(<escopo>): <assunto>

<corpo>

<rodapé>
```

#### Emojis Comuns e Seus Significados

| Emoji | Código | Significado | Equivalente Conventional Commits |
|-------|--------|-------------|----------------------------------|
| ✨    | `:sparkles:` | Nova funcionalidade | **feat** |
| 🐛    | `:bug:` | Correção de bug | **fix** |
| 📝    | `:memo:` | Documentação | **docs** |
| 💄    | `:lipstick:` | UI/Estilo | **style** |
| ♻️     | `:recycle:` | Refatoração | **refactor** |
| ⚡️    | `:zap:` | Performance | **perf** |
| ✅    | `:white_check_mark:` | Testes | **test** |
| 🔧    | `:wrench:` | Configuração | **chore** |
| 🚀    | `:rocket:` | Deploy | - |
| 🔖    | `:bookmark:` | Release/Versão | - |
| 🔒    | `:lock:` | Segurança | - |
| ⬆️     | `:arrow_up:` | Atualização de dependências | - |
| 🚧    | `:construction:` | Trabalho em progresso | - |
| 💩    | `:poop:` | Código ruim que precisa ser melhorado | - |
| 🔀    | `:twisted_rightwards_arrows:` | Merge de branches | - |

#### Exemplos com Gitmoji

```
✨ feat(auth): implementa autenticação por dois fatores

Adiciona suporte para autenticação via SMS e e-mail.
Inclui testes de integração e documentação.

Closes #123
```

```
🐛 fix(api): corrige erro no endpoint de pagamento

Resolve o problema de timeout que ocorria em transações acima de R$10.000

Issue: #456
```

#### Como Usar na Prática

1. No terminal, ao fazer commit:
   ```
   git commit -m "✨ feat(auth): implementa autenticação por dois fatores"
   ```

2. Ou usando editores como Vim:
   ```
   ✨ feat(auth): implementa autenticação por dois fatores

   Adiciona suporte para autenticação via SMS e e-mail.
   Inclui testes de integração e documentação.

   Closes #123
   ```

3. Existem ferramentas como o [gitmoji-cli](https://github.com/carloscuesta/gitmoji-cli) que facilitam o uso:
   ```
   npm install -g gitmoji-cli
   gitmoji -c  # Inicia commit interativo com seleção de emoji
   ```

#### Guia Rápido do Vim para Mensagens de Commit

Quando você executa `git commit` sem a flag `-m`, o Git abre o editor padrão (frequentemente o Vim) para escrever a mensagem de commit. Aqui estão os comandos essenciais do Vim para esta tarefa:

| Comando | Ação | Contexto de Uso |
|---------|------|----------------|
| `Esc` | Sai do modo de inserção | Use quando terminar de digitar ou precisar executar um comando |
| `i` | Entra no modo de inserção | Use para começar a digitar texto |
| `a` | Entra no modo de inserção após o cursor | Útil para continuar escrevendo após um caractere |
| `o` | Insere uma nova linha abaixo e entra no modo de inserção | Ideal para adicionar o corpo da mensagem |
| `dd` | Exclui a linha atual | Remover linhas não desejadas (comentários, etc.) |
| `:wq` | Salva e sai | Quando terminar sua mensagem de commit |
| `:q!` | Sai sem salvar | Para cancelar o commit |

**Fluxo típico para mensagem de commit no Vim:**

1. Git abre o Vim com um template da mensagem de commit
2. Pressione `i` para entrar no modo de inserção
3. Digite a linha de assunto (ex: `✨ feat(auth): implementa login`)
4. Pressione `o` para criar uma linha em branco e continuar no modo de inserção
5. Digite o corpo da mensagem
6. Pressione `Esc` para sair do modo de inserção
7. Digite `:wq` e pressione `Enter` para salvar e finalizar o commit

**Dica:** Configure o Vim para destacar a sintaxe de mensagens de commit adicionando ao seu `~/.vimrc`:
```
autocmd FileType gitcommit setlocal spell textwidth=72
```

### Exemplos
```
feat(auth): implementa autenticação por dois fatores

Adiciona suporte para autenticação via SMS e e-mail.
Inclui testes de integração e documentação.

Closes #123
```

```
fix(api): corrige erro no endpoint de pagamento

Resolve o problema de timeout que ocorria em transações acima de R$10.000

Issue: #456
```

### Dicas
- Limite o assunto a 50 caracteres
- Use o imperativo presente no assunto ("adiciona", não "adicionando" ou "adicionado")
- Não termine o assunto com ponto
- Separe o assunto do corpo com uma linha em branco
- Use o corpo para explicar "o que" e "por que", não "como"
- Referencie issues e pull requests no rodapé

## Situações Comuns

### Ignorar Arquivos
Use um arquivo `.gitignore` para especificar arquivos ou diretórios que o Git deve ignorar.
- **Exemplo:** Crie um arquivo `.gitignore` e adicione padrões como `*.log`, `node_modules/`, etc.

### Resolver Conflitos
Quando o mesmo arquivo é modificado em diferentes branches, pode ocorrer um conflito durante o merge.
1. Git marca os conflitos nos arquivos
2. Edite os arquivos para resolver os conflitos
3. Adicione os arquivos resolvidos (`git add`)
4. Complete o merge (`git commit`)

### Salvar Alterações Temporárias
Use `git stash` para salvar alterações temporárias sem fazer commit.
- **Exemplo:** `git stash` (salva alterações)
- **Exemplo:** `git stash pop` (recupera alterações salvas)

### Editar o Último Commit

Existem várias razões para editar o último commit: corrigir a mensagem, adicionar arquivos esquecidos ou fazer pequenos ajustes no código. Aqui estão as maneiras de fazer isso:

#### 1. Alterar Apenas a Mensagem do Último Commit

```bash
git commit --amend -m "Nova mensagem melhorada"
```

#### 2. Adicionar Alterações ao Último Commit

```bash
# Faça as alterações nos arquivos
git add .                          # Adicione as alterações à área de preparação
git commit --amend --no-edit       # Adiciona ao último commit mantendo a mesma mensagem
```

#### 3. Editar a Mensagem com o Editor (Vim)

```bash
git commit --amend                 # Abre o editor para modificar a mensagem
```

Quando o editor abrir:
1. Pressione `i` para entrar no modo de inserção
2. Edite a mensagem
3. Pressione `Esc` e digite `:wq` para salvar e sair

#### 4. Editar Commit Já Enviado ao Repositório Remoto

Se você já enviou o commit para o repositório remoto, precisará usar força para substituí-lo:

```bash
git commit --amend                 # Faça as alterações necessárias
git push --force-with-lease origin <branch>  # Envia as alterações com segurança
```

**IMPORTANTE:** Nunca use `--force` ou `--force-with-lease` em branches compartilhadas como `main` ou `develop`. Isso pode causar problemas para outros desenvolvedores.

#### 5. Editar Commits Mais Antigos

Para editar commits além do último, use o rebase interativo:

```bash
git rebase -i HEAD~n               # Onde n é o número de commits para trás que você quer editar
```

### Resolver Erros Comuns durante Rebase e Merge

#### Erro: "Your local changes would be overwritten by checkout"

Este erro ocorre quando você tenta mudar de branch, fazer rebase ou merge com alterações não commitadas no working directory.

```
error: Your local changes to the following files would be overwritten by checkout:
        README.md
Please commit your changes or stash them before you switch branches.
Aborting
```

**Soluções:**

1. **Commit suas alterações primeiro:**
   ```bash
   git add .
   git commit -m "Mensagem descritiva sobre suas alterações"
   # Agora tente o rebase novamente
   git rebase -i HEAD~2
   ```

2. **Use stash para guardar temporariamente as alterações:**
   ```bash
   git stash save "Descrição das alterações"
   # Faça o rebase
   git rebase -i HEAD~2
   # Depois recupere as alterações
   git stash pop
   ```

3. **Se quiser descartar as alterações locais:**
   ```bash
   git checkout -- README.md  # Descarta mudanças em um arquivo específico
   # OU
   git reset --hard           # Descarta todas as mudanças (use com cuidado!)
   # Agora tente o rebase novamente
   git rebase -i HEAD~2
   ```

#### Erro: "Merge conflict in [arquivo]"

Este erro ocorre durante rebase ou merge quando o Git não consegue conciliar automaticamente as alterações:

**Soluções:**

1. **Resolva os conflitos manualmente:**
   - Abra os arquivos com conflitos e procure por marcadores como `<<<<<<<`, `=======`, e `>>>>>>>`
   - Edite os arquivos para resolver os conflitos
   - Adicione os arquivos resolvidos: `git add .`
   - Continue o rebase: `git rebase --continue`

2. **Abortar a operação:**
   ```bash
   git rebase --abort  # Para cancelar o rebase
   # OU
   git merge --abort   # Para cancelar o merge
   ```

### Navegar pelo Histórico e Trabalhar com Commits Antigos

#### Visualizar o Histórico de Commits

Para ver o histórico de commits de forma eficiente:

```bash
git log --oneline --graph --all    # Mostra histórico resumido com representação gráfica
git log -n 10                      # Mostra apenas os 10 commits mais recentes
git log --author="Nome"            # Filtra commits por autor
git log --since="1 week ago"       # Filtra commits da última semana
```

#### Voltar a um Commit Específico

Existem diferentes formas de voltar a um commit anterior, dependendo do objetivo:

1. **Para apenas examinar o código em um commit antigo (modo "detached HEAD"):**
   ```bash
   git checkout a1b2c3d            # Substitua a1b2c3d pelo hash do commit
   ```
   **Observação:** Neste modo, qualquer alteração que você fizer não estará associada a nenhuma branch.

2. **Para desfazer commits, mantendo as alterações no working directory:**
   ```bash
   git reset a1b2c3d               # Mantém as alterações dos commits desfeitos como não-commitadas
   ```

3. **Para desfazer completamente commits (descartando alterações):**
   ```bash
   git reset --hard a1b2c3d        # Retorna ao estado exato do commit a1b2c3d
   ```
   **CUIDADO:** Esta operação descarta permanentemente todas as alterações feitas após o commit especificado.

4. **Para reverter um commit, criando um novo commit que desfaz as alterações:**
   ```bash
   git revert a1b2c3d              # Cria um novo commit que desfaz as alterações do commit a1b2c3d
   ```
   Este é o método mais seguro para branches compartilhadas.

#### Criar uma Nova Branch a Partir de um Commit Antigo

Para experimentar alternativas ou corrigir bugs a partir de um ponto específico do histórico:

```bash
# Método 1: A partir do estado atual
git checkout a1b2c3d               # Primeiro, vá para o commit desejado
git checkout -b nova-feature       # Crie uma nova branch a partir deste commit

# Método 2: Diretamente em um comando
git checkout -b nova-feature a1b2c3d  # Cria a branch e faz checkout em um único comando

# Método 3: Usando branch sem mudar para ela
git branch nova-feature a1b2c3d    # Cria a branch mas mantém você na branch atual
```

**Uso Comum:** Esta técnica é útil para:
- Criar uma branch de correção baseada em uma versão específica
- Experimentar caminhos alternativos de desenvolvimento
- Recuperar código que foi removido em commits posteriores

## Operações Avançadas

### Rebase
Reaplica commits de uma branch em cima de outra branch. Diferente do merge, o rebase reescreve o histórico de commits, criando uma linha de desenvolvimento mais limpa.

- **Exemplo básico:** `git rebase main` (estando em uma branch feature, reaplica os commits da feature em cima da main)
- **Exemplo interativo:** `git rebase -i HEAD~3` (modo interativo para os últimos 3 commits)

### Squash
Combina múltiplos commits em um único commit. Geralmente usado para criar um histórico mais limpo antes de mesclar uma branch.

- **Exemplo:** Usando rebase interativo (`git rebase -i HEAD~3`), mude `pick` para `squash` ou `s` nas linhas dos commits que deseja combinar com o commit anterior.

### Cherry-pick
Aplica as alterações de commits específicos para a branch atual.

- **Exemplo:** `git cherry-pick abc123` (aplica as alterações do commit abc123 à branch atual)
- **Exemplo múltiplo:** `git cherry-pick abc123 def456` (aplica vários commits)

### Rebase Interativo
O rebase interativo permite manipular commits de diversas formas, usando um editor de texto (como Vim, Nano ou o que estiver configurado no Git).

Ao executar `git rebase -i HEAD~n` (onde n é o número de commits a serem editados), você verá uma lista de commits e poderá usar os seguintes comandos:

```
# Comandos disponíveis no rebase interativo:
# p, pick <commit> = usar commit sem alterações
# r, reword <commit> = usar commit, mas editar a mensagem de commit
# e, edit <commit> = usar commit, mas pausar para fazer alterações (amend)
# s, squash <commit> = usar commit, mas combiná-lo com o commit anterior
# f, fixup [-C | -c] <commit> = como "squash", mas descarta a mensagem deste commit
#                    Se -C for usado, descarta a mensagem do commit anterior
#                    Se -c for usado, abre o editor para editar a mensagem combinada
# x, exec <comando> = executa um comando shell durante o rebase
# b, break = pausa o rebase neste ponto (continue depois com 'git rebase --continue')
# d, drop <commit> = remove completamente o commit
# l, label <label> = define um rótulo para o HEAD atual
# t, reset <label> = redefine o HEAD para um rótulo definido anteriormente
# m, merge [-C <commit> | -c <commit>] <label> [# <oneline>] = cria um commit de merge
```

**Detalhes dos comandos:**

1. **pick**: O comando padrão. Mantém o commit como está.
   - Exemplo: `pick abc123 Adiciona funcionalidade de login`

2. **reword**: Permite alterar apenas a mensagem do commit.
   - Exemplo: `reword abc123 Adiciona funcionalidade de login`
   - O rebase pausará e abrirá um editor para você modificar a mensagem.

3. **edit**: Permite fazer alterações no commit.
   - Exemplo: `edit abc123 Adiciona funcionalidade de login`
   - O rebase pausará após aplicar este commit, permitindo que você faça alterações com `git commit --amend`.
   - Continue com `git rebase --continue` após terminar.

4. **squash**: Combina o commit com o commit anterior, mantendo ambas as mensagens.
   - Exemplo: `squash def456 Corrige bug na funcionalidade de login`
   - O rebase abrirá um editor para você editar a mensagem combinada.

5. **fixup**: Combina o commit com o anterior, mas descarta a mensagem deste commit.
   - Exemplo: `fixup def456 Corrige bug na funcionalidade de login`
   - Com `-C`: `fixup -C def456` mantém apenas a mensagem deste commit.
   - Com `-c`: `fixup -c def456` abre o editor para editar, mas prioriza a mensagem deste commit.

6. **exec**: Executa um comando shell.
   - Exemplo: `exec npm test` (executa testes após cada commit processado)
   - Útil para verificar se o código ainda funciona durante o rebase.

7. **break**: Pausa o rebase para você fazer alterações manuais.
   - Continue posteriormente com `git rebase --continue`.

8. **drop**: Remove completamente um commit.
   - Exemplo: `drop abc123 Commit desnecessário`

9. **label**: Define um rótulo (referência) para o estado atual.
   - Exemplo: `label base_stable`

10. **reset**: Retorna ao estado marcado por um rótulo.
    - Exemplo: `reset base_stable`

11. **merge**: Cria um commit de merge durante o rebase.
    - Exemplo: `merge feature_xyz Nova versão da funcionalidade XYZ`

**Como usar:**
1. Execute `git rebase -i HEAD~n`
2. Seu editor de texto será aberto com a lista de commits
3. Para cada linha, substitua `pick` pelo comando desejado
4. Salve e feche o arquivo para continuar o rebase
5. Siga as instruções adicionais se necessário

**Exemplo prático:**
```
# Original:
pick abc123 Adiciona recurso de login
pick def456 Corrige erro de digitação
pick ghi789 Adiciona testes para login

# Para combinar os dois últimos commits com o primeiro:
pick abc123 Adiciona recurso de login
s def456 Corrige erro de digitação
s ghi789 Adiciona testes para login

# Para remover o commit do meio:
pick abc123 Adiciona recurso de login
d def456 Corrige erro de digitação
pick ghi789 Adiciona testes para login
```

**Dicas para rebase interativo:**
- Ordem de processamento: do mais antigo (topo) para o mais recente (baixo)
- Você pode reordenar as linhas para mudar a ordem dos commits
- Se ocorrerem conflitos, resolva-os e use `git rebase --continue`
- Para cancelar o rebase, use `git rebase --abort`
- Nunca faça rebase de commits que já foram enviados para um repositório compartilhado

### Reflog
Mantém um registro de todas as alterações na referência HEAD, mesmo após operações como reset, rebase, etc. É uma ferramenta de recuperação poderosa.

- **Exemplo:** `git reflog` (mostra o histórico de referências)
- **Exemplo de recuperação:** `git reset --hard HEAD@{2}` (volta para o estado de 2 operações atrás)

### Bisect
Ajuda a encontrar qual commit introduziu um bug usando busca binária.

- **Exemplo:**
  ```
  git bisect start
  git bisect bad  # marca o commit atual como ruim
  git bisect good abc123  # marca um commit conhecido como bom
  # Git fará checkout de um commit intermediário para você testar
  # Após testar, use "git bisect good" ou "git bisect bad" para continuar
  git bisect reset  # quando terminar
  ```

---
*Este mini dicionário é um guia básico. Para informações mais detalhadas, consulte a [documentação oficial do Git](https://git-scm.com/doc).*