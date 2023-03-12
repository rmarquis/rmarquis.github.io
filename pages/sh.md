---
layout: default
permalink: /sh
---

## [Home](/) >> Shell

Shell prompt customization, using [Starship](https://starship.rs/) as a minimal, fast and customizable cross-shell.

### Install

Install starship.

#### Windows

    > winget install Starship.Starship

Launch it from `<%USERPROFILE%>\Documents\PowerShell\Microsoft.PowerShell_profile.ps1`:

```
Invoke-Expression (&starship init powershell)
```

#### WSL/Linux

    $ sudo pacman -S starship

Launch it from `~/.bashrc`:

```
eval "$(starship init bash)"
```

### Configure

Add the shell [configuration](https://github.com/rmarquis/dotfiles/blob/main/.config/starship.toml) in `~/.config/starship.toml`.
