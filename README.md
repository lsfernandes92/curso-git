<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [Outro guia de git](#outro-guia-de-git)
    - [Trabalhando em Equipe com Controle e Segurança](#trabalhando-em-equipe-com-controle-e-seguran%C3%A7a)
      - [Principais benefícios do Git:](#principais-benef%C3%ADcios-do-git)
    - [Alguns comandos de funcionalidade do git:](#alguns-comandos-de-funcionalidade-do-git)
    - [$git rebase](#git-rebase)
    - [$git stash](#git-stash)
    - [$git checkout](#git-checkout)
    - [$git reset HEAD [nome_arquivo]](#git-reset-head-nome_arquivo)
    - [$git reset [hash_commit]](#git-reset-hash_commit)
- [Editando commits](#editando-commits)
    - [O que acabei de comitar?](#o-que-acabei-de-comitar)
    - [Escrevi a ultima mensagem de commit errada antes de dar push](#escrevi-a-ultima-mensagem-de-commit-errada-antes-de-dar-push)
    - [Escrevi a mensagem de commit errada antes de dar push](#escrevi-a-mensagem-de-commit-errada-antes-de-dar-push)
    - [Quero juntar meus commits](#quero-juntar-meus-commits)
    - [Quero adicionar minhas novas alterações no ultimo commit](#quero-adicionar-minhas-novas-altera%C3%A7%C3%B5es-no-ultimo-commit)
    - [Comitei com o usuario e email errado](#comitei-com-o-usuario-e-email-errado)
    - [Quero deletar meu ultimo commit](#quero-deletar-meu-ultimo-commit)
    - [Acidentalmente eu dei um reset hard para outro commit, como volto reverto isso?](#acidentalmente-eu-dei-um-reset-hard-para-outro-commit-como-volto-reverto-isso)
    - [Todos meus commits foram com email e autor errado, consigo alterar?](#todos-meus-commits-foram-com-email-e-autor-errado-consigo-alterar)
- [Staging](#staging)
    - [Queria adicionar alterações Staged's(após git add) no commit anterior](#queria-adicionar-altera%C3%A7%C3%B5es-stagedsap%C3%B3s-git-add-no-commit-anterior)
- [Untracked files](#untracked-files)
    - [Como deleto o tal dos untracked files do meu `git status`](#como-deleto-o-tal-dos-untracked-files-do-meu-git-status)
- [Branches](#branches)
    - [Quero deletar minha branch remota](#quero-deletar-minha-branch-remota)
    - [Quero renomear uma branch](#quero-renomear-uma-branch)
    - [Acidentalmente exclui minha branch, e agora?](#acidentalmente-exclui-minha-branch-e-agora)
    - [Acidentalmente exclui minha branch, mas ela não aparece no `reflog`. E agora?](#acidentalmente-exclui-minha-branch-mas-ela-n%C3%A3o-aparece-no-reflog-e-agora)
- [Outros](#outros)
    - [Tutoriais](#tutoriais)
    - [Dicas](#dicas)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# Outro guia de git
### Trabalhando em Equipe com Controle e Segurança

Um guia que explora os benefícios de utilizar o Git como ferramenta de controle de versão para projetos em qualquer linguagem, em qualquer plataforma.

#### Principais benefícios do Git:
* Funciona de maneira distribuída
* Permite a edição concorrente de arquivos do projeto
* Não depende de uma conexão ativa com um servidor
* Mantém histórico do que é feito no projeto
* Marca diferentes versões para o projeto
* Controle total do que se passa e do que pode ser feito com o seu repositóriooo

### Alguns comandos de funcionalidade do git:
### $git rebase
* Evita vários commits de merge
* Evita commits de merge desnecessários

### $git stash
* Utilizado para deixar o desenvolvimento atual salvo
* Usado para arrumar bugs antes de fazer commits inacabados

### $git checkout
* Apaga tudo feito no working directory

### $git reset HEAD [nome_arquivo]
* Apaga tudo que está no index

### $git reset [hash_commit]
* Reseta tudo até o hash do commit

# Editando commits
### O que acabei de comitar?
`$git show` ou `$git log --oneline`

### Escrevi a ultima mensagem de commit errada antes de dar push
`$git commit --amend`

ou

`$git commit --amend -m "xxxxx"`

### Escrevi a mensagem de commit errada antes de dar push
Supondo um git log igual ao abaixo:

´´´
fbb654d (HEAD -> master) Update editing commits section
e3228e7 Update README with untracked files section and more tips and tutorials
9489f92 Added section for recover branch deleted with none reflog
05ca271 Deleted '.DS_Store' files
´´´

Também supondo que quero alterar texto do commit **05ca271**

`$git rebase -i '05ca271^'`

No seu editor de texto padrao irá aparecer algo como:

´´´
 1 pick 05ca271 Deleted '.DS_Store' files
 2 pick 9489f92 Added section for recover branch deleted with none reflog
 3 pick e3228e7 Update README with untracked files section and more tips and tutorials
 4 pick fbb654d Update editing commits section
 5
 6 # Rebase 82e0d8a..fbb654d onto 82e0d8a (4 commands)
 7 #
 8 # Commands:
 9 # p, pick = use commit
10 # r, reword = use commit, but edit the commit message
11 # e, edit = use commit, but stop for amending
12 # s, squash = use commit, but meld into previous commit
13 # f, fixup = like "squash", but discard this commit's log message
14 # x, exec = run command (the rest of the line) using shell
15 # d, drop = remove commit
´´´

Alteramos a linha 1 para `1 reword 05ca271 Delete '.DS_Store' file`

No seu editor que irá abrir faça as alterações e salve

### Quero juntar meus commits
Supondo um git log igual ao abaixo:

´´´
fbb654d (HEAD -> master) Update editing commits section
e3228e7 Update README with untracked files section and more tips and tutorials
9489f92 Added section for recover branch deleted with none reflog
05ca271 Deleted '.DS_Store' files
´´´

Também supondo que quero juntar os dois ultimos commits

`$git rebase -i '05ca271^'`

No seu editor de texto padrao irá aparecer algo como:

´´´
 1 pick 05ca271 Deleted '.DS_Store' files
 2 pick 9489f92 Added section for recover branch deleted with none reflog
 3 pick e3228e7 Update README with untracked files section and more tips and tutorials
 4 pick fbb654d Update editing commits section
 5
 6 # Rebase 82e0d8a..fbb654d onto 82e0d8a (4 commands)
 7 #
 8 # Commands:
 9 # p, pick = use commit
10 # r, reword = use commit, but edit the commit message
11 # e, edit = use commit, but stop for amending
12 # s, squash = use commit, but meld into previous commit
13 # f, fixup = like "squash", but discard this commit's log message
14 # x, exec = run command (the rest of the line) using shell
15 # d, drop = remove commit
´´´

Alteramos a linha 1 para `2 squash 9489f92 Added section for recover branch deleted with none reflog`

No seu editor que irá abrir faça as alterações com a nova mensagem de commit e salve

### Quero adicionar minhas novas alterações no ultimo commit

`$git add .` para adicionar as alterações para stage

`$git commit --amend --no-edit` para adicionar as alterações no commit anterior sem editar a mensagem de já comitada. Ou sem a opção **--no-edit** para editar a mensagem do commit anterior.

### Comitei com o usuario e email errado
`$git commit --amend --author "Novo author <emailautor@dominio.com>"`

### Quero deletar meu ultimo commit
Não recomendado e pois alguem pode peder a referencia dos commits resetados, mas um jeito de deletar um commit após o push é:

`$git reset HEAD^ --hard`

`$git push --force-with-lease [remote] [branch]`

Jeito recomendado...

`$git revert <SHAdoCommitEraddo>`

Para resetar se você ainda não deu push

`$git reset --mixed HEAD^` - (default) retorna o commit e as mudanças ficam no working directory
`$git reset --soft HEAD^` - retorna commit e mudanças permanecem staged(index)
`$git reset --hard HEAD^` - apaga tudo, retorna commit, unstage e deleta

Para todas opções pode-se utilizar **HEAD~1** no lugar do **HEAD^**

### Acidentalmente eu dei um reset hard para outro commit, como volto reverto isso?
Você acidentalmente fez isso? Se fodeo! Já era! Brinks... O git mantém um log de tudo por alguns dias(foda, não?).

`(master)$ git reflog`

Você verá uma lista dos commits passados. Só escolher o SHA do tal commit e resetar para ele.

`(master)$ git reset --hard <SHACommitResetaHardimente>`

### Todos meus commits foram com email e autor errado, consigo alterar?
Yes! Github tem uma página pública com isso, mas basicamente é o seguinte:

* Abra o terminal
* De um "bare" clone
  * `git clone --bare https://github.com/user/repo.git`
  * `cd repo.git`
* Copie e cole o script alterando as variáveis(OLD_EMAIL, CORRECT_NAME, CORRECT_EMAIL) com suas informações
```
git filter-branch --env-filter '
OLD_EMAIL="your-old-email@example.com"
CORRECT_NAME="Your Correct Name"m
CORRECT_EMAIL="your-correct-email@example.com"
if [ "$GIT_COMMITTER_EMAIL" = "$OLD_EMAIL" ]
then
    export GIT_COMMITTER_NAME="$CORRECT_NAME"
    export GIT_COMMITTER_EMAIL="$CORRECT_EMAIL"
fi
if [ "$GIT_AUTHOR_EMAIL" = "$OLD_EMAIL" ]
then
    export GIT_AUTHOR_NAME="$CORRECT_NAME"
    export GIT_AUTHOR_EMAIL="$CORRECT_EMAIL"
fi
' --tag-name-filter cat -- --branches --tags
```
* Dê um enter
* Revise o log de commits
* Dê um push para o repo
  * `git push --force --tags origin 'refs/heads/*'`
* Apague o repo temporário
  * `cd ..`
  * `rm -rf repo.git`

[Link referência do GitHub](https://help.github.com/articles/changing-author-info/)

# Staging
### Queria adicionar alterações Staged's(após git add) no commit anterior
`(branch)$git commit --amend`

# Untracked files
### Como deleto o tal dos untracked files do meu `git status`
Primeiro, para saber quais arquivos serão apagados

`git clean -n`

E o comando seguinte irá deletar os arquivos _untracked_

`git clean -f`

Ou também...

`git clean -fd` para remover diretórios

`git clean -fX` para remover _ignored files_

`git clean -fx` para remover _ignored files_  e _non-ignored files_

# Branches
### Quero deletar minha branch remota
Para uma branch remota...

`(master)$git push origin -d nome_branch`

ou

`(master)$git push origin :nome_branch`

E para uma local

`(master)$git branch -d nome_branch`

### Quero renomear uma branch
Para uma branch local atual(checkout)...

`(master)$git branch -m novo_nome`

Ou uma outra local mas não dada checkout

`(master)$git branch -m nome_branch_antiga nome_nome_branch`

### Acidentalmente exclui minha branch, e agora?
Irei simular possível acontecimento.

Começarei criando uma branch para trabalhar.

`(master)$git checkout -b test_branch_to_delete`

Agora vou editar meu arquivo README.md com esse passo-a-passo de como *(spoiler alert)"resetar"* minha branch excluída e irei commitar o resultado.
```
(test_branch_to_delete)$git add .
(test_branch_to_delete)$git commit -m "Added section 'Reset branch after deleted'"
[test_branch_to_delete cc7e264] Added section 'Reset branch after deleted'
 1 file changed, 9 insertions(+)

(test_branch_to_delete)$git log
commit cc7e2644bfbf94e962d0cdad6cdd03247702338e
Author: xb193513 <p000lufernandes@prservicos.com.br>
Date:   Tue Nov 21 17:40:09 2017 -0200

    Added section 'Reset branch after deleted'
```

Hora de voltar para master e "acidentalmente" excluir minha branch

```
(test_branch_to_delete)$git checkout master
Switched to branch 'master'
Your branch is up-to-date with 'origin/master'.

(master)$git branch -D test_branch_to_delete
Deleted branch test_branch_to_delete (was cc7e264).
```

É ai que entra nossa amigo `reflog`. Que funciona como um logger dos acontecimento do repo.

```
(master)$git reflog
17ea9fe HEAD@{0}: checkout: moving from test_branch_to_delete to master
cc7e264 HEAD@{1}: commit: Added section 'Reset branch after deleted'
06d3d90 HEAD@{2}: commit: <--commit-filter 'if [ = p000lufernandes@prservicos.com.br ]; START doctoc generated TOC please keep comment here to allow auto update -->
17ea9fe HEAD@{3}: checkout: moving from master to test_branch_to_delete
17ea9fe HEAD@{4}: commit: Added sections BRANCHES and Staging
1925529 HEAD@{5}: checkout: moving from outra_branch_teste to master
```

Agora basta pegar o hash do commit da branch deletada e restaurar nossa branch deletada

```
(master)$git checkout -b temp_branch
Switched to a new branch 'temp_branch'

(temp_branch)$git reset --hard cc7e264
HEAD is now at cc7e264 Added section 'Reset branch after deleted
```

Sucesso! Ouvi um amém? :D

### Acidentalmente exclui minha branch, mas ela não aparece no `reflog`. E agora?
Assim que fiz o item acima eu pensei: Como eu recuperaria minha branch se o commit não estivesse no `reflog`? Essa situação se replica quando não sou dono da branch, portanto não estaria com o histórico de commits para recuperar um estado dela. Então achei esse esse passo-a-passo no [stackoverflow](https://stackoverflow.com/questions/16793637/recover-deleted-branch-in-git). Parece verídico, mas não testei em uma situação real.

Use `fsck` para listar commits danificados

`git fsck --full --no-reflogs --unreachable --lost-found`

`cat-file` para mostra algumas informações adicionais para nós guiar

`git cat-file -p SHACommitsDanificados`

E como no tópico anterior basta pegar o hash do blob/commit danificada e restaurar em uma branch temporária

```
(master)$git checkout -b temp_branch
Switched to a new branch 'temp_branch'

(temp_branch)$git reset --hard cc7e264
HEAD is now at cc7e264...
```

# Outros
### Tutoriais
* [git - guia prático](http://rogerdudler.github.io/git-guide/index.pt_BR.html) - Guia prático e sem complicação
* [Learn Git Branching](https://learngitbranching.js.org/) - Tutorial iterativo de git branch

### Dicas
* [Flight rules for git](https://github.com/k88hudson/git-flight-rules) - Guia do que fazer quando fazemos alguma caquinha (onde me espelhei)
* [Commit messages guide](https://github.com/RomuloOliveira/commit-messages-guide) - Um guia para entender a importância dos commits
* [Git command Explorer](https://gitexplorer.com/) - Um jeito facil de procurar comandos do git
* [Git cheatsheet](http://www.ndpsoftware.com/git-cheatsheet/previous/git-cheatsheet.html#loc=local_repo;) - "Gráfico" dos estados do de um arquivo gerenciado pelo git
* [Anatomia dos pull requests](https://opensource.com/article/18/6/anatomy-perfect-pull-request) - Um guia de como escrever pull requests
* [Como escrever commits](https://chris.beams.io/posts/git-commit/) - Como escrever commits de qualidade
