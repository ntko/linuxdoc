<!-- TOC -->

- [Linux下使用vscode开发Dart环境配置相关问题](#linux下使用vscode开发dart环境配置相关问题)
    - [Install Dart VM SDK:](#install-dart-vm-sdk)
    - [Install Dart vscode plugin](#install-dart-vscode-plugin)
    - [Install Markdown-TOC plugin for markdown file](#install-markdown-toc-plugin-for-markdown-file)
    - [Howto Use startup lib stagehand](#howto-use-startup-lib-stagehand)
    - [DartLang Basic](#dartlang-basic)
    - [Final and const](#final-and-const)
    - [Numbers](#numbers)
        - [int](#int)
        - [double](#double)
    - [Strings](#strings)
    - [Lists](#lists)
    - [Maps](#maps)
    - [Runes](#runes)
    - [How do I reverse a String in Dart?](#how-do-i-reverse-a-string-in-dart)
    - [Symbols](#symbols)
    - [Functions](#functions)
        - [The main() function](#the-main-function)
        - [Functions Basic](#functions-basic)
        - [Optional parameters](#optional-parameters)
            - [Optional named parameters](#optional-named-parameters)
            - [Optional positional parameters](#optional-positional-parameters)
        - [Functions as first-class objects](#functions-as-first-class-objects)
        - [Anonymous functions](#anonymous-functions)
        - [Lexical closures](#lexical-closures)
        - [Testing functions for equality](#testing-functions-for-equality)
    - [Operators](#operators)
    - [Conditional expressions](#conditional-expressions)
    - [Cascade notation (..)](#cascade-notation-)
    - [Control flow statements](#control-flow-statements)
        - [Switch and case](#switch-and-case)
    - [Exceptions](#exceptions)
        - [Throw](#throw)
        - [Catch](#catch)
        - [Finally](#finally)
    - [Classes](#classes)
        - [Instance variables](#instance-variables)
        - [Constructors Basic](#constructors-basic)
        - [Default constructors](#default-constructors)
        - [Named constructors](#named-constructors)
        - [Invoking a non-default superclass constructor](#invoking-a-non-default-superclass-constructor)
        - [Initializer list](#initializer-list)
        - [Redirecting constructors](#redirecting-constructors)
        - [Constant constructors](#constant-constructors)
        - [Factory constructors](#factory-constructors)
        - [Instance methods](#instance-methods)
        - [Getters and setters](#getters-and-setters)
        - [Abstract classes and Abstract methods](#abstract-classes-and-abstract-methods)
        - [Overridable operators](#overridable-operators)
        - [Implementing map keys](#implementing-map-keys)
        - [Implicit interfaces](#implicit-interfaces)
        - [Extending a class](#extending-a-class)
        - [noSuchMethod()](#nosuchmethod)
        - [Enumerated types](#enumerated-types)
            - [Using enums](#using-enums)
        - [Adding features to a class: mixins](#adding-features-to-a-class-mixins)
        - [Static variables and methods](#static-variables-and-methods)
    - [Generics](#generics)
        - [Using collection literals](#using-collection-literals)
        - [Using parameterized types with constructors](#using-parameterized-types-with-constructors)
        - [Generic collections and the types they contain](#generic-collections-and-the-types-they-contain)
        - [Restricting the parameterized type](#restricting-the-parameterized-type)
        - [Using generic methods](#using-generic-methods)
    - [Libraries and visibility](#libraries-and-visibility)
        - [Using libraries](#using-libraries)
        - [Specifying a library prefix](#specifying-a-library-prefix)
        - [Importing only part of a library](#importing-only-part-of-a-library)
        - [Lazily loading a library](#lazily-loading-a-library)
        - [Implementing libraries](#implementing-libraries)
    - [Handling Futures](#handling-futures)
        - [Declaring async functions](#declaring-async-functions)
    - [Handling Streams](#handling-streams)
    - [Generators](#generators)
        - [Synchronous Generators](#synchronous-generators)
        - [Asynchronous Generators](#asynchronous-generators)
        - [Generators use recursive code](#generators-use-recursive-code)
    - [Callable classes](#callable-classes)
        - [The call() method](#the-call-method)
        - [How does it work?](#how-does-it-work)
        - [The apply() method](#the-apply-method)
        - [Symbols](#symbols-1)
        - [Function types](#function-types)
    - [Isolates](#isolates)
    - [Typedefs](#typedefs)

<!-- /TOC -->

## Linux下使用vscode开发Dart环境配置相关问题

### Install Dart VM SDK:

> [REF:https://www.dartlang.org/tools/sdk#install](https://www.dartlang.org/tools/sdk#install)

### Install Dart vscode plugin

* Start VS Code
* Invoke View>Command Palette…
* Type ‘install’, and select the ‘Extensions: Install Extension’ action
* Enter flutter in the search field, select ‘Dart’ in the list, and click Install
* Select ‘OK’ to reload VS Code

### Install Markdown-TOC plugin for markdown file

* alanwalk.markdown-toc

### Howto Use startup lib stagehand

    $ pub global activate stagehand
    $ stagehand console-full  //create console demo app.

> TIP`:Because use flutter first, dart has been already installed with flutter pachage tool. and when examine the `/usr/lib/dart/bin`, we can find that `pub` is alreay there. so,just add this path to $PATH by adding to ~/.profile and run `$ .profile`. and also when cann't find the `stagehand` script.

    PATH="$PATH:/usr/lib/dart/bin"
    PATH="$PATH":"~/.pub-cache/bin"

### DartLang Basic

> Note: The assert() call is ignored in production code. During development, assert(condition) throws an exception unless condition is true.

### Final and const

If you never intend to change a variable, use final or const, either **instead of var** or **in addition to** a type. A final variable can be set only once; a const variable is a compile-time constant. (Const variables are implicitly final.) A final top-level or class variable is initialized the first time it’s used.

Here’s an example of creating and setting a final variable:

    final name = 'Bob'; // Without a type annotation
    // name = 'Alice';  // Uncommenting this causes an error
    final String nickname = 'Bobby';

Use const for variables that you want to be compile-time constants. If the const variable is at the class level, mark it **`static const`**. Where you declare the variable, set the value to a compile-time constant such as a number or string literal, a const variable, or the result of an arithmetic operation on constant numbers:

    const bar = 1000000; // Unit of pressure (dynes/cm2)
    const double atm = 1.01325 * bar; // Standard atmosphere

> Note: Instance variables can be final but not const.

Built-in types
The Dart language has special support for the following types:

* numbers
* strings
* booleans
* lists (also known as arrays)
* maps
* runes (for expressing Unicode characters in a string)
* symbols

### Numbers
Dart numbers come in two flavors:

#### int
Integer values no larger than 64 bits, depending on the platform. On the Dart VM, values can be from -263 to 263 - 1. Dart that’s compiled to JavaScript uses JavaScript numbers, allowing values from -253 to 253 - 1.

#### double
64-bit (double-precision) floating-point numbers, as specified by the IEEE 754 standard.

Both int and double are subtypes of `num`. The num type includes basic operators such as +, -, /, and *, and is also where you’ll find abs(), ceil(), and floor(), among other methods. (Bitwise operators, such as >>, are defined in the int class.) If num and its subtypes don’t have what you’re looking for, the dart:math library might.

    int x = 1;
    int hex = 0xDEADBEEF;
    
If a number includes a decimal, it is a double. Here are some examples of defining double literals:

    double y = 1.1;
    double exponents = 1.42e5;

Here’s how you turn a string into a number, or vice versa:

    // String -> int
    var one = int.parse('1');
    assert(one == 1);

    // String -> double
    var onePointOne = double.parse('1.1');
    assert(onePointOne == 1.1);

    // int -> String
    String oneAsString = 1.toString();
    assert(oneAsString == '1');

    // double -> String
    String piAsString = 3.14159.toStringAsFixed(2);
    assert(piAsString == '3.14');

### Strings

A Dart string is a sequence of UTF-16 code units. You can use either single or double quotes to create a string:

### Lists
Perhaps the most common collection in nearly every programming language is the array, or ordered group of objects. In Dart, arrays are List objects, so most people just call them lists.

Dart list literals look like JavaScript array literals. Here’s a simple Dart list:

    var list = [1, 2, 3];
Note: The analyzer infers that list has type List<int>. If you try to add non-integer objects to this list, the analyzer or runtime raises an error. For more information, read about **`type inference`**.

Lists use zero-based indexing, where 0 is the index of the first element and list.length - 1 is the index of the last element. You can get a list’s length and refer to list elements just as you would in JavaScript:

    var list = [1, 2, 3];
    assert(list.length == 3);
    assert(list[1] == 2);

    list[1] = 1;
    assert(list[1] == 1);
To create a list that’s a compile-time constant, add const before the list literal:

    var constantList = const [1, 2, 3];
    // constantList[1] = 1; // Uncommenting this causes an error.

### Maps
In general, a map is an object that associates keys and values. Both keys and values can be any type of object. Each key occurs only once, but you can use the same value multiple times. Dart support for maps is provided by map literals and the Map type.

Here are a couple of simple Dart maps, created using map literals:

    var gifts = {
      // Key:    Value
      'first': 'partridge',
      'second': 'turtledoves',
      'fifth': 'golden rings'
    };

    var nobleGases = {
      2: 'helium',
      10: 'neon',
      18: 'argon',
    };
> Note: The analyzer infers that gifts has the type Map<String, String> and nobleGases has the type Map<int, String>. If you try to add the wrong type of value to either map, the analyzer or runtime raises an error. For more information, read about type inference.

You can create the same objects using a Map constructor:

    var gifts = new Map();
    gifts['first'] = 'partridge';
    gifts['second'] = 'turtledoves';
    gifts['fifth'] = 'golden rings';

    var nobleGases = new Map();
    nobleGases[2] = 'helium';
    nobleGases[10] = 'neon';
    nobleGases[18] = 'argon';

Add a new key-value pair to an existing map just as you would in JavaScript:

    var gifts = {'first': 'partridge'};
    gifts['fourth'] = 'calling birds'; // Add a key-value pair
Retrieve a value from a map the same way you would in JavaScript:

    var gifts = {'first': 'partridge'};
    assert(gifts['first'] == 'partridge');

If you look for a key that isn’t in a map, you get a null in return:

    var gifts = {'first': 'partridge'};
    assert(gifts['fifth'] == null);

Use .length to get the number of key-value pairs in the map:

    var gifts = {'first': 'partridge'};
    gifts['fourth'] = 'calling birds';
    assert(gifts.length == 2);

To create a map that’s a compile-time constant, add const before the map literal:

    final constantMap = const {
        2: 'helium',
        10: 'neon',
        18: 'argon',
    };

    // constantMap[2] = 'Helium'; // Uncommenting this causes an error.

### Runes
In Dart, runes are the UTF-32 code points of a string.

Unicode defines a unique numeric value for each letter, digit, and symbol used in all of the world’s writing systems. Because a Dart string is a sequence of UTF-16 code units, expressing 32-bit Unicode values within a string requires special syntax.

The usual way to express a Unicode code point is \uXXXX, where XXXX is a 4-digit hexidecimal value. For example, the heart character (♥) is \u2665. To specify more or less than 4 hex digits, place the value in curly brackets. For example, the laughing emoji (😆) is \u{1f600}.

The String class has several properties you can use to extract rune information. The codeUnitAt and codeUnit properties return 16-bit code units. Use the runes property to get the runes of a string.

The following example illustrates the relationship between runes, 16-bit code units, and 32-bit code points:

    main() {
      var clapping = '\u{1f44f}';
      print(clapping);
      print(clapping.codeUnits);
      print(clapping.runes.toList());

      Runes input = new Runes(
          '\u2665  \u{1f605}  \u{1f60e}  \u{1f47b}  \u{1f596}  \u{1f44d}');
      print(new String.fromCharCodes(input));
    }

> Note: Be careful when manipulating runes using list operations. This approach can easily break down, depending on the particular language, character set, and operation. For more information, see How do I reverse a String in Dart? on Stack Overflow.

### How do I reverse a String in Dart?

    var input = "Music \u{1d11e} for the win"; // Music 𝄞 for the win
    print(input.split('').reversed.join()); // niw eht rof

The split function explicitly warns against this problem (with an example):

> Splitting with an empty string pattern ('') splits at UTF-16 code unit boundaries and not at rune boundaries[.]

There is an easy fix for this: instead of reversing the individual code-units one can reverse the runes:

    var input = "Music \u{1d11e} for the win"; // Music 𝄞 for the win
    print(new String.fromCharCodes(input.runes.toList().reversed)); // niw eht rof 𝄞 cisuM

But that's not all. Runes, too, can have a specific order. This second obstacle is much harder to solve. A simple example:

    var input =  'Ame\u{301}lie'; // Amélie
    print(new String.fromCharCodes(input.runes.toList().reversed)); // eiĺemA
Note that the accent is on the wrong character.

### Symbols
A Symbol object represents an operator or identifier declared in a Dart program. You might never need to use symbols, but they’re invaluable for APIs that refer to identifiers by name, because minification changes identifier names but not identifier symbols.

To get the symbol for an identifier, use a symbol literal, which is just # followed by the identifier:

    #radix
    #bar
Symbol literals are compile-time constants.

### Functions

#### The main() function
Every app must have a top-level main() function, which serves as the entrypoint to the app. The main() function returns void and has an optional List<String> parameter for arguments.

Here’s an example of the main() function for a web app:

    void main() {
      querySelector('#sample_text_id')
        ..text = 'Click me!'
        ..onClick.listen(reverseText);
    }

> Note: The `..` syntax in the preceding code is called a cascade. With cascades, you can perform multiple operations on the members of a single object.

Here’s an example of the main() function for a command-line app that takes arguments:

    // Run the app like this: dart args.dart 1 test
    void main(List<String> arguments) {
      print(arguments);

      assert(arguments.length == 2);
      assert(int.parse(arguments[0]) == 1);
      assert(arguments[1] == 'test');
    }

#### Functions Basic

Dart is a true object-oriented language, so even functions are objects and have a type, Function. This means that functions can be assigned to variables or passed as arguments to other functions. You can also call an instance of a Dart class as if it were a function. For details, see `Callable classes`.

Here’s an example of implementing a function:

    bool isNoble(int atomicNumber) {
      return _nobleGases[atomicNumber] != null;
    }
Although Effective Dart recommends `type annotations for public APIs`, the function still works if you omit the types:

    isNoble(atomicNumber) {
      return _nobleGases[atomicNumber] != null;
    }
For functions that contain just one expression, you can use a shorthand syntax:

    bool isNoble(int atomicNumber) => _nobleGases[atomicNumber] != null;

The => expr syntax is a shorthand for { return expr; }. The => notation is sometimes referred to as **`fat arrow syntax`**.

> Note: Only an expression—not a statement—can appear between the arrow (=>) and the semicolon (;). For example, you can’t put an if statement there, but you can use a conditional expression.

A function can have two types of parameters: required and optional. The required parameters are listed first, followed by any optional parameters.

#### Optional parameters
Optional parameters can be either positional or named, **but not both**.

##### Optional named parameters

When defining a function, use **`{param1, param2, …}`** to specify named parameters:

    /// Sets the [bold] and [hidden] flags ...
    void enableFlags({bool bold, bool hidden}) {
      // ...
    }

When calling a function, you can specify named parameters using paramName: value. For example:

    enableFlags(bold: true, hidden: false);

default values for named parameters:

    /// Sets the [bold] and [hidden] flags ...
    void enableFlags({bool bold = false, bool hidden = false}) {
      // ...
    }

    // bold will be true; hidden will be false.
    enableFlags(bold: true);    

##### Optional positional parameters
Wrapping a set of function parameters **`in [] marks`** them as optional positional parameters:

    String say(String from, String msg, [String device]) {
      var result = '$from says $msg';
      if (device != null) {
        result = '$result with a $device';
      }
      return result;
    }
Here’s an example of calling this function without the optional parameter:

    assert(say('Bob', 'Howdy') == 'Bob says Howdy');

default values for positional parameters:

    String say(String from, String msg,
        [String device = 'carrier pigeon', String mood]) {
      var result = '$from says $msg';
      if (device != null) {
        result = '$result with a $device';
      }
      if (mood != null) {
        result = '$result (in a $mood mood)';
      }
      return result;
    }   

> You can also pass lists or maps as default values. The following example defines a function, doStuff(), that specifies a default list for the list parameter and a default map for the gifts parameter.

    void doStuff(
        {List<int> list = const [1, 2, 3],
        Map<String, String> gifts = const {
          'first': 'paper',
          'second': 'cotton',
          'third': 'leather'
        }}) {
      print('list:  $list');
      print('gifts: $gifts');
    }    

#### Functions as first-class objects
You can pass a function as a parameter to another function. For example:

    void printElement(int element) {
      print(element);
    }

    var list = [1, 2, 3];

    // Pass printElement as a parameter.
    list.forEach(printElement);

> TIP:when we say `first-class-object`,means the function is `AS SAME AS VARIABLE`,can be assgined to variables, or, as be passed as parameter to other functions.

You can also assign a function to a variable, such as:

    var loudify = (msg) => '!!! ${msg.toUpperCase()} !!!';
    assert(loudify('hello') == '!!! HELLO !!!');

This example uses an anonymous function. More about those in the next section.

#### Anonymous functions

Most functions are named, such as main() or printElement(). You can also create a nameless function called an anonymous function, or sometimes a lambda or closure. You might assign an anonymous function to a variable so that, for example, you can add or remove it from a collection.

An anonymous function looks similar to a named function— zero or more parameters, separated by commas and optional type annotations, between parentheses.

The code block that follows contains the function’s body:

    ([[Type] param1[, …]]) { 
      codeBlock; 
    }; 

The following example defines an anonymous function with an untyped parameter, item. The function, invoked for each item in the list, prints a string that includes the value at the specified index.

    var list = ['apples', 'bananas', 'oranges'];
    list.forEach((item) {
      print('${list.indexOf(item)}: $item');
    });

#### Lexical closures

A **`closure`** is a function object that has access to variables in its lexical scope, even when the function is used outside of its original scope.

Functions can close over variables defined in surrounding scopes. In the following example, makeAdder() captures the variable addBy. Wherever the returned function goes, it remembers addBy.

    /// Returns a function that adds [addBy] to the
    /// function's argument.
    Function makeAdder(num addBy) {
        return (num i) => addBy + i;
    }

    void main() {
      // Create a function that adds 2.
      var add2 = makeAdder(2);

      // Create a function that adds 4.
      var add4 = makeAdder(4);

      assert(add2(3) == 5);
      assert(add4(3) == 7);
    }

#### Testing functions for equality

Here’s an example of testing top-level functions, static methods, and instance methods for equality:

    void foo() {} // A top-level function

    class A {
      static void bar() {} // A static method
      void baz() {} // An instance method
    }

    void main() {
      var x;

      // Comparing top-level functions.
      x = foo;
      assert(foo == x);

      // Comparing static methods.
      x = A.bar;
      assert(A.bar == x);

      // Comparing instance methods.
      var v = new A(); // Instance #1 of A
      var w = new A(); // Instance #2 of A
      var y = w;
      x = w.baz;

      // These closures refer to the same instance (#2),
      // so they're equal.
      assert(y.baz == x);

      // These closures refer to different instances,
      // so they're unequal.
      assert(v.baz != w.baz);
    }

### Operators    

In dart, there are some unique(unusual) Operators. for example:

* `??`  (if null)
* `..`  (cascade)
* `??=` (assignment)
* `~/`	Divide, returning an integer result
* `?.`	Conditional member access Like ., but the leftmost operand can be null; 

example: 

    var a = foo?.bar;

selects property bar from expression foo unless foo is null (in which case the value of foo?.bar is null)

And type test operators:

* `as`	 Typecast
* `is`	 True if the object has the specified type
* `is!`	 False if the object has the specified type


examples:

    // Assign value to b if b is null; otherwise, b stays the same
    b ??= value;

    assert(5 / 2 == 2.5); // Result is a double
    assert(5 ~/ 2 == 2); // Result is an int
    assert(5 % 2 == 1); // Remainder
    assert('5/2 = ${5~/2} r ${5%2}' == '5/2 = 2 r 1'); 

### Conditional expressions

Dart has two operators that let you concisely evaluate expressions that might otherwise require if-else statements:

> `condition ? expr1 : expr2`

If condition is true, evaluates expr1 (and returns its value); otherwise, evaluates and returns the value of expr2.

> `expr1 ?? expr2`

If expr1 is non-null, returns its value; otherwise, evaluates and returns the value of expr2.

> When you need to assign a value based on a boolean expression, consider using ?:.

    var visibility = isPublic ? 'public' : 'private';

> If the boolean expression tests for null, consider using ??.

    String playerName(String name) => name ?? 'Guest';

### Cascade notation (..)

Cascades (..) allow you to make a sequence of operations on the same object. In addition to function calls, you can also access fields on that same object.

examples:

    querySelector('#confirm') // Get an object.
      ..text = 'Confirm' // Use its members.
      ..classes.add('important')
      ..onClick.listen((e) => window.alert('Confirmed!'));

### Control flow statements

You can control the flow of your Dart code using any of the following:

* if and else
* for loops
* while and do-while loops
* break and continue
* switch and case
* assert

You can also affect the control flow using **`try-catch` and `throw`**, as explained in Exceptions.



#### Switch and case

Switch statements in Dart compare integer, string, or compile-time constants using ==. The compared objects must all be instances of the same class (and not of any of its subtypes), and the class must not override ==. Enumerated types work well in switch statements.

> Note: Switch statements in Dart are intended for limited circumstances, such as in interpreters or scanners.

Each non-empty case clause ends with a break statement, as a rule. Other valid ways to end a non-empty case clause are a continue, throw, or return statement.

Use a default clause to execute code when no case clause matches:

    var command = 'OPEN';
    switch (command) {
      case 'CLOSED':
        executeClosed();
        break;
      case 'PENDING':
        executePending();
        break;
      case 'APPROVED':
        executeApproved();
        break;
      case 'DENIED':
        executeDenied();
        break;
      case 'OPEN':
        executeOpen();
        break;
      default:
        executeUnknown();
    }
The following example omits the break statement in a case clause, thus generating an error:

    var command = 'OPEN';
    switch (command) {
      case 'OPEN':
        executeOpen();
        // ERROR: Missing break

      case 'CLOSED':
        executeClosed();
        break;
    }
However, Dart does support empty case clauses, allowing a form of fall-through:

    var command = 'CLOSED';
    switch (command) {
      case 'CLOSED': // Empty case falls through.
      case 'NOW_CLOSED':
        // Runs for both CLOSED and NOW_CLOSED.
        executeNowClosed();
        break;
    }

If you really want fall-through, you can use a continue statement and a label:

    var command = 'CLOSED';
    switch (command) {
      case 'CLOSED':
        executeClosed();
        continue nowClosed;
      // Continues executing at the nowClosed label.
    
      nowClosed:
      case 'NOW_CLOSED':
        // Runs for both CLOSED and NOW_CLOSED.
        executeNowClosed();
        break;
    }

### Exceptions

Your Dart code can throw and catch exceptions. If the exception isn’t caught, the isolate that raised the exception is suspended, and typically the isolate and its program are terminated.

In contrast to Java, all of Dart’s exceptions are unchecked exceptions. Methods do not declare which exceptions they might throw, and you are not required to catch any exceptions.

Dart provides `Exception` and `Error` types, as well as numerous predefined subtypes. You can, of course, define your own exceptions. However, Dart programs can throw any non-null object—not just Exception and Error objects—as an exception.

#### Throw
Here’s an example of throwing, or raising, an exception:

    throw new FormatException('Expected at least 1 section');

You can also throw arbitrary objects:

    throw 'Out of llamas!';

> Note: Production-quality code usually throws types that implement Error or Exception.

Because **`throwing an exception`** is an **`expression`**, you can throw exceptions in => statements, as well as anywhere else that allows expressions:

    void distanceTo(Point other) =>
        throw new UnimplementedError();
#### Catch

Catching, or capturing, an exception **`stops the exception from propagating (unless you rethrow the exception)`**. Catching an exception gives you a chance to handle it:

    try {
      breedMoreLlamas();
    } on OutOfLlamasException {
      buyMoreLlamas();
    }

To handle code that can throw more than one type of exception, you can specify multiple catch clauses. The first catch clause that matches the thrown object’s type handles the exception. If the catch clause does not specify a type, that clause can handle any type of thrown object:

    try {
      breedMoreLlamas();
    } on OutOfLlamasException {
      // A specific exception
      buyMoreLlamas();
    } on Exception catch (e) {
      // Anything else that is an exception
      print('Unknown exception: $e');
    } catch (e) {
      // No specified type, handles all
      print('Something really unknown: $e');
    }

As the preceding code shows, you can use either on or catch or both. Use **`on`** when you need to specify the exception type. Use **`catch`** when your exception handler **needs the exception object**.

You can specify one or two parameters to catch(). The first is the exception that was thrown, and the second is the stack trace (a StackTrace object).

    try {
      // ···
    } on Exception catch (e) {
      print('Exception details:\n $e');
    } catch (e, s) {
      print('Exception details:\n $e');
      print('Stack trace:\n $s');
    }

To partially handle an exception, while allowing it to propagate, use the **`rethrow`** keyword.

    void misbehave() {
      try {
        dynamic foo = true;
        print(foo++); // Runtime error
      } catch (e) {
        print('misbehave() partially handled ${e.runtimeType}.');
        rethrow; // Allow callers to see the exception.
      }
    }

    void main() {
      try {
        misbehave();
      } catch (e) {
        print('main() finished handling ${e.runtimeType}.');
      }
    }

#### Finally

To ensure that some code runs whether or not an exception is thrown, use a finally clause. If no catch clause matches the exception, the exception is propagated after the finally clause runs:

    try {
      breedMoreLlamas();
    } finally {
      // Always clean up, even if an exception is thrown.
      cleanLlamaStalls();
    }

The finally clause runs after any matching catch clauses:

    try {
      breedMoreLlamas();
    } catch (e) {
      print('Error: $e'); // Handle the exception first.
    } finally {
      cleanLlamaStalls(); // Then clean up.
    }

Learn more by reading the Exceptions section.

### Classes

Dart is an object-oriented language with classes and mixin-based inheritance. Every object is an instance of a class, and all classes descend from `Object`. 

To create an object, you can use the new keyword with a constructor for a class. Constructor names can be either ClassName or **`ClassName.identifier`**. For example:

    // Create a Point using Point().
    var p1 = new Point(2, 2);

    // Create a Point using Point.fromJson().
    var p2 = new Point.fromJson({'x': 1, 'y': 2});

> Dart 2 note: You can omit the new before the constructor. Example: p1 = Point(2, 2). NOTE: **`--preview-dart-2 VM options need to be set.`**

> TIP: Use **`?.`** instead of **`.`** to avoid an exception when the leftmost operand is null:

    // If p is non-null, set its y value to 4.
    p?.y = 4;

#### Instance variables

Here’s how you declare instance variables:

    class Point {
      num x; // Declare instance variable x, initially null.
      num y; // Declare y, initially null.
      num z = 0; // Declare z, initially 0.
    }

All uninitialized instance variables have the value null.

All instance variables generate an implicit getter method. Non-final instance variables also generate an implicit setter method. For details, see `Getters and setters`.

    class Point {
      num x;
      num y;
    }

    void main() {
      var point = new Point();
      point.x = 4; // Use the setter method for x.
      assert(point.x == 4); // Use the getter method for x.
      assert(point.y == null); // Values default to null.
    }
    
If you initialize an instance variable where it is declared (instead of in a constructor or method), the value is set **when the instance is created, which is before the constructor and its initializer list execute**.

#### Constructors Basic

A function with the same name as its class (plus, optionally, an additional identifier as described in **`Named constructors`**). The most common form of constructor, the generative constructor, creates a new instance of a class. example:

    class Point {
      num x, y;

      Point(num x, num y) {
        // There's a better way to do this, stay tuned.
        this.x = x;
        this.y = y;
      }
    }

The **`this`** keyword refers to the current instance.

> Note: Use **`this`** only when there is a name conflict. Otherwise, Dart style omits the this.

The pattern of assigning a constructor argument to an instance variable is so common, Dart has **`syntactic sugar`** to make it easy:

class Point {
  num x, y;

  // Syntactic sugar for setting x and y
  // before the constructor body runs.
  Point(this.x, this.y);
}

#### Default constructors
If you don’t declare a constructor, a default constructor is provided for you. The default constructor has no arguments and invokes the no-argument constructor in the superclass.

> #### Constructors aren’t inherited
> Subclasses don’t inherit constructors from their superclass. A subclass that declares no constructors has only the default (no argument, no name) constructor.

#### Named constructors
Use a named constructor to implement multiple constructors for a class or to provide extra clarity:

    class Point {
      num x, y;

      Point(this.x, this.y);

      // Named constructor
      Point.origin() {
        x = 0;
        y = 0;
      }
    }

> Remember that constructors are **`not inherited`**, which means that a superclass’s named constructor is not inherited by a subclass. If you want a subclass to be created with a named constructor defined in the superclass, **`you must implement that constructor in the subclass`**.

#### Invoking a non-default superclass constructor
By default, a constructor in a subclass calls the superclass’s unnamed, no-argument constructor. The superclass’s constructor is called at the beginning of the constructor body. If an initializer list is also being used, it executes before the superclass is called. In summary, the order of execution is as follows:

1. initializer list
1. superclass’s no-arg constructor
1. main class’s no-arg constructor

If the superclass doesn’t have an unnamed, no-argument constructor, then you **`must manually call one of the constructors in the superclass`**. Specify the superclass constructor after a colon (:), just before the constructor body (if any).

    class Person {
      String firstName;

      Person.fromJson(Map data) {
        print('in Person');
      }
    }

    class Employee extends Person {
      // Person does not have a default constructor;
      // you must call super.fromJson(data).
      Employee.fromJson(Map data) : super.fromJson(data) {
        print('in Employee');
      }
    }

#### Initializer list
Besides invoking a superclass constructor, you can also initialize instance variables before the constructor body runs. `Separate initializers with commas`.

    // Initializer list sets instance variables before
    // the constructor body runs.
    Point.fromJson(Map<String, num> json)
        : x = json['x'],
          y = json['y'] {
      print('In Point.fromJson(): ($x, $y)');
    }    

> Warning: The right-hand side of an initializer does not have access to **`this`**.    

> Initializer lists are handy when setting up final fields.For example:

    import 'dart:math';

    class Point {
      final num x;
      final num y;
      final num distanceFromOrigin;

      Point(x, y)
          : x = x,
            y = y,
            distanceFromOrigin = sqrt(x * x + y * y);
    }

    main() {
      var p = new Point(2, 3);
      print(p.distanceFromOrigin);
    }

#### Redirecting constructors

Sometimes a constructor’s only purpose is to redirect to another constructor in the same class. A redirecting constructor’s body is empty, with the constructor call appearing after a colon (:).

    class Point {
      num x, y;
    
      // The main constructor for this class.
      Point(this.x, this.y);
    
      // Delegates to the main constructor.
      Point.alongXAxis(num x) : this(x, 0);
    }    

#### Constant constructors
If your class produces objects that never change, you can make these objects compile-time constants. To do this, define a const constructor and make sure that all instance variables are final.

    class ImmutablePoint {
      static final ImmutablePoint origin =
          const ImmutablePoint(0, 0);

      final num x, y;

      const ImmutablePoint(this.x, this.y);
    }    

#### Factory constructors
Use the factory keyword when implementing a constructor that doesn’t always create a new instance of its class. For example, a factory constructor might return an instance from a cache, or it might return an instance of a subtype.

The following example demonstrates a factory constructor returning objects from a cache:

    class Logger {
      final String name;
      bool mute = false;

      // _cache is library-private, thanks to
      // the _ in front of its name.
      static final Map<String, Logger> _cache =
          <String, Logger>{};

      factory Logger(String name) {
        if (_cache.containsKey(name)) {
          return _cache[name];
        } else {
          final logger = new Logger._internal(name);
          _cache[name] = logger;
          return logger;
        }
      }

      Logger._internal(this.name);

      void log(String msg) {
        if (!mute) print(msg);
      }
    }

> Note: Factory constructors have no access to this.

To invoke a factory constructor, you use the new keyword:

    var logger = new Logger('UI');
    logger.log('Button clicked');    

#### Instance methods

Instance methods on objects can access instance variables and this. The distanceTo() method in the following sample is an example of an instance method:

    import 'dart:math';

    class Point {
      num x, y;

      Point(this.x, this.y);

      num distanceTo(Point other) {
        var dx = x - other.x;
        var dy = y - other.y;
        return sqrt(dx * dx + dy * dy);
      }
    }
#### Getters and setters

Getters and setters are special methods that provide read and write access to an object’s properties. Recall that each instance variable has an implicit getter, plus a setter if appropriate. You can create additional properties by implementing getters and setters, using the **`get and set`** keywords:

    class Rectangle {
      num left, top, width, height;

      Rectangle(this.left, this.top, this.width, this.height);

      // Define two calculated properties: right and bottom.
      num get right => left + width;
      set right(num value) => left = value - width;
      num get bottom => top + height;
      set bottom(num value) => top = value - height;
    }

    void main() {
      var rect = new Rectangle(3, 4, 20, 15);
      assert(rect.left == 3);
      rect.right = 12;
      assert(rect.left == -8);
    }

> TIP: With getters and setters, you can start with instance variables, later wrapping them with methods, all without changing client code.

> Note: Operators such as increment (++) work in the expected way, whether or not a getter is explicitly defined. To avoid any unexpected side effects, the operator calls the getter exactly once, saving its value in a temporary variable.

> THINK: what if rect.right++ in the previous code?? TESTED: left is changed!

#### Abstract classes and Abstract methods 

**`Instance, getter, and setter methods can be abstract`**, defining an interface but leaving its implementation up to other classes. Abstract methods can **`only exist in abstract classes`**.

To make a method abstract, use a semicolon (;) instead of a method body:

    abstract class Doer {
      // Define instance variables and methods...

      void doSomething(); // Define an abstract method.
    }

    class EffectiveDoer extends Doer {
      void doSomething() {
        // Provide an implementation, so the method is not abstract here...
      }
    }

Calling an abstract method results in a runtime error.

#### Overridable operators

Here’s an example of a class that overrides the + and - operators:

    class Vector {
      final int x, y;

      const Vector(this.x, this.y);

      /// Overrides + (a + b).
      Vector operator +(Vector v) {
        return new Vector(x + v.x, y + v.y);
      }

      /// Overrides - (a - b).
      Vector operator -(Vector v) {
        return new Vector(x - v.x, y - v.y);
      }
    }

    void main() {
      final v = new Vector(2, 3);
      final w = new Vector(2, 2);

      // v == (2, 3)
      assert(v.x == 2 && v.y == 3);

      // v + w == (4, 5)
      assert((v + w).x == 4 && (v + w).y == 5);

      // v - w == (0, 1)
      assert((v - w).x == 0 && (v - w).y == 1);
    }

> If you override ==, you should also override Object’s `hashCode getter`. For an example of overriding == and hashCode, see `Implementing map keys` as followed.

#### Implementing map keys

Each object in Dart automatically provides an integer hash code, and thus can be used as a key in a map. However, you can override the hashCode getter to generate a custom hash code. If you do, you might also want to override the == operator. Objects that are equal (via ==) **`must have identical hash codes`**. A hash code doesn’t have to be unique, but it should be well distributed.

    class Person {
      final String firstName, lastName;

      Person(this.firstName, this.lastName);

      // Override hashCode using strategy from Effective Java,
      // Chapter 11.
      @override
      int get hashCode {
        int result = 17;
        result = 37 * result + firstName.hashCode;
        result = 37 * result + lastName.hashCode;
        return result;
      }

      // You should generally implement operator == if you
      // override hashCode.
      @override
      bool operator ==(dynamic other) {
        if (other is! Person) return false;
        Person person = other;
        return (person.firstName == firstName &&
            person.lastName == lastName);
      }
    }

    void main() {
      var p1 = new Person('Bob', 'Smith');
      var p2 = new Person('Bob', 'Smith');
      var p3 = 'not a person';
      assert(p1.hashCode == p2.hashCode);
      assert(p1 == p2);
      assert(p1 != p3);
    }


For more information on overriding, in general, see `Extending a class`.

#### Implicit interfaces

Every class implicitly defines an interface containing all the instance members of the class and of any interfaces it implements. If you want to create a class A that supports class B’s API without inheriting B’s implementation, class A should implement the B interface.

A class implements one or more interfaces by declaring them in an **`implements`** clause and then providing the APIs required by the interfaces. For example:

    // A person. The implicit interface contains greet().
    class Person {
      // In the interface, but visible only in this library.
      final _name;

      // Not in the interface, since this is a constructor.
      Person(this._name);

      // In the interface.
      String greet(String who) => 'Hello, $who. I am $_name.';
    }

    // An implementation of the Person interface.
    class Impostor implements Person {
      get _name => '';

      String greet(String who) => 'Hi $who. Do you know who I am?';
    }

    String greetBob(Person person) => person.greet('Bob');

    void main() {
      print(greetBob(new Person('Kathy')));
      print(greetBob(new Impostor()));
    }

Here’s an example of specifying that a class implements multiple interfaces:

    class Point implements Comparable, Location {
      // ···
    }

#### Extending a class

Use **`extends`** to create a subclass, and super to refer to the superclass.

Overriding members
Subclasses can override instance methods, getters, and setters. You can use the **`@override`** annotation to indicate that you are intentionally overriding a member:

    class SmartTelevision extends Television {
      @override
      void turnOn() {
        // ···
      }
      // ···
    }

To narrow the type of a method parameter or instance variable in code that is type safe, you can use the **`covariant`** keyword.

#### noSuchMethod()

To detect or react whenever code attempts to use a non-existent method or instance variable, you can override noSuchMethod():

    class A {
      // Unless you override noSuchMethod, using a
      // non-existent member results in a NoSuchMethodError.
      @override
      void noSuchMethod(Invocation invocation) {
        print('You tried to use a non-existent member: ' +
            '${invocation.memberName}');
      }
    }

Here is another example:

    class Foo {
      num foo(x)=> 1.2;
      }

    class MockFoo implements Foo {
      @override
      noSuchMethod(Invocation i) {
        if (i.memberName == #foo) {
          if (i.isMethod &&
              i.positionalArguments.length == 1 &&
              i.namedArguments.isEmpty) {
            // ... implement mock behavior for `foo` here.
            print("\n MockFoo:noSuchMethod:${i.memberName} invoked with argu $   {i.positionalArguments[0]}\n");
            return 1.5;
          }
          else{
            return super.noSuchMethod(i);
          }
        }
        else{
          return super.noSuchMethod(i);
        }
      }
    }

You can’t invoke an unimplemented method unless one of the following is true:

* The receiver has the static type dynamic.
* The receiver has a static type that defines the unimplemented method (abstract is OK), and the dynamic type of the receiver has an implemention of noSuchMethod() that’s different from the one in class Object.

#### Enumerated types

Enumerated types, often called enumerations or enums, are a special kind of class used to represent a fixed number of constant values.

##### Using enums
Declare an enumerated type using the enum keyword:

    enum Color { red, green, blue }

Each value in an enum has an index getter, which returns the zero-based position of the value in the enum declaration. For example, the first value has index 0, and the second value has index 1.

    assert(Color.red.index == 0);
    assert(Color.green.index == 1);
    assert(Color.blue.index == 2);

To get a list of all of the values in the enum, use the enum’s values constant.

    List<Color> colors = Color.values;
    assert(colors[2] == Color.blue);

You can use enums in switch statements, and you’ll get a warning if you don’t handle all of the enum’s values:

    var aColor = Color.blue;

    switch (aColor) {
      case Color.red:
        print('Red as roses!');
        break;
      case Color.green:
        print('Green as grass!');
        break;
      default: // Without this, you see a WARNING.
        print(aColor); // 'Color.blue'
    }

Enumerated types have the following limits:

* You can’t subclass, mix in, or implement an enum.
* You can’t explicitly instantiate an enum.

#### Adding features to a class: mixins

> NOTE: Minxins is not quite understandable, the example here is not good too. perhaps should read more source code of library.

Mixins are a way of reusing a class’s code in multiple class hierarchies.

To use a mixin, use the with keyword followed by one or more mixin names. The following example shows two classes that use mixins:

    class Musician extends Performer with Musical {
      // ···
    }

    class Maestro extends Person
        with Musical, Aggressive, Demented {
      Maestro(String maestroName) {
        name = maestroName;
        canConduct = true;
      }
    }

To implement a mixin, create a class that extends Object, declares no constructors, and has no calls to super. For example:

    abstract class Musical {
      bool canPlayPiano = false;
      bool canCompose = false;
      bool canConduct = false;

      void entertainMe() {
        if (canPlayPiano) {
          print('Playing piano');
        } else if (canConduct) {
          print('Waving hands');
        } else {
          print('Humming to self');
        }
      }
    }

#### Static variables and methods

Use the **`static`** keyword to implement class-wide variables and methods.

Static variables (class variables) are useful for class-wide state and constants:

    class Queue {
      static const int initialCapacity = 16;
      // ···
    }

    void main() {
      assert(Queue.initialCapacity == 16);
    }

> Static variables aren’t initialized until they’re used.

Static methods (class methods) do not operate on an instance, and thus do not have access to this. For example:

    import 'dart:math';

    class Point {
      num x, y;
      Point(this.x, this.y);

      static num distanceBetween(Point a, Point b) {
        var dx = a.x - b.x;
        var dy = a.y - b.y;
        return sqrt(dx * dx + dy * dy);
      }
    }

    void main() {
      var a = new Point(2, 2);
      var b = new Point(4, 4);
      var distance = Point.distanceBetween(a, b);
      assert(2.8 < distance && distance < 2.9);
      print(distance);
    }

> Note: Consider using top-level functions, instead of static methods, for common or widely used utilities and functionality.

You can use static methods as compile-time constants. For example, you can pass a static method as a parameter to a constant constructor.

### Generics

If you look at the API documentation for the basic array type, List, you’ll see that the type is actually List<E>. The <…> notation marks List as a generic (or parameterized) type—a type that has formal type parameters. By convention, type variables have single-letter names, such as **`E, T, S, K, and V`**.

Example:

    var names = new List<String>();
    names.addAll(['Seth', 'Kathy', 'Lars']);
    names.add(42); // Error
    
Generic types can save you the trouble of code duplication:

    abstract class Cache<T> {
      T getByKey(String key);
      void setByKey(String key, T value);
    }

In this code, **`T`** is the stand-in type. It’s a placeholder that you can think of as a type that a developer will define later.

#### Using collection literals

List and map literals can be parameterized. Parameterized literals are just like the literals you’ve already seen, except that you add <type> (for lists) or <keyType, valueType> (for maps) before the opening bracket. Here is example of using typed literals:

    var names = <String>['Seth', 'Kathy', 'Lars'];
    var pages = <String, String>{
      'index.html': 'Homepage',
      'robots.txt': 'Hints for web robots',
      'humans.txt': 'We are people, not machines'
    };

#### Using parameterized types with constructors

To specify one or more types when using a constructor, put the types in angle brackets (<...>) just after the class name. For example:

    var names = new List<String>();
    names.addAll(['Seth', 'Kathy', 'Lars']);
    var nameSet = new Set<String>.from(names);

The following code creates a map that has integer keys and values of type View:

    var views = new Map<int, View>();

#### Generic collections and the types they contain

Dart generic types are reified, which means that they carry their type information around at runtime. For example, you can test the type of a collection:

    var names = new List<String>();
    names.addAll(['Seth', 'Kathy', 'Lars']);
    print(names is List<String>); // true

> Note: In contrast, generics in Java use erasure, which means that generic type parameters are removed at runtime. In Java, you can test whether an object is a List, but you can’t test whether it’s a List<String>.

#### Restricting the parameterized type

When implementing a generic type, you might want to limit the types of its parameters. You can do this using extends.

    class Foo<T extends SomeBaseClass> {
      // Implementation goes here...
      String toString() => "Instance of 'Foo<$T>'";
    }

    class Extender extends SomeBaseClass {...}

It’s OK to use SomeBaseClass or any of its subclasses as generic argument:

    var someBaseClassFoo = new Foo<SomeBaseClass>();
    var extenderFoo = new Foo<Extender>();

It’s also OK to specify no generic argument:

    var foo = new Foo();
    print(foo); // Instance of 'Foo<SomeBaseClass>'

Specifying any non-SomeBaseClass type results in an error:

    var foo = new Foo<Object>();

#### Using generic methods

Initially, Dart’s generic support was limited to classes. A newer syntax, called generic methods, allows type arguments on methods and functions:

    T first<T>(List<T> ts) {
      // Do some initial work or error checking, then...
      T tmp = ts[0];
      // Do some additional checking or processing...
      return tmp;
    }

Here the generic type parameter on first (<T>) allows you to use the type argument T in several places:

* In the function’s return type (T).
* In the type of an argument (List<T>).
* In the type of a local variable (T tmp).

For more information about generics, see Using Generic Methods.

### Libraries and visibility

The import and library directives can help you create a modular and shareable code base. Libraries not only provide APIs, but are a unit of privacy: identifiers that start with an underscore (_) are visible only inside the library. **`Every Dart app is a library, even if it doesn’t use a library directive`**.

Libraries can be distributed using packages. See Pub Package and Asset Manager for information about pub, a package manager included in the SDK.

#### Using libraries
Use import to specify how a namespace from one library is used in the scope of another library.

![Dart library use](imgs/dartlibuse.png)

For example, Dart web apps generally use the dart:html library, which they can import like this:

    import 'dart:html';

The only required argument to import is a URI specifying the library. For built-in libraries, the URI has the special dart: scheme. For other libraries, you can use a file system path or the package: scheme. The package: scheme specifies libraries provided by a package manager such as the pub tool. For example:

    import 'package:test/test.dart';

#### Specifying a library prefix
If you import two libraries that have conflicting identifiers, then you can specify a prefix for one or both libraries. For example, if library1 and library2 both have an Element class, then you might have code like this:

    import 'package:lib1/lib1.dart';
    import 'package:lib2/lib2.dart' as lib2;

    // Uses Element from lib1.
    Element element1 = new Element();

    // Uses Element from lib2.
    lib2.Element element2 = new lib2.Element();

#### Importing only part of a library
If you want to use only part of a library, you can selectively import the library. For example:

    // Import only foo.
    import 'package:lib1/lib1.dart' show foo;

    // Import all names EXCEPT foo.
    import 'package:lib2/lib2.dart' hide foo;

#### Lazily loading a library

Deferred loading (also called lazy loading) allows an application to load a library on demand, if and when it’s needed. Here are some cases when you might use deferred loading:

* To reduce an app’s initial startup time.
* To perform A/B testing—trying out alternative implementations of an * algorithm, for example.
* To load rarely used functionality, such as optional screens and dialogs.

To lazily load a library, you must first import it using deferred as.

    import 'package:greetings/hello.dart' deferred as hello;

When you need the library, invoke loadLibrary() using the library’s identifier.

    Future greet() async {
      await hello.loadLibrary();
      hello.printGreeting();
    }

In the preceding code, the await keyword pauses execution until the library is loaded. For more information about async and await, see asynchrony support.

You can invoke loadLibrary() multiple times on a library without problems. The library is loaded only once.

Keep in mind the following when you use deferred loading:

1. A deferred library’s constants aren’t constants in the importing file. Remember, these constants don’t exist until the deferred library is loaded.
You can’t use types from a deferred library in the importing file. Instead, consider moving interface types to a library imported by both the deferred library and the importing file.

1. Dart implicitly inserts loadLibrary() into the namespace that you define using deferred as namespace. The loadLibrary() function returns a Future.

#### Implementing libraries

See Create Library Packages for advice on how to implement a library package, including:

* How to organize library source code.
* How to use the export directive.
* When to use the part directive.

### Handling Futures

When you need the result of a completed Future, you have two options:

* Use async and await.
* Use the Future API, as described in the library tour.

Code that uses async and await is asynchronous, **`To use await, code must be in an async function—a function marked as async`**:

    Future checkVersion() async {
      var version = await lookUpVersion();
      // Do something with version
    }

> Note: Although an async function might perform time-consuming operations, it doesn’t wait for those operations. Instead, the async function executes only until it encounters its first await expression (details). Then it returns a Future object, resuming execution only after the await expression completes.

Use try, catch, and finally to handle errors and cleanup in code that uses await:

    try {
      version = await lookUpVersion();
    } catch (e) {
      // React to inability to look up the version
    }

You can use await multiple times in an async function. For example, the following code waits three times for the results of functions:

    var entrypoint = await findEntrypoint();
    var exitCode = await runExecutable(entrypoint, args);
    await flushThenExit(exitCode);

In await expression, the value of expression is usually a Future; if it isn’t, then the value is automatically wrapped in a Future. This Future object indicates a promise to return an object. The value of await expression is that returned object. The await expression makes execution pause until that object is available.

If you get a compile-time error when using await, make sure await is in an async function. For example, to use await in your app’s main() function, the body of main() must be marked as async:

    Future main() async {
      checkVersion();
      print('In main: version is ${await lookUpVersion()}');
    }

#### Declaring async functions

An async function is a function whose body is marked with the async modifier.

Adding the async keyword to a function makes it return a Future. For example, consider this synchronous function, which returns a String:

    String lookUpVersion() => '1.0.0';

If you change it to be an async function—for example, because a future implementation will be time consuming—the returned value is a Future:

    Future<String> lookUpVersion() async => '1.0.0';
    
Note that the function’s body doesn’t need to use the Future API. Dart creates the Future object if necessary.

If your function doesn’t return a useful value, make its return type Future<void>.

### Handling Streams

When you need to get values from a Stream, you have two options:

* Use async and an asynchronous for loop (`await for`).
* Use the Stream API, as described in the library tour.

> Note: Before using await for, be sure that it makes the code clearer and that you really do want to wait for all of the stream’s results. For example, you usually **`should not use await for for UI event listeners`**, because UI frameworks send endless streams of events.

An asynchronous for loop has the following form:

    await for (varOrType identifier in expression) {
      // Executes each time the stream emits a value.
    }

The value of expression must have type Stream. Execution proceeds as follows:

  1. Wait until the stream emits a value.
  1. Execute the body of the for loop, with the variable set to that emitted value.
  1. Repeat 1 and 2 until the stream is closed.

To stop listening to the stream, you can use a `break` or `return` statement, which breaks out of the for loop and unsubscribes from the stream.

If you get a compile-time error when implementing an asynchronous for loop, make sure the **`await for is in an async function`**. 

For more information about asynchronous programming, in general, see the dart:async section of the library tour. Also see the articles Dart Language Asynchrony Support: Phase 1 and Dart Language Asynchrony Support: Phase 2, and the Dart language specification.

### Generators

When you need to lazily produce a sequence of values, consider using a generator function. Dart has built-in support for two kinds of generator functions:

* Synchronous generator: Returns an Iterable object.
* Asynchronous generator: Returns a Stream object.

> why? if we implement generators ourself, it may be too chicky.

#### Synchronous Generators

To implement a **`synchronous`** generator function, mark the function body as `sync*`, and use `yield` statements to deliver values:

    Iterable<int> naturalsTo(int n) sync* {
      int k = 0;
      while (k < n) yield k++;
    }

When called, naturalsTo immediately returns an iterable (much like a function marked async immediately returns a future), from which you can extract an iterator. The body of the function won’t start running until one calls `moveNext` on that iterator. It will run until it hits the yield statement the first time. The yield statement contains an expression, which it evaluates. Then, the function suspends, and `moveNext` returns true to its caller.

The function will resume execution the next time `moveNext` is called. When the loop ends, the method implicitly executes a return, which causes it to terminate. At that point, `moveNext` returns false to its caller.

#### Asynchronous Generators

To asynchronously produce a sequence, we use streams. To implement an **`asynchronous`** generator function, mark the function body as `async*`, and use `yield` statements to deliver values:

    Stream<int> asynchronousNaturalsTo(int n) async* {
      int k = 0;
      while (k < n) yield k++;
    }

and the `await-for loop` is designed to play well with streams:

    var asycStream = asynchronousNaturalsTo(5);
    await for (int i in asycStream) { 
      print('event loop $i'); 
    }

Every time an element is added to the stream, the loop body is run. After each iteration, the function enclosing the loop suspends until the next element is available or the stream is done. 

>NOTE: Just like await expressions, await-for loops can only appear inside asynchronous functions.    

#### Generators use recursive code

If your generator is recursive, you can improve its performance by using `yield*`:

    Iterable<int> naturalsDownFrom(int n) sync* {
      if (n > 0) {
        yield n;
        yield* naturalsDownFrom(n - 1);
      }
    }

For more information about generators, see the article Dart Language Asynchrony Support: Phase 2.

### Callable classes

To allow your Dart class to be called like a function, implement the `call()` method.

In the following example, the WannabeFunction class defines a call() function that takes three strings and concatenates them, separating each with a space, and appending an exclamation. Click the run button ( red-run.png ) to execute the code.

    class WannabeFunction {
      call(String a, String b, String c) => '$a $b $c!';
    }
    
    main() {
      var wf = new WannabeFunction();
      var out = wf("Hi","there,","gang");
      print('$out');
    }

#### The call() method
In the following example, we have an ordinary class WannabeFunction that happens to define a method named call().

    class WannabeFunction {
      call(int a, int b) => a + b;
    }

The call() method is special, in that anyone who defines a call() method is presumed to dynamically emulate a function. This allows us to use instances of WannabeFunction as if they were functions that take two integer arguments:

    var wf = new WannabeFunction();
    wf(3, 4); // 7

There are cases where this ability can be quite useful. It is also core to the design philosophy of the Dart language:

* What matters about an object is its behavior. If object a has a procedural interface that is compatible with that of another object b, a may substitute for b.
* The interface of any kind of object can always be emulated by another suitably defined object.

#### How does it work?

When x(a1, .., an) is evaluated, if it is a normal function, it gets called in the normal way. If it isn’t we just invoke call() on it. If x supports a call() method with suitable arguments it gets called.

Otherwise, noSuchMethod() gets invoked. The default implementation of noSuchMethod() checks to see whether it was invoked due to an attempt to use call(), and if so issues a helpful error message suggesting you might have wanted to use a closure.

#### The apply() method

The class Function defines the static method apply() with the following signature:

    static apply(Function function,
                      List positionalArguments,
                      [Map<Symbol, dynamic> namedArguments]);
                      
The apply() function allows functions to be called in generic fashion. The last argument is positional, and is only needed if the function we mean to call takes named arguments. These are provided via map from argument names to their values. One thing to pay attention to is that names are described via instances of class **`Symbol`**.

#### Symbols

You can create symbols from strings:

    new Symbol('myFavoriteMethodName');

If possible, create constant symbol objects:

    const Symbol('myFavoriteMethodName');

Using constant symbols helps dart2js minify your code.

#### Function types

An additional issue is how user-defined function classes relate to the type system. To simulate functions properly, we want them to be members of the appropriate function type:

typedef BinaryFunction(a,b);
...
new WannabeFunction() is BinaryFunction; // true

Therefore, we decree that an object is a member of a function type if the object’s class has a call() method and that method is a member of the function type.

### Isolates

Most computers, even on mobile platforms, have multi-core CPUs. To take advantage of all those cores, developers traditionally use shared-memory threads running concurrently. However, shared-state concurrency is error prone and can lead to complicated code.

Instead of threads, all Dart code runs inside of isolates. Each isolate has its own memory heap, ensuring that no isolate’s state is accessible from any other isolate.

For more information, see the dart:isolate library documentation.

### Typedefs

In Dart, functions are objects, just like strings and numbers are objects. A typedef, or function-type alias, gives a function type a name that you can use when declaring fields and return types. A typedef retains type information when a function type is assigned to a variable.

Consider the following code, which doesn’t use a typedef:

    class SortedCollection {
      Function compare;

      SortedCollection(int f(Object a, Object b)) {
        compare = f;
      }
    }

    // Initial, broken implementation.
    int sort(Object a, Object b) => 0;

    void main() {
      SortedCollection coll = new SortedCollection(sort);

      // All we know is that compare is a function,
      // but what type of function?
      assert(coll.compare is Function);
    }

Type information is lost when assigning f to compare. The type of f is (Object, Object) → int (where → means returns), yet the type of compare is Function. If we change the code to use explicit names and retain type information, both developers and tools can use that information.

    typedef Compare = int Function(Object a, Object b);

    class SortedCollection {
      Compare compare;

      SortedCollection(this.compare);
    }

    // Initial, broken implementation.
    int sort(Object a, Object b) => 0;

    void main() {
      SortedCollection coll = new SortedCollection(sort);
      assert(coll.compare is Function);
      assert(coll.compare is Compare);
    }

>Note: Currently, typedefs are restricted to function types. We expect this to change.

Because typedefs are simply aliases, they offer a way to check the type of any function. For example:

    typedef Compare<T> = int Function(T a, T b);

    int sort(int a, int b) => a - b;

    void main() {
      assert(sort is Compare<int>); // True!
    }




