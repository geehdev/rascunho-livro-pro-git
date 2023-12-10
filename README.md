Rascunho bastante avançado que eu obtive do livro "Pro Git", aqui contém algumas informações, comandos que achei bastante importante pra quem deseja usar, aprender Git.

## 4.1 OS PROTOCOLOS:
🐧 O Git pode usar quatro protocolos distintos para transferir dados: Local, HTTP, Secure Shell (SSH) e Git. 

#### HTTP vs SSH:
*Use SSH como uma opção mais segura e HTTPS para uso básico do Git baseado em senha. Como o SSH é mais seguro do que inserir credenciais por HTTPS, ele é recomendado para empresas que lidam com dados confidenciais e críticos. Depois de gerar as chaves SSH, apenas as máquinas com o arquivo de chave no disco poderão acessar o repositório remoto.*


## 1.1 SISTEMA DE CONTROLE DE VERSÃO (VCS):
🐧 Um sistema que registra alterações em um arquivo ou conjunto de arquivos ao longo do tempo para que você possa lembrar versões específicas mais tarde. 


## 1.2 BREVE HISTÓRIA DO GIT:
🐧 O Git surgiu em 2005 através da comunidade que desenvolvia o Karnel/núcleo do Linux, após a proprietária do Sistema de Controle de Versão BitKeeper remover a licença comunidade que permitia os desenvolvedores do Linux de utilizar a ferramenta de forma gratuita! 


## 1.3 OS TRÊS ESTADOS DE UM PROJETO GIT:
#### Working Directory (Diretório de Trabalho):
🐧 Uma simples cópia de uma versão do projeto. Esses arquivos são pegos do banco de dados compactado no diretório Git e colocados no disco para serem usados ou modificados por você.

#### Staging Area (Área de Preparo):
🐧 Um arquivo que geralmente está contido em seu diretório Git, ele armazena informações sobre o quê será adicionado ao seu próximo snapshot/commit.

#### Local Repository (.git Directory):
🐧 0nde o Git armazena os metadados e o banco de dados de objetos de seu projeto. É esse arquivo que é copiado quando você clona um repositório.


## AS TRÊS SEÇÕES DE UM PROJETO GIT:
#### Commited (Confirmado):
🐧 Os dados estão armazenados de forma segura em seu banco de dados local (.git Directory);

#### Staged (Preparado):
🐧 Você marcou a versão atual de um arquivo para fazer parte de seu próximo snapshot/commit.

#### Modified (Modificado):
🐧 Você alterou o arquivo, mas ainda não preparou para serem enviados ao seu próximo snapshot/commit.

> *Se uma versão específica de um arquivo estiver no diretório Git (Local Repository), é considerado commited/confirmada. Se for modificado, mas foi adicionado a área de preparo (Staging Area), ele será preparado. E se tiver sido alterado desde o check-out, mas não tiver sido preparado, ele será modificado.*


## 2.2 OS DOIS ESTADOS DE UM PROJETO GIT:
#### Tracked (Rastreado):
🐧 Arquivos que foram incluídos no último snapshot/commit, bem como quaisquer arquivos recém-preparados (Staged), eles podem ser não modificados, modificados ou preparados. Resumindo, arquivos rastreados são arquivos que o Git conhece.

#### Untracked (Não rastreado):
🐧 Arquivos em seu diretório de trabalho (Working Directory) que não estavam em seu último snapshot/commit e ainda não foram para Staged.

> *Conforme você edita arquivos, o Git os vê como modificados, porque você os alterou desde seu último commit. À medida que você trabalha, você prepara seletivamente esses arquivos modificados e, em seguida, confirma todas as alterações preparadas, e o ciclo se repete.*


## IGNORANDO ARQUIVOS (.gitignore):
🐧 Configurar um arquivo .gitignore, antes de você começar um repositório, geralmente é uma boa ideia para que você não inclua acidentalmente em seu repositório Git arquivos que você não quer;

#### EXEMPLO DE ARQUIVO (.gitignore):
```
# Ignora quaisquer arquivos que terminem em ".o" ou ".a".
*.[oa]

# Ignora todos os arquivos cujo nome termine com um til (~)
*~

# Ignore todos os arquivos .a
*.a

# Ignore apenas o arquivo TODO no diretório atual, não subdir/TODO
/TODO

# Ignore todos os arquivos em qualquer diretório chamado build
build/

# Ignore doc/notes.txt, mas não doc/server/arch.txt
doc/*.txt

# Ignore todos os arquivos .pdf no diretório doc/ e qualquer um de seus subdiretórios
doc/**/*.pdf
```

> *O GitHub mantém uma lista bastante abrangente de bons arquivos .gitignore de exemplos para dezenas de projetos e idiomas em [**A collection of .gitignore**](https://github.com/github/gitignore)  se desejar um ponto de partida para seu projeto.*


## COMANDOS GIT:
🐧 Aqui Cobre alguns comandos básicos que você precisa para fazer a grande maioria das coisas que você eventualmente gastará seu tempo fazendo com o Git.

`$ git config [--list]`
- Lista suas configurações do Git.

`$ git clone <path>`
- Clona um repositório remoto, além disso é possível clonar o repositório em um diretório passando <path> após url do projeto;

`$ git add`
- Prepara os arquivos do diretório de trabalho (Working Directory) para serem adicionados ao próximo snapshot/commit.

`git status`
- Verifica os status de seus arquivos de forma completa.

`$ git status [-s]/[--short]`
- Verifica os status de seus arquivos de forma curta, se não tiver nenhum arquivo novo, modificado nada será retornado.

> Arquivos novos que não são rastreados têm um (??) do lado, novos arquivos que foram adicionados à área de stage têm um (A), arquivos modificados têm um (M), arquivos modificado, foi para o stage e foi modificado de novo, (MM). 

`$ git diff`
- Compara o quê está no seu diretório de trabalho (Working Directory) com o quê está na Staging Área, exibe as linhas que foram adicionadas, removidas, retorna nada se os arquivos já foram adicionados a Staged ou se eles não tiverem nenhuma modificação.

`$ git diff [--staged]`
- Compara o quê está na Staging Area com o quê está no seu último snapshot/commit, [--staged é sinônimo de [--cached.

`$ git commit`
- Fazendo isso, será aberto seu editor de texto local, em qualquer linha do arquivo colocamos o quê será usado como título do commit, após fechar o editor, o Git criará seu commit;

> *Toda vez que você executa um commit, você está gravando um snapshot do seu projeto que você pode usar posteriormente para fazer comparações, ou mesmo restaurá-lo.*

`$ git commit [-a] [-m]`
- Adicionando o parâmetro [-a] faz com que o Git prepare/Staged automaticamente cada arquivo modificado antes de fazer o commit.
> *Não precisa correr git add, o parâmetro [-a] inclui apenas arquivos que foram alterados.*

`$ git commit --amend` #TOP
- Modifica o snapshot/commit mais recente, permite combinar alterações preparadas com o commit anterior em vez de criar um commit totalmente novo.

`$ git rm <file>`
- Excluí o arquivo <file> do seu diretório de trabalho (Working Directory). Se o arquivo tiver sido alterado ou se já tiver adicionado à área de stage, você terá que forçar a remoção com a opção [-f].

> *Para remover um arquivo do Git (.git), você tem que removê-lo dos seus arquivos rastreados (mais precisamente, removê-lo da sua área de stage) e então fazer um commit.*

> *Se você simplesmente remover o arquivo do seu diretório de trabalho, ele aparecerá sob a área “Changes not staged for commit” (isto é, fora do stage), Mas, se você executar git rm, o arquivo será preparado para remoção (retirado do stage).*

`$ git rm [--cached] <file>`
- Excluí o arquivos <file> da staged mas mantém em seu diretório de trabalho (Working Directory).

> *Em outras palavras, você pode querer manter o arquivo no seu disco rígido, mas não deixá-lo mais sob controle do Git.*

`$ git mv <nome_arq_origem> <nome_arq_destino>`
- Se você quiser renomear um arquivo no Git, use esse comando.

`$ git log [-p]`
- Mostra as diferenças (diff) introduzidas em cada snapshot/commit, você pode também especificar o parâmetro [-2], que lista no retorno apenas os dois últimos itens:

`$ git log [--stat]`
- Mostra algumas estatísticas abreviadas para cada snapshot/commit, ele também coloca um resumo das informações.

`$ git log [--pretty]=oneline/short/full/fuller`
- Saida de forma bonita, mostra algumas informações sobre cada snapshot/commit.

`$ git log [--graph]`
- Um pequeno gráfico ASCII mostrando seu histórico de ramificações/branchs e mesclagem/merge ao longo do tempo.

`$ git remote`
- Lista os nomes abreviados de cada repositório remoto que você especificou. 

> *Especifando o parâmetro [-v], mostra as URLs que o Git tem armazenado pelo nome abreviado a ser usado para ler ou gravar naquele repositório remoto.*

`$ git remote add <shortname> <url>`
- Adicionar um novo repositório remoto.

`$ git remote rename <nome_remote_origem> <nome_remote_destino>`
- Renomeia o nome curto de servidores remotos.

`$ git remote rm <remote-name>`
- Remove um servidor remoto.

`$ git remote show <remote-name>`
- Fornece algumas informações sobre o <remote-name>.

####  Trabalhando de forma remota
1. *Fetch (Obter);*
2. *Merge (mesclar/fundir);*
3. *Pull (Obter + Atualizar);*
4. *Push (Enviar).*

`$ git fetch <remote-name>`
- Baixa todos os dados de um repositório remoto, o Git armazena esses dados em seu repósitorio local (Local Repository/.git), usaremos "git merge" para atualizar seu diretório de trabalho (Working Directory) com os novos dados que foram obtidos do remoto.

`$ git merge <branch_name>`
- Mescla os dados da ramificação <branch_name> em sua ramificação atual (aquele em que você está atualmente).

`$ git pull`
- Combina "git fetch" e "git merge" funções em uma, baixa o histórico e incorpora as mudanças em seu diretório de trabalho (Working Directory) automaticamente.

`$ git push [-u] <remote-name> <branch-name>`
- Envia todos os snapshot/commit da ramificação/branch para o repósitorio remoto;

`$ git push [-u] [--all/--branchs] <remote-name>`
- Envia todas as ramificações/branchs e seus snapshots/commits para o repósitorio remoto;

`$ git push origin [--delete] <branch-name>`
- Deleta uma ramificaçoes/branch no repósitorio remoto.

`$ git branch <name_branch>`
- Cria uma nova ramificação/branch.

`$ git branch [-M] <nome_branch_origem> <nome_branch_origem>`
- Renomeia uma ramificação/branch.

`$ git branch [-v]`
- Mostra o último snapshot/commit em cada ramificaçoes/branch.

`$ git branch [--merged]`
- Mostra apenas snapshot/commit que já foram mesclados/merge na sua ramificação atual.

`$ git branch [--no-merged]`
- Mostra apenas snapshot/commit que ainda não foram mesclados/merge na sua ramificação atual.

`$ git branch [-d] <nome_branch>:`
- Deleta uma ramificação/branch, se ela já estiver mesclada/merge com qualquer outra ramificação. [-D] em vez de [-d] força a exclusão.

`$ git rebase <nome_branch>`
- Além de git merge, rebase é uma outra forma que podemos usar pra fazer mesclagem. Rebase pegar todas as alterações que foram confirmadas/commited em um ramificação/brach e reproduz tudo em outra brach. Lembre-se, antes devemos ir pra branch que queremos aplicar a mesclagem com os novos dados da <nome_branch>.

`$ git checkout <nome_branch>`
- Altera de ramificação/brach pra <nome_branch>.

- > *Quando você troca de branche, o Git reseta seu diretório de trabalho para a forma que era na última vez que você commitou naquele branch.*

`$ git checkout [-b] <nome_branch>`
- Combina git branch e git checkout funções em uma, ou seja, cria uma nova ramificação/branch e muda para ela automaticamente.


## Mais informações
*Nesse ponto, você já pode executar todas as operações locais básicas do Git - como criar ou clonar um repositório, fazer alterações, usar staged e commit para essas alterações e visualizar o histórico de todas as alterações pelas quais o repositório passou.*

1. "Checkout" == Clonar repositório de alguém;

> *Um branch de tópico é um branch de curta duração que você cria e usa para um único recurso específico ou trabalho relacionado.*

> *“Tracking branch” são branches locais que têm um relacionamento direto com um branch remoto.*

2. **HEAD** em Git significa a ramificação/branch atual que você está.


![imag](https://github.com/genilsonbick/rascunho-livro-pro-git/assets/104036619/6b2cb4ef-f4bb-4aca-99c4-f37c8250a785)


