![github](images/github.png)

# Git e GitHub - Guia prático

## O que é Git?

O Git é um sistema de controle de versão. Podemos imaginá-lo como uma **máquina do tempo** do nosso projeto: ele permite salvar "fotografias" do estado atual do código em diferentes momentos. Cada uma dessas fotografias é chamada de **commit**. Assim, a cada etapa concluída do projeto, fazemos um commit para registrar as mudanças feitas. Isso nos permite rastrear, comparar e até reverter modificações ao longo do tempo.

Link para um vídeo rápido que explica o que é Git/GitHub e como usar: https://www.youtube.com/watch?v=-l4Aa8wef8s&t=112s


## O que é o GitHub

O GitHub, por sua vez, é uma plataforma online onde podemos hospedar e gerenciar nossos repositórios Git.

Ele funciona como uma nuvem para os projetos versionados com Git — assim, o que está salvo localmente no seu computador pode ser sincronizado com o GitHub para ficar disponível em qualquer lugar e para outras pessoas.

Uma diferença importante que costuma confundir no começo: **Git** é a ferramenta que roda no seu computador; **GitHub** é o site onde você guarda e compartilha o que o Git versionou. Dá pra usar Git sem nunca tocar no GitHub — mas juntos eles ficam muito mais poderosos.

Além do armazenamento, o GitHub oferece várias ferramentas que facilitam o trabalho em equipe e o desenvolvimento colaborativo, como:

- **Pull requests:** para propor e revisar alterações no código;
- **Issues:** para registrar tarefas, bugs ou ideias de melhorias;
- **Wikis e Documentações;**
- **GitHub Actions**, que permitem automatizar testes e implantações.

Existem outras plataformas parecidas, como o GitLab e o Bitbucket, mas o GitHub é, atualmente, a mais popular e amplamente utilizada na comunidade de desenvolvedores.

## Tá, mas por que usar o Git/GitHub?
- **Organização e histórico:** mantenha o registro completo de todas as alterações feitas no projeto, podendo voltar a qualquer versão anterior.
- **Reprodutibilidade:** garante que qualquer pessoa consiga reproduzir exatamente o estado de um projeto em um determinado momento.
- **Trabalho em equipe:** facilita o desenvolvimento colaborativo, permitindo que várias pessoas contribuam ao mesmo tempo.
- **Experimentação segura:** permite criar **ramificações (branches)** para testar novas ideias sem comprometer a versão principal do projeto.

## Como instalar o Git
[Link](https://git-scm.com/downloads) para instalação do Git em cada sistema operacional.

No terminal podemos verificar se o git já foi instalado:

```bash
git --version
```

Se aparecer um número de versão, está tudo certo.

> 💡 **Dica extra:** se você está em uma IDE ou no terminal, depois de instalar feche e abra novamente para o git ser reconhecido normalmente.

## Configurações iniciais
Agora é importante que você crie uma conta no [GitHub](https://github.com).

As configurações a seguir servem para conectar o nosso computador com a nossa conta do GitHub. Elas dizem ao Git quem é você — esse nome e e-mail vão aparecer carimbados em cada commit que você fizer.

```bash
git config --global user.email "voce@email.com"
git config --global user.name "Seu Nome"
```

> 💡 Use o mesmo e-mail da sua conta do GitHub. Assim os seus commits ficam corretamente vinculados ao seu perfil.

### Gerando a chave SSH

Além disso, precisamos gerar uma **chave SSH** e adicioná-la no GitHub. Pense nela como um crachá: é o que permite o seu computador "provar" pro GitHub que é você, sem precisar digitar senha toda hora. Para gerar, digitamos no terminal:

```bash
ssh-keygen -t ed25519 -C "seu_email@example.com"
```

Pode dar Enter em todas as perguntas para aceitar o padrão. Isso cria uma pasta oculta chamada `.ssh` com **dois** arquivos:

- `id_ed25519` → a chave **privada**. É a sua senha secreta. **Nunca** compartilhe nem suba para lugar nenhum.
- `id_ed25519.pub` → a chave **pública**. Essa sim é a que vai pro GitHub.

Para ver o conteúdo da chave pública e copiar:

```bash
cat ~/.ssh/id_ed25519.pub
```

Copie tudo o que aparecer (começa com `ssh-ed25519 ...`). Agora vá no seu [GitHub → Settings → SSH and GPG keys](https://github.com/settings/keys), clique em **"New SSH key"** e cole a chave pública ali.

Para mais detalhes, vale ler a [documentação oficial](https://docs.github.com/pt/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent).

> ⚠️ **Deu erro mais pra frente?** Se em algum momento aparecer `Permission denied (publickey)` ao tentar enviar algo, quase sempre é a chave SSH que não foi configurada direito. Volte aqui e confira se você colou a chave **pública** (`.pub`) no GitHub.

## Criando um repositório

Na sua conta, clique no ícone verde **"New"** para criar um novo repositório.

Na página de criação, você pode definir:

- o nome do repositório,
- uma descrição opcional,
- se ele será público ou privado,
- e se deseja iniciar com um README (não indico adicionar nesse momento, por enquanto).

Após criar o repositório, o GitHub exibirá uma página com um tutorial de comandos básicos — é ali que aprendemos como conectar o repositório local (no nosso computador) com o repositório remoto (no GitHub).

![new](images/create_repo.png)

Em seguida, abriremos o terminal **dentro da pasta do projeto que queremos versionar** e rodaremos esses comandos. Mas, antes de sair copiando e colando, vamos entender o que cada um faz nas próximas etapas. 👇


## Entendendo o fluxo do Git

Antes dos comandos, segura uma ideia que organiza tudo. No Git, um arquivo passa por **estágios** até chegar ao GitHub. Não é um pulo direto do seu computador pra nuvem:

```
📁 working directory  →  📥 stage  →  💾 repositório local  →  ☁️ repositório remoto
   (seus arquivos)        git add       git commit               git push
```

- **working directory:** a sua pasta, onde você de fato edita os arquivos.
- **stage (área de preparação):** uma "fila" do que vai entrar no próximo commit. É pra aqui que o `git add` manda os arquivos — e **só pra aqui**, nada ainda foi pro GitHub.
- **repositório local:** quando você dá `git commit`, a fotografia é gravada no histórico, mas ainda só no seu computador.
- **repositório remoto:** só com o `git push` é que tudo isso finalmente sobe pro GitHub.

Tendo esse mapa na cabeça, os comandos a seguir param de parecer mágica. 🪄


## Inicializando o Git no diretório

Para inicializar o Git, ou seja, para converter uma pasta comum do computador em um repositório Git, usamos:

```bash
git init
```

> 💡 **Dica:** confira se você está mesmo dentro da pasta que quer versionar antes de rodar esse comando.

Em seguida podemos ver o estado dos arquivos — o que já está sendo rastreado e o que ainda não entrou em nenhum commit (como estamos começando agora, ele vai mostrar tudo que tem dentro da pasta):

```bash
git status
```

Para mandar os arquivos da pasta para a **área de stage** (lembrando: ainda não é o GitHub!), usamos:

```bash
git add <nome_do_arquivo_ou_pasta>
```

Ou então, para adicionar todos os arquivos de uma vez:

```bash
git add .
```

> ⚠️ **Atenção:** cuidado com o que você adiciona aqui. Evite subir **dados grandes** (o GitHub tem limite de tamanho (100MB por aquivo e 1GB para todo o repo)) ou **dados sensíveis** (senhas, planilhas privadas, etc.). Para ignorar arquivos que você não quer enviar, tem um tópico sobre o `.gitignore` mais à frente — e o ideal é criar esse arquivo **antes** do primeiro `git add .`.

Para registrar essa fotografia no histórico (agora sim virou um commit, mas ainda no seu computador), usamos:

```bash
git commit -m "nome_do_commit"
```

O nome do commit deve trazer uma pequena descrição das alterações feitas. Existem [boas práticas e convenções](https://github.com/iuricode/padroes-de-commits) que ajudam a padronizar esses nomes, deixando mais fácil entender o propósito de cada mudança no histórico.

Uma boa mensagem de commit ajuda, por exemplo, quando você quer voltar a um ponto específico do projeto — tipo "antes de eu adicionar aquele filtro novo" ou "no momento em que integrei a nova base de dados".

Exemplo:

```bash
git commit -m "feat: adiciona etapa de normalização log2 nas contagens"
```

> 💡 Aquela palavrinha inicial (`feat`, `fix`, etc.) **não é obrigatória**, é só uma boa prática das convenções que linkei acima.


## O que é uma branch?

Agora precisamos informar em qual **branch**, ou seja, em qual linha do tempo do projeto, queremos guardar o nosso commit. Voltando à analogia da máquina do tempo: a branch é uma realidade paralela onde você pode mexer no projeto sem bagunçar a versão "oficial".

![branch](images/branch.png)

Por padrão, todo repositório começa com uma branch principal, chamada **main**. Ela representa a versão estável do projeto — geralmente aquela que está funcionando e que será disponibilizada para os usuários.

Quando queremos fazer atualizações, corrigir erros ou testar novas funcionalidades **sem risco de quebrar o que já funciona**, criamos novas branches. Elas são linhas do tempo alternativas, cópias da main onde dá pra trabalhar de forma isolada. Tudo que você faz ali não afeta o código principal até estar pronto e testado.

Depois de revisar e testar, podemos **mesclar (merge)** essa branch com a main — ou seja, juntar as duas linhas do tempo de volta —, atualizando o projeto com segurança.

Para começar, vamos garantir que a nossa branch principal se chame `main`:

```bash
git branch -M main
```

> 📝 O `-M` **renomeia** (à força) a branch atual para `main`. Em versões mais antigas do Git a branch inicial vinha como `master`, então esse comando é o que garante o padrão `main` que o GitHub usa hoje.

#### Comandos extras para criar ou trocar de branch

```bash
git branch                      # ver quais branches existem
git branch <nome_da_branch>     # criar uma nova branch
git checkout <nome_da_branch>   # trocar para outra branch

# ou então, para criar e já ir pra nova branch de uma vez:
git switch -c <nova_branch>
git checkout -b <nova_branch>
```

## Conectando a pasta local com o repositório remoto

Para ligar o nosso repositório local ao repositório online, usamos a URL que o GitHub mostrou na criação:

```bash
git remote add origin <url_do_repositorio>
```

> 💡 Como configuramos uma **chave SSH** lá atrás, use a URL **SSH** (ela começa com `git@github.com:...`). A URL **HTTPS** (`https://github.com/...`) também funciona, mas aí o GitHub pode pedir login/token em vez da chave. As duas aparecem na página do repositório — é só escolher a aba certa.

Feito o link, enviamos tudo para o GitHub com:

```bash
git push -u origin main
```

O `-u origin main` só é necessário na **primeira vez**: ele "casa" a sua branch local com a remota. Nas próximas, basta:

```bash
git push
```

Pronto, seu repositório já está no ar! Atualize a página do GitHub para ver seus arquivos. 🎉

## Resumo do uso no dia a dia

Considerando que você já criou o repositório e quer só ir atualizando, aqui vai o ciclo do dia a dia:

```bash
git status                      # ver o que mudou
git add .                       # mandar as mudanças pro stage
git commit -m "nome_do_commit"  # gravar a fotografia
git push                        # enviar pro repositório remoto
```

É esse loop que você vai repetir o tempo todo. 🔁

## Como trabalhar com outras pessoas

O primeiro passo para colaborar no projeto de outra pessoa é **clonar** o repositório do GitHub para o seu computador. Para isso, crie ou abra uma pasta vazia, abra o terminal dentro dela e execute:

```bash
git clone <url_do_repositorio>
```

#### 🔑 Permissões de colaboração

Para conseguir **enviar** alterações direto para o repositório, o dono precisa te adicionar como colaborador em **Settings → Collaborators**, usando o seu nome de usuário do GitHub. Sem isso, você consegue clonar e ver, mas não dar push.

Depois de clonar, o fluxo saudável é trabalhar **em uma branch separada**, não direto na main:

```bash
git switch -c minha-feature   # cria e entra numa branch nova
# ... edita arquivos, git add, git commit ...
git push -u origin minha-feature   # sobe a sua branch pro GitHub
```

#### 🔀 E aí, como junta com a main?

Depois de subir a sua branch, você abre um **Pull Request (PR)** lá no GitHub. O PR é justamente o lugar de **propor** que a sua linha do tempo seja mesclada na main — as outras pessoas conseguem revisar, comentar e, se estiver tudo certo, aprovar o merge. É assim que a colaboração acontece sem ninguém pisar no código do outro.

## 🔄 Atualizando seu repositório local

Quando outros colaboradores fizerem mudanças e você quiser trazer as novidades para o seu computador, use:

```bash
git pull origin main
```

> 💡 **Dica importante:** sempre dê um `git pull` **antes** de começar a trabalhar. Isso evita conflitos chatos com o que outras pessoas já enviaram.

## E quando dá conflito? (não entra em pânico)

Por mais que você dê `git pull` direitinho, uma hora vai acontecer: você e outra pessoa editaram **a mesma parte do mesmo arquivo**, e o Git não sabe qual versão manter. Aí ele para tudo e te avisa que existe um **conflito de merge**. É normal, faz parte, e tem solução. 🙂

Quando isso rola, o Git **marca** o trecho conflitante dentro do próprio arquivo, mais ou menos assim:

```
<<<<<<< HEAD
filtro de qualidade com threshold 30
=======
filtro de qualidade com threshold 20
>>>>>>> minha-feature
```

A leitura é simples:

- Entre `<<<<<<< HEAD` e `=======` está a **sua** versão (a que já estava ali).
- Entre `=======` e `>>>>>>>` está a versão que **veio de fora** (a outra branch).

Para resolver, você edita o arquivo na mão e decide o que fica: pode manter uma das versões, juntar as duas ou reescrever do zero. O importante é que, no fim, **você apague os marcadores** (`<<<<<<<`, `=======`, `>>>>>>>`) e deixe só o código final que você quer.

Depois de arrumar, é só seguir o fluxo normal pra confirmar que resolveu:

```bash
git add <arquivo_que_estava_em_conflito>
git commit            # o Git já sugere uma mensagem de merge, pode aceitar
```

> 💡 Conflito **não é erro seu** nem sinal de que algo quebrou — é só o Git pedindo pra você bater o martelo numa decisão que ele não pode tomar sozinho. Resolveu, commitou, segue o jogo.

## Voltando no tempo (com cuidado!)

Aqui é onde a máquina do tempo fica perigosa, então atenção: **três comandos parecidos, mas que fazem coisas bem diferentes.** 👇

Primeiro, para qualquer um deles, normalmente você precisa do **ID do commit**. Para ver o histórico:

```bash
git log              # histórico completo
git log --oneline    # versão resumida, uma linha por commit (mais fácil de ler)
```

**1. Desfazer um commit com segurança → `git revert`**

```bash
git revert <ID_do_commit>
```

Esse cria um **commit novo** que desfaz as mudanças de um commit anterior. Ele **não apaga** nada do histórico, só registra "voltei atrás aqui". É o único da lista seguro de usar em algo que **já foi pro GitHub**.

**2. Corrigir o último commit → `git commit --amend`**

```bash
git commit --amend -m "nome_corrigido"
```

Edita **apenas o último commit** (a mensagem ou o conteúdo). Útil quando você errou a mensagem ou esqueceu de adicionar um arquivo.

**3. Apagar commits de verdade → `git reset`**

```bash
git reset --hard <id_do_commit_anterior>
```

Esse **apaga** commits e **descarta** as alterações — não tem desfazer fácil. Use só quando tem certeza absoluta.

> ⚠️ **Cuidado de verdade:** o `--amend` e o `git reset --hard` **reescrevem o histórico**. Se você já deu `push` ou está trabalhando em equipe, isso vira dor de cabeça (a sua linha do tempo e a dos outros deixam de bater e dá conflito feio). A regra prática: **em commit que já foi pro GitHub, prefira o `git revert`.**

## ⚠️ Cuidado com arquivos grandes (importante!)

Esse tópico merece atenção especial, principalmente pra quem trabalha com dados pesados (FASTQ, BAM, matrizes de contagem, imagens, etc.). O Git **não foi feito** para arquivos grandes, e ignorar isso entope o repositório de um jeito difícil de reverter.

Pontos pra ter em mente:

- O GitHub tem um **limite de 100 MB por arquivo**. Acima disso ele simplesmente recusa o push. E recomenda manter o repositório inteiro abaixo de ~1 GB.
- A pegadinha cruel: depois que um arquivo grande entra num commit, ele **fica no histórico para sempre** — mesmo que você delete o arquivo depois. Lembra da máquina do tempo? Aquela fotografia já foi tirada. Dar `git rm` remove o arquivo do estado atual, mas ele continua lá no histórico pesando o repositório, e tirar de verdade dá um trabalho enorme.

Por isso a **prevenção** é tudo, e é aí que o `.gitignore` (logo abaixo) entra: bloqueie os arquivos grandes **antes** do primeiro `git add .`, e eles nunca chegam a virar fotografia.

E se você **precisa** versionar arquivos grandes de propósito? Existe o **Git LFS** (Large File Storage), uma extensão do Git pensada exatamente pra isso: em vez de guardar o arquivo gigante no histórico, ele guarda um "ponteiro" leve e mantém o arquivo de verdade separado. Vale pesquisar [a documentação do Git LFS](https://git-lfs.com) se esse for o seu caso.

> 💡 Resumindo: dado bruto e arquivo pesado, na dúvida, **não vão pro Git**. Eles ficam no `.gitignore` ou no LFS — nunca soltos num `git add .`.

## Arquivos comuns em repositórios

#### ❕ requirements.txt

Esse arquivo lista o nome de todas as bibliotecas e frameworks usadas no projeto. Quem for rodar o seu código precisa instalar todas elas.

Você pode montar a lista de duas formas automáticas:

```bash
# Opção 1: lista tudo que está instalado no ambiente atual
pip freeze > requirements.txt
```

```bash
# Opção 2: lista só o que foi realmente importado no código (mais enxuto)
pip install pipreqs
pipreqs .
```

> 💡 O `pip freeze` é o mais comum, mas pega **tudo** do ambiente — por isso ele combina tão bem com o uso de ambiente virtual (mais abaixo), pra não encher o arquivo com biblioteca que você nem usa. Já o `pipreqs` olha o seu código e lista só o necessário.

#### 📝 README.md

É um arquivo escrito em **Markdown** que serve para **apresentar o seu projeto**. Ele é uma forma de **documentação** que fica visível direto na página do repositório no GitHub (este guia aqui, por exemplo, é um `.md`!). No `README.md`, costumamos incluir:

- O que o projeto faz;
- Quais ferramentas e bibliotecas ele utiliza;
- Como está estruturado o código;
- Instruções para instalação e uso;
- Autores, licença e agradecimentos (opcional).

> 💡 Um bom README é o **"cartão de visita"** do projeto — ajuda outras pessoas (e você mesma no futuro!) a entenderem rapidamente do que se trata.

[Link de como fazer um README bonitão](https://raullesteves.medium.com/github-como-fazer-um-readme-md-bonitão-c85c8f154f8)

#### 🚫 .gitignore

O **`.gitignore`** é o arquivo onde listamos **tudo o que NÃO queremos que o Git rastreie**. Ou seja, ele define o que **não será enviado para o repositório remoto**. Isso é essencial para manter o repositório limpo e seguro, evitando subir coisas como:

- Dados **privados** (ex.: planilhas com informações sensíveis);
- Arquivos **temporários** do sistema;
- Ambientes virtuais (`.venv/`);
- Saídas geradas automaticamente (`__pycache__/`, arquivos `.log`, etc.).

Para criar, basta adicionar um arquivo chamado `.gitignore` na raiz do projeto e listar nele os arquivos ou pastas que o Git deve ignorar.

Exemplo:

```bash
# Ambiente virtual
.venv/

# Dados brutos
data/raw/

# Arquivos temporários
__pycache__/
*.log
```

> ⚠️ Crie o `.gitignore` **antes** do primeiro `git add .`. Se um arquivo já entrou no commit antes de ser ignorado, o Git continua rastreando ele mesmo depois — aí precisa removê-lo do rastreamento na mão.

Neste [link](https://www.toptal.com/developers/gitignore) você informa as linguagens/ferramentas que está usando e ele gera um `.gitignore` básico pra você.

### 💡 Boa prática (opcional): criar um ambiente virtual Python (também dá pra fazer com R)

Ao trabalhar em projetos Python, é uma boa prática criar um **ambiente virtual**. Ele isola as dependências do projeto, evitando conflitos entre bibliotecas de projetos diferentes na sua máquina. Para criar e ativar:

```bash
python -m venv .venv
source .venv/bin/activate
```

Depois, instale as dependências listadas no `requirements.txt`:

```bash
pip install -r requirements.txt
```

> 💡 Lembre de colocar a pasta `.venv/` no `.gitignore` — ela não precisa ir pro GitHub, já que qualquer pessoa recria o ambiente a partir do `requirements.txt`.

## Chegamos ao fim! 🎉

E é isso! Se você seguiu até aqui, já tem o essencial pra versionar seus projetos, colaborar com outras pessoas e dormir tranquila sabendo que dá pra voltar no tempo quando precisar.

No fundo, o dia a dia com Git é mais simples do que parece — quase tudo se resume àquele loop:

```bash
git status
git add .
git commit -m "o que mudou"
git push
```

O resto (branches, conflitos, desfazer commits) você vai pegando no susto, na prática, conforme aparecer. E não tem problema nenhum em consultar este guia de novo sempre que bater a dúvida — é exatamente pra isso que ele existe.

Bons commits! 🚀