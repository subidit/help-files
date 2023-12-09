# Zsh Guide

## Startup Files

Startup files in the `/etc` directory are put by the system administrator and are run for all users. 

Startup files in the `$HOME` or `~` directory is for each user. It is the usual location of `$ZDOTDIR`.

| Startup file    | Description                            |
| --------------- | -------------------------------------- |
| `/etc/zshenv`   | Always run for every zsh.              |
| `~/.zshenv`     | Usually run for every zsh (see below). |
| `/etc/zprofile` | Run for login shells.                  |
| `~/.zprofile`   | Run for login shells.                  |
| `/etc/zshrc`    | Run for interactive shells.            |
| `~/.zshrc`      | Run for interactive shells.            |
| `/etc/zlogin`   | Run for login shells.                  |
| `~/.zlogin`     | Run for login shells.                  |

So, order of running is **`.zprofile > .zshrc > .zlogin`**
The file `/etc/zshenv` is always run at the start of any zsh.
First Law of Zsh Administration: put as little as possible in the file /etc/zshenv, as every single zsh which starts up has to read it. 

## Keypress shortcuts

| Key combination | Effect                                             |
| --------------- | -------------------------------------------------- |
| Control-A       | jump to start of line                              |
| Control-E       | jump to end of line                                |
| Meta-B          | move back one word                                 |
| Meta-F          | move forward one word                              |
| Control-D       | delete character forwards/list completions/log out |
| Control-K       | delete to end of line                              |
| Control-U       | delete whole line                                  |
| Meta-Backspace  | delete one word to the left                        |
| Meta-D          | delete one word to the right                       |
| Control-T       | transpose two characters                           |
| Meta-T          | transpose two words                                |

## Types of shell

1. **Interactive shell**: When you are typing at a prompt and waiting for each command to run. eg. `ls`
2. **Non-interactive shell**: When the shell is reading commands from a file. eg. `zsh filename`
3. **Login shell**: When you first log into the computer, the shell you are presented with is interactive, but it is also a login shell.

## Expectations

* Prompt
  * Date and time
  * Visual effects
  * Colour
  * Conditional Substrings in Prompts
* Expansion
  1. History Expansion
  2. Alias Expansion
  3. Process Substitution
  4. Parameter Expansion
  5. Command Substitution
  6. Arithmetic Expansion
  7. Brace Expansion
* Highlighting / Colour coding output
* File navigation - intiutive, easy


## Shell Commands

1. `echo`
2. `pwd`
3. `source <file>`
4. `sleep 3`
5. `which`


## Notes

- The shell tries to guess whether to use emacs or vi from the environment variables `$VISUAL` or `$EDITOR`, in that order.
- Simple `.zshrc` for history
```zsh
HISTSIZE=1000
SAVEHIST=1000
HISTFILE=~/.history
```
- History options
  - `INC_APPEND_HISTORY`, `SHARE_HISTORY`, `HIST_EXPIRE_DUPS_FIRST`, `HIST_IGNORE_ALL_DUPS`, `HIST_SAVE_NO_DUPS` and `HIST_NO_FUNCTIONS`
- The main prompt is in a parameter called either `$PS1` or `$PROMPT` or `$prompt`.
  - There is also `$RPS1`, which prints a prompt at the right of the screen.
  - `$PS2` is shown when the shell is waiting for some more input.
  - `$PS3` is shown within a loop started by the shell's *select* mechanism, when the shell wants you to input a choice: see the *zshmisc* manual page.
  - `$PS4` is useful in debugging.
- `NO_BEEP`, `AUTO_CD`
- `alias foo='print I said foo'`
- The `|` (pipe) connects the output of the first command to the input of the next

```zsh
% pwd               # show the current directory
  ~
% zsh               # start a new shell, which 
                    # is a separate process
% cd tmp
% pwd               # now I'm in a different
                    # directory...
  ~/tmp
% exit              # leave the new shell...
% pwd               # now I'm back where I was...
  ~
```

### Symbolic links

```sh
ln -s existing-file-name name-of-link
#for example
ln -s /usr/bin/ln ln
```


## Reference

1. [A User's Guide to the Z-Shell](https://zsh.sourceforge.io/Guide/zshguide.html)
2. Zsh homepage - [zsh.org](https://www.zsh.org/)


<!-- (-no space->)
# Plugins
* zsh-autosuggestions
* zsh-completions
* fast-syntax-highlighting

## CLI Commands and utilities

* 2048-cli - A command-line version of the popular 2048 puzzle game.
* aafire - Displays a fire animation using ASCII art.
* aafire - Generates an ASCII art fire animation.
* asciiart - A tool to convert images into ASCII art.
* asciinema - Record and share terminal sessions as animated text.
* asciiquarium - Turns your terminal into a colorful, animated aquarium with ASCII fish and bubbles.
* awk - Text processing tool for data extraction.
* bastet - A Tetris clone that intentionally gives you the worst possible pieces to challenge your skills.
* battleship - Play the classic game of Battleship in the terminal.
* bb - A simple ASCII art demo that displays animated ASCII art.
* bbcolors - A fun utility that displays color codes and color charts in your terminal.
* bbpager - A "bouncing ball" pager that bounces a ball around your terminal as you scroll.
* boxes - Draw shapes and boxes around text in your terminal.
* boxes - Draws shapes and boxes around text in your terminal, adding a creative touch.
* cacademo - Showcases various ASCII art animations and effects.
* cat - Concatenate and display the content of files.
* cd - Change the current directory.
* cmatrix - Simulate the "Matrix" digital rain.
* cmatrix - Simulates the "Matrix" digital rain effect for a visually engaging experience.
* cmatrix - Simulates the "Matrix" digital rain, similar to the movie's iconic falling code.
* codenames - A word game where you generate codenames for fun and interactive word association.
* cowsay - Generate ASCII art with an animal saying a message.
* cowsay - Make an ASCII cow or other animals say anything you want.
* curl - Transfer data from or to a server.
* dopewars - A text-based drug dealing game where you aim to make a profit.
* espeak - A text-to-speech synthesizer for the terminal.
* figlet - Create large text banners.
* figlet - Creates large text banners in various styles, perfect for fun messages or ASCII art.
* figlet - Generate large text banners in various fonts.
* figlet-fonts - An extensive collection of fonts for the "figlet" utility, allowing for creative text art.
* find - Search for files and directories.
* fortune - Display random, humorous quotes.
* fortune-mod - Provides a wide collection of witty and humorous sayings, quotes, and phrases.
* git - Version control system for tracking changes in files.
* greed - A puzzle game where you select numbers to maximize your score.
* grep - Search for text within files.
* hangman - A simple hangman game for word-guessing fun.
* htop - Interactive system process viewer.
* httrack - Download entire websites for offline viewing.
* lolcat - Adds rainbow colors to your terminal output, making it visually entertaining.
* lolcat - Colorize text in rainbow colors, making your terminal more vibrant.
* ls - List files and directories in a folder.
* mkdir - Create a new directory.
* motd - A utility to display the "Message of the Day" or welcome message when you log in.
* nano or vim - Text editors for the terminal.
* ncdu - Disk usage analyzer with an interactive interface.
* nethack - A classic and highly detailed terminal-based dungeon-crawling adventure game.
* ninvaders - A space invaders game for your terminal.
* nSnake - A classic Snake game that you can play in the terminal.
* nudoku - A console-based Sudoku game.
* nyancat - Displays a colorful, animated Nyan Cat as it flies across your terminal.
* nyancat - Displays an animated Nyan Cat, complete with the catchy Nyan Nyan Nyan song.
* oneko - Displays a cat that follows your mouse cursor around the terminal.
* pianobar - A command-line Pandora radio player that lets you listen to music from your terminal.
* ponysay - Like cowsay, but with ponies and other characters delivering your messages.
* pwd - Print the current working directory.
* rasterbator - Enlarge images to multiple pages for creating wall posters.
* remind - A sophisticated calendar and alarm utility that can be used for reminders and to-do lists.
* rev - Reverse the characters in each line of text.
* rm - Remove files or directories.
* rsync - Synchronize files and directories between systems.
* sed - Stream editor for text manipulation.
* sl - A mistyped "ls" command that displays a fun train animation as punishment for your typo.
* sl - Mistyped "ls" command, a fun train animation.
* sl - Shows a whimsical steam locomotive when you mistype "ls."
* slurm - A network load monitor that displays a moving train animation based on network activity.
* speedtest-cli - Check your internet speed from the terminal.
* ssh - Securely connect to remote servers.
* teapot - Display a 3D ASCII art teapot and spin it around.
* tetris-bsd - Another version of Tetris for terminal gaming.
* tldr - Simplified and community-driven man pages.
* toilet - Create large text banners with various fonts and styles.
* top - Monitor system processes and resource usage.
* touch - Create an empty file.
* tree - Display directory structures in a tree-like format.
* tty-solitaire - Play the classic Solitaire card game in your terminal.
* wget - Download files from the web.
* wordgrinder - A simple and distraction-free word processor for the terminal.
* xcowsay - Similar to cowsay but with a graphical cow speaking your message.
* xeyes - Pairs of eyes that follow your mouse cursor on the screen.
* xkcdpass - Generates secure and humorous passwords inspired by XKCD comics.
* youtube-dl - Download videos from YouTube and other sites.






# Terminal Commands

`alias` - Create command shortcuts.
`alias` - Create command shortcuts.
`apropos` - Search the manual page names and descriptions.
`apropos` - Search the manual page names and descriptions.
`autoload` - Load Zsh functions from files.
`awk` - Text processing tool for data extraction.
`banner` - Display large text banners.
`basename` - Strip directory and suffix from filenames.
`bash` - GNU Bourne-Again SHell.
`bc` - Arbitrary precision calculator language.
`bc` - Arbitrary precision calculator.
`bcftools` - Manipulate VCF/BCF files.
`bindkey` - Configure key bindings.
`cal` - Display a calendar.
`cat` - Concatenate and display file content.
`cc` - C compiler.
`cd` - Change the current directory.
`cd` - Change the current directory.
`chmod` - Change file permissions.
`chown` - Change file ownership.
`chsh` - Change the user's login shell.
`chsh` - Change the user's login shell.
`clear` - Clear the terminal screen.
`clear` - Clear the terminal screen.
`clear` - Clear the terminal screen.
`cmp` - Compare two files byte by byte.
`colors` - Configure terminal colors.
`comm` - Compare two sorted files line by line.
`command_not_found_handler` - Customize command not found behavior.
`compinit` - Initialize Zsh completion system.
`complete` - Define custom completions.
`cowsay` - Generate ASCII art with an animal saying a message.
`cp` - Copy files and directories.
`curl` - Transfer data from or to a server.
`curl` - Transfer data with URLs.
`cut` - Remove sections from each line of files.
`date` - Display or set the system date and time.
`date` - Display or set the system date and time.
`dd` - Convert and copy a file.
`df` - Display disk space usage.
`df` - Display disk space usage.
`diff` - Compare files line by line.
`diff` - Compare files line by line.
`dirs` - Manage directory stack.
`du` - Estimate file and directory space usage.
`du` - Estimate file and directory space usage.
`echo` - Display text on the terminal.
`echo` - Display text on the terminal.
`echo` - Display text on the terminal.
`egrep` - Search text files using extended regular expressions.
`env` - Display environment variables.
`env` - Display, set, or remove environment variables.
`exit` - Exit the shell or terminal.
`export` - Set environment variables.
`expr` - Evaluate expressions.
`factor` - Print prime factors.
`fc` - Edit and re-execute commands from history.
`file` - Determine file type.
`find` - Search for files and directories.
`finger` - User information lookup program.
`fmt` - Reformat paragraph text.
`fold` - Wrap text to fit a specified width.
`free` - Display system memory usage.
`fsck` - File system consistency check and interactive repair.
`ftp` - File Transfer Protocol.
`functions` - Define custom Zsh functions.
`git` - Set up Git aliases and configuration.
`grep` - Search for text within files.
`head` - Display the beginning of a file.
`history` - Customize command history settings.
`hostname` - Display or set the system's hostname.
`if` - Define conditional statements.
`kill` - Terminate processes.
`kill` - Terminate processes.
`less` - View text files with pagination.
`less` - View text files with pagination.
`ln` - Create links between files.
`ln` - Create links between files.
`local` - Define local variables.
`locate` - Find files by name.
`login` - Begin session on the system.
`lp` - Print files.
`ls` - Configure `ls` command behavior.
`ls` - List files and directories.
`mail` - Process mail messages.
`man` - Display manual pages.
`mkdir` - Create directories with specific permissions.
`mkdir` - Create directories.
`mktemp` - Create temporary files and directories.
`mv` - Alias for moving files and directories.
`mv` - Move or rename files and directories.
`mv` - Move or rename files and directories.
`nice` - Modify the priority of a command.
`nohup` - Run a command immune to hangups.
`open` - Open files and directories with default applications.
`passwd` - Change user password.
`passwd` - Change user password.
`paste` - Merge lines of files.
`path` - Modify the `PATH` environment variable.
`plugins` - Load and configure Zsh plugins.
`printenv` - Display environment variables.
`printf` - Format and print data.
`prompt` - Customize the Zsh prompt.
`ps` - Display information about running processes.
`ps` - Report a snapshot of the current processes.
`pushd` - Navigate the directory stack.
`pwd` - Customize the display of the current working directory.
`pwd` - Print the current working directory.
`rm` - Remove files and directories.
`rmdir` - Alias for removing empty directories.
`rmdir` - Remove empty directories.
`rsync` - Remote file copy and synchronization.
`sed` - Stream editor for text manipulation.
`seq` - Print sequences of numbers.
`setopt` - Configure Zsh options.
`sha1sum` - Compute and check SHA-1 message digest.
`sha256sum` - Compute and check SHA-256 message digest.
`sleep` - Delay for a specified amount of time.
`sort` - Sort lines of text files.
`source` - Execute a script or load configuration files.
`sync` - Synchronize data on disk with memory.
`tac` - Concatenate and print files in reverse.
`tail` - Display the end of a file.
`tmux` - Set up and configure Tmux.
`touch` - Create empty files or update file timestamps.
`touch` - Create empty files with specified attributes.
`tr` - Translate or delete characters.
`ulimit` - Set process resource limits.
`unalias` - Remove command aliases.
`uname` - Display system information.
`unset` - Remove environment variables.
`vared` - Edit variables interactively.
`wait` - Wait for background jobs to complete.
`wc` - Word, line, character, and byte count.
`whence` - Find the location of a command.
`which` - Display the full path of an executable.
`which` - Display the path of an executable.
`who` - Display information about logged-in users.
`xargs` - Build and execute command lines from input.
`yes` - Repeatedly output a line with a specified string.
`zargs` - Process input with custom functions.
`zcat` - Decompress and display compressed files.
`zcompile` - Compile Zsh scripts for faster execution.
`zle-keymap-select` - Define keymap-specific behavior.
`zle-line-init` - Customize the ZLE initialization.
`zle` - Customize Zsh line editor (ZLE) behavior.
`zmv` - Perform batch file renaming.
`zplug` - Configure and load Zsh plugins.
`zstyle` - Customize completion and formatting styles.
`zstyle` - Define styles for Zsh completion system.



## File Management

| Name  | Description                                         |
| ----- | --------------------------------------------------- |
| cat   | Concatenate and display the content of files.       |
| mkdir | Create a new directory.                             |
| rm    | Remove files or directories.                        |
| touch | Create an empty file.                               |
| tree  | Display directory structures in a tree-like format. |

## Text Processing

| Name | Description                                  |
| ---- | -------------------------------------------- |
| awk  | Text processing tool for data extraction.    |
| grep | Search for text within files.                |
| sed  | Stream editor for text manipulation.         |
| rev  | Reverse the characters in each line of text. |
| find | Search for files and directories.            |

## System Monitoring and Management

| Name | Description                                                                       |
| ---- | --------------------------------------------------------------------------------- |
| htop | Interactive system process viewer.                                                |
| top  | Monitor system processes and resource usage.                                      |
| pwd  | Print the current working directory.                                              |
| ncdu | Disk usage analyzer with an interactive interface.                                |
| motd | A utility to display the "Message of the Day" or welcome message when you log in. |

## Networking and Communication

| Name          | Description                                        |
| ------------- | -------------------------------------------------- |
| curl          | Transfer data from or to a server.                 |
| ssh           | Securely connect to remote servers.                |
| rsync         | Synchronize files and directories between systems. |
| wget          | Download files from the web.                       |
| speedtest-cli | Check your internet speed from the terminal.       |

## Text Editing and Manipulation

| Name        | Description                                                                                |
| ----------- | ------------------------------------------------------------------------------------------ |
| nano or vim | Text editors for the terminal.                                                             |
| fortune     | Display random, humorous quotes.                                                           |
| git         | Version control system for tracking changes in files.                                      |
| wordgrinder | A simple and distraction-free word processor for the terminal.                             |
| remind      | A sophisticated calendar and alarm utility that can be used for reminders and to-do lists. |

## Data Transfer and Synchronization

| Name  | Description                                        |
| ----- | -------------------------------------------------- |
| rsync | Synchronize files and directories between systems. |
| wget  | Download files from the web.                       |
| scp   | Securely copy files between systems.               |
| sftp  | Securely transfer files over SSH.                  |
| ncftp | FTP client with support for multiple connections.  |

## File and Directory Search

| Name     | Description                                              |
| -------- | -------------------------------------------------------- |
| find     | Search for files and directories.                        |
| locate   | Quickly find files and directories by name.              |
| whereis  | Locate binary and source code files.                     |
| updatedb | Update the database used by the locate command.          |
| fd       | A simple, fast, and user-friendly alternative to 'find'. |

## Terminal Customization and Visualization

| Name    | Description                                                                   |
| ------- | ----------------------------------------------------------------------------- |
| lolcat  | Adds rainbow colors to your terminal output, making it visually entertaining. |
| cmatrix | Simulate the "Matrix" digital rain.                                           |
| xcowsay | Similar to cowsay but with a graphical cow speaking your message.             |
| cowsay  | Make an ASCII cow or other animals say anything you want.                     |
| boxes   | Draw shapes and boxes around text in your terminal.                           |

## Web Browsing and Downloading

| Name  | Description                                      |
| ----- | ------------------------------------------------ |
| curl  | Transfer data from or to a server.               |
| wget  | Download files from the web.                     |
| links | A text-based web browser.                        |
| w3m   | A terminal-based web browser with image support. |
| lynx  | A highly configurable text-based web browser.    |

## Audio and Multimedia

| Name       | Description                                                     |
| ---------- | --------------------------------------------------------------- |
| cmus       | A powerful music player with a simple and efficient interface.  |
| mpv        | A multimedia player based on MPlayer and mplayer2.              |
| nvlc       | A terminal-based media player based on libVLC.                  |
| youtube-dl | Download videos from YouTube and other sites.                   |
| mocp       | Music on Console (MoC) - A simple and easy-to-use music player. |

## Calendar and Reminders

| Name         | Description                                                                                |
| ------------ | ------------------------------------------------------------------------------------------ |
| remind       | A sophisticated calendar and alarm utility that can be used for reminders and to-do lists. |
| khal         | A powerful and extensible command-line calendar program.                                   |
| calcurse     | A text-based calendar and scheduling application.                                          |
| todo.txt-cli | A simple and todo.txt-based task manager for the command line.                             |
| hcalendar    | A simple command-line tool for viewing and managing hCalendar events.                      |

## Version Control and Development

| Name      | Description                                             |
| --------- | ------------------------------------------------------- |
| git       | Version control system for tracking changes in files.   |
| svn       | A version control system designed to be a better CVS.   |
| mercurial | A distributed version control system.                   |
| fossil    | A distributed software configuration management system. |
| bzr       | A distributed version control system.                   |

## Text-to-Speech and Speech Synthesis

| Name      | Description                                          |
| --------- | ---------------------------------------------------- |
| espeak    | A text-to-speech synthesizer for the terminal.       |
| festival  | A general multi-lingual speech synthesis system.     |
| pico2wave | Text-to-speech conversion using the Pico TTS engine. |
| speak     | A simple utility for text-to-speech conversion.      |
| flite     | A small, fast, run-time synthesis                    |


## Games and Entertainment

| Name          | Description                                                                                     |
| ------------- | ----------------------------------------------------------------------------------------------- |
| 2048-cli      | A command-line version of the popular 2048 puzzle game.                                         |
| bastet        | A Tetris clone that intentionally gives you the worst possible pieces to challenge your skills. |
| battleship    | Play the classic game of Battleship in the terminal.                                            |
| ninvaders     | A space invaders game for your terminal.                                                        |
| nSnake        | A classic Snake game that you can play in the terminal.                                         |
| nudoku        | A console-based Sudoku game.                                                                    |
| tty-solitaire | Play the classic Solitaire card game in your terminal.                                          |
| tetris-bsd    | Another version of Tetris for terminal gaming.                                                  |
| slurm         | A network load monitor that displays a moving train animation based on network activity.        |

## Text Art and Animation

| Name         | Description                                                                                |
| ------------ | ------------------------------------------------------------------------------------------ |
| aafire       | Displays a fire animation using ASCII art.                                                 |
| asciiart     | A tool to convert images into ASCII art.                                                   |
| asciiquarium | Turns your terminal into a colorful, animated aquarium with ASCII fish and bubbles.        |
| bb           | A simple ASCII art demo that displays animated ASCII art.                                  |
| cmatrix      | Simulate the "Matrix" digital rain.                                                        |
| cacademo     | Showcases various ASCII art animations and effects.                                        |
| figlet       | Create large text banners.                                                                 |
| figlet-fonts | An extensive collection of fonts for the "figlet" utility, allowing for creative text art. |
| nyancat      | Displays a colorful, animated Nyan Cat as it flies across your terminal.                   |
| oneko        | Displays a cat that follows your mouse cursor around the terminal.                         |
| toilet       | Create large text banners with various fonts and styles.                                   |
| xeyes        | Pairs of eyes that follow your mouse cursor on the screen.                                 |
| xcowsay      | Similar to cowsay but with a graphical cow speaking your message.                          |


## Text Processing and Manipulation

| Utility | Description                                           |
| ------- | ----------------------------------------------------- |
| grep    | Search and match text using regular expressions.      |
| sed     | Text processing tool for substitution, deletion, etc. |
| cut     | Extract specific fields or columns from text.         |
| sort    | Sort lines of text files or input streams.            |
| tr      | Translate, delete, or squeeze characters in text.     |
| jq      | JSON processor for querying and manipulating JSON.    |

## Data Transfer and Networking

| Utility | Description                                            |
| ------- | ------------------------------------------------------ |
| curl    | Transfer data with URLs, supporting various protocols. |
| nc      | A simple utility for reading/writing network data.     |
| wget    | Retrieve files from the web via HTTP, HTTPS, and FTP.  |

## Terminal Multiplexing and Monitoring

| Utility | Description                                                      |
| ------- | ---------------------------------------------------------------- |
| tmux    | Terminal multiplexer for managing multiple sessions.             |
| screen  | Full-screen window manager that multiplexes a physical terminal. |
| htop    | Interactive process viewer for monitoring system resources.      |

## File and Disk Management

| Utility  | Description                                                   |
| -------- | ------------------------------------------------------------- |
| ncdu     | Disk usage analyzer with a text-based interface.              |
| df       | Display disk space usage of file systems.                     |
| du       | Estimate file and directory space usage.                      |
| find     | Search and locate files and directories within a file system. |
| dupeguru | A GUI utility to find duplicate files in your system.         |

## Parallel Processing and Batch Jobs

| Utility  | Description                                            |
| -------- | ------------------------------------------------------ |
| parallel | Execute multiple jobs or commands in parallel.         |
| xargs    | Build and execute command lines from standard input.   |
| jobber   | A task manager and job scheduler for batch processing. |


