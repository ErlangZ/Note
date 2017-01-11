#Cuda安装说明
1. 下载cuda的安装。       
   注：请使用local安装的方式本地安装（网络安装几乎没有成功过），cuda-XX.run脚本   
```
#mkdir cuda-install
#cp cuda-XX.run cuda-install
```

2. Alt + Ctrl + F1 进入纯控制台模式       
   注： 必须关闭X-server，否则显卡驱动无法安装   
```
#sudo etc/init.d/lightdm stop  ##关闭X-server
#cd cuda-install  
#bash cuda-XX.run              ##然后根据指令一路next
一切正常的话，系统会提示你驱动安装完毕， 需要重启。  
===============  
=    Summary  =  
===============  
Driver: Reboot required to continue  
Cuda-Toolkit: Skip  
```

3. 重启以后很可能发现你的屏幕显示不正常，分辨率很低，而且没发调。  
   不用慌张，因为cuda没装完。重新跑一边上边的过程，这次变成了  
 ===============  
 =   Summary   =  
 ===============  
 Driver: Installed  
 Cuda-Toolkit: Installed  
