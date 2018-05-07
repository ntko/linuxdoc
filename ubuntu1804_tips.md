### ubuntu linux 桌面技巧

##### 高分屏相关问题
* 高分屏需要通过system setting的display设定分辨率

##### 如何在崩溃后重启桌面

> 要重启桌面，按下Alt + F2 将会打开一个命令菜单，输入r并按下回车。

##### 桌面死机的处理

> CTRL+ALT+F1[F2]似乎是两个图形终端,CTRL+ALT+F3~F6是字符终端,可以用TOP命令查找,KILL XORG进程即可.

##### 图形处理软件GIMP安装失败报错相关依赖库无法安装

> 在Software & updates 设定中开启Canonical相关的软件即可找到.

##### How to disable animations in Ubuntu 17.10 or 18.04?

* To disable animations,first install Gnome Tweak Tool:

    `sudo apt install gnome-tweak-tool`

> Then launch tool either from command line by running
>
> gnome-tweak-tool or by using dash and searching for Tweak.
>
> On the first tab Appearance there is a toggle switch
>
> Animations. That's it!

![disable animations](imgs/disableanimation.png)

#### [6 Ways to Speed Up Your Ubuntu PC](https://www.howtogeek.com/115797/6-ways-to-speed-up-ubuntu/)

1. Install Preload: `sudo apt-get install preload`
1. Control Startup apps: DOCK->search startup,可以看到启动应用.如果要看到所有的系统启动应用,可以运行`sudo sed -i "s/NoDisplay=true/NoDisplay=false/g" /etc/xdg/autostart/*.desktop`,然后重新查看启用应用就可以看到系统应用了.
1. 使用更轻量级的桌面和应用.
1. setting里面关闭search
1. 编辑GRUB,加速系统启动.`sudo vi /etc/default/grub` Change the value of GRUB_TIMEOUT to 2,然后,`sudo update-grub2` 使改变生效.
1. 参考上面一条关闭动画.