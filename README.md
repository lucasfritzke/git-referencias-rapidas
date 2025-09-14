# Mini Dicionário de Git

Este é um guia rápido com os termos e comandos mais comuns do Git.

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
- **Exemplo:** `git log`
- **Exemplo:** `git log --oneline` (formato resumido)

### git diff
Mostra as diferenças entre arquivos, commits ou branches.
- **Exemplo:** `git diff` (diferenças não adicionadas à staging area)
- **Exemplo:** `git diff --staged` (diferenças já adicionadas à staging area)

### git reset
Desfaz alterações ou remove arquivos da staging area.
- **Exemplo:** `git reset HEAD arquivo.txt` (remove um arquivo da staging area)
- **Exemplo:** `git reset --hard HEAD~1` (desfaz o último commit)

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
# Comandos disponíveis:
# p, pick = usar commit
# r, reword = usar commit, mas editar a mensagem
# e, edit = usar commit, mas parar para fazer alterações
# s, squash = usar commit, mas mesclar com o commit anterior
# f, fixup = como "squash", mas descarta a mensagem do commit
# d, drop = remover commit
```

**Como usar:**
1. Execute `git rebase -i HEAD~n`
2. Seu editor de texto será aberto com a lista de commits
3. Para cada linha, substitua `pick` pelo comando desejado:
   - Para remover um commit, substitua `pick` por `d` ou `drop`
   - Para combinar com o commit anterior, use `s` ou `squash`
   - Para editar a mensagem, use `r` ou `reword`
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