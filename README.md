![logogithub](github.png)
# Git e Github - Guia prático e rápido

## O que é Git?

O Git é um sistema de controle de versão. Podemos imaginá-lo como uma máquina do tempo do nosso projeto: ele permite salvar "fotografias" do estado atual do código em diferentes momentos. Cada uma dessas fotografias é chamada de commit. Assim, a cada etapa concluída do projeto, fazemos um commit para registrar as mudanças feitas. Isso nos permite rastrear, comparar e até reverter modificações ao longo do tempo.

link para um vídeo rápido que explica o que é Git/GitHub e como usar: https://www.youtube.com/watch?v=-l4Aa8wef8s&t=112s


## O que é o GitHub

O GitHub, por sua vez, é uma plataforma online onde podemos hospedar e gerenciar nossos repositórios Git. 

Ele funciona como uma nuvem para os projetos versionados com Git — assim, o que está salvo localmente no seu computador pode ser sincronizado com o GitHub para ficar disponível em qualquer lugar e para outras pessoas.

Além do armazenamento, o GitHub oferece várias ferramentas que facilitam o trabalho em equipe e o desenvolvimento colaborativo, como:

- Pull requests: para propor e revisar alterações no código;
- Issues: para registrar tarefas, bugs ou ideias de melhorias;
- Wikis e Documentações;
- GitHub Actions, que permitem automatizar testes e implantações.

Existem outras plataformas parecidas, como o GitLab e o Bitbucket, mas o GitHub é, atualmente, a mais popular e amplamente utilizada na comunidade de desenvolvedores.

## Tá, mas por que usar o Git/GitHub?
- **Organização e histórico:** mantenha o registro completo de todas as alterações feitas no projeto, podendo voltar a qualquer versão anterior.
- **Reprodutibilidade:** garante que qualquer pessoa consiga reproduzir exatamente o estado de um projeto em um determinado momento.
- **Trabalho em equipe:** facilita o desenvolvimento colabor ativo, permitindo que várias pessoas contribuam ao mesmo tempo.
- **Experimentação segura:** permite criar **ramificações (branches)** para testar novas ideias sem comprometer a versão principal do projeto.

## Como instalar o Git:
[Link](https://git-scm.com/downloads) para instalação do Git em cada sistema operacional.

no terminal podemos verificar se o git já foi instalado

```bash
git --version
```

Dica extra: Se você está em uma IDE ou no terminal, depois de instalado tente fechar e abrir novamente para assim usar o git normalmente.

## Configurações iniciais
Agora é importante que você crie uma conta no [Github](https://github.com).

As configurações a seguir serão feitas para conectar o nosso computador com a nossa conta do GitHub.

```bash
git config --global user.email "you@email.com"
git config --global user.name "Your Name"
```
Além disso, precisamos gerar uma chave SSH e adicionar no GitHub para fazer esse link, para isso digitamos o seguinte comando no terminal

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

será criado uma pasta oculta chamada .ssh, ao entrar nela um dos arquivos conterá a chave pública SSH que precisamos.

agora, temos que ir no nosso [github → settings → SSH and GPG keys](https://github.com/settings/keys). clicar em “New SSH key”, e adicionar a chave SSH Pública que geramos com o comando acima.

Para mais informações sobre essa chave SSH, pode ler na [documentação](https://docs.github.com/pt/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent).

## Criando um repositório

