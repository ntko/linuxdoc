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

#### create a new repository on the command line

    echo "# vscodeFirst" >> README.md
    git init
    git add README.md
    git commit -m "first commit"
    git remote add origin https://github.com/ntko/vscodeFirst.git
    git push -u origin master

####  push an existing repository from the command line

    git remote add origin https://github.com/ntko/vscodeFirst.git
    git push -u origin master


#### Meaning of the GitHub message: push declined due to email privacy restrictions

ORIGIN: [This information is from stackoberflow](https://stackoverflow.com/questions/43378060/meaning-of-the-github-message-push-declined-due-to-email-privacy-restrictions)

> cause: The remote repository has been configured to disallow you pushing a commit that would reveal your personal e-mail address. For example in GitHub you have checked the Block command line pushes that expose my email checkbox to enable this.

1. You can see your personal e-mail address, which is used by default for your commits in Git:

    `git config --global user.email`

1. Find your GitHub noreply address in your GitHub's [Personal Settings → Emails](https://github.com/settings/emails). It's mentioned in the description of the Keep my email address private checkbox. Usually, it starts with a unique identifier, plus your username:

    `{ID}+{username}@users.noreply.github.com`

1. Change the global user e-mail address setting to be your GitHub noreply address:

    `git config --global user.email {ID}+{username}@users.noreply.github.com`

1. Reset the author information on your last commit:

    `git commit --amend --reset-author`

    If you have multiple commits with your private e-mail address, see this [answer](https://stackoverflow.com/a/25815116/146622).

1. Now you can push the commit with the noreply e-mail address, and future commits will have the noreply e-mail address as well.

     `git push`

#### .gitignore FILE

> [A collection of useful .gitignore templates](https://github.com/github/gitignore)

> 用来配置哪些文件将被忽略.一个示例文件如下:

>

    # ignore all .a or .o files
    *.[oa]

    # ignore files end with ~
    *~

    # but do track lib.a, even though you're ignoring .a files above
    !lib.a

    # only ignore the TODO file in the current directory, not subdir/TODO
    /TODO

    # ignore all files in the build/ directory
    build/

    # ignore doc/notes.txt, but not doc/server/arch.txt
    doc/*.txt

    # ignore all .pdf files in the doc/ directory and any of its subdirectories
    doc/**/*.pdf
