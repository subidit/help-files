- init.lua
- lazy.nvim
- colorsceme
- telescope
- treesitter

Using Lua files on startup
====
Mac or Linux `~/.config/nvim/init.lua`

Windows `~/AppData/Local/nvim/init.lua`

Nvim supports using `init.vim` or `init.lua` as the configuration file, but not both at the same time. Note that you can use Lua in `init.vim` and Vimscript in `init.lua`, which will be covered below.

To run an arbitrary Vim command from Lua, pass it as a string to `vim.cmd()`. If you want to build your Vim command programmatically, the following form can be useful 
```lua
vim.cmd.colorscheme("habamax")
vim.cmd.highlight({ "Error", "guibg=red" })
vim.cmd.highlight({ "link", "Warning", "Error" })
```

lazy.nvim is a modern plugin manager for Neovim.
[link](https://github.com/folke/lazy.nvim)

Catppuccin for (Neo)vim. [Link](https://github.com/catppuccin/nvim) 

telescope.nvim is a highly extendable fuzzy finder over lists. [link](https://github.com/nvim-telescope/telescope.nvim)

[treesitter](https://github.com/nvim-treesitter/nvim-treesitter/wiki/Installation)