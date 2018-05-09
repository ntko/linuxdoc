### ubuntu linux 桌面技巧

#### REF:

* [Things to do After Installing Ubuntu 18.04](https://itsfoss.com/things-to-do-after-installing-ubuntu-18-04/)
* [24 Must Have Essential Linux Applications](https://itsfoss.com/essential-linux-applications/)
* [Top 20 GNOME Extensions You Should Be Using Right Now](https://itsfoss.com/best-gnome-extensions/)

#### 高分屏相关问题
* 高分屏需要通过system setting的display设定分辨率

#### 如何在崩溃后重启桌面

> 要重启桌面，按下Alt + F2 将会打开一个命令菜单，输入r并按下回车。

#### 桌面死机的处理

> CTRL+ALT+F1[F2]似乎是两个图形终端,CTRL+ALT+F3~F6是字符终端,可以用TOP命令查找,KILL XORG进程即可.

#### 图形处理软件GIMP安装失败报错相关依赖库无法安装

> 在Software & updates 设定中开启Canonical相关的软件即可找到.

#### Ubuntu中设定点击DOCK图标最小化应用.

from: [http://tipsonubuntu.com/2018/04/15/click-icon-minimize-application-window-ubuntu-18-04/](http://tipsonubuntu.com/2018/04/15/click-icon-minimize-application-window-ubuntu-18-04/)

> 1. `gsettings set org.gnome.shell.extensions.dash-to-dock click-action 'minimize'|'previews'`  //其中preview是原始值
> 1. 以上可以使用`gsettings reset org.gnome.shell.extensions.dash-to-dock click-action`恢复.
> 1. 使用Dconf Editor软件.参考上面的值修改.

#### How to disable animations in Ubuntu 17.10 or 18.04?

* To disable animations,first install Gnome Tweak Tool:

    `sudo apt install gnome-tweak-tool`

> Then launch tool either from command line by running gnome-tweak-tool or by using dash and searching for Tweak. On the first tab Appearance there is a toggle switch Animations. That's it!

![disable animations](imgs/disableanimation.png)

#### 安装Sogou拼音再次卸载之后,软件更新报错

> 在用 sudo apt-get update 时出现这样的报错：

> W: GPG error: http://archive.ubuntukylin.com:10006/ubuntukylin xenial InRelease: The following signatures couldn't be verified because the public key is not available: NO_PUBKEY D259B7555E1D3C58

    E: The repository 'http://archive.ubuntukylin.com:10006/ubuntukylin xenial InRelease' is not signed.
    N: Updating from such a repository can't be done securely, and is therefore disabled by default.
    N: See apt-secure(8) manpage for repository creation and user configuration details.

解决方案:

>  `sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys <PUBKEY>`

这里 <PUBKEY> 为D259B7555E1D3C58

然后再

>  `sudo apt-get update`

#### [6 Ways to Speed Up Your Ubuntu PC](https://www.howtogeek.com/115797/6-ways-to-speed-up-ubuntu/)

1. Install Preload: `sudo apt-get install preload`
1. Control Startup apps: DOCK->search startup,可以看到启动应用.如果要看到所有的系统启动应用,可以运行`sudo sed -i "s/NoDisplay=true/NoDisplay=false/g" /etc/xdg/autostart/*.desktop`,然后重新查看启用应用就可以看到系统应用了.
1. 使用更轻量级的桌面和应用.
1. setting里面关闭search
1. 编辑GRUB,加速系统启动.`sudo vi /etc/default/grub` Change the value of GRUB_TIMEOUT to 2,然后,`sudo update-grub2` 使改变生效.
1. 参考上面一条关闭动画.

####  Enable additional repositories for more software

Ubuntu has several repositories from where it provides software for your system. These repositories are:

* Main – Free and open-source software supported by Ubuntu team
* Universe – Free and open-source software maintained by the community
* Restricted – Proprietary drivers for devices.
* Multiverse – Software restricted by copyright or legal issues.
* Canonical Partners – Software packaged by Ubuntu for their partners 
* Enabling all these repositories will give you access to more software and proprietary drivers.


#### 安装Gnome扩展

> `sudo apt install gnome-shell-extensions`
> 在软件库中有很多扩展,包括天气,网络,系统等.

#### 安装多媒体相关软件

> `sudo apt install ubuntu-restricted-extras`


#### 关于GDM问题(a stop job is running for session c1 of user root 1 min 30 s)

> `sudo vi /etc/systemd/system.conf`

找到DefaultTimeoutStopSec=90s  //此处修改为10S即可.

然后执行：systemctl daemon-reload

#### 创建指向文件夹的快捷方式到dock

> 参考资料:
* [Desktop Entry Specification](https://specifications.freedesktop.org/desktop-entry-spec/latest/index.html)
* [How To Add Shortcuts To Favorites In Gnome-Shell [Ubuntu]](https://geekitdown.com/how-to-add-shortcuts-to-favorites-in-gnome-shell-ubuntu/)


>  在`"/usr/share/applications"`目录下,创建`devprojects.desktop`文件:

    #!/usr/bin/env xdg-open
    [Desktop Entry]
    Version=1.0
    Type=Application
    Icon[en_US]=gnome-panel-launcher
    Exec=nautilus /home/tanger/devprojects
    Name[en_US]=devprojects
    Comment[en_US]=devprojects
    Name=devprojects
    Comment=devprojects
    Icon=gnome-panel-launcher

#### 在文件管理器中,`Ctrl+D`快捷键可加入书签

#### 在文件管理器中,点击右上角的 Newtab按钮可使用多个页签