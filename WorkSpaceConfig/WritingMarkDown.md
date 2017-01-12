# 配置MarkDown中文工作环境
0.  下载安装 Sougou输入法  
   	注意必须将系统语言设置为中文，否则即使安装的Sougou输入法也无法使用。
1. 	下载安装 Remarkable MarkDown 编辑器
2. 	下载安装 Pandoc  
   	此工具可以将md转换成pdf，html等多种格式。但是原生的程序不支持中文
3. 	下载安装 TexLive  
   	sudo apt-get install texlive-full  
   	这样latex引擎中包含了xelatex引擎，可以支持中文  
4. 	在vimrc中添加,vim才会将\*.md识别为markdown文档  
   	"autocmd BufNewFile,BufRead \*.md,\*.mkdn,\*.markdown :set filetype=markdown"
5. 	安装中文字体  
	安装字体管理器  
   	$sudo apt-get install font-manager [中文字体说明](https://wiki.ubuntu.com.cn/%E5%85%8D%E8%B4%B9%E4%B8%AD%E6%96%87%E5%AD%97%E4%BD%93)  
   	需要下载文鼎宋体  
    ```
$sudo apt-get install fonts-moe-standard-song fonts-moe-standard-kai fonts-cns11643-sung  \
fonts-cns11643-kai fonts-arphic-ukai fonts-arphic-uming fonts-arphic-bkai00mp  \
fonts-arphic-bsmi00lp fonts-arphic-gbsn00lp fonts-arphic-gkai00mp fonts-cwtex-ming  \
fonts-cwtex-kai fonts-cwtex-heib fonts-cwtex-yen fonts-cwtex-fs fonts-cwtex-docs fonts-droid \
fonts-wqy-microhei fonts-wqy-zenhei xfonts-wqy fonts-hanazono
    ```
	- fonts-moe-standard-song - 「教育部標準宋體」
	- fonts-moe-standard-kai - 「教育部標準楷體」
	- fonts-cns11643-sung - 「全字庫正宋體」
	- fonts-cns11643-kai - 「全字庫正楷體」
	- fonts-arphic-ukai -「文鼎楷書體」
	- fonts-arphic-uming -「文鼎明體」
	- fonts-arphic-bkai00mp -「文鼎 PL 中楷」
	- fonts-arphic-bsmi00lp -「文鼎 PL 細上海宋」
	- fonts-arphic-gbsn00lp -「文鼎 PL 簡報宋」
	- fonts-arphic-gkai00mp -「文鼎 PL 簡中楷」
	- fonts-cwtex-ming -「cwTeX 明體」
	- fonts-cwtex-kai -「cwTeX 楷體」
	- fonts-cwtex-heib -「cwTeX 粗黑體」
	- fonts-cwtex-yen -「cwTeX 圓體」
	- fonts-cwtex-fs -「cwTeX 仿宋體」
	- fonts-droid -「Droid Sans Fallback」
	- fonts-wqy-microhei -「文泉驛微米黑」
	- fonts-wqy-zenhei -「文泉驛正黑體」
	- xfonts-wqy - 「文泉驛 X11 字體」
	- ttf-mscorefonts-installer -「微軟英文字型」  
   	*不能使用文泉驿字体*,点阵字体显示都不正常  
    $sudo apt-get install xfonts-wqy
6. 	在$HOME目录中建立~/.Pandoc目录  
    把WorkSpaceConfig/PanDoc中的内容复制到~/.PanDoc里。
7. 	在.bashrc的末尾加入如下内容,给pandoc命令建立别名  
```
# Define pandoc-pdf & pandoc-hmtl
function pandoc-pdf() {
    md_file=$1
    pandoc --mathjax \
           --highlight-style monochrome \
           --latex-engine=xelatex \
           --template=/home/erlangz/.PanDoc/default.latex \
           $md_file -o ${md_file%.md}.pdf
}
function pandoc-html() {
    md_file=$1
    pandoc --mathjax \
           --highlight-style monochrome \
           --css=http://kevinburke.bitbucket.org/markdowncss/markdown.css 
           $md_file -o ${md_file%.md}.html
}
```


