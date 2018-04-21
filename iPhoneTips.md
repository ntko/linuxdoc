  
### 更改iTunes备份地址释放C盘空间

* iTunes默认的备份目录是C:\Users\lucys\AppData\Roaming\Apple Computer\MobileSync\Backup
* 剪切Backup到其他盘，且根据需要重命名。比如剪切到G盘且重命名为: `G:\iTunesBackup`
* 管理员运行命令行，进入C:\Users\lucys\AppData\Roaming\Apple Computer\MobileSync\,且运行如下命令：

> `mklink /J Backup g:\iTunesBackup`

* 上述命令的作用是创建一个符号链接。(和快捷方式不同)
