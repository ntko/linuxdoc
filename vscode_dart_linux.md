### Linux下使用vscode开发Dart环境配置相关问题

#### Install Dart VM SDK:

> [REF:https://www.dartlang.org/tools/sdk#install](https://www.dartlang.org/tools/sdk#install)

#### Howto Use startup lib stagehand

    $ pub global activate stagehand
    $ stagehand console-full  //create console demo app.

> TIP: Because use flutter first, dart has been already installed with flutter pachage tool. and when examine the `/usr/lib/dart/bin`, we can find that `pub` is alreay there. so,just add this path to $PATH by adding to ~/.profile and run `$ .profile`. and also when cann't find the `stagehand` script.

    PATH="$PATH:/usr/lib/dart/bin"
    PATH="$PATH":"~/.pub-cache/bin"