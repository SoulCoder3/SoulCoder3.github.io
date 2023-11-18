---
layout:     post
title:      Vim operator
subtitle:   
date:       2023-11-16
author:     BY David
header-img: img/TechTool.jpg
catalog: true
tags:
    - Vim

---

## Vim Operation Guide
### Move
#### Move in character
`h`: shift left one character
`j`: shift down one character
`k`: shift up one character
`l`: shift right one character
`5l`: Like other shortcut keys, we can use numbers to move multiple characters, such as `5l` to move 5 characters to the left.

### Move in line
* `^`: move to the beiginning of first word in the line
* `$`: move the end of the line
* `:10`: move to line 10, `:set number` to show the line number
* `gg`: move the first line of the file
* `G`: move to the last line of the file

#### Move in word
* `w`: move to the beginning of the next word
* `b`: move to the beginning of the before word
* `e`: move to the end of the next word
* Word movement also supports numerical prefixes. `4w` can move backward 4 words. In addition, uppercase `W`, `B`, and `E` have the same function, except that lowercase uses punctuation to separate words, and uppercase uses spaces to separate words, which is more suitable for moving in the code.

### Delete
* `d0`: delete from the cursor to the beginning of the line
* `d$`: delete from the cursoor to the end of the line
* `D`: delete the whole line
* `dl`: delete the current character
* `dw`: delete until the end of a word
* `d3w`: delete until the end of next three words
* `db`: delete until the beginning of a word
* `d9e`: delete until the beginning of the next 9 words
* `dk`: delete two line up
* `dj`: delete two line down

### Search
* `/string`: search string in text
* `n`: jump to next match
* `N`: jump to pervious match

### Replace
* `:s/vim/jdb/g`: `:s=substitute`, replace all `vim` in text by `jdb`. `g=global`
* `cc`: replace for a whole line
* `ce`: replace until the end of the word

### Save
* `:w`: save and continue
* `:wq`: save and quit
* `:q!`: quit 