# Setting up interactive editing for Idris with Neovim

This guide assumes Ubuntu, but may work on other Linux distributions and Mac OS.

1. Install Neovim. I recommend using the [latest stable release](https://github.com/neovim/neovim/releases/latest). The version on your distro's official package repository may well be too old.
1. Install [Packer](https://github.com/wbthomason/packer.nvim) with e.g.
   ```bash
   git clone --depth 1 https://github.com/wbthomason/packer.nvim\
    ~/.local/share/nvim/site/pack/packer/start/packer.nvim
   ```
1. Install the [Idris _Language Server Protocol_ (LSP)](https://github.com/idris-community/idris2-lsp). I recommend using [Pack](https://github.com/stefan-hoeck/idris2-pack). With Pack installed (and ~/.pack/bin added to `PATH`), run
   ```bash
   pack install-app lsp
   ```
   You can check the LSP is working with
   ```bash
   idris2-lsp --version
   ```
1. Add LSP to your Neovim config at ~/.config/nvim/init.lua. A minimal config may look like
   ```lua
   require('packer').startup(function()
     use 'wbthomason/packer.nvim'
     use {'ShinKage/idris2-nvim', requires = {'neovim/nvim-lspconfig', 'MunifTanjim/nui.nvim'}}
   end)

   require('idris2').setup({})
   ```
1. Install configured plugins by running `:PackerSync` in Neovim.
1. Add a [package file](https://idris2.readthedocs.io/en/latest/reference/packages.html) to your project. You can create a new package file in the current directory with
   ```bash
   idris2 --init
   ```
   Make sure your project builds. If your package file is foo.ipkg, run
   ```bash
   idris2 --build foo.ipkg
   ```
1. (Optional) Add keyboard shortcuts for Idris2 commands. Add the following to your Neovim config
   ```lua
   vim.api.nvim_set_keymap('n', '<leader>h', ':lua vim.lsp.buf.hover()<CR>', {noremap = true})

   vim.api.nvim_set_keymap('n', '<leader>e',  ':lua require("idris2.repl").evaluate()<CR>', {noremap = true})
   vim.api.nvim_set_keymap('n', '<leader>cs', ':lua require("idris2.code_action").case_split()<CR>', {noremap = true})
   vim.api.nvim_set_keymap('n', '<leader>mc', ':lua require("idris2.code_action").make_case()<CR>', {noremap = true})
   vim.api.nvim_set_keymap('n', '<leader>ml', ':lua require("idris2.code_action").make_lemma()<CR>', {noremap = true})
   vim.api.nvim_set_keymap('n', '<leader>ac', ':lua require("idris2.code_action").add_clause()<CR>', {noremap = true})
   vim.api.nvim_set_keymap('n', '<leader>es', ':lua require("idris2.code_action").expr_search()<CR>', {noremap = true})
   vim.api.nvim_set_keymap('n', '<leader>gd', ':lua require("idris2.code_action").generate_def()<CR>', {noremap = true})
   vim.api.nvim_set_keymap('n', '<leader>rh', ':lua require("idris2.code_action").refine_hole()<CR>', {noremap = true})
   vim.api.nvim_set_keymap('n', '<leader>i' , ':lua require("idris2.code_action").intro()<CR>', {noremap = true})
   ```
   You may want to add other commands listed in the [plugin docs](https://github.com/ShinKage/idris2-nvim). With a default nvim setup, `<leader>` is backslash, so entering `\ac` with the cursor on a function type signature will add a template definition.
1. (Optional) Autosave on each editing action. To do this, add a callback to `require('idris2').setup({})` as
   ```lua
   local function save_hook(action)
     vim.cmd('silent write')
   end

   require('idris2').setup({code_action_post_hook = save_hook})
   ```

## Something's not working

* **Problem**
  Editing command doesn't work, and the command bar shows
  ```
  No code actions available
  ```
  **Solution**
  The LSP only works if the code in the current module, and the modules it imports, compiles. Note compiler errors don't always appear in the editor at the same place as the error: they can appear at the top of the module, for example. Try building the package from the command line. Fix compiler errors in the current module and those it imports.
