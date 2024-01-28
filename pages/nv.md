---
layout: default
permalink: /nv
---

## [Home](/) >> NeoVim editor

NeoVim cheatsheet and useful resources.

* TOC
{:toc}

## Cheatsheet

### Modes
* `Esc`: **Normal** mode: for navigation and inserting commands.
* `Esc i`: **Insert** mode: for inserting text.
* `Esc v`: **Visual** mode: for selecting and manipulating text.
  * `Esc S-v`: Visual line mode: select lines.
  * `Esc C-v`: Visual block mode: select columns.
* `Esc :` **Command** mode: for entering commands.

### Navigation (Motion)

* `h`: move left.
* `j`: move down.
* `k`: move up.
* `l`: move right.
* `w`: move start of next word.
* `b`: move start of previous word.
* `e`: move end of next word
* `W`: move start of next token.
* `B`: move start of previous token start.
* `E`: move end of next token.
* `t`: find till next char.
* `f`: find next char.
* `T`: find till previous char.
* `F`: find previous char.
* `0`: move start of line.
* `$`: move end of line.
* `^`: move first (non-blank) char of line.
* `gg`: go to the beginning of the file.
* `#G`: go to line number `#`.
* `G`: go to the end of the file.
* `%`: go to matching `(`,`)`,`[`,`]`,`{` or `}`.

### Edit (Operators)

* `i`: enter insert mode at the current cursor position.
* `a`: enter insert mode after the current cursor position.
* `I`: enter insert mode at the beginning of the line.
* `A`: enter insert mode at the end of the line.
* `o`: insert a new line below the current line and enter insert mode.
* `O`: insert a new line above the current line and enter insert mode.
* `x`: delete the character at the cursor position.
* `X`: delete the character before the cursor position.
* `d`: delete operator.
* `dd`: delete the current line.
* `D`: delete from the cursor position to the end of the line.
* `y`: copy operator.
* `yy`: copy the current line.
* `Y`: copy from the cursor position to the end of the line.
* `p`: paste the copied or deleted content after the cursor position.
* `P`: paste the copied or deleted content before the cursor position.
* `r`: replace character under the cursor.
* `c`: replace from the cursor to where the motion takes you.
* `C`: replace from cursor to end of line.
* `cc`: replace the current line.

* `u`: undo last change.
* `C-r`: redo last undone change.
* `.`: repeat last command.

### Indent

* `>>`: indent to the right.
* `<<`: indent to the left.
* `==`: autoindent line.


* `diw`: delete in word.
* `ciw`: change in word.
* `yiw`: yank in word.

### Visual selection

### Search

* `/pattern`: search `pattern` forward.
* `?patern`: search `pattern` backward.
* `n`: search next pattern.
* `N`: search previous pattern.
* `*`: find next occurence of token.
* `#`: find previous occurence of token.

### Substitute

* `:s/old/new`: substitute `new` for the first `old` in a line.
* `:s/old/new/g`: substitute `new` for all `old` on a line.
* `:#,#s/old/new/g`: substitute `new` for all `old` between two line `#`.
* `:%s/old/new/g`: substitute all occurrences in the file.
* `:%s/old/new/gi`: substitute all occurrences and make it case insensitive.
* `:%s/old/new/gc`: substitute all occurrences and ask for confirmation each time.

### Navigation (Screen)

* `H`: move to top of screen.
* `M`: move to middle of screen.
* `L`: move to bottom of screen.
* `zz`: center screen.
* `C-b`: move backward one full screen.
* `C-f`: move forward one full screen.
* `C-d`: move down half screen.
* `C-u`: move up half screen.
* `C-e`: scroll down one line.
* `C-y`: scroll up one line.
* `C-o`: move backward through jump history.
* `C-i`: move forward through jump history.

### Windows and Tabs

* `sp`: split window horizontally.
* `vsp`:  split window vertically.
* `C-w-w`: cycle through open windows.
* `C-w-h`: move to window on the left.
* `C-w-j`: move to window below.
* `C-w-k`: move to window above.
* `C-w-l`: move to window on the right.

* `:tabnew`: open new tab.
* `:tabclose`: close current tab.

### Save and Exit

* `:w`: save file.
* `:w <filename>`: save file as `<filename>`.
* `:q`: quit.
* `:qw`: save file and quit.
* `:q!` discard changes and quit.

### Various

* `C-g`: display location and file status.

### Commands

* `:!<command>` run command.

### Macro

* `qa`: record macro `a`.
* `q`: stop recoding macro.
* `@a`: run macro `a`.
* `@@`: run last macro again.

### Help

* `:help`: open help.
* `:help <topic>`: open help for `<topic>`.

## Configuration

* `:set number`: show line numbers.
* `:set relativenumber`: set relative line numbers.
* `:set tabstop=4`:
* `:set shiftwidth=4`:
* `:set softtabstop=4`:
* `:set autoindent`:
* `:set smarttab`:
* `:set list`: show invisible characters.
* `:set mouse=a`:
* `:set encoding=UTF-8`:
* `:colorscheme=default`: set colorsheme `default`.

## Resources

### Plugin

* [Awesome Neovim](https://github.com/rockerBOO/awesome-neovim)

### NeoVim distributions

* [LazyVim](https://www.lazyvim.org/)
* [NvChad](https://nvchad.com/)
* [AstroNvim](https://astronvim.com/)
* [LunarVim](https://www.lunarvim.org/)

### Cheatsheets

* [Awesome Vim Cheat Sheets to Help You Learn Vim](https://linuxhandbook.com/vim-cheat-sheet/)
