# Vim相关配置
1. 升级vim版本至8.0  
```
sudo apt-get remove vim
sudo apt-get remove vim-gnome
git clone https://github.com/vim/vim.git
cd vim
./configure --with-features=huge \
            --enable-multibyte \
            --enable-rubyinterp=yes \
            --enable-pythoninterp=yes \
            --with-python-config-dir=/usr/lib/python2.7/config \
            --enable-perlinterp=yes \
            --enable-luainterp=yes \
            --enable-gui=gtk2 \
            --enable-cscope 
            --prefix=/usr            # 默认安装到/usr/local/bin目录中
            #--enable-python3interp=yes \ #可以打开如下的选项
            #--with-python3-config-dir=/usr/lib/python3.5/config \
make 
sudo make install
```

2. 安装[Vundle](https://github.com/VundleVim/Vundle.vim)插件管理工具  
- 在.vim/bundle/YouCompleteMe目录中运行python install.py --clang-completer --enable-coverage 
  --system-libclang 完成安装
- cp ~/.vim/bundle/YouCompleteMe/third_party/ycmd/examples/.ycm_extra_conf.py ~/  
  在.ycm_extra_conf.py中添加两行
```
'-isystem',                                                                                         
'/usr/include/c++/4.8',
```
- 用如下的代码替换~/.vimrc  

```
"Vundle插件配置
set nocompatible              " 去除VI一致性,必须
filetype off                  " 必须
" 设置包括vundle和初始化相关的runtime path
set rtp+=~/.vim/bundle/Vundle.vim
call vundle#begin()
" 另一种选择, 指定一个vundle安装插件的路径
"call vundle#begin('~/some/path/here')

" 让vundle管理插件版本,必须
Plugin 'VundleVim/Vundle.vim'
Plugin 'godlygeek/tabular'
Plugin 'plasticboy/vim-markdown'
Plugin 'Valloric/YouCompleteMe'
" 你的所有插件需要在下面这行之前
call vundle#end()            " 必须
filetype plugin indent on    " 必须

"语法和缩进
set nocompatible 
filetype on 
syntax on
set hlsearch
filetype plugin indent on

"tab相关设置
set tabstop=4
set softtabstop=4
set shiftwidth=4
set expandtab

"颜色方案
set t_Co=256
colorscheme desert
"vim 7.3版本以上支持高亮某一列
set colorcolumn=100
set cc=100
set cursorline
hi CursorLine  cterm=NONE   ctermbg=darkred ctermfg=white
hi CursorColumn cterm=NONE ctermbg=darkred ctermfg=white

"字符编码设置
set fileencodings=ucs-bom,utf-8,cp936,gb18030,big5,euc-jp,euc-kr,latin1         
set encoding=utf-8                                                              
set fileencoding=utf-8                                                          
set termencoding=utf-8                                                          
set langmenu=zh_CN.UTF-8                                                        
set fileencodings=ucs-bom,utf-8,cp936,gb18030,big5,euc-jp,euc-kr,latin1         
set laststatus=2
language message zh_CN.UTF-8       

"文件类型对应
autocmd BufNewFile,BufRead \*.md,\*.mkdn,\*.markdown :set filetype=markdown"
autocmd filetype javascript set dictionary+=~/.vim/bundle/vim-dict/dict/javascript.dic
autocmd filetype css set dictionary+=~/.vim/bundle/vim-dict/dict/css.dic
autocmd filetype php set dictionary+=~/.vim/bundle/vim-dict/dict/php.dic

"配置YouComplete
let g:ycm_global_ycm_extra_conf='~/.ycm_extra_conf.py'
let g:ycm_python_binary_path='python'
let g:ycm_confirm_extra_conf='0'
```

