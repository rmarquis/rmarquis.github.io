---
layout: default
permalink: /sh
---

## [Home](/) >> Shell customization

Shell prompt customization, using [Starship](https://starship.rs/) as a minimal, fast and customizable cross-shell.

* TOC
{:toc}

* * *

## Prerequisites

Install a [Nerd Font](https://www.nerdfonts.com/) and enable it in your terminal. For example, try:

* the [Caskaydia Cove Nerd Font](https://www.nerdfonts.com/font-downloads), based on [Cascadia Code](https://learn.microsoft.com/en-us/windows/terminal/cascadia-code)
* the [JetbrainsMono Nerd Font](https://www.nerdfonts.com/font-downloads), based on [JetBrains Mono](https://www.jetbrains.com/lp/mono/)

## Install

### Windows

Install starship:

    > winget install Starship.Starship

Launch it from `<%USERPROFILE%>\Documents\PowerShell\Microsoft.PowerShell_profile.ps1`:

```
Invoke-Expression (&starship init powershell)
```

### Linux/WSL

The Bash shell does not support the right prompt, so ensure to use [Zsh](https://wiki.archlinux.org/title/Zsh) instead.

Install Starship:

    $ sudo pacman -S starship

Launch it from `~/.zshrc`:

```
eval "$(starship init zsh)"
```

## Configure

Add the shell [configuration](https://github.com/rmarquis/dotfiles/blob/main/.config/starship.toml) in `~/.config/starship.toml`.
