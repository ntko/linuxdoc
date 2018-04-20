### linux Mint桌面技巧

#### 安装完毕之后的步骤

##### 高分屏相关问题
* 高分屏需要通过system setting的display设定分辨率
* 默认桌面窗口的边框阴影丑陋，需要通过system setting的preference的extensions安装
Better transparency for windows以及CUstom Shadows两个扩展即可
* 似乎是windows10主机安装了Intel驱动之后，就不再出现上述问题，还需要核实是否是Intel驱动没装引起的问题。

##### 中文输入相关问题
原始文档：[Linux Mint Fitcx中文输入法无候选框](http://www.voidcn.com/article/p-cueldmsk-gz.html "Linux Mint Fitcx中文输入法无候选框")

* 可以通过去掉qimpanel模块来实现,在终端中输入以下命令移除qimpanel模块:

    `sudo apt-get remove fcitx-ui-qimpanel`
    
> 移除完之后重新启动,在输入法切换到中文时就可以看到sunpinyin的提示,并且会弹出候选框列表,而且此时Fcitx配置中外观选项也出现了有效信息.
* 除了此方法以外还可以通过设置Fcitx的Addon选项来解决该问题即禁止Fcitx中Kimpanel的支持
