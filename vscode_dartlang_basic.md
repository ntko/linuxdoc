## Linux下使用vscode开发Dart环境配置相关问题

### Install Dart VM SDK:

> [REF:https://www.dartlang.org/tools/sdk#install](https://www.dartlang.org/tools/sdk#install)

### Install Dart vscode plugin

* Start VS Code
* Invoke View>Command Palette…
* Type ‘install’, and select the ‘Extensions: Install Extension’ action
* Enter flutter in the search field, select ‘Dart’ in the list, and click Install
* Select ‘OK’ to reload VS Code

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