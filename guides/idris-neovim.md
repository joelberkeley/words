# Idris Neovim

_How to set up interactive editing in Neovim for Idris 2 on Ubuntu_

Note: I use the words Idris and Idris2 interchangeably. I'll always mean Idris2.

1. Install Neovim. I strongly recommend using the [latest stable release](https://github.com/neovim/neovim/releases/latest). The version on your distro's official package repository may well be too old.
1. Install [Packer](https://github.com/wbthomason/packer.nvim) with e.g.
   ```bash
   git clone --depth 1 https://github.com/wbthomason/packer.nvim\
    ~/.local/share/nvim/site/pack/packer/start/packer.nvim
   ```
1. Install the [Idris _Language Server Protocol_ (LSP)](https://github.com/idris-community/idris2-lsp). I recommend using pack. With pack, use
   ```bash
   pack install-app lsp
   ```
1. Add LSP to your Neovim config at ~/.config/nvim/init.lua. A minimal config may look like
   ```lua
   require('packer').startup(function()
     use 'wbthomason/packer.nvim'
     use {'ShinKage/idris2-nvim', requires = {'neovim/nvim-lspconfig', 'MunifTanjim/nui.nvim'}}
   end)

   require('idris2').setup({})
   ```
1. Add a [.ipkg file](https://idris2.readthedocs.io/en/latest/reference/packages.html) to your project. You can create a new package file in the current directory with
   ```bash
   idris2 --init
   ```
1. (Optional) Add keyboard shortcuts for Idris2 commands. Add the following to your config
   ```lua
   vim.api.nvim_set_keymap('n', '<leader>cs', ":lua require('idris2.code_action').case_split()<CR>", {noremap = true})
   vim.api.nvim_set_keymap('n', '<leader>mc', ":lua require('idris2.code_action').make_case()<CR>", {noremap = true})
   vim.api.nvim_set_keymap('n', '<leader>ml', ":lua require('idris2.code_action').make_lemma()<CR>", {noremap = true})
   vim.api.nvim_set_keymap('n', '<leader>ac', ":lua require('idris2.code_action').add_clause()<CR>", {noremap = true})
   vim.api.nvim_set_keymap('n', '<leader>es', ":lua require('idris2.code_action').expr_search()<CR>", {noremap = true})
   vim.api.nvim_set_keymap('n', '<leader>gd', ":lua require('idris2.code_action').generate_def()<CR>", {noremap = true})
   vim.api.nvim_set_keymap('n', '<leader>rh', ":lua require('idris2.code_action').refine_hole()<CR>", {noremap = true})
   vim.api.nvim_set_keymap('n', '<leader>i' , ":lua require('idris2.code_action').intro()<CR>", {noremap = true})
   vim.api.nvim_set_keymap('n', '<leader>e',  ':lua require("idris2.repl").evaluate()<CR>', {noremap = true})
   ```
   You may want to add other commands listed in the [plugin docs](https://github.com/ShinKage/idris2-nvim).
1. (Optional) Autosave on each editing action. To do this, replace the line `require('idris2').setup({})` shown above with
   ```lua
   local function save_hook(action)
     vim.cmd('silent write')
   end

   require('idris2').setup({code_action_post_hook = save_hook})
   ```
