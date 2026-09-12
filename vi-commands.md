# Vim / gVim Command Reference

> Personal notes, cleaned up and organized by category.
> Original notes started: 15-May-2016

**Key notation used below:** `Ctrl-x` means hold Control and press `x`.
This matches Vim's own `:help` docs, which write it as `CTRL-X` (e.g. `:help CTRL-V`) — same key, just style/case.
Code blocks that show actual `.vimrc` mapping syntax use Vim's angle-bracket form instead (e.g. `<C-r>`, `<Esc>`, `<CR>`), since that's the literal syntax Vim expects in a mapping.

## Table of Contents

- [Quick Reference / Handy One-Liners](#quick-reference--handy-one-liners)
- [Modes & Entering Insert Mode](#modes--entering-insert-mode)
- [Movement](#movement)
- [Screen Movement](#screen-movement)
- [Words vs WORDs](#words-vs-words)
- [Find & Till (Character Search)](#find--till-character-search)
- [Bookmarks / Marks](#bookmarks--marks)
- [Delete / Change / Undo](#delete--change--undo)
- [Cut / Copy / Paste (Yank)](#cut--copy--paste-yank)
- [Registers](#registers)
- [System Clipboard](#system-clipboard)
- [Paste in Insert Mode](#paste-in-insert-mode)
- [Visual Mode & Text Objects](#visual-mode--text-objects)
- [Search](#search)
- [Find & Replace](#find--replace)
- [Find & Replace Across Multiple Files](#find--replace-across-multiple-files)
- [Global Commands (`:g`)](#global-commands-g)
- [Sorting & Reversing Lines](#sorting--reversing-lines)
- [Macros & Repeats](#macros--repeats)
- [Command-Line History](#command-line-history)
- [Buffers](#buffers)
- [Tabs](#tabs)
- [Windows / Splits](#windows--splits)
- [File Explorer (netrw)](#file-explorer-netrw)
- [Folding](#folding)
- [Sessions](#sessions)
- [Encrypting a File](#encrypting-a-file)
- [Shell Interaction](#shell-interaction)
- [gVim Startup Settings (.vimrc / _vimrc)](#gvim-startup-settings-vimrc-_vimrc)
- [Changing the Default Font (gVim)](#changing-the-default-font-gvim)
- [Changing the Color Scheme](#changing-the-color-scheme)
- [Useful Tips](#useful-tips)
- [FAQ / Gotchas](#faq--gotchas)

---

## Quick Reference / Handy One-Liners

| Command | Description |
|---|---|
| `Ctrl-r *` (in command-line, after `:` or `/`) | Paste system clipboard text into the command line to search/use |
| `Ctrl-r "` (in command-line, after `:` or `/`) | Paste last yank/delete (unnamed register) into the command line |
| `:bro[wse] ol[dfiles]` | List recently opened files with numbers; type number + Enter to open (space to page, `q` to quit) |
| `:ol[dfiles]` | Show recent files list; open file *n* with `:e #<n>` |
| `:Vex d:\n<Tab>` | Open a vertically split file explorer at `d:\n...` |
| `:tabnew` | Open a new tab with a new untitled `[No Name]` file |
| `:browse tabnew` | Open a new tab via a file-open dialog |
| `ggVG` | Select entire file (`gg` top, `V` line-select, `G` bottom) |
| `ggVG"*y` | Select all and copy to system clipboard |
| `"*yy` | Yank current line to system clipboard (no newline) |
| `vt"y` | Select up to (not including) the next `"` and yank — cursor must start right after opening quote |
| `vt"p` | Same selection, but paste over it |
| `v%` | Select (character-wise) the block enclosed by `{}`, `()`, or `[]` — cursor must be on one of the brackets (opening or closing). Using `V%` instead selects all *whole lines* from the cursor to the matching bracket, not just the enclosed content — usually not what you want here |
| `*` / `#` | Find next / previous occurrence of word under cursor |
| `:'<,'>s/red/green/g` | Find & replace only within a visually selected range of **lines** |
| `:s/\%Vold/new/g` | Find & replace only within the exact visually selected **characters** (`%V` atom) |

---

## Modes & Entering Insert Mode

| Command | Description |
|---|---|
| `i` | Insert text before cursor |
| `I` | Insert text at start of line |
| `a` | Append text after cursor |
| `A` | Append text at end of line |
| `o` | Open new line below and insert |
| `O` | Open new line above and insert |
| `R` | Enter Replace (overwrite) mode until `Esc` |
| `v` | Character-wise visual mode |
| `V` | Line-wise visual mode |
| `Ctrl-v` / `Ctrl-q` | Block/column-wise visual mode |
| `Esc` | Return to Normal mode |
| `gi` | Insert at the position where insert mode was last left |

---

## Movement

| Command | Description |
|---|---|
| `h j k l` | Move left, down, up, right |
| `gj` / `gk` | Move down/up by display line (respects line-wrap) |
| `w` / `W` | Move forward by word / WORD, cursor at start of word |
| `b` / `B` | Move backward by word / WORD, cursor at start of word |
| `e` / `E` | Move forward to end of word / WORD |
| `ge` / `gE` | Move backward to end of previous word / WORD |
| `0` | Move to beginning of line (column 0) |
| `^` | Move to first non-blank char of line |
| `$` | Move to end of line |
| `g_` | Move to last non-blank char of line |
| `H` | Move to top of current screen |
| `M` | Move to middle of current screen |
| `L` | Move to bottom of current screen |
| `gg` | Move to top of file |
| `G` | Move to end of file |
| `100G` or `:100` | Go to line 100 |
| `10\|` | Go to column 10 |
| `%` | Jump to matching `(`, `{`, `[` — cursor must be on the bracket |
| `[(` / `])` | Jump to previous/next unmatched parenthesis |
| `[{` / `]}` | Jump to previous/next unmatched brace |
| `(` / `)` | Jump backward/forward one sentence |
| `{` / `}` | Jump backward/forward one paragraph |
| `J` | Join current line with the next |
| `gJ` | Join lines without inserting a space |
| `Ctrl-f` | Page forward |
| `Ctrl-b` | Page backward |
| `Ctrl-d` | Scroll down half a page |
| `Ctrl-u` | Scroll up half a page |
| `Ctrl-l` | Redraw/refresh screen |
| `Ctrl-o` | Jump back to older cursor position (jump list) |
| `Ctrl-i` | Jump forward to newer cursor position (jump list) |

---

## Screen Movement

| Command | Description |
|---|---|
| `z.` | Center screen on cursor line, moving cursor to first non-blank char |
| `zz` | Center screen on cursor line, keeping the current column (unlike `z.`) |
| `zt` | Scroll so cursor line is at top of screen |
| `zb` | Scroll so cursor line is at bottom of screen |

> `z<CR>` and `z-` are the "move to first non-blank" variants of `zt` and `zb` — same relationship as `z.` has to `zz`.

---

## Words vs WORDs

- **word** — a sequence of letters, digits, and underscores (or a sequence of other non-blank chars), delimited by whitespace or punctuation.
- **WORD** — a sequence of non-blank characters, separated only by whitespace.

Example — `192.168.1.1`:
- As a single **WORD**: `192.168.1.1`
- As seven **word**s: `192` `.` `168` `.` `1` `.` `1`

---

## Find & Till (Character Search)

| Command | Description |
|---|---|
| `fx` | Find next occurrence of char `x` on the line |
| `Fx` | Find previous occurrence of char `x` on the line |
| `tx` | Move till just before next `x` |
| `Tx` | Move till just after previous `x` |
| `;` | Repeat latest `f`/`t`/`F`/`T` [count] times |
| `,` | Repeat latest `f`/`t`/`F`/`T` in the opposite direction |
| `dtx` | Delete up to (not including) `x` |
| `dfx` | Delete up to and including `x` |
| `ctx` | Change up to (not including) `x` |
| `cfx` | Change up to and including `x` |

---

## Bookmarks / Marks

| Command | Description |
|---|---|
| `` m{a-zA-Z} `` | Set a mark at cursor position |
| `` `{a-z} `` | Go to marked position (line & column) — file-local |
| `` '{a-z} `` | Go to marked line (cursor at first non-blank) — file-local |
| `` `{A-Z} `` | Go to marked position (line & column) — global, works across files |
| `` '{A-Z} `` | Go to marked line — global, works across files |
| `` '' `` | Go to line of position before last jump |
| `` `` `` | Go to exact position (line & column) before last jump |
| `` '. `` | Go to line of the last change |
| `:marks` | List all marks |

> You may edit ten files, and each could have a lowercase mark `a`, but only **one** file can hold uppercase mark `A` at a time — uppercase marks are global.
> To jump to a mark: `'` (apostrophe) jumps to the **start of the line**; `` ` `` (backtick) jumps to the **exact line & column**.

---

## Delete / Change / Undo

| Command | Description |
|---|---|
| `x` | Delete char under cursor (forward delete) |
| `X` | Delete char before cursor (backspace) |
| `dw` | Delete word |
| `d$` or `D` | Delete to end of line |
| `dd` | Delete (cut) whole line — `p` to paste |
| `ndd` | Delete `n` lines |
| `ce` | Change to end of word |
| `c$` or `C` | Change from cursor to end of line |
| `~` | Toggle case of char under cursor |
| `u` | Undo (repeat for further undo) |
| `U` | Undo all latest changes on one line |
| `Ctrl-r` | Redo |

---

## Cut / Copy / Paste (Yank)

| Command | Description |
|---|---|
| `y` | Yank (copy) |
| `yy` or `Y` | Yank current line |
| `x` | Cut (delete) char, also fills unnamed register |
| `p` | Paste after cursor / below line |
| `P` | Paste before cursor / above line |
| `yVj` | Copy 2 lines (`V` selects current line, each `j` adds the next line) |
| `yiw` | Yank inner word (word under cursor) |
| `viwp` | Select word under cursor and replace it with last yank |
| `viw"0p` | Select word under cursor and replace with contents of the **yank register `"0`** (survives deletes) |
| `s` | Substitute char (delete char, enter insert mode) |
| `S` | Substitute whole line |
| `r` | Replace a single character |
| `R` | Replace (overwrite) mode until `Esc` |

### Copying an HTML/XML Tag Block

| Command | Description |
|---|---|
| `vat` | Select the full tag block including `<tag>...</tag>` — cursor anywhere inside |
| `vit` | Select only the inner text of a tag block (excludes the tags) |

### Copying Non-Consecutive Lines Into a Register

```text
"aY   - yank current line into register a       (Y is synonym for yy)
"AY   - append current line to register a       (uppercase = append, not overwrite)
"ap   - paste the accumulated lines from register a
```

---

## Registers

Vim has **nine types of registers**:

1. The unnamed register `""` — always holds the most recent yank/delete
2. Numbered registers `"0`–`"9` — `"0` holds the last yank, `"1`–`"9` rotate through recent deletes
3. The small-delete register `"-` — holds deletes smaller than a line
4. Named registers `"a`–`"z` / `"A`–`"Z` — user-managed; uppercase **appends** instead of overwriting
5. Read-only registers `":`, `".`, `"%`, `"#` — last command, last inserted text, current filename, alternate filename
6. The expression register `"=` — evaluate an expression and insert the result
7. Selection/drop registers `"*`, `"+`, `"~` — `"*` is the system clipboard (Windows/macOS) or the X11 PRIMARY selection (Linux); `"+` is the X11 CLIPBOARD selection (Linux only — same as `"*` on Windows/macOS); `"~` holds the last drag-and-dropped text
8. The black-hole register `"_` — discard text without affecting other registers
9. Last search-pattern register `"/`

| Command | Description |
|---|---|
| `:reg` | View contents of all registers |
| `"fy` | Copy visual selection into register `f` |
| `"fp` | Paste from register `f` |
| `"_dd` | Delete a line without clobbering the unnamed register |

**Multiple clipboards example:**
```text
"fy - copy firstname to register f (after selecting in visual mode)
"ly - copy lastname  to register l
"fp - paste firstname from register f
"lp - paste lastname  from register l
```

---

## System Clipboard

| Command | Description |
|---|---|
| `"*` | Represents the system clipboard |
| `"*yy` | Copy current line to system clipboard |
| `"*p` | Paste from system clipboard |
| `v$"*y` | Visually select to end of line and copy to system clipboard |
| `v}"*y` | Visually select paragraph and copy to system clipboard |
| `vg_"*y` | Yank from cursor to the last non-blank char of the line (excludes trailing whitespace, unlike `v$`) to system clipboard |

> Requires Vim built `+clipboard` (gVim usually has this by default).

---

## Paste in Insert Mode

1. Enter insert mode (`i`, `a`, `A`, etc.)
2. Press `Ctrl-r` followed by a register name to insert its text inline:
   - `Ctrl-r "` — insert from the unnamed (last yank/delete) register
   - `Ctrl-r *` — insert from the system clipboard
   - `Ctrl-r <a-zA-Z>` — insert from any named register

> `"` is the register-selector prefix; after pressing `Ctrl-r`, Vim shows a `"` at the cursor and waits for you to name the register.

---

## Visual Mode & Text Objects

| Command | Description |
|---|---|
| `v` | Start character-wise visual selection |
| `V` | Start line-wise visual selection |
| `Ctrl-v` / `Ctrl-q` | Start block/column visual selection |
| `Alt + Mouse` (gVim) | Block/column selection via mouse drag |
| `gv` | Reselect the last visual selection |

### Text Objects

Text objects combine with operators (`d`, `c`, `y`, `v`) and a scope: `i` (inner, excludes delimiters) or `a` (a, includes delimiters/surrounding space).

| Object | Meaning |
|---|---|
| `iw` / `aw` | inner word / a word (includes trailing space) |
| `is` / `as` | inner sentence / a sentence (includes trailing space) |
| `ip` / `ap` | inner paragraph / a paragraph |
| `it` / `at` | inner tag / a tag (HTML/XML) |
| `i(` `i)` `ib` | inside `()` |
| `i{` `i}` `iB` | inside `{}` |
| `i[` `i]` | inside `[]` |
| `i"` `i'` `` i` `` | inside quotes |

Examples:
- `das` — delete current sentence including trailing space
- `vit` — select inner text of an HTML tag (e.g. cursor on `m` of `<font>my text</font>` selects `my text`)
- `vat` — select the full tag including `<font>...</font>`
- `ci"` — change text inside the nearest quotes
- `yi(` — yank text inside the nearest parentheses

### Block (Column) Visual Mode Example

```text
1. Ctrl-v          - enter block visual mode
2. j (x5)          - extend selection down 5 lines
3. $                - extend selection to end of line on each line
4. I                - enter Block-Insert mode
5. type * <Esc>     - prepend "*" to the first line
   → Vim then applies the insert to all selected lines
```
See `:help v_b_I` for details.

---

## Search

| Command | Description |
|---|---|
| `/pattern` | Search forward |
| `?pattern` | Search backward |
| `n` | Repeat search, same direction |
| `N` | Repeat search, opposite direction |
| `*` | Search forward for word under cursor |
| `#` | Search backward for word under cursor |
| `:noh` | Clear search highlighting |
| `:set hls` | Highlight all search matches |
| `:set incsearch` | Show matches while typing |
| `:set ignorecase smartcase` | Case-insensitive search, unless uppercase is used |

---

## Find & Replace

| Command | Description |
|---|---|
| `:%s/fff/rrrrr` | For every line, replace first occurrence of `fff` with `rrrrr` |
| `:%s/fff/rrrrr/g` | Replace **all** occurrences on every line |
| `:%s/fff/rrrrr/gc` | Replace all, with confirmation per match |
| `:%s/fff/rrrrr/gi` | Replace all, ignoring case |
| `:5,20s/fff/rrrrr/gc` | Replace only within line range 5–20 |
| `:'a,'bs/fff/rrr/gi` | Replace only between lines marked `a` and `b` |
| `:%s/ *$//` | Delete trailing whitespace on every line |
| `:%s/\(.*\):\(.*\)/\2:\1/` | Swap two `:`-delimited fields on every line |
| `:%s#<[^>]\+>##g` | Strip HTML tags, keep text content |
| `:%s/^\(.*\)\n\1$/\1/` | Remove consecutive duplicate lines |
| `:%s/,/\r/g` | Replace every comma with an end-of-line (splits into new lines) |
| `:%s/^/\=line(".") . ". "/` | Prefix every line with its line number |

### Use a Visual Selection as the Search Pattern (replace across whole file)

To replace every occurrence of some text in the file with something else, without typing the search text yourself:

1. Visually select the text you want to search for (`v`, `V`, or `Ctrl-v`).
2. Yank it: `y`
3. Type `:%s/`, then press `Ctrl-r` followed by `"` to paste the last yank in as the search pattern, then type `/replacement/g` and press Enter:
   ```
   :%s/                <- type this
   Ctrl-r  "           <- press these two keys to paste the yank
   /replacement/g      <- finish typing this, then Enter
   ```

**If the selected text has special regex characters** (`.`, `*`, `/`, `[`, `\`, etc.), paste it literally and safely using `\V` (very-nomagic) with `escape()` — this is real Vim command-line syntax, typed as shown:
```
:%s/\V<C-r>=escape(@", '/\')<CR>/replacement/g
```
- `\V` — turns off regex magic so the pasted text is matched almost literally
- `<C-r>=escape(@", '/\')<CR>` — evaluates an expression that escapes `/` and `\` in register `"` before inserting it (`<C-r>` and `<CR>` here are literal keys you press: Ctrl-r and Enter)

**Reusable mapping** — add to `.vimrc`/`_vimrc`:
```vim
vnoremap <leader>s y:%s/\V<C-r>=escape(@", '/\')<CR>//g<Left><Left>
```
Select text → `<leader>s` → cursor lands between the last two `/` → type the replacement → Enter.

### Find/Replace Within a Visual Selection

**By lines:**
```text
Select lines in visual mode, then press ':'
Vim auto-fills the range:
:'<,'>s/red/green/g
```
- `'<` / `'>` — bookmarks for the **start/end line** of the last visual selection
- `` `< `` / `` `> `` — bookmarks for the exact **start/end character**
- `gv` — reselect the last visual selection

**By exact characters (not whole lines):**
```text
:s/\%Vold/new/g
```
Uses the `%V` atom (escaped as `\%V`) to restrict matches to exactly the visually selected characters, rather than the whole line(s) touched by the selection.

### Whole-Word Match (avoid partial matches)

```text
Text:   This is his idea
:s/\<his\>/her/
Result: This is her idea
```
Without `\<` `\>`, the `his` inside `This` would also match.

### Multiple Alternatives via Regex

```text
Text:   Linux is good. Life is nice.
:%s/\(good\|nice\)/awesome/g
Result: Linux is awesome. Life is awesome.
```

### Escaping Special Characters (custom delimiter)

```text
Text:   c:/windows/system32/
:%s!/!\\!g
Result: c:\windows\system32\
```
Use `!` (or any character not in the pattern) instead of `/` as the separator when the search/replace text itself contains `/`.

---

## Find & Replace Across Multiple Files

### Across all open buffers

```text
:bufdo %s/pattern/replace/ge | update
:wa                                      " save all buffers afterward
```

To review each change before saving:
```text
:bufdo! %s/pattern/replace/ge
```

### Across a file set (current + sub-directories)

```text
:arg **/*.cpp          " all .cpp files in and below current directory
:argadd **/*.h         " also add all .h files
:arg                   " (optional) show current arglist
:argdo %s/pattern/replace/ge | update
```

### Replace the word under cursor, across all files in arglist

```text
:arg *.cpp
:argadd *.h
...                    " move cursor onto the word to replace
*                      " search for that exact word
:argdo %s//replace/ge | update
```

---

## Global Commands (`:g`)

`:g/pattern/command` applies an Ex command to every line matching `pattern`.

| Command | Description |
|---|---|
| `:g/temp/d` | Delete every line containing "temp" |
| `:g/^#/d` | Delete every line starting with `#` (`:g` defaults to the whole file — same as `:%g/^#/d` or `:1,$g/^#/d`) |
| `:g!/^#/d` | Delete every line **not** starting with `#` (inverse match) |
| `:5,10m0` | Move lines 5–10 to above line 1 |
| `:g/pattern/normal @a` | Run macro `a` on every matching line |

---

## Sorting & Reversing Lines

| Command | Description |
|---|---|
| `:'a,'b !sort` | Sort the block of lines between marks `a` and `b` |
| `:%!sort` | Sort the entire file |
| `:%!sort -u` | Sort and remove duplicate lines |
| `:'a,'b !tac` | Reverse line order between marks `a` and `b` (`tac` is GNU/Linux; on macOS/BSD use `tail -r` instead) |
| `:r !date` (some Windows gVim builds need `:r !!date`) | Insert the output of shell command `date` into the buffer |

---

## Macros & Repeats

| Command | Description |
|---|---|
| `.` | Repeat the last change |
| `Ctrl-n` / `Ctrl-p` | Autocomplete word (next/previous match) in insert mode |
| `qa` | Start recording macro into register `a` |
| `q` | Stop recording |
| `@a` | Replay macro `a` |
| `@@` | Replay the last-run macro |
| `10@a` | Replay macro `a` 10 times |

---

## Command-Line History

| Command | Description |
|---|---|
| `:` then `↑` / `↓` | Recall previous commands (editable before running) |
| `q:` | Open command-line history in a `[Command Line]` window; navigate with `j`/`k`, `Enter` on a line to run it |
| `Esc` or `Ctrl-c` (in `[Command Line]` window) | Close the window without running anything |
| `:his` | List command-line history |
| `:his /` | List search history |

---

## Buffers

| Command | Description |
|---|---|
| `:ls` or `:buffers` | List all open buffers |
| `:b 1` | Switch to buffer 1 |
| `:b <Tab>` | Autocomplete menu of all buffers |
| `:b car<Tab>` | Autocomplete buffers matching "car" (e.g. `car.c`, `car.h`) |
| `:b! 2` | Force-switch to buffer 2, hiding buffer 1 with its changes kept |
| `:bufdo bd` | Close all buffers (can skip some, since the buffer list shifts mid-iteration — `:%bd` is a more reliable one-shot alternative) |
| `:bd` | Close (delete) current buffer |
| `:set hidden` | Allow switching away from a modified buffer without saving it |
| `:set confirm` | Prompt to save/discard/cancel when abandoning unsaved changes |
| `:set autowrite` / `:set autowriteall` | Auto-save buffer changes before it's hidden |

---

## Tabs

| Command | Description |
|---|---|
| `vim -p file1.txt file2.txt` | Open multiple files, each in its own tab |
| `:tabnew` | Open a new empty tab |
| `:tabs` | List all tabs |
| `:tabfirst` | Go to the first tab page (navigation only) |
| `:tablast` | Go to the last tab page (navigation only) |
| `:tabmove 0` (or `:tabm 0`) | Move the *current* tab page to the first position (reorders tabs) |
| `:tabmove` (or `:tabm`, no argument) | Move the current tab page to the last position (reorders tabs) |
| `:tabn` or `gt` | Go to next tab page (wraps after the last) |
| `:tabp` or `gT` | Go to previous tab page |
| `{count}gt` (e.g. `1gt`) | Go to tab page number `{count}` |
| `:tabclose` | Close current tab |
| `:tabonly` | Close all tabs except current |

> `:tabmove`/`:tabm` *reorders* tabs; `:tabfirst`/`:tablast` just *navigate* — they aren't interchangeable, despite both landing you on "the first tab" in the simple case.
> `0gt` is **not** the same as `1gt`: a leading `0` is always its own "move to column 0" motion, never the start of a count, so `0gt` runs `0` then `gt` (next tab) as two separate commands — not "go to tab 1".

---

## Windows / Splits

| Command | Description |
|---|---|
| `:sp` | Split window horizontally |
| `:vsp` | Split window vertically |
| `Ctrl-w s` / `Ctrl-w v` | Split horizontally / vertically (normal mode) |
| `Ctrl-w w` | Cycle to next window |
| `Ctrl-w h/j/k/l` | Move to window in that direction |
| `Ctrl-w q` | Close current window |
| `Ctrl-w =` | Equalize window sizes |
| `Ctrl-w _` | Maximize height of current window |
| `Ctrl-w \|` | Maximize width of current window |

---

## File Explorer (netrw)

| Command | Description |
|---|---|
| `:Explore` (`:Ex`) | Browse current directory; press over a file to open it |
| `:Sexplore` (`:Sex`) | Browse by splitting a new horizontal window |
| `:Vexplore` (`:Vex`) | Browse in a vertical split |
| `:Vex d:\some\path` | Open a vertical split explorer rooted at the given path |

---

## Folding

| Command | Description |
|---|---|
| `zf{motion}` | Create a fold over the motion (e.g. `zfap` folds a paragraph) |
| `zo` / `zc` | Open / close fold under cursor |
| `za` | Toggle fold under cursor |
| `zR` | Open all folds |
| `zM` | Close all folds |
| `:set foldmethod=indent\|syntax\|manual\|marker\|expr\|diff` | Choose how folds are determined |

> `zf{motion}` only works when `'foldmethod'` is `manual` or `marker` — with `indent`, `syntax`, `expr`, or `diff`, folds are computed automatically and `zf` has no effect.

---

## Sessions

```text
1. With multiple files/tabs open, save the session:
   :mksession d:\vim_session

2. Reopen later:
   gVim74.exe -S D:\vim_session
   (or update the shortcut's target to add -S session_file)
```

---

## Encrypting a File

```text
:X                                " prompts to enter a password twice
:w d:/encrypted_file.txt          " saves the file encrypted
```
Close Vim completely, then reopen `d:/encrypted_file.txt` — Vim will prompt for the password to decrypt it.

> **Note:** Closing and reopening the file within the *same* Vim session will NOT re-prompt for the password.

---

## Shell Interaction

| Command | Description |
|---|---|
| `:sh` | Open a shell from within Vim |
| `exit` | Exit the shell, return to Vim |
| `:r !cmd` | Insert the output of a shell command into the buffer |
| `:%!cmd` | Filter the whole buffer through an external shell command |
| `!!cmd` | Filter current line through an external shell command |

---

## gVim Startup Settings (.vimrc / _vimrc)

On Windows, gVim 7.4: **Edit → Startup Settings** creates/opens `_vimrc`.
On Linux/macOS: create/edit `~/.vimrc`.

```vim
" turn on line numbering
set number

" highlight all search matches
set hlsearch
set incsearch

" wrap long lines (line break) at word boundaries
set linebreak

" enable syntax highlighting
syntax on

" font (gVim only)
set guifont=Lucida_Console:h9:cDEFAULT
```

Toggle line wrap dynamically:
```text
:set wrap
:set nowrap
```

### Suggested additions

```vim
set ignorecase smartcase   " smart case-insensitive search
set hidden                 " allow switching buffers without saving
set autowriteall           " auto-save when switching buffers
set clipboard=unnamed      " sync unnamed register with system clipboard (Linux: use unnamedplus for the Ctrl-C/Ctrl-V clipboard instead of the PRIMARY selection)
set expandtab tabstop=4 shiftwidth=4   " spaces instead of tabs
set autoindent smartindent
set showmatch               " briefly jump to matching bracket
```

---

## Changing the Default Font (gVim)

Reference: http://www.troubleshooters.com/linux/vifont.htm

1. gVim → **Edit → Startup Settings** (opens `_vimrc`)
2. In command mode: `:set guifont=*` — opens a font picker dialog
3. Choose a font/size (e.g. Lucida Console, size 12)
4. Confirm the resulting setting: `:set guifont?`
5. Copy the line it prints into `_vimrc` to make it permanent:
   ```vim
   set guifont=Lucida_Console:h12:cANSI
   ```

> Any space after `=` in a `set` command must be escaped with a backslash:
> ```vim
> set guifont=Monospace\ 12
> ```

---

## Changing the Color Scheme

1. Note the scheme name at **gVim → Edit → Color Scheme**
2. Add to `_vimrc` / `.vimrc`:
   ```vim
   colors slate
   ```

---

## Useful Tips

**Draw a horizontal rule of repeated characters (e.g. 100 dashes):**
```text
i-<Esc>x100p
```
- `i` — enter insert mode
- `-` — type the character to repeat
- `<Esc>` — return to normal mode
- `x` — delete that char (copies it into the unnamed register `"`)
- `100p` — paste it 100 times from the unnamed register

**Replace every comma in a line with an end-of-line (splits into new lines):**
```text
:%s/,/\r/g
```

---

## FAQ / Gotchas

**Q: Why doesn't a second `p` paste what I originally copied?**
A: `p` (paste) implicitly yanks any text it *replaces* into the unnamed register, so a subsequent `p` pastes that replaced text instead of your original copy.
**Fix:** use named registers for anything you need to paste more than once:
```text
"fy - copy firstname into register f
"ly - copy lastname  into register l
"fp - paste firstname from register f
"lp - paste lastname  from register l
```
Alternatively, use the numbered register `"0`, which always holds the last **yank** (not delete): `"0p`.

**Q: Where can I find standard editor shortcuts (Ctrl-c/Ctrl-v/etc.) in Vim?**
A: http://vim.wikia.com/wiki/Using_standard_editor_shortcuts_in_Vim

**Q: How do I see all my registers at once?**
A: `:reg`
