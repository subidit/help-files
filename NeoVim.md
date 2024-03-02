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

# Contents <!-- omit in toc -->
- [Neo-vim configuration](#neo-vim-configuration)
  - [Installing neovim](#installing-neovim)
  - [init.lua](#initlua)
  - [NVIM\_APPNAME](#nvim_appname)
- [Package Manager](#package-manager)
  - [lazy.nvim](#lazynvim)
  - [Colorscheme](#colorscheme)
  - [Telescope](#telescope)
  - [Treesitter](#treesitter)
  - [Neo Tree](#neo-tree)
- [Structuring Your Plugins](#structuring-your-plugins)
    - [File Structure](#file-structure)
  - [Lualine](#lualine)
- [LSP](#lsp)
  - [Mason](#mason)
  - [telescope-ui-select.nvim](#telescope-ui-selectnvim)
- [Linters \& Formatters](#linters--formatters)
  - [alpha-nvim](#alpha-nvim)
- [Autocompletion \& Snippets](#autocompletion--snippets)
- [Debuggers](#debuggers)
- [Packages](#packages)
- [Commands](#commands)


# Neo-vim configuration
Neo-vim configuration from scratch. 

## Installing neovim
```sh
# MacOS
brew install neovim

# Windows
winget install Neovim.Neovim
```

## init.lua
Nvim supports using `init.vim` or `init.lua` as the configuration file, but not both at the same time.
The `runtimepath` of nvim expects this file to be in `~/.config/nvim/init.lua` in Mac or Linux and for Windows in `~/AppData/Local/nvim/init.lua`.


## NVIM_APPNAME
The standard directories can be further configured by the `$NVIM_APPNAME` [environment variable](https://neovim.io/doc/user/starting.html#%24NVIM_APPNAME). This variable controls the sub-directory that Nvim will read from (and auto-create) in each of the base directories. For example, setting `$NVIM_APPNAME` to "foo" before starting will cause Nvim to look for configuration files in `$XDG_CONFIG_HOME/foo` instead of `$XDG_CONFIG_HOME/nvim`. `$NVIM_APPNAME` must be a name, such as "foo", or a relative path, such as "foo/bar".


```
set expandtab
set tabstop=2
set softtabstop=2
set shiftwidth=2
```

`:source %` source this file. This is for sourcing vimscript file.

To set vim scripts and configurations in lua file we need `meta-accessors` to expose lower level vim commands in lua runtime. `vim.cmd` function takes the vim commands and converts it for lua. Thus the previous commands should be- 

```lua
vim.cmd("set expandtab")
vim.cmd("set tabstop=2")
vim.cmd("set softtabstop=2")
vim.cmd("set shiftwidth=2")
```

# Package Manager 
1. packer.nvim
2. lazy.nvim

## lazy.nvim
Instructions at [GitHub](https://github.com/folke/lazy.nvim?tab=readme-ov-file#-installation).
You can add the following Lua code to your init.lua to bootstrap lazy.nvim:

```lua
-- install and/or check for lazy.nvim
local lazypath = vim.fn.stdpath("data") .. "/lazy/lazy.nvim"
if not vim.loop.fs_stat(lazypath) then
  vim.fn.system({
    "git",
    "clone",
    "--filter=blob:none",
    "https://github.com/folke/lazy.nvim.git",
    "--branch=stable", -- latest stable release
    lazypath,
  })
end
vim.opt.rtp:prepend(lazypath)

-- declare variables for the next command
local plugins = {}
local opts = {}

-- load lazy.nvim and key bindings
require("lazy").setup(plugins, opts)
```

## Colorscheme
Get [catppuccin](https://github.com/catppuccin/nvim).

```lua
{ "catppuccin/nvim", name = "catppuccin", priority = 1000 }

-- add it to local plugins tuple 
local plugins = {
  { "catppuccin/nvim", name = "catppuccin", priority = 1000 }
}
```
This installs the plugin but doesn't enable it.
To enable most packages we need `require` and `setup` function. The `setup` function imports all the package functionality in lua runtime for neovim to execute it. So add the following after requiring lazy-

```lua
require("lazy").setup(plugins, opts)

require("catppuccin").setup()
vim.cmd.colorscheme "catppuccin"
```

## Telescope
For fuzzy finding files and grep through project. [link](https://github.com/nvim-telescope/telescope.nvim).

Add to local plugins

```lua
local plugins = {
  { "catppuccin/nvim", name = "catppuccin", priority = 1000 },
  {
    'nvim-telescope/telescope.nvim', tag = '0.1.5',
    dependencies = { 'nvim-lua/plenary.nvim' }
  }
}
```
Now to initialize it add the following after require lazy- 
```lua
require("lazy").setup(plugins, opts)

local builtin = require("telescope.builtin")
vim.keymap.set('n', '<C-p>', builtin.find_files, {})
vim.keymap.set('n', '<leader>fg', builtin.live_grep, {})
```
`find_files` is the function withing `telescope.builtin` which is loaded by `require`. This allows us to fuzzy find files in our project.


## Treesitter
[Tool](https://github.com/nvim-treesitter/nvim-treesitter) for generating abstract syntax tree. Used for code highlighting, indenting etc. `TSUpdate` updates treesitter itself. Add to local plugin. 

```lua
local plugins = {
  { "catppuccin/nvim", name = "catppuccin", priority = 1000 },
  {
    'nvim-telescope/telescope.nvim', tag = '0.1.5',
    dependencies = { 'nvim-lua/plenary.nvim' }
  },
  {"nvim-treesitter/nvim-treesitter", build = ":TSUpdate"}
}
```
Then require `nvim-treesitter.configs` and assign it to a local variable, eg. config. then `config.setup`

```lua
local config = require("nvim-treesitter.configs")
config.setup({
  ensure_installed = {"lua", "javascript"},
  highlight = { enable = true },
  indent = { enable = true },  
})
```

## Neo Tree
File explorer tree. There is neo-tree and nvim-tree. Add neo-tree to local plugins

```lua
local plugins = {
  { "catppuccin/nvim", name = "catppuccin", priority = 1000 },
  {
    'nvim-telescope/telescope.nvim', tag = '0.1.5',
    dependencies = { 'nvim-lua/plenary.nvim' }
  },
  {"nvim-treesitter/nvim-treesitter", build = ":TSUpdate"},
  {
    "nvim-neo-tree/neo-tree.nvim",
    branch = "v3.x",
    dependencies = {
      "nvim-lua/plenary.nvim",
      "nvim-tree/nvim-web-devicons", 
      "MunifTanjim/nui.nvim",
    }
  }
}
```
Then add key mapping `vim.keymap.set('n', '<C-n>', ':Neotree filesystem reveal left<CR>')`


# Structuring Your Plugins
Every spec file under the "plugins" directory will be loaded automatically by `lazy.nvim`. To split plugin specs in multiple files, create `lua/plugins.lua` which will `return` (instead of `local plugins =`) all plugins list. All plugin specific `setup` could be placed in separate files inside plugins folder, it is not needed to add `require` calls in your main plugin file anymore.

Now `require("lazy").setup("plugins")` in `~/.config/nvim/init.lua` will use the list from `~/.config/nvim/lua/plugins.lua`. Any lua file in `~/.config/nvim/lua/plugins/*.lua` will be automatically merged in the main plugin spec.


### File Structure
```
nvim/
├── init.lua
├── lua/
    ├── plugins.lua
    ├── plugins/
        ├── telescope.lua
        ├── neo-tree.lua etc. ├
```

```
~/.config/nvim
├── lua
│   ├── config
│   │   ├── autocmds.lua
│   │   ├── keymaps.lua
│   │   ├── lazy.lua
│   │   └── options.lua
│   └── plugins
│       ├── spec1.lua
│       ├── **
│       └── spec2.lua
└── init.lua
```

For plugin specific setups we can move those to the `plugins/*.lua` with plugin spec `config`. `config` is executed when the plugin loads. The default implementation will automatically run `require(MAIN).setup(opts)`. 

Move the plugin setup commands within `config = function() ... end`. 
Put `require("plugin").setup()` inside config function. 

```lua
return { 
  "catppuccin/nvim", 
  config = function() 
    vim.cmd.colorscheme "catppuccin"
  end
}
```
To move remaining vim settings from `init.lua` to a new file we can just `require("file-name")`. It should be placed in the `lua` folder like `nvim/lua/file-name.lua`.


## Lualine
Create `lualine.lua` in plugins folder. `return` the following also add `config` if required.

```lua
return{
  'nvim-lualine/lualine.nvim',
  dependencies = { 'nvim-tree/nvim-web-devicons' },
  config = function 
    require('lualine').setup({
      options = {
        theme = 'dracula'
      }
    })
  end
}
```

# LSP
Language Server Protocol. Allows communication between text editors and language servers in the local machine. Provides language intelligence features like go to definition, code actions, quick fixes, hover documentation etc. 

## Mason
`mason` is the LSP manager plugin. 
`mason-lspconfig` closes some gaps that exist between `mason.nvim` and `lspconfig`. `mason-lspcofig` provides `ensure_installed` property.
`nvim-lspconfig` sets up communication between neovim and language servers. Also provides key bindings.

```lua
return {
  "williamboman/mason.nvim",
  "williamboman/mason-lspconfig.nvim",
  "neovim/nvim-lspconfig",
}

-- full lsp-config.lua with setups and configuration
return {
  {
    "williamboman/mason.nvim",
    config = function()
      require("mason").setup()
    end
  },
  {
    "williamboman/mason-lspconfig.nvim",
    config = function()
      require("mason-lspconfig").setup({
        ensure_installed = { "lua-ls" }
      })
    end
  },
  {
    "neovim/nvim-lspconfig",
    config = function()
      local lspconfig = require("lspconfig")
      lspconfig.lua_ls.setup({})

      vim.keymap.set('n', 'gd', vim.lsp.buf.definition, {})
      vim.keymap.set('n', 'K', vim.lsp.buf.hover, {})
      vim.keymap.set({ 'n', 'v' }, '<leader>ca', vim.lsp.buf.code_action, {})
    end
  }
}
```

## telescope-ui-select.nvim
It sets `vim.ui.select` to telescope. That means for example that neovim core stuff can fill the telescope picker. Example would be `lua vim.lsp.buf.code_action()`.


# Linters & Formatters 
Usually linters are CLI tools, `null-ls` plugin brings these functionality to neovim LSP. It is archived now so use `none-ls`.

`null_ls.builtins.formatting.stylua,` this integrates stylua functionalities with LSP. We need to install `stylua` from `mason > Formatter`. Install each linter and formatter for all languages (python [black, isort], javascript [eslint_d, prettier] etc) you want to use.

## alpha-nvim
alpha is a fast and fully programmable greeter for neovim. `startify` theme gives the latest files you used in the dashboard.


# Autocompletion & Snippets
1. `nvim-cmp` - completion engine
2. `LuaSnip` - snippet engine
3. `cmp_luasnip` - completion source for nvim-cmp
4. `Friendly Snippets` - Snippets collection for a set of different programming languages.
5. `cmp-nvim-lsp` - nvim-cmp source for neovim's built-in language server client.

If you're using LuaSnip make sure to use `require("luasnip.loaders.from_vscode").lazy_load()`, and add `friendly-snippets` as a dependency for LuaSnip, otherwise snippets might not be detected. If you don't use `lazy_load()` you might notice a slower startup-time.


# Debuggers
Debug adapter protocol (DAP). Two plugins `nvim-dap` and `nvim-dap-ui`. Features - breakpoints, step over function, step into function, variable tracing.

Also install language specific [Debug Adapter](https://github.com/mfussenegger/nvim-dap/wiki/Debug-Adapter-installation).

# Packages
1. Catppuccin
2. Telescope
3. Treesitter
4. Neotree
5. Lualine
6. Mason
7. mason-lspconfig.nvim
8. nvim-lspconfig
9. telescope-ui-select.nvim
10. none-ls.nvim
11. Dashboard alpha-nvim
12. nvim-cmp completion engine
13. LuaSnip snippet engine
14. cmp_luasnip completion source for nvim-cmp
15. Friendly Snippets
16. cmp-nvim-lsp
17. nvim-dap
18. nvim-dap-ui


# Commands
1. Record macro - `qq`, to stop `q`
2. Paste macro - `@q`
3. `\` - search
4. `:source %` source this file. 
5. `:Lazy` - lazy GUI
6. `:Telescope find_files<cr>` to see if telescope.nvim is installed correctly.
7. `Ctrl p` - find files by telescope
8. `<leader>fg` - Live Grep
9. `:TSUpdate` - update parsers 
10. `:TSInstall` - install parsers
11. `:Neotree` - Press ? in the Neo-tree window to view the list of mappings.
12. `Ctrl n` - reveal file tree
13. `:LspInfo` - by nvim-lspconfig, shows LSPs connected to current buffer
14. `:h vim.lsp.buf` - help doc showing all available functions in vim.lsp.buf module
15. `K` over a function - display documentation of that function
16. `Ctrl x o` - LSP builtin omni func
17. `<leader>gf` - formatting with `vim.lsp.buf.format`
18. `<Leader>dt` - debugging toggle breakpoint
19. `<Leader>dc` - debugging continue

## Other plugins
1. [Neovide](https://neovide.dev/configuration.html#cursor-settings) Cursor animation
2. [Oil](https://github.com/stevearc/oil.nvim) Neovim file explorer: edit your filesystem like a buffer
3. [Harpoon](https://github.com/ThePrimeagen/harpoon)
