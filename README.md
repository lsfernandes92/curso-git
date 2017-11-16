# Outro guia de git
### Trabalhando em Equipe com Controle e Segurança

Um guia que explora os benefícios de utilizar o Git como ferramenta de controle de versão para projetos em qualquer linguagem, em qualquer plataforma.

#### Principais benefícios:
* Funciona de maneira distribuída
* Permite a edição concorrente de arquivos do projeto
* Não depende de uma conexão ativa com um servidor

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [Alguns comandos de funcionalidade do git:](#alguns-comandos-de-funcionalidade-do-git)
    - [$git rebase](#git-rebase)
    - [$git stash](#git-stash)
    - [$git checkout](#git-checkout)
    - [$git reset HEAD [nome_arquivo]](#git-reset-head-nome_arquivo)
    - [$git reset [hash_commit]](#git-reset-hash_commit)
- [Editando commits](#editando-commits)
    - [O que acabei de comitar?](#o-que-acabei-de-comitar)
    - [Escrevi a mensagem de commit errada antes de dar push](#escrevi-a-mensagem-de-commit-errada-antes-de-dar-push)
    - [Comitei com o usuario e email errado](#comitei-com-o-usuario-e-email-errado)
    - [Quero deletar meu ultimo commit](#quero-deletar-meu-ultimo-commit)
    - [Acidentalmente eu dei um reset hard, como volto reverto isso?](#acidentalmente-eu-dei-um-reset-hard-como-volto-reverto-isso)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

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
``` $git show ```

### Escrevi a mensagem de commit errada antes de dar push
``` $git commit --amend ```

``` $git commit --amend -m "xxxxx" ```

### Comitei com o usuario e email errado
``` $git commit --amend --author "Novo author <emailautor@dominio.com>" ```

### Quero deletar meu ultimo commit
Não recomendado e não faça isso, mas um jeito de deletar um commit após o push é:

``` git reset HEAD^ --hard ```

``` git push --force-with-lease [remote] [branch] ```

Jeito recomendado...

``` git revert <SHAdoCommitEraddo> ```

Para resetar se você ainda não deu push e mantendo mudanças staged

``` (branch)$ git reset --soft HEAD@{1} ```

### Acidentalmente eu dei um reset hard, como volto reverto isso?
Você acidentalmente fez isso? Se fodeo! Já era! Brinks... O git mantém um log de tudo por alguns dias(foda, não?).

``` (master)$ git reflog ```

TESET RESET HARD

Você verá uma lista dos commits passados. Só escolher o SHA do tal commit e resetar para ele.

``` (master)$ git reset --hard <SHACommitResetaHardimente> ```
