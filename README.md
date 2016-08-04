# My-bash-vim-configurations

The follwing plugins and configurations are my personal preference.

1. zsh and oh-my-zsh (bash counterpart, more plugins and friendly to programmers)
  - [Official Link]()
  - [Personal configuration](https://github.com/lovexi/My-bash-vim-configurations#zsh-and-oh-my-zsh)
2. solarized (color theme)
  - [Official Link](http://ethanschoonover.com/solarized)
  - [Github repo](https://github.com/altercation/solarized)
  - [Personal configuration](https://github.com/lovexi/My-bash-vim-configurations#solarized)
3. powerline (a statusline which can be embeded in various applitions, provides status line and prompts)


## Zsh and Oh-My-Zsh

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
