### Linux下使用vscode开发Dart环境配置相关问题

#### Install Dart VM SDK:

> [REF:https://www.dartlang.org/tools/sdk#install](https://www.dartlang.org/tools/sdk#install)

#### Howto Use startup lib stagehand

    $ pub global activate stagehand
    $ stagehand console-full  //create console demo app.

> TIP: Because use flutter first, dart has been already installed with flutter pachage tool. and when examine the `/usr/lib/dart/bin`, we can find that `pub` is alreay there. so,just add this path to $PATH by adding to ~/.profile and run `$ .profile`. and also when cann't find the `stagehand` script.

    PATH="$PATH:/usr/lib/dart/bin"
    PATH="$PATH":"~/.pub-cache/bin"

#### First web server powered by Aqueduct

* [SEE:https://aqueduct.io/](https://aqueduct.io/)

*  [ORIGINAL:Building RESTful Web APIs with Dart, Aqueduct, and PostgreSQL — Part 1](https://itnext.io/building-restful-web-apis-with-dart-aqueduct-and-postgresql-3cc9b931f777)

##### Aqueduct:

An object-oriented, multi-threaded HTTP framework mobile developers will love.

#####  install Aqueduct:

    pub global activate aqueduct

#####  Change to working directory and create our project:

    aqueduct create websvr && cd websvr    

We should now be in the websvr directory with all the project files. For now we’ll focus on:

    bin/
    main.dart
    lib/
    fave_reads_sink.dart
    pubspec.yaml

**`bin/main.dart`** creates our server and starts the app
**`lib/fave_reads_sink.dart`** sets up your application with its configuration
**`pubspec.yaml`** contains metadata about the project. Similar to having a **`package.json`** for **`Node.js`** development. Now we can start the application using either commands below:

    aqueduct serve # or `dart bin/main.dart`

> TIP: Instead, `aqueduct serve` and `dart bin/main.dart` have different behaviors. It seems `aqueduct serve` always listen to the port 8081(or through `config.yaml` may be?), although we specified 8080:

    ..configuration.port = 8080;

![aqueduct serve listen on port 8081](imgs/aqueductserve.png)

##### About the "'unnecessary_brace_in_string_interp' is not a recognized lint rule" lint message

just put a `#` in front of the line as comment.

