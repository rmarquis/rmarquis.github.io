---
layout: default
permalink: /vi
---

## [Home](/) >> NeoVim editor

NeoVim cheatsheet and useful resources.

* TOC
{:toc}

## Cheatsheet

Interactive tutorial: `:Tutor`.

### Modes
* `Esc`: **Normal** mode: for navigation and inserting commands.
* **Insert** mode: for inserting text. `Esc i`
* **Visual** mode: for selecting and manipulating text. `Esc v`
  * Visual line mode: select lines. `Esc S-v`
  * Visual block mode: select columns. `Esc C-v`
* **Command** mode: for entering commands. `Esc :`

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


diw
ciw

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

## NeoVim distributions

* [LazyVim](https://www.lazyvim.org/)
* [NvChad](https://nvchad.com/)
* [AstroNvim](https://astronvim.com/)
* [LunarVim](https://www.lunarvim.org/)

## Cheatsheets

* [Awesome Vim Cheat Sheets to Help You Learn Vim](https://linuxhandbook.com/vim-cheat-sheet/)

## Summary

### Lesson 1
*Moving, Exiting, Deletion, Insertion, Appending, Editing*

1. The cursor is moved using either the arrow keys or the hjkl keys.
h (left)   j (down)       k (up)       l (right)

2. To start Neovim from the shell prompt type:

```sh
$ nvim FILENAME
```
3. To exit Neovim type: `<Esc>`{normal} `:q!`{vim} `<Enter>`{normal} to trash all changes.
  OR type: `<Esc>`{normal} `:wq`{vim} `<Enter>`{normal} to save the changes.

4. To delete the character at the cursor type: `x`{normal}

5. To insert or append text type:
`i`{normal} insert text `<Esc>`{normal}     insert before the cursor.
`A`{normal} append text `<Esc>`{normal}     append after the line.

NOTE: Pressing `<Esc>`{normal} will place you in Normal mode or will cancel
an unwanted and partially completed command.
      

### Lesson 2
*Deletion, Operators and motions, Count for a motion, Count to delete, Operating on lines, Undo*

1. To delete from the cursor up to the next word type:    `dw`{normal}

2. To delete from the cursor to the end of a line type:   `d$`{normal}

3. To delete a whole line type:                           `dd`{normal}

4. To repeat a motion prepend it with a number:           `2w`{normal}

5. The format for a change command is:

operator   [number]   motion

where:

operator -   is what to do, such as [d](d) for delete
[number] -   is an optional count to repeat the motion
motion   -   moves over the text to operate on, such as:
[w](w) (word),
[$]($) (to the end of line), etc.

6. To move to the start of the line use a zero: [0](0)

7. To undo previous actions, type:            `u`{normal}  (lowercase u)
   To undo all the changes on a line, type:   `U`{normal}  (capital U)
   To undo the undo's, type:                  `<C-r>`{normal}

### Lesson 3
*Put, Replace, Change*

1. To put back text that has just been deleted, type [p](p). This puts the
deleted text AFTER the cursor (if a line was deleted it will go on the
line below the cursor).

2. To replace the character under the cursor, type [r](r) and then the
character you want to have there.

3. The [change operator](c) allows you to change from the cursor to where
the motion takes you. Type `ce`{normal} to change from the cursor to the
end of the word, `c$`{normal} to change to the end of a line, etc.

4. The format for change is:

c   [number]   motion

### Lesson 4
*Cursor location and file status, Search, Matching parentheses search, Substitute*

1.  `<C-g>`{normal}     displays your location and the file status.
    `G`{normal}         moves to the end of the file.
    number `G`{normal} moves to that line number.
    `gg`{normal}        moves to the first line.

2. Typing `/`{normal} followed by a phrase searches FORWARD for the phrase.
Typing `?`{normal} followed by a phrase searches BACKWARD for the phrase.
After a search type `n`{normal} to find the next occurrence in the same
direction or `N`{normal} to search in the opposite direction.
`<C-o>`{normal} takes you back to older positions, `<C-i>`{normal} to
  newer positions.

3. Typing `%`{normal} while the cursor is on a (,),[,],{, or } goes to its
match.

4. To substitute new for the first old in a line type
```cmd
:s/old/new
```
To substitute new for all 'old's on a line type
```cmd
:s/old/new/g
```
To substitute phrases between two line #'s type
```
:#,#s/old/new/g
```
To substitute all occurrences in the file type
```
:%s/old/new/g
```
To ask for confirmation each time add 'c'
```
:%s/old/new/gc
```

### Lesson 5
*Execute external command, More on writing files, Selecting text to write, Retrieving ane merging files*

1. [:!command](:!cmd) executes an external command.

Some useful examples are:
`:!ls`{vim}                    - shows a directory listing
`:!rm FILENAME`{vim}           - removes file FILENAME

2. [:w](:w) FILENAME              writes the current Neovim file to disk with
name FILENAME.

3. [v](v)  motion  :w FILENAME   saves the Visually selected lines in file
FILENAME.

4. [:r](:r) FILENAME              retrieves disk file FILENAME and puts it
below the cursor position.

5. [:r !dir](:r!)                  reads the output of the dir command and
puts it below the cursor position.


### Lesson 6
*Open, Append, Another way to replace, Copy and paste, Set option*

1. Type `o`{normal} to open a line BELOW the cursor and start Insert mode.
Type `O`{normal} to open a line ABOVE the cursor.

2. Type `a`{normal} to insert text AFTER the cursor.
Type `A`{normal} to insert text after the end of the line.

3. The `e`{normal} command moves to the end of a word.

4. The `y`{normal} operator copies text, `p`{normal} pastes it.

5. Typing a capital `R`{normal} enters Replace mode until `<Esc>`{normal} is
  pressed.

6. Typing "[:set](:set) xxx" sets the option "xxx". Some options are:

'ic' 'ignorecase'   ignore upper/lower case when searching
'is' 'incsearch'    show partial matches for a search phrase
'hls' 'hlsearch'    highlight all matching phrases

You can either use the long or the short option name.

7. Prepend "no" to switch an option off:
```
:set noic
```
8. Prepend "inv" to invert an option:
```
:set invic
```

### Lesson 7
*Getting help, Create a startup script, Completion*

1. Type `:help`{vim}
or press `<F1>`{normal} or `<Help>`{normal} to open a help window.

2. Type `:help TOPIC`{vim} to find help on TOPIC.

3. Type `<C-w><C-w>`{normal} to jump to another window

4. Type `:q`{vim} to close the help window

5. Create an init.vim startup script to keep your preferred settings.

6. While in command mode, press `<C-d>`{normal} to see possible completions.
  Press `<Tab>`{normal} to use one completion.
