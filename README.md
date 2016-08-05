# My-bash-vim-configurations

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
