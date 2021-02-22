# VIM Cheatsheet

## Navigation

### Basic Navigation
* _k_ = up 1 line
* _j_ = down 1 line
* _h_ = left 1 char
* _l_ = right 1 char
* _w_ = forward 1 word
* _b_ = backward 1 word
* _e_ = end of word
* _$_ = end of line
* _0_ = beginning of line
* _^_ = first non-blank char of line
* _{_ = previous paragraph
* _}_ = next paragraph

### Navigation by search
* _f_ + __char__ = next instance of __char__
* _/_ + __searchTerm__ + _Enter_ = goto next instance of __searchTerm__
* _?_ + __searchTerm__ + _Enter_ = goto previous instance of __searchTerm__
* _*_ = goto next instance of word at cursors current position
* _n_ = goto next instance of last search (use with _/_, _?_, _*_)
* _N_ = goto previous instance of last search (use with _/_, _?_, _*_)

### Screen / File Navigation
* _gg_ = top of file
* _G_ = bottom of file
* _Ctrl_ + _u_ = up 1/2 screen
* _Ctrl_ + _d_ = down 1/2 screen
* _Ctrl_ + _b_ = up 1 screen
* _Ctrl_ + _f_ = down 1 screen
* _H_ = top of screen
* _L_ = bottom of screen
* _zz_ or _z._ = center screen on cursor
* _zt_ = move screen so cursor is at top
* _zb_ = move screen so cursor is at bottom


## Redo/Undo
* _u_ = undo
* _Ctrl_ + _r_ = redo


## Repeat Previous Commands
* . = repeat whatever was last done, but at current cursor
* _q_ + __char__ + __do stuff__ + _q_ = store __do stuff__ in register on __char__ as repeatable action
  * _@@_ = repeat last action
  * _@_ + __char__ = repeat action stored in __char__


## Copy / Paste
* _yw_ = yank (copy) word
* _Y_ or _yy_ = yank line
* _"_ + __char__ + __copy stuff__ = store __copy stuff__ in register on __char__
  * paste it in later with _"_ + __char__ + _p_
* _p_ paste after
* _P_ paste before


## Cut / Delete
* _dw_ = delete word
* _dd_ = delete line
* _x_ = delete char at cursor
* _s_ = swap/delete char at cursor & switch to insert mode
* _S_ = swap/delete current line & switch to insert mode
* _cw_ = delete from cursor to end of current word & switch to insert mode
* _ciw_ = delete current inner word & switch to insert mode
* _C_ = delete from cursor to end of line & switch to insert mode


## Switch to Insert Mode
* _o_ = start insert mode on new line below current
* _O_ = start insert mode on new line above current
* _a_ = start insert mode after current char
* _A_ = start insert mode at end of current line
* _i_ = start insert mode before current char
* _I_ = start insert mode at first non-blank char of line


## Visual Mode
* _v_ = enter visual mode to select stuff for copy/delete, etc
* _viw_ = enter visual mode and select inside word at current cursor position
* _vi{_ = enter visual mode and select inside curly brackets (or parens or quotes or square brackets)
* _va{_ = enter visual mode and select curly brackets and everything inside (or parens or quotes or square brackets)
* _V_ = enter visual mode and select current line
* _Ctrl_ + _v_ = enter __Visual Block Mode__ and edit multiple lines at once


## Search and Replace
* _:_ + _%s/_ + __searchTerm__ + _/_ + __replacement__ + _/gc_ =
  Search (% for whole file) for all occurances of __searchTerm__ and replace with __replacement__ (_c_ means confirm)
* _:_ + _10,20s/_ + __searchTerm__ + __/__ + __replacement__ + _/gc_ =
  Search the range (lines 10 to 20) for all occurances of __searchTerm__ and replace with __replacement__.


## Surround
* _ds_ __existingChar__ = delete existing surround
* _cs_ __existingChar__ __desiredChar__ = change surround existing to desired
* _ys_ __motion__ __desiredChar__ = surround something with something using motion (as in "you surround")
  * e.g.: _ysiw_ + _'_ = "you surround inner word" with single quote
* _S_ __desiredChar__ = surround when in visual modes (surrounds full selection)


## Resources
* https://www.factorpad.com/tech/vim-cheat-sheet.html
* http://vim.wikia.com/wiki/Replace_a_word_with_yanked_text
* https://www.cs.oberlin.edu/~kuperman/help/vim/registers.html
* https://www.brianstorti.com/vim-registers/
* http://www.vimgolf.com/
* https://www.openvim.com/
