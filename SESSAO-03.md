# Comandos avançados de git

## Recapitulando:

`git clone` -> copia um repo remoto para a tua máquina local (fica dentro de uma pasta)

`git init` -> inicializa um novo repositório (local) na pasta atual

`git add <ficheiro>` -> adiciona o ficheiro à área de staging, pronto para ser commited

`git commit -m “stuff”` - faz commit das alterações, ficam guardadas localmente

`git push` -> nada está remoto até esta ação

`git pull` -> ir buscar as atualizações remotas para a máquina local

`git checkout -b <branch>` - criar e ir para um novo branch. É como se estivessemos a ir para uma cópia do branch atual.



## Comandos Sagrados

`git status` - verificar se adicionamos os ficheiros a área de staging

`git log --oneline` - verifica os commits anteriores, numa unica linha por commit

## Rebase vs Merge

#### Exercicio

Merge:
1- fazer checkout -b  (desde main) para um novo branch merge-test\
2- Adicionar uma linha ao readme e commit “b1”\
3- voltar a main, criar um ficheiro novo e commit “a2”\
4- voltar ao branch merge-test\
5- git push do branch\
6- git log --oneline\
(6.1- git checkout -b rebase-test para copiares o branch para o próximo exercício)\
7- git merge main\
8- git log --graph --decorate --oneline\
9- git push outra vez\

Merge: cria uma bifurcação com dois caminhos - um do main e outro das alterações do branch atual. Ficam unidos pelo merge commit. É possivel ver isto com o ponto 8


Rebase: (podes saltar os passos 1 a 4 se tiveres feito o 6.1 do anterior)\
1- fazer checkout -b  (desde main) para um novo branch rebase-test\
2- Adicionar uma linha ao readme e commit “b1”\
3- voltar a main, criar um ficheiro novo e commit “a2”\
4- voltar ao branch rebase-test\
5- git push do branch\
6- git log --oneline\
7- git rebase main\
8- git log --graph --decorate --oneline\
9- git log --oneline\
10 - git push outra vez -> não vai funcionar. Tentar git push -f

Rebase: muda a base - é como se tivesses logo feito as alterações sobre o main atualizado. Já não tem merge commit

## Comandos úteis:

`git commit --amend` ou `git commit --amend --no-edit` 

`git cherry-pick <commit-hash>`

`git rebase -i HEAD~5` - aqui olhamos apenas para os ultimos 5 commits

`git revert <commit-hash>`

`git reset --hard HEAD~1` - apaga totalmente o ultimo commit

`git reset --soft HEAD~1`

`git tag`

`git tag v1.0`

`git tag -a “v1.0” -m “my version v1.0”`

`git push --tags`

`git fetch`


## git hooks
docs: https://git-scm.com/docs/githooks
Estão definidos em .git/hooks
Tipos de hooks:\
pre-commit\
pre-push\
pre-rebase\
prepare-commit-msg\
commit-msg\
post-push\
post-commit \
…

## commit conventions
documentação: https://www.conventionalcommits.org/en/v1.0.0/


Possíveis nomes:
- build, ci, docs, feat, fix, perf, refactor, style, test, chore

#### Exemplo de githook com commit conventions

em commit-msg:
```
#!/usr/bin/python3
import sys

commit_msgs = ["build", "ci", "docs", "feat", "fix", "perf", "refactor", "style", "test", "chore"]
with open(sys.argv[1], "r") as f:
    lines = f.readlines()
    header = lines[0]
    for msg in commit_msgs:
        if header.startswith(msg):
            sys.exit(0)
    print("invalid message format")
    sys.exit(1)
```


## Exercicios extra:
- Criar e apagar git tags (localmente e remoto)
- Novo git hook que imprime uma mensagem a cada commit
