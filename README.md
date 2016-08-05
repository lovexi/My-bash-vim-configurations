# My-bash-vim-configurations

> *All following plugins and configurations are built in iTerm2 on Mac. For windows configurations, it may vary in some steps. More precise detailed information is provided in each official user guide*

The follwing plugins and configurations are my personal preference.

1. zsh and oh-my-zsh (bash counterpart, more plugins and friendly to programmers)
  - [zsh Official Link](http://zsh.sourceforge.net/)
  - [oh-my-zsh github repo](https://github.com/robbyrussell/oh-my-zsh)
  - [Personal configuration](https://github.com/lovexi/My-bash-vim-configurations#zsh-and-oh-my-zsh)
2. solarized (color theme)
  - [Official Link](http://ethanschoonover.com/solarized)
  - [Github repo](https://github.com/altercation/solarized)
  - [Personal configuration](https://github.com/lovexi/My-bash-vim-configurations#solarized)
3. powerline (a statusline which can be embeded in various applitions, provides status line and prompts)
  - [Official Link](https://powerline.readthedocs.io/en/latest/)
  - [Github repo](https://github.com/powerline/powerline)
  - [Personal configuration](https://github.com/lovexi/My-bash-vim-configurations#powerline)
4. Vim Plugins
  - [Vundle Official Link](https://github.com/VundleVim/Vundle.vim)
  - [Vundle Setup](https://github.com/lovexi/My-bash-vim-configurations#vundle)
  - [Personal preferred plugins](https://github.com/lovexi/My-bash-vim-configurations#plugins)

## Zsh and Oh-My-Zsh

### Zsh

Zsh is a shell designed for interactive use, although it is also a powerful scripting language. Zsh can be a good counterpart with bash.

For most of linux distributions, zsh is already installed in system with bash. `echo $SHELL` can echo your current shell on screen. Default shell for Terminal.app in mac or iTerm is bash.

```bash
$ echo $SHELL
/bin/zsh
```

Or you can install zsh on mac like:

```bash
$ brew install zsh
```

replace shell bash with zsh by modifying `/etc/shells` file. Add `/usr/local/bin/zsh`. Then run command `chsh -s /usr/local/bin/zsh` to change login shell.

> `chsh` changes a user's login shell. Usage: chsh [-s login_shell] [user]

### Oh-My-Zsh

Zsh is a community-driven open-source framework for managing zsh configurations.

![Oh-My-Zsh](https://camo.githubusercontent.com/5c385f15f3eaedb72cfcfbbaf75355b700ac0757/68747470733a2f2f73332e616d617a6f6e6177732e636f6d2f6f686d797a73682f6f682d6d792d7a73682d6c6f676f2e706e67)

#### Installation

Two ways to install oh-my-zsh:

**via curl**
```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

**via wget**
```bash
sh -c "$(wget https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"
```

#### Configuration

Most frequently used plugins already exists in ~/.oh-my-zsh/plugins. In order to initialize the plugins you want, you are required to add those plugins in zsh configuration file `~/.zshrc`:

For instance:
```bash
plugins=(git autojump osx)
```

## Solarized

It provides precious color theme for machine and people. Vim, [iterm2](https://github.com/lovexi/My-bash-vim-configurations#iterm2-configuration) and Intellij are supported.

command to get the lastest version:
```bash
git clone git://github.com/altercation/solarized.git
```

### Vim configuration

1. Go into solorized directory, move solarized.vim file to .vim/colors directory.
```bash
$ cd vim-colors-solarized/colors
$ mv solarized.vim ~/.vim/colors/
```
2. Modify vimrc configuration
```bash
$ vim ~/.vimrc
```
And append the following command into .vimrc file
```bash
syntax enable
# choose light or dark theme
set background=dark
colorscheme solarized
```

### Iterm2 configuration
Go into solorized directory, double click `solarized/iterm2-colors-solarized/`. Then go to preference in Iterm2 to choose color theme: light/dark.

> One issue may raise here, after solarized color theme is configured, the UI of Iterm2 is still in black-white. Try iTerm2 - Preferences - Profiles - Text - Text Rendering and unclick `Draw bold text in bright colors` option.

## Powerline

Powerline is a statusline plugin for vim, and provides statuslines and prompts for several other applications.

![Powerline Statusline](http://www.tecmint.com/wp-content/uploads/2015/10/Powerline-Vim-Statuslines.png)

> Python is required for powerline, since it is based on python code. `python -v` can be used to make sure the installation in your local machine.

### Installation

```bash
pip install powerline-status
```

> `pip show powerline-status` can provide actual installation path for powerline, it varies from different OS. 

### Bash configuration

The configuration command depends on exact bash you are using

#### Bash prompts

```bash
. {repository_root}/powerline/bindings/bash/powerline.sh
```

#### Zsh prompts

```bash
. {repository_root}/powerline/bindings/zsh/powerline.zsh
```

This can be set in `~/.bashrc` or `~/.zshrc` conf file, in order to start powerline prompts everytime bash/zsh is initialized.

> The font in powerline is not included in [Unicode](http://cenalulu.github.io/linux/character-encoding/). For a better font support, You can do the following commands.

```bash
$ git clone https://github.com/powerline/fonts.git
$ cd fonts
$ ./install.sh
```

Then check Perference -> Profiles -> Text. Change both Regular Font and Non-ASCII font, for any fonts suppporting for powerline.

![Powerline Font Configuration](http://cenalulu.github.io/images/linux/powerline/fonts.png)

### Vim Configuration

Simple step to add powerline feature for vim: Adding `set rtp+=/Library/Python/2.7/site-packages/powerline/bindings/vim` in `~/.vimrc` conf file.

Personal vim conf for powerline is:

```bash
set rtp+=/Library/Python/2.7/site-packages/powerline/bindings/vim

" These lines setup the environment to show graphics and colors correctly.
set nocompatible
set t_Co=256
 
let g:minBufExplForceSyntaxEnable = 1
python from powerline.vim import setup as powerline_setup
python powerline_setup()
python del powerline_setup
 
if ! has('gui_running')
   set ttimeoutlen=10
   augroup FastEscape
      autocmd!
      au InsertEnter * set timeoutlen=0
      au InsertLeave * set timeoutlen=1000
   augroup END
endif
 
set laststatus=2 " Always display the statusline in all windows
set guifont=Inconsolata\ for\ Powerline:h14
set noshowmode " Hide the default mode text (e.g. -- INSERT -- below the statusline)
```

## Vim

As we all know, [Vim](http://www.vim.org/) is widely used editor based on shell, it can be a powerful IDE for programmers, with proper plugins.

### Vundle

A Vim Bundle Manager which can save programmers time to configure bundles and plugins in vim. 

#### Installation

```bash
$ git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim
```

#### Initialization

Put the following piece of code on the top of `~/.vimrc` conf file. Remove those plugin codes you don't need, some of them are for demonstration purposes.

```vim
set nocompatible              " be iMproved, required
filetype off                  " required

" set the runtime path to include Vundle and initialize
set rtp+=~/.vim/bundle/Vundle.vim
call vundle#begin()
" alternatively, pass a path where Vundle should install plugins
"call vundle#begin('~/some/path/here')

" let Vundle manage Vundle, required
Plugin 'VundleVim/Vundle.vim'

" The following are examples of different formats supported.
" Keep Plugin commands between vundle#begin/end.
" plugin on GitHub repo
Plugin 'tpope/vim-fugitive'
" plugin from http://vim-scripts.org/vim/scripts.html
Plugin 'L9'
" Git plugin not hosted on GitHub
Plugin 'git://git.wincent.com/command-t.git'
" git repos on your local machine (i.e. when working on your own plugin)
Plugin 'file:///home/gmarik/path/to/plugin'
" The sparkup vim script is in a subdirectory of this repo called vim.
" Pass the path to set the runtimepath properly.
Plugin 'rstacruz/sparkup', {'rtp': 'vim/'}
" Install L9 and avoid a Naming conflict if you've already installed a
" different version somewhere else.
Plugin 'ascenator/L9', {'name': 'newL9'}

" All of your Plugins must be added before the following line
call vundle#end()            " required
filetype plugin indent on    " required
" To ignore plugin indent changes, instead use:
"filetype plugin on
"
" Brief help
" :PluginList       - lists configured plugins
" :PluginInstall    - installs plugins; append `!` to update or just :PluginUpdate
" :PluginSearch foo - searches for foo; append `!` to refresh local cache
" :PluginClean      - confirms removal of unused plugins; append `!` to auto-approve removal
"
" see :h vundle for more details or wiki for FAQ
" Put your non-Plugin stuff after this line
```

### Plugins

#### NerdTree

It allows you to export the external filesystem and interact between the external directories and internal file context.

1. Adding `Bundle 'The-NERD-tree'` in `~/.vimrc` conf file
2. Switch into vim, call vim cmd `:PluginInstall` to install plugins

Some personal tips are listed:
- You can start nerdtree plugin in vim automatically whenever your vim is initialized by adding following code in `~/.vimrc`

```vim
autocmd VimEnter * NERDTree
autocmd VimEnter * wincmd p
```

- Use `:qa` and `:qa!` instead of `:q` and `:q!`, since you have two windows now when you start another window to show filesystem. Otherwise, we have to manually close all windows twice.
