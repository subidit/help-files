# Vim 101

## The Basics Of Moving In Vim

| Key  | Description                                    |
| ---- | ---------------------------------------------- |
| `h`  | moves the cursor one character to the left.    |
| `j`  | moves the cursor down one line.                |
| `k`  | moves the cursor up one line.                  |
| `l`  | moves the cursor one character to the right.   |
| `0`  | moves the cursor to the beginning of the line. |
| `$`  | moves the cursor to the end of the line.       |
| `w`  | move forward one word.                         |
| `b`  | move backward one word.                        |
| `G`  | move to the end of the file.                   |
| `gg` | move to the beginning of the file.             |
| \`.  | move to the last edit.                         |

## Editing Vim Style

| Key      | Description                               |
| -------- | ----------------------------------------- |
| `d`      | starts the delete operation.              |
| `dw`     | will delete a word.                       |
| `d0`     | will delete to the beginning of a line.   |
| `d$`     | will delete to the end of a line.         |
| `dgg`    | will delete to the beginning of the file. |
| `dG`     | will delete to the end of the file.       |
| `u`      | will undo the last operation.             |
| `Ctrl-r` | will redo the last undo.                  |

## Searching And Replacing

| Key                            | Description                                                                                                             |
| ------------------------------ | ----------------------------------------------------------------------------------------------------------------------- |
| `/text`                        | search for text in the document, going forward.                                                                         |
| `n`                            | move the cursor to the next instance of the text from the last search. This will wrap to the beginning of the document. |
| `N`                            | move the cursor to the previous instance of the text from the last search.                                              |
| `?text`                        | search for text in the document, going backwards.                                                                       |
| `:%s/text/replacement text/g`  | search through the entire document for text and replace it with replacement text.                                       |
| `:%s/text/replacement text/gc` | search through the entire document and confirm before replacing text.                                                   |

## Copying And Pasting

| Keys     | Description                        |
| -------- | ---------------------------------- |
| `v`      | highlight one character at a time. |
| `V`      | highlight one line at a time.      |
| `Ctrl-v` | highlight by columns.              |
| `p`      | paste text after the current line. |
| `P`      | paste text on the current line.    |
| `y`      | yank text into the copy buffer.    |


# Vim School

## NAVIGATION

| Key | Description                                       |
| --- | ------------------------------------------------- |
| h   | Left key                                          |
| j   | Down key                                          |
| k   | Up key                                            |
| l   | Right key                                         |
|     |                                                   |
| zt  | Move the screen to the top of the window          |
| zz  | Move the screen to the middle of the window       |
| zb  | Move the screen to the bottom of the window       |
|     |                                                   |
| H   | Move the cursor to the highest line on the screen |
| M   | Move the cursor to the middle line on the screen  |
| L   | Move the cursor to the lowest line on the screen  |
|     |                                                   |
| gg  | Move the cursor to the begin of file              |
| G   | Move the cursor to the end of file                |
|     |                                                   |
| ``  | Return to the previous place                      |
| “   | Return to previous line                           |
|     |                                                   |
| ^   | Move to first char in begin line                  |
| 0   | Move to begin line                                |
| $   | Move to end line                                  |
|     |                                                   |
| w   | Move to begin with next word                      |
| e   | Move to end of current word                       |
| b   | Move to begin with the previous word              |
| ge  | Move to end of the previous word                  |
|     |                                                   |
| fc  | Jump to next char found                           |
| Fc  | Jump to previous char found                       |
| tc  | Jump to next char found(go to previous char)      |
| Tc  | Jump to previous found (go to next char)          |
|     |                                                   |
| ;   | Jump to next char found                           |
| ,   | Jump to previous char found                       |
|     |                                                   |
| *   | Jump to next word found                           |
| #   | Jump to the previous word found                   |


## EDITING

 | Key     | Description                       |
 | ------- | --------------------------------- |
 | y space | Yank char under the cursor        |
 | yy      | Yank the line under the cursor    |
 | 2yy     | Yank the 2 lines under the cursor |
 | yw      | Yank word                         |
 | y$      | Yank to end of line               |
 |         |                                   |
 | p       | Paste after the cursor            |
 | P       | Paste before the cursor           |
 |         |                                   |
 | dd      | Delete the line under the cursor  |
 | dw      | Delete the word                   |
 | x       | Delete current char               |
 | X       | Delete previous char              |
 | xp      | Transpose to letters              |
 | D       | Delete to end of line             |
 |         |                                   |
 | s       | Delete char under the cursor      |
 | S       | Delete line under the cursor      |


## Links

- [VimAwesome](https://vimawesome.com/) - 19,462 Plugins
- [Vim Adventures](https://vim-adventures.com/) - Learning Game


# Vim Tutor

## Lesson 1

- Lesson 1.1: MOVING THE CURSOR
- Lesson 1.2: EXITING NEOVIM
- Lesson 1.3: TEXT EDITING - DELETION
- Lesson 1.4: TEXT EDITING: INSERTION
- Lesson 1.5: TEXT EDITING: APPENDING
- Lesson 1.6: EDITING A FILE

### Lesson 1 SUMMARY

 1. The cursor is moved using either the arrow keys or the hjkl keys.
     h (left)   j (down)       k (up)       l (right)

 2. To start Neovim from the shell prompt type:
~~~ sh
    $ nvim FILENAME
~~~
 3. To exit Neovim type: `<Esc>`{normal} `:q!`{vim} `<Enter>`{normal} to trash all changes.
                OR type: `<Esc>`{normal} `:wq`{vim} `<Enter>`{normal} to save the changes.

 4. To delete the character at the cursor type: `x`{normal}

 5. To insert or append text type:
    `i`{normal} insert text `<Esc>`{normal}     insert before the cursor.
    `A`{normal} append text `<Esc>`{normal}     append after the line.

NOTE: Pressing `<Esc>`{normal} will place you in Normal mode or will cancel
      an unwanted and partially completed command.


## Lesson 2

- Lesson 2.1: DELETION COMMANDS
- Lesson 2.2: MORE DELETION COMMANDS
- Lesson 2.3: ON OPERATORS AND MOTIONS
- Lesson 2.4: USING A COUNT FOR A MOTION
- Lesson 2.5: USING A COUNT TO DELETE MORE
- Lesson 2.6: OPERATING ON LINES
- Lesson 2.7: THE UNDO COMMAND

### lesson 2 SUMMARY

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


## Lesson 3

- Lesson 3.1: THE PUT COMMAND
- Lesson 3.2: THE REPLACE COMMAND
- Lesson 3.3: THE CHANGE OPERATOR
- Lesson 3.4: MORE CHANGES USING `c`{normal}

### Lesson 3 SUMMARY

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

Now go on to the next lesson.


## Lesson 4

- Lesson 4.1: CURSOR LOCATION AND FILE STATUS
- Lesson 4.2: THE SEARCH COMMAND
- Lesson 4.3: MATCHING PARENTHESES SEARCH
- Lesson 4.4: THE SUBSTITUTE COMMAND


### Lesson 4 SUMMARY

 1. `<C-g>`{normal}     displays your location and the file status.
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
~~~ cmd
        :s/old/new
~~~
    To substitute new for all 'old's on a line type
~~~ cmd
        :s/old/new/g
~~~
    To substitute phrases between two line #'s type
~~~ cmd
        :#,#s/old/new/g
~~~
    To substitute all occurrences in the file type
~~~ cmd
        :%s/old/new/g
~~~
    To ask for confirmation each time add 'c'
~~~ cmd
        :%s/old/new/gc
~~~


## Lesson 5

- Lesson 5.1: HOW TO EXECUTE AN EXTERNAL COMMAND
- Lesson 5.2: MORE ON WRITING FILES
- Lesson 5.3: SELECTING TEXT TO WRITE
- Lesson 5.4: RETRIEVING AND MERGING FILES

### Lesson 5 SUMMARY

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


## Lesson 6

- Lesson 6.1: THE OPEN COMMAND
- Lesson 6.2: THE APPEND COMMAND
- Lesson 6.3: ANOTHER WAY TO REPLACE
- Lesson 6.4: COPY AND PASTE TEXT
- Lesson 6.5: SET OPTION

### Lesson 6 SUMMARY

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
~~~ cmd
        :set noic
~~~
 8. Prepend "inv" to invert an option:
~~~ cmd
        :set invic
~~~


## Lesson 7

- Lesson 7.1: GETTING HELP
- Lesson 7.2: CREATE A STARTUP SCRIPT
- Lesson 7.3: COMPLETION

### Lesson 7 SUMMARY

 1. Type `:help`{vim}
    or press `<F1>`{normal} or `<Help>`{normal} to open a help window.

 2. Type `:help TOPIC`{vim} to find help on TOPIC.

 3. Type `<C-w><C-w>`{normal} to jump to another window

 4. Type `:q`{vim} to close the help window

 5. Create an init.vim startup script to keep your preferred settings.

 6. While in command mode, press `<C-d>`{normal} to see possible completions.
    Press `<Tab>`{normal} to use one completion.

