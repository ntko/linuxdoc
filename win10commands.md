  
## Windows10命令工具

### Windows10下如何查看哪些软件或进程占用了网速
    运行perfmon -res 即可。
 
### Windows10升级之后oem分区自动显示了
    可以将这个多出来的oem分区给隐藏起来，可以以管理员的方式打开cmd，然后输入以下命令行：
    mountvol G: /d
    
### 重命名win10家庭版用户名    
    wmic useraccount where name='currentname' rename newname
    
### 命令行将文件内容复制到剪贴板    
    clip < a.txt
    
