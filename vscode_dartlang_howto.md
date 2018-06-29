<!-- TOC -->

- [Dart commonly used operations howto](#dart-commonly-used-operations-howto)
    - [files op support](#files-op-support)
        - [Reading a file](#reading-a-file)
        - [Writing a file](#writing-a-file)
    - [Getting environment information](#getting-environment-information)
    - [Setting exit codes](#setting-exit-codes)

<!-- /TOC -->
# Dart commonly used operations howto

## files op support

### Reading a file

    Directory current = Directory.current;
    print('current Directory:$current');
    var configPath = current.path + '/bin/config.txt';
    var config = new File(configPath);
    int lineNumber = 1;
    Stream<List<int>> inputStream = config.openRead();
    var lines = inputStream.transform(utf8.decoder).transform(new LineSplitter());
    try {
      await for (var line in lines) {
        if (showLineNumbers) {
          stdout.write('--${lineNumber++} ');
        }
        stdout.writeln(line);
      }
    } catch (e) {
      _handleError(configPath);
      stderr.writeln(e);
    }

### Writing a file

The easiest way to write text to a file is to create a File object and use the `writeAsString()` method:

    File quotesFile = new File('quotes.txt');
    String stronger = 'That which does not kill us makes us stronger. -Nietzsche';

    try {
      await quotesFile.writeAsString(stronger, mode: FileMode.append);
      print('Data written.');
    } catch (e) {
      print('Oops!');
    }
    
The writeAsString() method writes the data asynchronously. It opens the file before writing and closes the file when done. To append data to an existing file, you can use the optional parameter mode and set its value to FileMode.append. Otherwise, the mode is FileMode.write and the previous contents of the file, if any, are overwritten.

If you want to write more data, you can open the file for writing. The openWrite() method returns an IOSink (the same type as stdin and stderr). You can continue to write to the file until done, at which time, you must close the file. The close() method is asynchronous and returns a Future.

    IOSink quotes = new File('quotes.txt').openWrite(mode: FileMode.append);

    quotes.write('A woman is like a tea bag; ');
    quotes.write('you never know how strong it is until it\'s in hot water.');
    quotes.writeln(' -Eleanor Roosevelt');
    await quotes.close();
    print('Done!');

## Getting environment information
Use the Platform class to get information about the machine and OS that the program is running on. 
> Note: Use the Platform class from the dart:io library, not from the dart:html library.

Platform.environment provides a copy of the environment variables in an immutable map. If you need a mutable map (modifiable copy) you can use `Map.from(Platform.environment)`.

    Map environmentVars = Platform.environment;

    print('PWD = ${environmentVars["PWD"]}');
    print('LOGNAME = ${environmentVars["LOGNAME"]}');
    print('PATH = ${environmentVars["PATH"]}');

Platform provides other useful properties that give information about the machine, OS, and currently running program. For example:

    Platform.isMacOS()
    Platform.numberOfProcessors
    Platform.script.path

## Setting exit codes
The dart:io library defines a top-level property, `exitCode`, that you can change to set the exit code for the current invocation of the Dart VM. An exit code is a number passed from the Dart program to the parent process to indicate the success, failure, or other state of the execution of the program.

The dcat program sets the exit code in the _handleError() function to indicate that an error occcurred during execution.

    Future _handleError(String path) async {
      if (await FileSystemEntity.isDirectory(path)) {
        stderr.writeln('error: $path is a directory');
      } else {
        exitCode = 2;
      }
    }
    
An exit code of 2 indicates that the program encountered an error.

An alternative to using exitCode is to use the top-level `exit()` function, which sets the exit code and quits the program immediately. For example, the _handleError() function could call `exit(2)` instead of setting exitCode to 2, but exit() would quit the program and it might not process all of the files on the command line.

Generally speaking, you are better off using the exitCode property, which sets the exit code but allows the program to continue through to its natural completion.

Although you can use any number for an exit code, by convention, the codes in the table below have the following meanings:

    Code	Meaning
---
    0	    Success
    1	    Warnings
    2	    Errors