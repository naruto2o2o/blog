# vim配置

## 安装插件管理软件Bundle

```shell
	 git clone https://github.com/gmarik/Vundle.vim.git ~/.vim/bundle/Vundle.vim
```



## 操作原理

在`.vimrc` 配合文件中输入配置plugin即可使用bundle安装

之后再vim中 `BundleInstall`

## 完整配置文件示例

```shell
set mouse=c
set nu
set hlsearch
set autoindent
set ruler
set showmode
set bg=dark
syntax on
set wrap
set shiftwidth=4
set tabstop=4
set softtabstop=4
set expandtab
set smartindent
set backspace=indent,eol,start
set nocompatible
set rtp+=~/.vim/bundle/Vundle.vim
call vundle#begin()
" 加载插件
Plugin 'VundleVim/Vundle.vim'
Plugin 'scrooloose/nerdtree'
Plugin 'vim-airline/vim-airline'
Plugin 'vim-airline/vim-airline-themes'
Plugin 'michaelHL/awesome-vim-colorschemes'
Plugin 'Tagbar'
Plugin 'Tabular'
Plugin 'Shougo/neocomplete'
call vundle#end()
filetype plugin indent on
if has("autocmd")
    au BufReadPost * if line("'\"") > 1 && line("'\"") <= line("$") | exe "normal! g'\"" | endif
endif

nmap <leader>t :NERDTreeToggle<CR>
autocmd bufenter * if (winnr("$") == 1 && exists("b:NERDTree") && b:NERDTree.isTabTree()) | q | endif
let g:NERDTreeDirArrowExpandable = '►'
let g:NERDTreeDirArrowCollapsible = '▼'
let NERDTreeAutoCenter=1
let NERDTreeShowLineNumbers=1
let NERDTreeShowHidden=1
let NERDTreeWinSize=55
let g:nerdtree_tabs_open_on_console_startup=1
let NERDTreeIgnore=['\.pyc','\~$','\.swp']
let g:NERDTreeIndicatorMapCustom = {
      \ "Modified"  : "✹",
      \ "Staged"    : "✚",
      \ "Untracked" : "✭",
      \ "Renamed"   : "➜",
      \ "Unmerged"  : "═",
      \ "Deleted"   : "✖",
      \ "Dirty"     : "✗",
      \ "Clean"     : "✔︎",
      \ 'Ignored'   : '☒',
      \ "Unknown"   : "?"
      \ }
autocmd vimenter * if !argc()|NERDTree|endif

```



