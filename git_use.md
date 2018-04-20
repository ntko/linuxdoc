### git使用问题
#### git config 以及 --glocal 和 --system 有什么不同
[git config 以及 --glocal 和 --system](https://www.daixiaorui.com/read/240.html "git config 以及 --glocal 和 --system的区别")    
1. `git config` config the file in the Git directory. (that is, .git/config) file.
1. `git config --glocal` config global config specified to you. (~/.gitconfig or ~/.config/git/config) file.
1. `git config --system` config for all users in system. (/etc/gitconfig) file.

    Mostly, we use `git config --global`
    
#### 初始化git
    $ git config --global user.name "Last First"
    $ git config --global user.email fakeuser@msn.com
    
> 使用 `git config --global -e` 可以查看config文件所在的位置。
> 在linux mint上，global的位置为：/home/`current_username`/.gitconfig
