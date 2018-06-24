<!-- TOC -->

- [git使用问题](#git使用问题)
    - [git config 以及 --glocal 和 --system 有什么不同](#git-config-以及---glocal-和---system-有什么不同)
    - [配置git](#配置git)
    - [初始化git repository](#初始化git-repository)
    - [Caching your GitHub password in Git](#caching-your-github-password-in-git)
    - [Using credential helpers to cache passwords](#using-credential-helpers-to-cache-passwords)
    - [create a new repository on the command line](#create-a-new-repository-on-the-command-line)
    - [push an existing repository from the command line](#push-an-existing-repository-from-the-command-line)
    - [Meaning of the GitHub message: push declined due to email privacy restrictions](#meaning-of-the-github-message-push-declined-due-to-email-privacy-restrictions)
    - [.gitignore FILE](#gitignore-file)
    - [Delete File](#delete-file)
    - [Moving Files](#moving-files)
    - [Inspecting a Remote](#inspecting-a-remote)

<!-- /TOC -->

## git使用问题

### git config 以及 --glocal 和 --system 有什么不同
[git config 以及 --glocal 和 --system](https://www.daixiaorui.com/read/240.html "git config 以及 --glocal 和 --system的区别")    
1. `git config` config the file in the Git directory. (that is, .git/config) file.
1. `git config --glocal` config global config specified to you. (~/.gitconfig or ~/.config/git/config) file.
1. `git config --system` config for all users in system. (/etc/gitconfig) file.

    Mostly, we use `git config --global`
    
### 配置git

    $ git config --global user.name "Last First"
    $ git config --global user.email fakeuser@msn.com
    
> 使用 `git config --global -e` 可以查看config文件所在的位置。

> 在linux mint上，global的位置为：/home/`current_username`/.gitconfig

> 使用`git config --list`可以查看当前配置。

### 初始化git repository

> 使用 `$ git init` 可以将当前目录初始化为git repository

> 使用 `$ git clone https://github.com/libgit2/libgit2` 从远程仓库初始化.

### Caching your GitHub password in Git

> 1. In Terminal, enter the following:

    $ git config --global credential.helper cache
    # Set git to use the credential memory cache

> 2. To change the default password cache timeout, enter the following:

    $ git config --global credential.helper 'cache --timeout=3600'
    # Set the cache to timeout after 1 hour (setting is in seconds)

if we use github and don't want to enter password anyway, use this:

    git remote set-url origin https://<USERNAME>:<PASSWORD>@github.com/yourusername/repo.git

### Using credential helpers to cache passwords

> [REF:https://git.seveas.net/using-credential-helpers-to-cache-passwords.html](https://git.seveas.net/using-credential-helpers-to-cache-passwords.html)

While the cache helper is certainly useful, it still makes you type in your password regularly. There are a few other helpers that actually store your password on disk, some more secure than others.

    git config --global credential.helper store
    git config --global credential.helper netrc

The store and netrc helpers use unencrypted plain-text files for storing credentials. The store helper has its own format, the netrc helper will read your .netrc file. These are useful if you cannot use any of the credential helpers below, which all require a desktop environment.

    git config --global credential.helper store wincred
    git config --global credential.helper store osxkeychain
    git config --global credential.helper store gnome-keyring

The wincred, osxkeychain and gnome-keyring credential helpers integrate with the secure credential storage provided by Windows, OSX and Gnome. These are the preferred credential helpers as they never store passwords unencrypted.

### create a new repository on the command line

    echo "# vscodeFirst" >> README.md
    git init
    git add README.md
    git commit -m "first commit"
    git remote add origin https://github.com/ntko/vscodeFirst.git
    git push -u origin master

###  push an existing repository from the command line

    git remote add origin https://github.com/ntko/vscodeFirst.git
    git push -u origin master


### Meaning of the GitHub message: push declined due to email privacy restrictions

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

### .gitignore FILE

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

### Delete File

To remove a file from Git, you have to remove it from your tracked files (more accurately, remove it from your staging area) and then commit. The git rm command does that, and also removes the file from your working directory so you don’t see it as an untracked file the next time around.

If you simply remove the file from your working directory, it shows up under the “Changes not staged for commit”

    $ rm PROJECTS.md

Then, if you run git rm, it stages the file’s removal.

    $ git rm PROJECTS.md

Another useful thing you may want to do is to keep the file in your working tree but remove it from your staging area. In other words, you may want to keep the file on your hard drive but not have Git track it anymore. This is particularly useful if you forgot to add something to your .gitignore file and accidentally staged it, like a large log file or a bunch of .a compiled files. To do this, use the --cached option:

    $ git rm --cached README

You can pass files, directories, and file-glob patterns to the git rm command. That means you can do
things such as:

    $ git rm log/\*.log

Note the backslash (\) in front of the *. This is necessary because Git does its own filename expansion in addition to your shell’s filename expansion. This command removes all files that have the .log extension in the log/ directory. Or, you can do something like this:

    $ git rm \*~

This command removes all files whose names end with a ~.

### Moving Files

Unlike many other VCS systems, Git doesn’t explicitly track file movement. If you rename a file in Git, no metadata is stored in Git that tells it you renamed the file. However, Git is pretty smart about figuring that out after the fact — we’ll deal with detecting file movement a bit later. Thus it’s a bit confusing that Git has a mv command. If you want to rename a file in Git, you can run something like:

    $ git mv README.md README 

However, this is equivalent to running something like this:

    $ mv README.md README
    $ git rm README.md
    $ git add README    

### Inspecting a Remote

    $ git remote show origin