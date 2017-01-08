# 配置MarkDown中文工作环境
0. 下载安装 Sougou输入法
   注意必须将系统语言设置为中文，否则即使安装的Sougou输入法也无法使用。
1. 下载安装 Remarkable MarkDown 编辑器
2. 下载安装 Pandoc
   此工具可以将md转换成pdf，html等多种格式。但是原生的程序不支持中文
3. 下载安装 TexLive
   sudo apt-get install texlive-full
   这样latex引擎中包含了xelatex引擎，可以支持中文
4. 在vimrc中添加,vim才会将\*.md识别为markdown文档
   "autocmd BufNewFile,BufRead \*.md,\*.mkdn,\*.markdown :set filetype=markdown"
5. 安装中文字体
   sudo apt-get install font-manager
   https://wiki.ubuntu.com.cn/%E5%85%8D%E8%B4%B9%E4%B8%AD%E6%96%87%E5%AD%97%E4%BD%93
6. 在$HOME目录中建立~/.Pandoc目录
   alias pandoc-markdown="pandoc --toc -c ~/.Pandoc/Markdown.css "
