# Idris environment for Linux

This very short guide should help setting up a basic Idris2 environment
including the Idris2 package manager and interactive editing with Neovim.

This is a work in progress and can contain some erroneous instructions or
missing parts.Therefore, please be careful.


## Prerequisites

- git
- cmake
- gcc
- chezScheme
    - `sudo apt install chezscheme`


## Tmux

Tmux enables multiple terminals on one screen and the handling of their
position.

1. Install tmux via the apt-get tool
    - `sudo apt-get install tmux`

2. Clone the tmux plugin manager from github
    - `git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm`

3. Replace or initially place the `tmux.conf` in the `.conf/tmux` folder
    - new prefix `Ctrl-a`
    - activates mouse support
    - add plugins

4. Reload tmux environment or restart tmux manually
    - tmux source `~/.tmux.conf`

5. Install plugins
    - `prefix + I`

### Key-Bindings

[`cheatcheat`](https://tmuxcheatsheet.com/)

- prefix + : => opens command line for tmux commands
- split screen (prefix + %)
- turn planes (prefix + <space>)
- go to next window (prefix + n)
- overview sessions (prefix + w)
- scroll in command line history (prefix + esc)


## Neovim

Neovim will be the editor for coding Idris2 due to the great support for the
interactive editing possible with Idris2.

Either the apt tool can be used or Neovim can be installed from source:

* apt
    - `sudo apt install neovim`

* from source
    1. clone repository
        - ssh
            - `git clone git@github.com/neovim/neovim.git`
        - https
            - `git clone https://github.com/neovim/neovim`
    2. `cd neovim && make CMAKE_BUILD_TYPE=RelWithDebInfo`
    3. `sudo make install`

### Plugin manager

To enabling nvim-plugins, a vim-plug manager is needed (compatible with nvim).

- download plug.vim and place it inside the autoload folder
    - `sh -c 'curl -fLo "${XDG_DATA_HOME:-$HOME/.local/share}"/nvim/site/autoload/plug.vim --create-dirs https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim'`

### Config

- copy the `init.vim` to `.config/nvim`
    - run in Neovim: `:PlugUpdate` to install the nvim-plugins
    - Plugins included:
        - [syntastic](https://github.com/vim-syntastic/syntastic)
        - [tabular](https://github.com/godlygeek/tabular)
        - [vim color scheme holokai](https://github.com/mrjohannchang/color-scheme-holokai.vim)
        - [nvim-lspconfig](https://github.com/neovim/nvim-lspconfig)
        - [idris2-nvim](https://github.com/idris-community/idris2-nvim)
        - [nui.nvim](https://github.com/MunifTanjim/nui.nvim)
        - [nerdtree](https://github.com/preservim/nerdtree)
            - open explorer view with `nvim +NERDTree`
            - local leader `<ctrl> w`
            - switch pane inside nerdtree (ll h(left) or l(right))
            - split vertical (:vs)

###  Tutorial

For Neovim-Beginners there is a quite nice tutorial. Simply enter `:Tutor`
inside a nvim session and work it through.


## Idris2-pack

Idris pack is used for maintaining the correct version of Idris2 and Idris2-lsp
and maintaining Idris2 projects.

### Installation

1. `git clone git@github.com:stefan-hoeck/idris2-pack.git`
2. `cd idris2-pack`
3. install idris2-pack: `make micropack SCHEME=chezscheme`
4. replace the pack.toml file (in `.pack/user`)
5. check $PATH after installation
    - `echo $PATH`
    - if `$HOME/.pack` does not exist, add
      `export PATH="$HOME/.pack/bin:$HOME/.idris2/bin:$PATH"` at the end of the
      .bashrc or .zshrc file

### Config

- `pack update`:   Update the pack installation by downloading and building
  the current main branch of https://github.com/stefan-hoeck/idris2-pack
- `pack switch latest`:  Switch to the given package collection. This will
  adjust your `$PACK_DIR/user/pack.toml` file to use the given package
  collection. It will also install all auto libs and apps from the
  given package collection.
  Note: It is also possible to switch to the latest package
  collection by using "latest" as the collection name.


## Setup Test

If pack is working correctly, the following command should create a basic Idris2
project inside a new folder named "testInstallation" :
`pack new lib testInstallation`.

With the command `pack run test/test.ipkg` the project's tests can be run and
therefore tested, if Idris2 is correctly installed.
Further, the correct highlighting can be tested by opening the only file in the
`src` folder.
