# Introdução ao Git e ao GitHub

## Comandos básicos para um bom desempenho no terminal
 - dir/ls: lista de diretórios
 - cd: navegação entre diretórios
 - cls/clear: limpar terminal
 - mkdir: criar diretório
 - echo blablabla > hello.txt: cria arquivo
 - (windows) del: deleta apenas arquivos
 - (windows) rmdir workspace /S /Q: deleta diretório
 - (Linux) rm -rf workspace/ : deleta diretório 

[Download git](https://git-scm.com/download/win)

Tree(armazena e aponta para blob ou outras árvores):

Commit(dá sentido, responsável e origem às estruturas e atualizações):

Chave SSH e Token:

**SSH: Forma de estabelecer uma conexão segura e encriptada entre duas máquinas(Chave pública e chave privada)**

Comando executados no git bash para gerar as chaves SSH para autenticar o github:
ssh-keygen -t ed25519 -C _email_

Local onde ficará gerada a chave(isso é exibido no terminal durante a geração da chave):
Enter file in which to save the key (/c/Users/ma/.ssh/id_????)

**ed25519 é o tipo de criptografia**

Comandos para visualizar conteúdo da chave pública SSH git:
ma@MARCELA MINGW64 ~
$ cd /c/users/ma/.ssh

ma@MARCELA MINGW64 /c/users/ma/.ssh
$ cat id_?????.pub

**a chave que é configurada no github é a chave pública.**

É necessário também ativar o SSH Agent para gerenciar as chaves:
$ eval $(ssh-agent -s)

Após iniciado o serviço do agente na máquina, informamos o SSH privado:
$ ssh-add id_?????

Outra opção de autenticação:
Gerado um token de acesso no git e em todo commit é solicitado o token. 
Não é tão seguro quanto o SSH, pois é difícil de memorizá-lo e precisa ser salvo em um lugar seguro. 
Depois de gerado uma vez, não é possível visualizar ele novamente no site do github, se perder precisa gerar outro.

## Iniciando o Git e criando um commit:

git init: iniciar o git dentro de um diretório para gerenciar o versionamento dos arquivos. Inicializa um repositório

git add: move o arquivo untracked ou modified para Staged
git commit: envelopa os arquivos em uma mensagem, dando significância a eles, e volta o status para working tree clean(sem modificações adicionadas)

ls -a: o -a exibe pastas ocultas

Configuração para primeiro uso do git. Aplicar autor, email e nickname:
$ git config --global user.email _email_
$ git config --global user.name _nome_

O arquivo de exemplo usado no curso foi feito em Markdown, é bem legal dá pra personalizar os arquivos como um HTML e até colocar emoji, dá pra testar no editor on line: https://stackedit.io/app#

$ git add *
$ git commit -m "commit inicial"

Ciclo de vida dos arquivos:
Tracked: Rastreado pelo git
O fonte só é considerado tracked depois de rodar o add para ele.

Essas transações de status são realizadas na máquina local, no diretório que o git foi iniciado.

Repositório:
O repositório local do git, dentro da workspace, é composto pelos dados enviados no commit.

Git Status: monitora os status dos arquivos no working directory


- O comando mv move os arquivos e pastas
$ mv _arquivo_ ./receitas/

 - Comando usado para informar o git que o arquivo foi movido de pasta:
$ git add _arquivo_ receitas/


 - Comando para desfazer o add do git, e voltar o arquivo para untracked:
"git restore --staged <file>..."  to unstage

 - Criar arquivo readme:
$ echo > README.md

 - Mostrar as configurações do git no repositório 
$ git config --list
**aperte a letra q para sair**

 - Para remover e corrigir uma configuração:
$ git config --global --unset user.email

## GitHub - mãos na massa:

Criar repositório na nuvem

 - Depois de criado o repositório no git, para vincular ao repositório local, usa o comando:
$ git remote add origin _repositório do Git_
Esse comando define qual vai ser a origem remota do repositório conectado, e define para ela o alias(apelido) origin.

 - Lista de repositório remotos cadastradas
$ git remote -v

 - Comando usado para replicar as informações do repositório local para o remoto(lembrando para identificar os arquivos no push, antes deve ser aplicado o commit):
$ git push origin master

 - Comando para baixar as atualizações do repositório remoto para o local:
$ git pull origin master

 - Comando para baixar o repositório remoto para o local:
$ git clone _repositório do Git_

Para estudar mais sobre branchs:
https://blog.betrybe.com/git/git-checkout/

## Possíveis Problemas
O problema de merge entre os arquivos acontece quando existe no repositório remoto uma versão dos arquivos que não existe no repositório local. O git exibe a mensagem abaixo quando é executado o comando push:

Para resolver o problema, é preciso executar o pull, baixar o arquivo modificado para a máquina, e editar a solução do conflito.
O git demonstra qual parte do arquivo está em conflito assim:

O que estiver dentro de <<<<<<< HEAD…======= é sua versão, o que estiver depois de >>>>>>> é a divergência que está no repositório remoto.

Após ajustar o arquivo:

Executa novamente os comandos git add, git commit e git push.