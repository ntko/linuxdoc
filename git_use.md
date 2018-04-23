### git使用问题
#### git config 以及 --glocal 和 --system 有什么不同
[git config 以及 --glocal 和 --system](https://www.daixiaorui.com/read/240.html "git config 以及 --glocal 和 --system的区别")    
1. `git config` config the file in the Git directory. (that is, .git/config) file.
1. `git config --glocal` config global config specified to you. (~/.gitconfig or ~/.config/git/config) file.
1. `git config --system` config for all users in system. (/etc/gitconfig) file.

    Mostly, we use `git config --global`
    
#### 配置git
    $ git config --global user.name "Last First"
    $ git config --global user.email fakeuser@msn.com
    
> 使用 `git config --global -e` 可以查看config文件所在的位置。

> 在linux mint上，global的位置为：/home/`current_username`/.gitconfig

> 使用`git config --list`可以查看当前配置。

#### 初始化git repository

> 使用 `$ git init` 可以将当前目录初始化为git repository

> 使用 `$ git clone https://github.com/libgit2/libgit2` 从远程仓库初始化.
