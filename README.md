# Outro guia de git
### Trabalhando em Equipe com Controle e Segurança

Um guia que explora os benefícios de utilizar o Git como ferramenta de controle de versão para projetos em qualquer linguagem, em qualquer plataforma.

#### Principais benefícios:
* Funciona de maneira distribuída
* Permite a edição concorrente de arquivos do projeto
* Não depende de uma conexão ativa com um servidor

### Alguns comandos de funcionalidade do git:
#### $git rebase
* Evita vários commits de merge
* Evita commits de merge desnecessários

#### $git stash
* Utilizado para deixar o desenvolvimento atual salvo
* Usado para arrumar bugs antes de fazer commits inacabados

#### $git checkout
* Apaga tudo feito no working directory

#### $git reset HEAD [nome_arquivo]
* Apaga tudo que está no index

#### $git reset [hash_commit]
* Reseta tudo até o hash do commit

### Editando commits
#### O que acabei de comitar?
``` $git show ```

#### Escrevi a mensagem de commit errada antes de dar push
``` $git commit --amend ```

``` $git commit --amend -m "xxxxx" ```

#### Comitei com o usuario e email errado
``` $git commit --amend --author "Novo author <emailautor@dominio.com>" ```
