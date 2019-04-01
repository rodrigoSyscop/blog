---
title: "MacOS Mojave Like a Boss"
date: 2019-03-31T15:29:23-03:00
draft: false
---

# MacOS Mojave Like a Boss

Eu tenho o costume de fazer uma instalação limpa do MacOS sempre que há o lançamento de uma nova versão do sistema operacional da maçã, por isso acabei compilando este guia com as principais ações realizadas logo após a instalação. Fique à vontade para copiar, adaptar e recompartilhar este guia conforme a sua necessidade.

## Homebrew

Para quem vem do Linux como eu, o Homebrew (ou somente brew) funciona como um gerenciador de pacotes para o MacOS.

### Instalação

```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

Ref.: [https://brew.sh](https://brew.sh)


Com o `brew` instalado fica fácil procurar e instalar novos aplicativos sem precisar recorrer ao browser:

```bash
# procura e instala o wget, uma ferramenta de linha de comando
brew search wget
brew install wget

# instala o vlc, uma aplicação gráfica
# sempre que quiser instalar um app gráfico, utilize o cask.
# você vai notar na saída do brew search se ele pertence ao cask ou não.
brew cask install vlc
```

### Instalando aplicativos pelo homebrew

A seguir eu instalo diversas ferramentas, aplicativos e fontes que eu costumo utilizar. Instale o que for útil para você.

```bash
# dev tools
brew install git
```

```bash

# ativa o "repositório" de fontes
brew tap caskroom/fonts

# fontes para terminal e editores de textos
brew cask install font-fira-code font-source-code-pro font-roboto-mono

# editor de texto
brew cask install visual-studio-code

# dev tools
brew cask install github-desktop tableplus docker

# social, groupware, communication
brew cask install slack skype telegram whatsapp zoomus

# downloads, players
brew cask install transmission vlc

# browsers
brew cask install firefox google-chrome

# extras
brew cask install kindle authy itsycal
```

Outro aplicativo que uso bastante é o [trello](https://trello.com), que não está mais disponível através do brew. No entanto, existe uma ferramenta CLI chamada [mas](https://github.com/mas-cli/mas) que pode ser utilizada para instalar aplicativos da Mac App Store via linha de comando:

```bash
brew install mas
# Talvez seja necessário fazer login na appstore
mas signin mas@example.com
# busca por apps com "trello" no nome
mas search trello
# instala o trello através do seu id 
mas install 1278508951
```

Para maiores informações sobre o **mas** consulte a página do projeto em [https://github.com/mas-cli/mas](https://github.com/mas-cli/mas).

## Bash Completions

Você deve ter reparado que após instalar certos aplicativos pelo `brew` ele exibe a seguinte mensagem:

```bash
==> Caveats
Bash completion has been installed to:
  /usr/local/etc/bash_completion.d
```

Isso significa que o programa instalado veio acompanhado de algumas macros que informam ao bash sobre seus possíveis argumentos, opções ou parâmetros do comando em questão quando você precionar a tecla `[TAB]` no terminal. O famoso recurso de autocompletar do shell do Linux.

Para tirar proveito disso você deve instalar o seguinte utilitário:

```bash
brew install bash-completion
```

Conforme sugerido pelo brew, ao final da instalação do `bash-completion`, você deve adicionar a instrução abaixo ao seu `.bash_profile`, que talvez nem exista ainda (neste caso basta criá-lo):

`~/.bash_profile`:
```bash
# Ativa bash completion
[ -f /usr/local/etc/bash_completion ] && . /usr/local/etc/bash_completion
```

Feche seu terminal e abra-o novamente ou simplesmente digite `source ~/.bash_profile`.
Agora teste digitando `git[TAB][TAB]`, por exemplo.

Você deve se deparar com todos os subcomandos possíveis do `git`.

Outros completions que podem ser instalados separadamente e que eu utilizo:

```bash
brew install docker-completion docker-compose-completion docker-machine-completion django-completion pip-completion 
```

## Chaves SSH

Eu utilizo criptografia de chave pública para conectar nos servidores que eu administro e recomendo fortemente, caso você ainda esteja utilizando senha para acessar seus servidores, a migrar para chaves ssh como eu.

### Gerar uma nova chave SSH

Minhas chaves privadas são protegidas por senha, então caso eu me descuide e tenha essas chaves comprometidas, ainda teriam que adivinhar minha _passphrase_ para efetivamente utilizarem minhas chaves. Até lá eu já teria revogado minhas chaves antigas e substituído por novas.

```bash
$ ssh-keygen -t rsa -b 4096 -C "$(whoami)@$(hostname)-$(date +'%Y-%m-%d')"
```

### Adicionar chaves ao agente SSH

Para não ter que digitar a _passphrase_ toda vez que precisar utilizar uma chave privada, eu uso o _Keychain_ do MacOS que interage com o agente SSH. Dessa forma só é preciso digitar a passphrase de uma chave privada uma única vez por sessão, isto é, a cada login no Mac.

_Se você instalou uma versão mais recente do cliente OpenSSH pelo brew, substituindo o cliente ssh da maçã, talvez a integração entre o Keychaing e o agente SSH não funcione._

`~/.ssh/config`:
```bash
Host *
    AddKeysToAgent yes
    ServerAliveInterval 5 # evita desconexões ssh por inatividade
```

Aproveite para comentar a seguinte opção no seu `/etc/ssh/ssh_config`:

```bash
Host *
#       SendEnv LANG LC_*  # <- comentar essa linha no final do arquivo
```

Caso contrário você pode se deparar com o seguinte aviso quando fizer um login remoto:

```bash
-bash: warning: setlocale: LC_CTYPE: cannot change locale (UTF-8): No such file or directory
```

## Terminal

Convenhamos, terminal com fundo branco!? Eu costumo utilizar o tema [peppermint](https://noahfrederick.com/log/lion-terminal-theme-peppermint), disponível para o Terminal nativo do MacOS e também para o iTerm2.

Basta fazer o download e dar um duplo clique sobre o arquivo. Se seu Mac reclamar que este não é um software assinado e reconhecido, vá em _System Preferences_ -> _Security & Privacy_:

Clique no botão _Open Anyway_ na aba _General_.

Agora vamos corrigir a bizarrice do peppermint. Com o terminal aberto e o tema do pappermint aplicado, pressione `CMD` + `,` para abrir as preferências do terminal.

- Vá em _Profiles_, na aba _Text_ mude a fonte para _Source Code Pro_ e um tamanho que te agrade (eu uso 12).
- Na aba _Windows_ mude o _Window Size_ para 80 x 20.

Terminando, certifique-se que o tema Peppermint está selecionado e clique no botão _Default_ para fazer dele o tema padrão.

As configurações para o iTerm2 são semelhantes, mas você vai precisar de um tema específico para ele: [peppermint for iTerm2](https://raw.githubusercontent.com/dotzero/iTerm-2-Peppermint/master/Peppermint.itermcolors).

### Cores para o Terminal

Insira o seguinte trecho no seu `~/.bash_profile`:

```bash
#-------------------------------------------------
#  Colorful Terminal
#-------------------------------------------------
#
# Tell ls to be colourful
export CLICOLOR=1
export LSCOLORS=Exfxcxdxbxegedabagacad

# Tell grep to highlight matches
export GREP_OPTIONS='--color=auto'
export TERM="xterm-color"
# colorful prompt
PS1='\[\e[0;33m\]\u\[\e[0m\]@\[\e[0;32m\]\h\[\e[0m\]:\[\e[0;34m\]\w\[\e[0m\]\$ '
```

## VIM melhorado

Insira as seguintes configurações no seu `~/.vimrc`:

```bash
syntax enable
set tabstop=4       " number of visual spaces per TAB
set softtabstop=4   " number of spaces in tab when editing
set expandtab       " tabs are spaces

set autoindent
set shiftwidth=4

filetype indent on  " load filetype-specific indent files
set wildmenu        " visual autocomplete for command menu
set lazyredraw      " redraw only when we need to
set showmatch       " highlight matching [{()}]

set incsearch       " search as characters are entered
set hlsearch        " highlight matches

colorscheme peachpuff
```

## VSCode

Acesse as preferências do usuário com `CMD` + `,`:

```json
{
    "telemetry.enableCrashReporter": false,
    "telemetry.enableTelemetry": false,
    "editor.fontSize": 13,
    "editor.fontFamily": "'Source Code Pro', 'Roboto Mono', Menlo, Monaco, 'Courier New', monospace",
    "editor.wordWrap": "on",
    "editor.lineHeight": 26,
    "terminal.integrated.fontFamily": "'Source Code Pro'",
    "editor.renderIndentGuides": false,
    "editor.renderLineHighlight": "none",
    "explorer.openEditors.visible": 0,
    "editor.minimap.enabled": false,
    "git.confirmSync": false,
    "git.autofetch": true,
    "explorer.confirmDelete": false
}
```

## Personalizações gerais

### Trackpad

Em _System Preferences_ -> _Trackpad_, na aba _Point & Click_:

- Tap to click
- Click: light
- Tracking speed: 5

Na aba _More Gestures_:
- App Exposé

### Keyboard

Em _System Preferences_ -> _Keyboard_, na aba _Keyboard_:

- Key Repeat: no máximo (Fast)
- Delay Until Repeat: no máximo (Short).

### Dock

- Size: por volta dos 20%.
- Magnification: desligado.

Marcar os dois checkboxes abaixo, ficando todos marcados exceto o _Show recent application in Dock_:

- _Minimize windows into application icon_.
- _Automatically hide and show the Dock_.

Eu uso bastante um recurso de arrastar janelas com três dedos, o qual foi bem escondido pela maçã nas últimas versões do MacOS. Se você também usa, ou utilizava e não sabe onde foi parar o recurso:

_System Preferences_ -> _Accessibility_ -> _Mouse & Trackpad_:

- Clique no botão _Trackpad Options..._
- Marque a opção _Enable dragging_
- No menu dropdown escolha: _three finger drag_

**Obs**: Com essa opção ativa, alguns jestos que antes utilizavam três dedos, passarão a requerer quatro.

### Safari

Em _Safari_ -> _Preferences_ -> _Advanced_:
- Show full website address
- Show Develop menu in menu bar

Em _View_ -> _Show status bar_ (ou `CMD` + `/`)
