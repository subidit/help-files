# dotfiles

- Dotfiles/
    - README.md (Main project readme)
    - Homebrew/
        - Brewfile (Homebrew packages and apps)
        - README.md (For explanations and guidance on Brewfile)
    - Zsh/
        - .zshrc (Zsh configuration)
        - README.md (For explanations and guidance on .zshrc)
    - Git/
        - .gitconfig (Git configuration)
        - .gitignore (Global gitignore)
        - README.md (For explanations and guidance on .gitconfig and .gitignore)
    - VSCode/
        - settings.json (VS Code settings)
        - keybindings.json (Custom keybindings)
        - README.md (For explanations and guidance on VS Code settings)
    - Docker/
        - .docker/config.json (Docker config)
        - README.md (For explanations and guidance on Docker config)
    - Nginx/
        - nginx.conf (Nginx web server config)
        - README.md (For explanations and guidance on nginx.conf)
    - Scripts/
        - custom-script.sh (Custom scripts)
        - README.md (For explanations and guidance on custom scripts)
    - web/
        - robots.txt
        - .htaccess
        - readme.md (for explanations and guidance on robots.txt and .htaccess)


.dotfiles
├── Brewfile
├── setup.sh
└── Zsh
    └── .zshrc


The ln command is a Unix command for creating links between files or directories³. A link is a reference to another file or directory. There are two types of links: hard links and soft links².

- A hard link is an additional name for an existing file. It points to the same memory location as the original file. You can create multiple hard links for a single file, but not for directories or files on different filesystems or partitions².
- A soft link, also known as a symbolic link or symlink, is a shortcut to another file or directory. It points to the name of the original file or directory, not the memory location. You can create soft links for files or directories on different filesystems or partitions².

The syntax for the ln command is:

`ln [option] target_file link_name`

To create a hard link, use the ln command without any option. To create a soft link, use the -s option². For example:

`ln -s source_file symbolic_link`

This will create a soft link named symbolic_link that points to source_file. The source_file is the real file and the symbolic_link is the symlinked file. You can verify this by using the ls -l command, which will show the file type flag (l for soft link) and the destination of the link².

Source:
(1) linux ln command - Unix Tutorial. https://www.unixtutorial.org/commands/ln.
(2) How to Use ln Command in Linux for Creating Soft & Hard Links. https://linuxhandbook.com/ln-command/.
(3) Ln Command in Linux (Create Symbolic Links) | Linuxize. https://linuxize.com/post/how-to-create-symbolic-links-in-linux-using-the-ln-command/.


```bash
#!/bin/bash
# This script creates symlinks for .zshrc and .config folder to /dotfiles/zsh and /dotfiles/config folder

# Check if the /dotfiles folder exists, if not create it
if [ ! -d "/dotfiles" ]; then
  mkdir /dotfiles
fi

# Check if the /dotfiles/zsh and /dotfiles/config folders exist, if not create them
if [ ! -d "/dotfiles/zsh" ]; then
  mkdir /dotfiles/zsh
fi

if [ ! -d "/dotfiles/config" ]; then
  mkdir /dotfiles/config
fi

# Move the .zshrc file and the .config folder to the /dotfiles folder
mv ~/.zshrc /dotfiles/zsh/.zshrc
mv ~/.config/* /dotfiles/config/

# Create symlinks for .zshrc and .config folder in the home directory
ln -s /dotfiles/zsh/.zshrc ~/.zshrc
ln -s /dotfiles/config/* ~/.config/
```
