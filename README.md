# Gittertaginson

# Git - Guia completo da Ecomp  <img src="https://git-scm.com/images/logos/downloads/Git-Icon-1788C.png" width="32" height="32">
Material de consulta para todos os membros da Ecomp

### O que é Git?

> O Git é um sistema de controle de versão distribuído gratuito e de código aberto projetado para lidar com tudo, de projetos pequenos a muito grandes, com velocidade e eficiência.
>O Git é fácil de aprender e tem uma pegada minúscula com desempenho extremamente rápido.

Fonte: https://git-scm.com/

## 1. Instalação

### 1.1. <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/3/35/Tux.svg/869px-Tux.svg.png" width="24" height="24"> Linux

O Git está disponível nos repositórios de programas nas mais diversas distribuições Linux. Para instalar o Git, use o gerenciador de pacotes da sua distribuição, por exemplo:

    apt-get install git

### 1.2. <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/d/da/Windows_logo_-_2002%E2%80%932012_%28Multicolored%29.svg/1165px-Windows_logo_-_2002%E2%80%932012_%28Multicolored%29.svg.png" width="24" height="24"> Windows

Para usar o Git no Windows, instale o Git Bash no link:
https://git-scm.com/download/win
Siga os passos para a instalação.

## 2. Configuração inicial

Após a instalação, deve ser feita a autenticação do usuário e dar permissão para que os mesmos escrevam no repositório. Para isso, o Git usa duas formas: SSH e HTTP.

> Para configurar sua conta em seus computadores pessoais, é interessante utilizar a chave SSH, pois não necessita de posteriores autenticações. Já em computadores públicos, como os da Ecomp, deve ser usado o HTTP por questões de segurança

### 2.1. SSH

SSH no Linux

Assim como o próprio Git, o SSH também está nos repositórios de programas de muitas distribuições. Basta usar o gerenciador de pacotes da distribuição usada, por exemplo: 

    apt-get install ssh

SSH no Windows

O Git Bash vem com um cliente SSH embutido. Para utilização do mesmo, siga os procedimentos abaixo.

#### Gerando uma chave:

O processo para gerar as chaves é o mesmo para todas as plataformas. Para isso, caso esteja no Linux, abra uma janela com o terminal, caso esteja no Windows, abra o Git Bash.

Use o comando `ssh-keygen -t rsa -C "seu@email.com"` para gerar uma chave SSH. Pressione enter para confirmar que a chave será salva na localização padrão, depois o programa vai pedir que o usuário escolha uma senha.

#### Protegendo sua chave:

Em uma rápida analogia, a chave SSH é como uma assinatura digital, e não é bom deixar esse arquivo “por aí”.
Use o comando `ssh-add ~/.ssh/id_rsa` para proteger a chave gerada.

#### Utilizando sua chave:

Para utilizar sua chave em uma plataforma do Git (GitHub, GitLab, GitLab da Ecomp, etc.), faça login na mesma, acesse Configurações da conta > Chaves SSH/ SSH Keys > Adicionar chave.

Se houver um campo Título, coloque uma identificação para a chave. 

No campo key é onde o conteúdo da chave será inserido. Para fazer isso, execute o comando `cat ~/.ssh/id_rsa.pub` e copie o output do programa para esse campo. Por fim clique no botão “Add key” para adicionar a chave no sistema.

### 2.2. HTTP
Algumas plataformas Git também usam HTTP para autenticação, mas para isso o Git deve ser configurado previamente. 

Para realizar esta operação, abra o arquivo `~/.gitconfig` com um editor de texto no Terminal (ou no Git Bash) e acrescente as linhas

	[http]
		sslVerify = false
e salve o arquivo.

Alternativamente, execute o comando `git config --global http.sslVerify false` em um repositório já existente.

### 2.3. Configurar usuário

O git necessita que o usuário se identifique, para isso, basta editar o arquivo de configuração do git usando o mesmo procedimento da etapa anterior. O que será adicionado nesse arquivo serão as seguintes linhas: 

    [user]
    email = seu@email.com
    name = Seu Nome

Alternativamente, o comando `git config --global user.email seu@email.com` e `git config --global user.name Seu Nome` dentro de um repositório já existente produzem o mesmo resultado.

## 3. Criar um repositório

> Existem várias plataformas do Git para manter seus repositórios, como: GitLab, GitHub, Bitbucket, Azure Repos, etc.. Alguns são gratuitos, com serviços Premium, e outros são pagos. 
> A Ecomp tem sua própria versão do GitLab, encontrado em gitlab.ecomp.co.

Para criar um repositório Git, selecione a plataforma desejada, entre no site da mesma no navegador e selecione a opção Create Repository.

Dê um nome ao repositório e selecione o nível de visibilidade (privado/público). Por fim, confirme a criação do repositório.

Repositório criado. Agora é necessário colocá-lo em seu computador. Para isso, execute a sequência de comandos no terminal ou Git Bash:

    // Crie a pasta com o nome do repositório
    mkdir 'nome_do_repo'
    
    // Vá para a pasta crida
    cd 'nome_do_repo'
    
    // Crie o repositório
    git init
    
    // Crie o primeiro arquivo
    touch README.md
    
    // Adicione o arquivo criado no repositório
    git add .
    
    // Escreva as mudanças realizadas no repositório
    git commit -m "Primeiro Commit"
    
    // Salve o repositório para seu endereço na plataforma
    git remote add origin endereço_do_repositório
    
    // Salve as alterações no repositório
    git push

Pronto. Foi criado um novo repositório.

## 4. Clonar um repositório

Para clonar um repositório, entre na plataforma desejada pelo navegador, procure pelo repositório que deseja e digite o comando abaixo em um Terminal ou Git Bash:

    git clone endereço_do_repositório

> Note que o endereço para usuários HTTP é diferente do endereço para
> usuários utilizando SSH.

Pronto. Agora o repositório está clonado no computador.

## 5. Trabalhar no repositório

Agora que o repositório já foi clonado, pode-se começar a trabalhar com ele. Os comandos mais utilizados são:

    git pull
Esse comando atuliza o seu repositório local com o remoto.
    
    git push origin <branch_de_destino>
Envia as alterações feitas no repositório local para o remoto. _origin_ indica de onde estão vindo as alterações, nesse caso, o repositório local.

<branch_de_destino> indica para qual branch do repositório remoto as alterações estão sendo enviadas. O que são branches e como funcionam será explicado posteriormente nesse tutorial, por enquanto, deve-se assumir que <branch_de_destino> é master.

Então o funcionamento básico do comando é:   `git push origin master`
   
    git add [opções] [arquivo1] [arquivo2] ... [arquivoN]
    
Esse comando adiciona arquivos arquivo1, arquivo2 ... arquivoN no repositório local.

Para adicionar todos os arquivos, utilize "git add ."

A opção mais utilizada é a opção -a, que adiciona todos os arquivos (não adicionados previamente) no repositório.
    
    git commit [opções] [arquivo1] [arquivo2] ... [arquivoN]
Esse comando salva as modificações feitas nos arquivos arquivo1, arquivo2 ... arquivoN no repositório local.

O commit indica quais alterações foram feitas nos arquivo, ou qual feature acabou de ser implementada. Cada commit tem uma messagem que indica resumidamente aquele commit e pode ter comentários associados.

Algumas opções utilizadas são:
- -m “Mensagem”: Quando utilizada, o editor de texto não será aberto para a edição da mensagem do commit, ao invés disso, o texto entre aspas duplas será utilizado no lugar.
- –ammend : Ao invés de criar um novo commit, as alterações serão mescladas ao commit anterior.
- -C : Utiliza mesma mensagem do commit anterior, geralmente utilizada junto a opção anterior.

`enter code here`

Diz quais as alterações feitas no repositório e que não foram informas ao git, por exemplo, arquivos modificados e que não foram “commitados”, ou arquivos adicionados no diretório, mas não foram adicionados ao git.

Nota importante: NUNCA use o opção -f ou –force em qualquer um desses comandos.

## 6. Branches

Branches podem ser descritos como áreas de trabalho. Por exemplo, a branch _master_ normalmente é usado apenas para códigos estáveis, então para implementar uma funcionalidade X, cria-se então uma área de trabalho para tal, não misturando os códigos dessa implementação com o de produção. Assim que a funcionalidade estiver implementada, testada e aprovada, o código da funcionalidade X pode ser mesclado no branch _master_. Todos esses processos serão descritos a seguir.

### 6.1. Criando branches

Para criar uma branch com o nome _“nova_branch”_, basta estar dentro de um repositório e executar o seguinte comando:

    git checkout -b nova_branch

Com esse comando, o usuário vai criar uma nova branch e essa branch passa ser a qual o usuário está trabalhando.

### 6.2. Mudando a branch atual

Para mudar de branch, por exemplo a branch master, basta executar o comando:

    git branch master

Para listar todas as branches, basta usar o comando:

    git branch

### 6.3. Deletando branches

Para deletar uma branch, por exemplo a branch nome_da_branch, use o comando:

    git branch -d nome_da_branch
    

### 6.4. Merging

Essa é a ação de mesclar o código entre branches. Os passos realizar essa operação são:

- Faça o commit de todas as modificações, pois somente assim o git irá realizar a operação corretamente.

- Mude para a branch na qual receberá o código.

- Execute o comando: `git merge branch_a_ser_mesclada` . Por exemplo,
para mesclar a branch feature_x à branch atual, utilize: `git merge feature_x`

### 6.5. Detectar alterações nas branches remotas

Para verificar se há alterações nas branches remotas, utilize o comando:

    git fetch

## 7. .gitignore

O arquivo .gitignore é um arquivo que indica ao git quais os tipos de arquivo o git vai ignorar, por exemplo, imagens, arquivos binários (.o, .class, .jar).

Para criar um .gitignore global, execute o seguinte comando em um repositório git:

    config --global core.excludesfile '~/.gitignore'

Para criar um .gitignore local, basta criar o arquivo dentro do repositório.

A sintaxe do que deve ser escrito no arquivo é a de expressões regulares:

    # Isso é um comentário
    *.tmp # Ignora todos os arquivos teminados em ".tmp"
    *log* # Ignora todos os arquivos que contenham em seu nome 'log'
    foo/ # Ignora o diretório chamado "foo".
    !*important* # NÃO ignora os arquivos que contém "important" no seu nome.








