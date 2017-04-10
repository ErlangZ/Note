# Win7 和 Ubuntu14.04双系统安装过程
## 安装需要准备的软件
0. 在Windows下，下载安装UltraISO用来制作启动U盘
1. 含有Win7安装镜像的启动U盘
2. 含有Ubuntu安装镜像的启动U盘
3. 一台空白的机器（我们先安装Windows，默认会整个格式化硬盘）
4. Windows下DiskGenius和EasyBCD两款软件的安装程序，用来对硬盘进行重新划分和安装引导程序。


## 安装过程
建议先安装Windows,然后安装Ubuntu。因为Windows的分区有点麻烦，它不会顾忌电脑上已经存在的操作系统,
而直接格式化整个硬盘。

1. 安装Windows  
如果是空白的主机，那么用U盘启动电脑，然后一路默认安装，格式化整个硬盘, 如同普通的安装过程。
2. 安装DiskGenius，划分出Ubuntu的硬盘分区  
使用这款软件，对硬盘的某个分区重新进行划分：它可以未存储数据的分区重新划分，划分出你希望的大小，设置
为“未使用分区”，用来安装Ubuntu。软件的使用很容易，就是图形化界面。一般情况下，Windows7系统分区要保留
至少40G，用来安装Windows系统和其他软件。Ubuntu的硬盘大小则取决与你希望使用的大小，Ubuntu下可以看到所
有的Windows硬盘的数据，但是反过来不行。
3. 安装Ubuntu之分区方案  
使用U盘引导启动电脑，按照一般的步骤进行安装。在安装过程的第四步，会让你选择系统的分区方案，请选择“自定义分区方案”，
然后“下一步”。  
这时，你就可以像在DiskGenius中看到的一样，再次看到整个硬盘的分区情况。然后，在我们之前划分的空白区域
上进行安装。我们电脑一般是作为桌面系统使用，请至少将/home和/两个目录单独分区，/目录请给出至少20G,也
是用来存储Ubuntu和我们下载安装使用的软件；/home目录请使用我们剩下所有的硬盘。这样即使系统因为某些原因
崩溃，我们只需要重新安装系统和相应的软件，保留用户数据。如果你希望做的细致一些，请参考下边的表格。
    * /boot 200M-400M   Linux内核镜像
    * /     10GB        系统根目录
    * /usr  20GB        应用软件安装位置
    * /opt  10GB        用户自性安装软件位置
    * /var  20GB        系统日志, apt安装包存储位置等，如果是服务器用，建议单独分区并且设置的比较大
    * /tmp  10GB        临时文件, 如果是服务器用，建议单独分区并且设置的比较大，防止被意外打满系统崩溃
    * /home 1TB         用户数据目录  
4. 安装Ubuntu之安装引导程序     
在窗口的下方，有安装引导程序的位置，建议选择/dev/sda（就是之前我们安装windows）的位置。这样，系统就会
使用Grub2来进行引导启动。在每次电脑启动时，会让你选择进入哪个系统。  
如果你希望使用Windows的引导程序引导启动，就把安装程序安装到/boot分区上。*注意*,这样选重启电脑后，你
只能进入Windows，然后需要在Windows里使用EasyBCD软件修改一下引导程序，把我们新安装的Ubuntu选项也加进
去，再启动电脑就能看到Linux的启动项了。
5. 安装完成   
进行完第4步后，一路默认安装，然后重启电脑就好啦。如果重启电脑，只能进入Windows，请参考第4步。

## 使用注意事项
1. 请一定把Ubuntu的自动更新关闭，或者仅仅保留“安装重要更新”和“推荐更新”,“有新版本时，选择通知我”。
否则，每次自动更新必崩溃。



