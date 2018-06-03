### ubuntu linux 桌面技巧

#### REF:

1. [Things to do After Installing Ubuntu 18.04](https://itsfoss.com/things-to-do-after-installing-ubuntu-18-04/)
1. [24 Must Have Essential Linux Applications](https://itsfoss.com/essential-linux-applications/)
1. [Top 20 GNOME Extensions You Should Be Using Right Now](https://itsfoss.com/best-gnome-extensions/)

#### 高分屏相关问题
1. 高分屏需要通过system setting的display设定分辨率

#### 如何在崩溃后重启桌面

> 要重启桌面，按下Alt + F2 将会打开一个命令菜单，输入r并按下回车。

#### 桌面死机的处理

> CTRL+ALT+F1[F2]似乎是两个图形终端,CTRL+ALT+F3~F6是字符终端,可以用TOP命令查找,KILL XORG进程即可.

#### 图形处理软件GIMP安装失败报错相关依赖库无法安装

> 在Software & updates 设定中开启Canonical相关的软件即可找到.

#### Ubuntu中设定点击DOCK图标最小化应用.

from: [http://tipsonubuntu.com/2018/04/15/click-icon-minimize-application-window-ubuntu-18-04/](http://tipsonubuntu.com/2018/04/15/click-icon-minimize-application-window-ubuntu-18-04/)

>    * `gsettings set org.gnome.shell.extensions.dash-to-dock click-action 'minimize'|'previews'`  //其中preview是原始值
>    * 以上可以使用`gsettings reset org.gnome.shell.extensions.dash-to-dock click-action`恢复.
>    * 使用Dconf Editor软件.参考上面的值修改.

#### How to disable animations in Ubuntu 17.10 or 18.04?

1. To disable animations,first install Gnome Tweak Tool:

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

1. Main – Free and open-source software supported by Ubuntu team
1. Universe – Free and open-source software maintained by the community
1. Restricted – Proprietary drivers for devices.
1. Multiverse – Software restricted by copyright or legal issues.
1. Canonical Partners – Software packaged by Ubuntu for their partners 
1. Enabling all these repositories will give you access to more software and proprietary drivers.


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
1. [Desktop Entry Specification](https://specifications.freedesktop.org/desktop-entry-spec/latest/index.html)
1. [How To Add Shortcuts To Favorites In Gnome-Shell [Ubuntu]](https://geekitdown.com/how-to-add-shortcuts-to-favorites-in-gnome-shell-ubuntu/)


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

#### 安装文件管理器扩展

> `sudo apt-get install nautilus-image-converter`


#### Ubuntu下的Chrome浏览器占用内存过多

> 关闭Setting里面的高级设定里面的GPU加速.

#### Linux下按进程实时统计网络带宽利用率

> 适用于Linux操作系统的开源网络监视工具.比如说,你可以用命令iftop来检查带宽使用情况. netstat用来查看接口统计报告,还有top监控系统当前运行进程.但是如果你想要找一个能够按进程实时统计网络带宽利用率,那么NetHogs就是你所需要的唯一工具.

`sudo nethogs`

#### User and group management related

> In GUI, Ubuntu software ,search `gnome-system-tools` and install;

OR

> `useradd` in command line.

##### /etc/passwd and /etc/shadow

> `cat /etc/passwd`

    tanger:x:1000:1000:tanger,,,:/home/tanger:/bin/bash
    postgres:x:121:127:PostgreSQL administrator,,,:/var/lib/postgresql:/bin/bash

The fields, in order from left to right, are:[1]

1. User name: the string a user would type in when logging into the operating system: the logname. Must be unique across users listed in the file.
1. Information used to validate a user's password; in most modern uses, this field is usually set to "x" (or "*", or some other indicator) with the actual password information being stored in a separate shadow password file. On Linux systems, setting this field to an asterisk ("*") is a common way to disable direct logins to an account while still preserving its name, while another possible value is "*NP*" which indicates to use an NIS server to obtain the password.[2] Without password shadowing in effect, this field would typically contain a cryptographic hash of the user's password (in combination with a salt).
1. user identifier number, used by the operating system for internal purposes. It need not be unique.
1. group identifier number, which identifies the primary group of the user; all files that are created by this user may initially be accessible to this group.
1. Gecos field, commentary that describes the person or account. Typically, this is a set of comma-separated values including the user's full name and contact details.
1. Path to the user's home directory.
1. Program that is started every time the user logs into the system. For an interactive user, this is usually one of the system's command line interpreters (shells).

> `sudo cat /etc/shadow`

    tanger:$1$EJkrNPNC$Xv2Mrg791YiK5hIml36tc1:17648:0:99999:7:::
    postgres:*:17683:0:99999:7:::

1. User login name
1. salt and hashed password OR a status exception value e.g.:
    * "$id$salt$hashed", the printable form of a password hash as produced by crypt (C), where "$id" is the algorithm used. (On GNU/Linux, "$1$" stands for MD5, "$2a$" is Blowfish, "$2y$" is Blowfish (correct handling of 8-bit chars), "$5$" is SHA-256 and "$6$" is SHA-512,[4] other Unix may have different values, like NetBSD. Key stretching is used to increase password cracking difficulty, using by default 1000 rounds of modified MD5,[5] 64 rounds of Blowfish, 5000 rounds of SHA-256 or SHA-512.[6] The number of rounds may be varied for Blowfish, or for SHA-256 and SHA-512 by using e.g. "$6$rounds=50000$".
    * Empty string – No password, the account has no password (reported by passwd on Solaris with "NP").[7]
    * "!" – the account is password locked, user will be unable to log in via password authentication but other methods (e.g. ssh key) may be still allowed.[8]
    * "*LK*" or "*" – the account is locked, user will be unable to log in via password authentication but other methods (e.g. ssh key) may be still allowed.[8]
    * "!!" – the password has never been set (RedHat)[9]
1. Days since epoch of last password change
1. Days until change allowed
1. Days before change required
1. Days warning for expiration
1. Days before account inactive
1. Days since epoch when account expires
Reserved    

##### change file/dir ownner,group,and permissions

    sudo chown postgres:adm postgresql-10-data.log 
    sudo chmod 640 postgresql-10-data.log
    sudo chown -R postgres:postgres data //where -R merns recursive