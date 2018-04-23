  
##LINUX命令工具

### 包管理工具apt

#### 参考文档： 

* [APT工作原理](https://blog.csdn.net/buguyiqie/article/details/4948661 "APT工作原理")
* [apt-get常用命令及工作原理](https://blog.csdn.net/mosquito_zm/article/details/63684608 "apt-get常用命令及工作原理")

#### apt-get 常用实例

*    apt-cache search packagename 搜索包
*    apt-cache show packagename 获取包的相关信息，如说*    明、大小、版本等
*    apt-get install packagename 安装包
*    apt-get install packagename --reinstall 重新安*    装包
*    apt-get -f install 修复安装”-f = –fix-missing”
*    apt-get remove packagename 删除包
*    apt-get remove packagename --purge 删除包，包括*    删除配置文件等
*    apt-get update 更新源
*    apt-get upgrade 更新已安装的包
*    apt-get dist-upgrade 升级系统
*    apt-get dselect-upgrade 使用 dselect 升级
*    apt-cache depends packagename 了解使用依赖
*    apt-cache rdepends packagename 是查看该包被哪些包*    依赖
*    apt-get build-dep packagename 安装相关的编译环境
*    apt-get source packagename 下载该包的源代码
*    apt-get clean 清理无用的包
*    apt-get autoclean 清理无用的包
*    apt-get check 检查是否有损坏的依赖

##Windows10命令工具

### Windows10下如何查看哪些软件或进程占用了网速
    运行perfmon -res 即可。

