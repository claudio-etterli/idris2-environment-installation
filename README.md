# Idris installation 2025

Maybe there is no `.config` folder => if so, create it

## Tmux

- sudo apt-get install tmux

- replace or initialy place the `tmux.conf` in the `.conf/tmux` folder
- [`cheatcheat`](https://tmuxcheatsheet.com/) (local leader == `Ctrl-a`)
    - `Ctrl-a + :` => opens command line for tmux commands
    - split screen (ll - %)
    - turn planes (ll - <space>)
    - go to next window(?) (ll - n)
    - overview sessions (ll - w)
    - scroll in command line history (ll - esc)

## Neovim

### Package manager
`sudo apt install neovim`

### From source
- install gcc and cmake (maybe already done)
- `git clone https://github.com/neovim/neovim`
- `cd neovim && make CMAKE_BUILD_TYPE=RelWithDebInfo`
- `sudo make install`

### Config

- copy the `init.vim` to `.config/nvim`
    - run in Neovim: `:PlugUpdate` to install the nvim-plugins

- nerdtree
    - open file system with `nvim +NERDTree`
    - local leader `<ctrl> w`
    - switch pane inside nerdtree (ll h(left) or l(right))
    - split vertical (:vs)
- tutorial
    - inside nvim editor `:Tutor` to begin tutorial
    - open file (or create new if not exists) (`nvim <filename>`)
    - save (:w)
    - quit/exit file (:q)

## Idris2-pack

### Prerequisites

- chezScheme
    - `sudo apt install chezscheme`
- bash

### Installation

- `git clone git@github.com:stefan-hoeck/idris2-pack.git`
- `cd idris2-pack`
- `make micropack SCHEME=chezscheme`

- replace the pack.toml file (in `.pack/user`)
- `pack update` to build get the newest changes
- `pack switch latest` to freshly check for updates (may take up to 10 min)

- check $PATH after installation
    - `echo $PATH`
    - if `$HOME/.pack` does not exist, add export `PATH="/Directory1:$PATH"`
      at the end of the .bashrc file
