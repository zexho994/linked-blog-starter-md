### windows 安装 neovim
在Windows上安装Neovim可以通过以下几种方式：
### 方法一：通过Chocolatey安装
1. **安装Chocolatey**（如果尚未安装）：
    - 打开PowerShell并以管理员身份运行，输入以下命令安装Chocolatey：
        
        `Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))`
        
2. **安装Neovim**：
    - 安装完成Chocolatey之后，在相同的PowerShell窗口中运行以下命令来安装Neovim：
        
        `choco install neovim`
        
### 方法二：通过scoop安装

1. **安装scoop**（如果尚未安装）：
    - 打开PowerShell并以管理员身份运行，输入以下命令安装scoop：
        `iex (new-object net.webclient).downloadstring('https://get.scoop.sh')`
2. **安装Neovim**：
    - 使用scoop来安装Neovim，运行以下命令：
        `scoop install neovim`
        
### 方法三：通过直接下载Zip文件
1. **下载Neovim**：
    - 访问[Neovim的官方GitHub发布页面](https://github.com/neovim/neovim/releases)，下载最新的Windows 64-bit Zip文件。
2. **解压文件**：
    - 将下载的Zip文件解压到您选择的目录，比如 `C:\Program Files\Neovim`。
3. **配置环境变量**：
    - 将解压后的Neovim目录添加到系统的路径中：
        1. 右键点击“此电脑”或“计算机”，选择属性。
        2. 点击“高级系统设置”。
        3. 在“系统属性”窗口中点击“环境变量”。
        4. 在“系统变量”部分找到并选择`Path`，点击“编辑”。
        5. 点击“新建”，然后输入Neovim的路径（例如`C:\Program Files\Neovim\bin`）。
        6. 点击“确定”保存更改。
### 方法四：通过Windows Package Manager (winget)

1. 打开PowerShell或命令提示符，并运行以下命令：
    `winget install Neovim.Neovim`
    
安装完成后，可以通过在命令提示符或PowerShell中输入`nvim`来验证Neovim是否正确安装。如果Neovim启动，则表示安装成功。


### 配置插件管理器

```shell
-- 基本配置示例
vim.o.number = true         -- 显示行号
vim.o.syntax = 'on'         -- 启用语法高亮
vim.o.tabstop = 4           -- 设置Tab宽度为4个空格
vim.o.shiftwidth = 4        -- 设置自动缩进宽度为4个空格
vim.o.expandtab = true      -- 将Tab转换为空格

-- Ensure packer.nvim is installed
local ensure_packer = function()
    local fn = vim.fn
    local install_path = fn.stdpath('data')..'/site/pack/packer/start/packer.nvim'
    if fn.empty(fn.glob(install_path)) > 0 then
        fn.system({'git', 'clone', '--depth', '1', 'https://github.com/wbthomason/packer.nvim', install_path})
        vim.cmd [[packadd packer.nvim]]
        return true
    end
    return false
end

local packer_bootstrap = ensure_packer()

-- Auto compile when there are changes in plugins.lua
vim.cmd([[
 augroup packer_user_config
   autocmd!
   autocmd BufWritePost init.lua source <afile> | PackerSync
 augroup end
]])

-- Use a protected call to avoid errors on first use
local status_ok, packer = pcall(require, "packer")
if not status_ok then
  return
end

-- Add your plugins here
packer.startup(function(use)
    use 'wbthomason/packer.nvim'  -- Packer manages itself

    use 'tpope/vim-sensible'
    use {
        'nvim-treesitter/nvim-treesitter',
        run = ':TSUpdate'
    }

    use 'hrsh7th/nvim-cmp'               -- Autocompletion plugin
    use 'hrsh7th/cmp-nvim-lsp'           -- LSP source for nvim-cmp
    use 'hrsh7th/cmp-buffer'             -- Buffer completions
    use 'hrsh7th/cmp-path'               -- Path completions
    use 'hrsh7th/cmp-vsnip'              -- Snippet completions
    use 'hrsh7th/vim-vsnip'              -- Snippet engine

    use 'jose-elias-alvarez/null-ls.nvim'

    use {
        'nvim-telescope/telescope.nvim',
        requires = { {'nvim-lua/plenary.nvim'} }
    }

    use {
        'lewis6991/gitsigns.nvim',
        requires = {
            'nvim-lua/plenary.nvim'
        },
        config = function()
            require('gitsigns').setup()
        end
    }

    use 'tpope/vim-commentary'
    use 'folke/which-key.nvim'
    use 'nvim-lua/plenary.nvim'
    use {
        'kyazdani42/nvim-tree.lua',
        requires = {
            'kyazdani42/nvim-web-devicons',
        },
        config = function()
            require'nvim-tree'.setup {}
        end
    }

    if packer_bootstrap then
        require('packer').sync()
    end
end)

-- Treesitter configuration
require'nvim-treesitter.configs'.setup {
    ensure_installed = { "java", "lua" },
    highlight = {
        enable = true,
    },
    indent = {
        enable = true
    },
    incremental_selection = {
        enable = true,
        keymaps = {
            init_selection = "gnn",
            node_incremental = "grn",
            scope_incremental = "grc",
            node_decremental = "grm",
        },
    },
}

-- CMP configuration
local cmp = require'cmp'
cmp.setup({
    snippet = {
        expand = function(args)
            vim.fn["vsnip#anonymous"](args.body)
        end,
    },
    sources = cmp.config.sources({
        { name = 'nvim_lsp' },
        { name = 'vsnip' },
    }, {
        { name = 'buffer' },
    })
})

-- Null LS configuration
local null_ls = require("null-ls")
null_ls.setup({
    sources = {
        null_ls.builtins.formatting.prettier,
        null_ls.builtins.diagnostics.eslint,
    },
})

-- Telescope configuration
require('telescope').setup{}

-- Which-key configuration
require("which-key").setup {}

```

### 可能需要安装的软件
如果出现这样的报错：
```
Error detected while processing C:\Users\admin\AppData\Local\nvim\init.lua: No C compiler found! "cc", "gcc", "clang", "cl", "zig" are not executable. No C compiler found! "cc", "gcc", "clang", "cl", "zig" are not executable. Press ENTER or type command to continue
```
需要安装C的编译器，推荐下面方式：
#### 使用MSYS2（推荐）
下载和安装MSYS2：
- 访问MSYS2官方网站并下载安装包：[MSYS2下载页面](https://www.msys2.org/)
- 安装完成后，启动MSYS2。
**更新MSYS2和安装GCC**：
- 在MSYS2终端中，执行以下命令：
	`pacman -Syu pacman -S base-devel mingw-w64-x86_64-toolchain`
- 确认安装。
**配置环境变量**：
- 按照上述方法打开系统“环境变量”设置。
- 添加MSYS2安装目录中的`mingw64\bin`路径（例如：`C:\msys64\mingw64\bin`）。
- 确认保存。

重新配置 nvim-treesitter 完成编译器安装和环境变量配置后，重启你的Neovim，并重新运行`PackerSync`以确保所有内容正确安装。

