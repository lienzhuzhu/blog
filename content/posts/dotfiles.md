+++
title = "My Setup"
date = "2023-08-04T15:09:31-07:00"
# description = ""

tags = ["engineering"]

draft = true
+++


When I watch YouTube videos of other computer scientists and software engineers I can't help but admire their sleek, clean development environment setups. They give off an air of control and mastery, having tamed their machines to which I could only heed my wit.

So, I have decided to work on setting up my own dotfiles more or less from scratch.


## Goals

- Each application installed must use an easy to read/ modify config file
- Each application installed must be compatible with MacOS and Ubuntu
- Write an `install.sh` script
- Minimize platform dependency


## Key applications:

- __Terminal Multiplexor__
[tmux](https://github.com/tmux/tmux)

- __Terminal Emulator__
[Alacritty](https://alacritty.org/)

- __Shell__
[zsh](https://zsh.org/)

- __Text Editor__
[Neovim](https://neovim.io/)

- __Prompt Customizer__
[Starship.rs](https://starship.rs/)


## Dependencies

- Rust
- Having some Nerd Font installed, I recommend just cloning the entire [repo](https://github.com/ryanoasis/nerd-fonts) and using the installation script
- Packer 
- ripgrep
