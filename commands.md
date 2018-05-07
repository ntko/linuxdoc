  
## LINUX命令工具

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

#### 缩放图像的工具

> `convert -scale 50%x50% installcppext.png installcppexts.png`

#### linux之sed用法

> 原始文档:[linux之sed用法](http://www.cnblogs.com/dong008259/archive/2011/12/07/2279897.html)

sed是一个很好的文件处理工具，本身是一个管道命令，主要是以行为单位进行处理，可以将数据行进行替换、删除、新增、选取等特定工作，下面先了解一下sed的用法
sed命令行格式为：

        sed [-nefri] ‘command’ 输入文本        

常用选项：

        -n∶使用安静(silent)模式。在一般 sed 的用法中，所有来自 STDIN的资料一般都会被列出到萤幕上。但如果加上 -n 参数后，则只有经过sed 特殊处理的那一行(或者动作)才会被列出来。
        -e∶直接在指令列模式上进行 sed 的动作编辑；
        -f∶直接将 sed 的动作写在一个档案内， -f filename 则可以执行 filename 内的sed 动作；
        -r∶sed 的动作支援的是延伸型正规表示法的语法。(预设是基础正规表示法语法)
        -i∶直接修改读取的档案内容，而不是由萤幕输出。       

常用命令：

        a   ∶新增， a 的后面可以接字串，而这些字串会在新的一行出现(目前的下一行)～
        c   ∶取代， c 的后面可以接字串，这些字串可以取代 n1,n2 之间的行！
        d   ∶删除，因为是删除啊，所以 d 后面通常不接任何咚咚；
        i   ∶插入， i 的后面可以接字串，而这些字串会在新的一行出现(目前的上一行；
        p  ∶列印，亦即将某个选择的资料印出。通常 p 会与参数 sed -n 一起运作～
        s  ∶取代，可以直接进行取代的工作哩！通常这个 s 的动作可以搭配正规表示法例如 1,20s/old/new/g 就是啦！

举例：（假设我们有一文件名为ab）

    删除某行

     [root@localhost ruby] # sed '1d' ab              #删除第一行 
     [root@localhost ruby] # sed '$d' ab              #删除最后一行
     [root@localhost ruby] # sed '1,2d' ab           #删除第一行到第二行
     [root@localhost ruby] # sed '2,$d' ab           #删除第二行到最后一行

    显示某行

     [root@localhost ruby] # sed -n '1p' ab           #显示第一行 
     [root@localhost ruby] # sed -n '$p' ab           #显示最后一行
     [root@localhost ruby] # sed -n '1,2p' ab        #显示第一行到第二行
     [root@localhost ruby] # sed -n '2,$p' ab        #显示第二行到最后一行

　　使用模式进行查询

     [root@localhost ruby] # sed -n '/ruby/p' ab    #查询包括关键字ruby所在所有行
     [root@localhost ruby] # sed -n '/\$/p' ab        #查询包括关键字$所在所有行，使用反斜线\屏蔽特殊含义

　　增加一行或多行字符串

     [root@localhost ruby]# cat ab
     Hello!
     ruby is me,welcome to my blog.
     end
     [root@localhost ruby] # sed '1a drink tea' ab  #第一行后增加字符串"drink tea"
     Hello!
     drink tea
     ruby is me,welcome to my blog. 
     end
     [root@localhost ruby] # sed '1,3a drink tea' ab #第一行到第三行后增加字符串"drink tea"
     Hello!
     drink tea
     ruby is me,welcome to my blog.
     drink tea
     end
     drink tea
     [root@localhost ruby] # sed '1a drink tea\nor coffee' ab   #第一行后增加多行，使用换行符\n
     Hello!
     drink tea
     or coffee
     ruby is me,welcome to my blog.
     end

　　代替一行或多行

     [root@localhost ruby] # sed '1c Hi' ab                #第一行代替为Hi
     Hi
     ruby is me,welcome to my blog.
     end
     [root@localhost ruby] # sed '1,2c Hi' ab             #第一行到第二行代替为Hi
     Hi
     end

　　替换一行中的某部分

　　格式：sed 's/要替换的字符串/新的字符串/g'   （要替换的字符串可以用正则表达式）
     
    [root@localhost ruby] # sed -n '/ruby/p' ab | sed 's/ruby/bird/g'    #替换ruby为bird
    [root@localhost ruby] # sed -n '/ruby/p' ab | sed 's/ruby//g'        #删除ruby

    插入

    [root@localhost ruby] # sed -i '$a bye' ab         #在文件ab中最后行直接输入"bye"

    [root@localhost ruby]# cat ab
    Hello!
    ruby is me,welcome to my blog.
    end
    bye

    删除匹配行

    sed -i '/匹配字符串/d'  filename  （注：若匹配字符串是变量，则需要“”，不是‘’。记得好像是）

    替换匹配行中的某个字符串

    sed -i '/匹配字符串/s/替换源字符串/替换目标字符串/g' filename

## Windows10命令工具

### Windows10下如何查看哪些软件或进程占用了网速
    运行perfmon -res 即可。
 
### Windows10升级之后oem分区自动显示了
    可以将这个多出来的oem分区给隐藏起来，可以以管理员的方式打开cmd，然后输入以下命令行：
    mountvol G: /d

