<!-- TOC -->

- [Dart lib tour](#dart-lib-tour)
    - [dart:core Strings](#dartcore-strings)
        - [Strings and regular expressions](#strings-and-regular-expressions)
        - [Searching inside a string](#searching-inside-a-string)
        - [Extracting data from a string](#extracting-data-from-a-string)
        - [Converting to uppercase or lowercase](#converting-to-uppercase-or-lowercase)
        - [Trimming and empty strings](#trimming-and-empty-strings)
        - [Replacing part of a string](#replacing-part-of-a-string)
        - [Building a string](#building-a-string)
        - [Regular expressions](#regular-expressions)
        - [More information](#more-information)
    - [dart:core Collections](#dartcore-collections)
        - [Lists](#lists)
        - [Sets](#sets)
        - [Maps](#maps)
        - [Common collection methods](#common-collection-methods)
    - [dart:core URIs](#dartcore-uris)
        - [Encoding and decoding fully qualified URIs](#encoding-and-decoding-fully-qualified-uris)
        - [Encoding and decoding URI components](#encoding-and-decoding-uri-components)
        - [Parsing URIs](#parsing-uris)
        - [Building URIs](#building-uris)
    - [dart:core Dates and times](#dartcore-dates-and-times)
    - [dart:core Utility classes](#dartcore-utility-classes)
        - [Comparing objects](#comparing-objects)
        - [Implementing map keys](#implementing-map-keys)
        - [Iteration](#iteration)
    - [dart:core Exceptions](#dartcore-exceptions)
        - [NoSuchMethodError](#nosuchmethoderror)
        - [ArgumentError](#argumenterror)
    - [dart:async Future](#dartasync-future)
        - [Using await](#using-await)
        - [Basic usage](#basic-usage)
        - [Chaining multiple asynchronous methods](#chaining-multiple-asynchronous-methods)
        - [Waiting for multiple futures](#waiting-for-multiple-futures)
        - [Stream](#stream)
        - [Using an asynchronous for loop](#using-an-asynchronous-for-loop)
        - [Listening for stream data](#listening-for-stream-data)
        - [Transforming stream data](#transforming-stream-data)
        - [Handling errors and completion](#handling-errors-and-completion)
    - [dart:math - math and random](#dartmath---math-and-random)
        - [Trigonometry](#trigonometry)
        - [Maximum and minimum](#maximum-and-minimum)
        - [Math constants](#math-constants)
        - [Random numbers](#random-numbers)
    - [dart:convert - decoding and encoding JSON, UTF-8, and more](#dartconvert---decoding-and-encoding-json-utf-8-and-more)
        - [Decoding and encoding JSON](#decoding-and-encoding-json)
        - [Decoding and encoding UTF-8 characters](#decoding-and-encoding-utf-8-characters)

<!-- /TOC -->

# Dart lib tour

## dart:core Strings

### Strings and regular expressions

A string in Dart is an immutable sequence of UTF-16 code units. The language tour has more information about strings. You can use regular expressions (`RegExp` objects) to search within strings and to replace parts of strings.

The String class defines such methods as `split()`, `contains()`, `startsWith()`, `endsWith()`, and more.

### Searching inside a string

You can find particular locations within a string, as well as check whether a string begins with or ends with a particular pattern. For example:

    // Check whether a string contains another string.
    assert('Never odd or even'.contains('odd'));

    // Does a string start with another string?
    assert('Never odd or even'.startsWith('Never'));

    // Does a string end with another string?
    assert('Never odd or even'.endsWith('even'));

    // Find the location of a string inside a string.
    assert('Never odd or even'.indexOf('odd') == 6);

### Extracting data from a string

You can get the individual characters from a string as Strings or ints, respectively. To be precise, you actually get individual UTF-16 code units; high-numbered characters such as the treble clef symbol (‘\u{1D11E}’) are two code units apiece.

You can also extract a substring or split a string into a list of substrings:

    // Grab a substring.
    assert('Never odd or even'.substring(6, 9) == 'odd');

    // Split a string using a string pattern.
    var parts = 'structured web apps'.split(' ');
    assert(parts.length == 3);
    assert(parts[0] == 'structured');

    // Get a UTF-16 code unit (as a string) by index.
    assert('Never odd or even'[0] == 'N');

    // Use split() with an empty string parameter to get
    // a list of all characters (as Strings); good for
    // iterating.
    for (var char in 'hello'.split('')) {
        print(char);
    }

    // Get all the UTF-16 code units in the string.
    var codeUnitList =
        'Never odd or even'.codeUnits.toList();
    assert(codeUnitList[0] == 78);
    
### Converting to uppercase or lowercase

You can easily convert strings to their uppercase and lowercase variants:

    // Convert to uppercase.
    assert('structured web apps'.toUpperCase() ==
        'STRUCTURED WEB APPS');

    // Convert to lowercase.
    assert('STRUCTURED WEB APPS'.toLowerCase() ==
        'structured web apps');

>Note: These methods don’t work for every language. For example, the Turkish alphabet’s dotless I is converted incorrectly.

### Trimming and empty strings

Remove all leading and trailing white space with trim(). To check whether a string is empty (length is zero), use isEmpty.

    // Trim a string.
    assert('  hello  '.trim() == 'hello');

    // Check whether a string is empty.
    assert(''.isEmpty);

    // Strings with only white space are not empty.
    assert('  '.isNotEmpty);

### Replacing part of a string

Strings are immutable objects, which means **`you can create them but you can’t change them`**. If you look closely at the String API docs, you’ll notice that none of the methods actually changes the state of a String. For example, the method replaceAll() returns a new String without changing the original String:

    var greetingTemplate = 'Hello, NAME!';
    var greeting =
        greetingTemplate.replaceAll(new RegExp('NAME'), 'Bob');

    // greetingTemplate didn't change.
    assert(greeting != greetingTemplate);

### Building a string

To programmatically generate a string, you can use StringBuffer. A StringBuffer doesn’t generate a new String object until toString() is called. The writeAll() method has an optional second parameter that lets you specify a separator—in this case, a space.

    var sb = new StringBuffer();
    sb
    ..write('Use a StringBuffer for ')
    ..writeAll(['efficient', 'string', 'creation'], ' ')
    ..write('.');

    var fullString = sb.toString();

    assert(fullString ==
        'Use a StringBuffer for efficient string creation.');

### Regular expressions

The RegExp class provides the same capabilities as JavaScript regular expressions. Use regular expressions for efficient searching and pattern matching of strings.

    // Here's a regular expression for one or more digits.
    var numbers = new RegExp(r'\d+');

    var allCharacters = 'llamas live fifteen to twenty years';
    var someDigits = 'llamas live 15 to 20 years';

    // contains() can use a regular expression.
    assert(!allCharacters.contains(numbers));
    assert(someDigits.contains(numbers));

    // Replace every match with another string.
    var exedOut = someDigits.replaceAll(numbers, 'XX');
    assert(exedOut == 'llamas live XX to XX years');
    
You can work directly with the RegExp class, too. The Match class provides access to a regular expression match.

    var numbers = new RegExp(r'\d+');
    var someDigits = 'llamas live 15 to 20 years';

    // Check whether the reg exp has a match in a string.
    assert(numbers.hasMatch(someDigits));

    // Loop through all matches.
    for (var match in numbers.allMatches(someDigits)) {
        print(match.group(0)); // 15, then 20
    }

### More information

Refer to the String API docs for a full list of methods. Also see the API docs for StringBuffer, Pattern, RegExp, and Match.

## dart:core Collections

Dart ships with a core collections API, which includes classes for `lists, sets, and maps`.

### Lists
As the language tour shows, you can use literals to create and initialize lists. Alternatively, use one of the List constructors. The List class also defines several methods for adding items to and removing items from lists.

    // Use a List constructor.
    var vegetables = new List();

    // Or simply use a list literal.
    var fruits = ['apples', 'oranges'];

    // Add to a list.
    fruits.add('kiwis');

    // Add multiple items to a list.
    fruits.addAll(['grapes', 'bananas']);

    // Get the list length.
    assert(fruits.length == 5);

    // Remove a single item.
    var appleIndex = fruits.indexOf('apples');
    fruits.removeAt(appleIndex);
    assert(fruits.length == 4);

    // Remove all elements from a list.
    fruits.clear();
    assert(fruits.length == 0);

    //Use indexOf() to find the index of an object in a list:

    var fruits = ['apples', 'oranges'];

    // Access a list item by index.
    assert(fruits[0] == 'apples');

    // Find an item in a list.
    assert(fruits.indexOf('apples') == 0);

Sort a list using the sort() method. You can provide a sorting function that compares two objects. This sorting function must return < 0 for smaller, 0 for the same, and > 0 for bigger. The following example uses `compareTo()`, which is defined by Comparable and implemented by String.

    var fruits = ['bananas', 'apples', 'oranges'];

    // Sort a list.
    fruits.sort((a, b) => a.compareTo(b));
    assert(fruits[0] == 'apples');

Lists are parameterized types, so you can specify the type that a list should contain:

    // This list should contain only strings.
    var fruits = new List<String>();

    fruits.add('apples');
    var fruit = fruits[0];
    assert(fruit is String);

    // Generates static analysis warning, num is not a string.
    fruits.add(5); // BAD: Throws exception in checked mode.

>Dart 2 note: Checked mode won’t be in Dart 2. For more information, see Dart 2 Updates.

Refer to the List API docs for a full list of methods.

### Sets

A set in Dart is an unordered collection of unique items. Because a set is unordered, **`you can’t get a set’s items by index (position)`**.

    var ingredients = new Set();
    ingredients.addAll(['gold', 'titanium', 'xenon']);
    assert(ingredients.length == 3);

    // Adding a duplicate item has no effect.
    ingredients.add('gold');
    assert(ingredients.length == 3);

    // Remove an item from a set.
    ingredients.remove('gold');
    assert(ingredients.length == 2);

Use `contains()` and `containsAll()` to check whether one or more objects are in a set:

    var ingredients = new Set();
    ingredients.addAll(['gold', 'titanium', 'xenon']);

    // Check whether an item is in the set.
    assert(ingredients.contains('titanium'));

    // Check whether all the items are in the set.
    assert(ingredients.containsAll(['titanium', 'xenon']));
    An intersection is a set whose items are in two other sets.

    var ingredients = new Set();
    ingredients.addAll(['gold', 'titanium', 'xenon']);

    // Create the intersection of two sets.
    var nobleGases = new Set.from(['xenon', 'argon']);
    var intersection = ingredients.intersection(nobleGases);
    assert(intersection.length == 1);
    assert(intersection.contains('xenon'));
    
Refer to the Set API docs for a full list of methods.

### Maps

A map, commonly known as a dictionary or hash, is an unordered collection of key-value pairs. Maps associate a key to some value for easy retrieval. Unlike in JavaScript, Dart objects are not maps.You can declare a map using a terse literal syntax, or you can use a traditional constructor:

    // Maps often use strings as keys.
    var hawaiianBeaches = {
        'Oahu': ['Waikiki', 'Kailua', 'Waimanalo'],
        'Big Island': ['Wailea Bay', 'Pololu Beach'],
        'Kauai': ['Hanalei', 'Poipu']
    };

    // Maps can be built from a constructor.
    var searchTerms = new Map();

    // Maps are parameterized types; you can specify what
    // types the key and value should be.
    var nobleGases = new Map<int, String>();

You add, get, and set map items using the bracket syntax. Use `remove()` to remove a key and its value from a map.

    var nobleGases = {54: 'xenon'};

    // Retrieve a value with a key.
    assert(nobleGases[54] == 'xenon');

    // Check whether a map contains a key.
    assert(nobleGases.containsKey(54));

    // Remove a key and its value.
    nobleGases.remove(54);
    assert(!nobleGases.containsKey(54));

You can retrieve all the values or all the keys from a map:

    var hawaiianBeaches = {
        'Oahu': ['Waikiki', 'Kailua', 'Waimanalo'],
        'Big Island': ['Wailea Bay', 'Pololu Beach'],
        'Kauai': ['Hanalei', 'Poipu']
    };

    // Get all the keys as an unordered collection
    // (an Iterable).
    var keys = hawaiianBeaches.keys;

    assert(keys.length == 3);
    assert(new Set.from(keys).contains('Oahu'));

    // Get all the values as an unordered collection
    // (an Iterable of Lists).
    var values = hawaiianBeaches.values;
    assert(values.length == 3);
    assert(values.any((v) => v.contains('Waikiki')));
    
>To check whether a map contains a key, use containsKey(). Because map values can be null, you cannot rely on simply getting the value for the key and checking for null to determine the existence of a key.

    var hawaiianBeaches = {
        'Oahu': ['Waikiki', 'Kailua', 'Waimanalo'],
        'Big Island': ['Wailea Bay', 'Pololu Beach'],
        'Kauai': ['Hanalei', 'Poipu']
    };

    assert(hawaiianBeaches.containsKey('Oahu'));
    assert(!hawaiianBeaches.containsKey('Florida'));
    
Use the putIfAbsent() method when you want to assign a value to a key if and only if the key does not already exist in a map. You must provide a function that returns the value.

    var teamAssignments = {};
    teamAssignments.putIfAbsent(
        'Catcher', () => pickToughestKid());
    assert(teamAssignments['Catcher'] != null);
    
Refer to the Map API docs for a full list of methods.

### Common collection methods

List, Set, and Map share common functionality found in many collections. Some of this common functionality is defined by the Iterable class, which List and Set implement.

>Note: Although Map doesn’t implement Iterable, you can get Iterables from it using the Map keys and values properties.

Use `isEmpty` or `isNotEmpty` to check whether a list, set, or map has items:

    var coffees = [];
    var teas = ['green', 'black', 'chamomile', 'earl grey'];
    assert(coffees.isEmpty);
    assert(teas.isNotEmpty);

To apply a function to each item in a list, set, or map, you can use `forEach()`:

    var teas = ['green', 'black', 'chamomile', 'earl grey'];

    teas.forEach((tea) => print('I drink $tea'));
    
When you invoke `forEach()` on a map, your function must take two arguments `(the key and value)`:

    hawaiianBeaches.forEach((k, v) {
        print('I want to visit $k and swim at $v');
        // I want to visit Oahu and swim at
        // [Waikiki, Kailua, Waimanalo], etc.
    });
    
Iterables provide the `map()` method, which gives you all the results in a single object:

    var teas = ['green', 'black', 'chamomile', 'earl grey'];
    var loudTeas = teas.map((tea) => tea.toUpperCase());
    loudTeas.forEach(print);

>Note: The object returned by map() is an Iterable that’s lazily evaluated: your function isn’t called until you ask for an item from the returned object.

>To force your function to be called immediately on each item, use `map().toList()` or `map().toSet()`:

    var loudTeas =
        teas.map((tea) => tea.toUpperCase()).toList();

Use Iterable’s `where()` method to get all the items that match a condition. Use Iterable’s `any()` and `every()` methods to check whether some or all items match a condition.

    var teas = ['green', 'black', 'chamomile', 'earl grey'];

    // Chamomile is not caffeinated.
    bool isDecaffeinated(String teaName) =>
        teaName == 'chamomile';

    // Use where() to find only the items that return true
    // from the provided function.
    var decaffeinatedTeas =
        teas.where((tea) => isDecaffeinated(tea));
    // or teas.where(isDecaffeinated)

    // Use any() to check whether at least one item in the
    // collection satisfies a condition.
    assert(teas.any(isDecaffeinated));

    // Use every() to check whether all the items in a
    // collection satisfy a condition.
    assert(!teas.every(isDecaffeinated));
    
For a full list of methods, refer to the Iterable API docs, as well as those for List, Set, and Map.

## dart:core URIs

The Uri class provides functions to encode and decode strings for use in URIs (which you might know as URLs). These functions handle characters that are special for URIs, such as & and =. The Uri class also parses and exposes the components of a URI—host, port, scheme, and so on.

### Encoding and decoding fully qualified URIs

To encode and decode characters except those with special meaning in a URI (such as /, :, &, #), use the `encodeFull()` and `decodeFull()` methods. These methods are good for encoding or decoding a fully qualified URI, leaving intact special URI characters.

    var uri = 'http://example.org/api?foo=some message';

    var encoded = Uri.encodeFull(uri);
    assert(encoded ==
        'http://example.org/api?foo=some%20message');

    var decoded = Uri.decodeFull(encoded);
    assert(uri == decoded);
    
Notice how only the space between some and message was encoded.

### Encoding and decoding URI components

To encode and decode all of a string’s characters that have special meaning in a URI, including (but not limited to) /, &, and :, use the `encodeComponent()` and `decodeComponent()` methods.

    var uri = 'http://example.org/api?foo=some message';

    var encoded = Uri.encodeComponent(uri);
    assert(encoded ==
        'http%3A%2F%2Fexample.org%2Fapi%3Ffoo%3Dsome%20message');

    var decoded = Uri.decodeComponent(encoded);
    assert(uri == decoded);
Notice how every special character is encoded. For example, / is encoded to %2F.

### Parsing URIs

If you have a Uri object or a URI string, you can get its parts using Uri fields such as path. To create a Uri from a string, use the `parse() static` method:

    var uri =
        Uri.parse('http://example.org:8080/foo/bar#frag');

    assert(uri.scheme == 'http');
    assert(uri.host == 'example.org');
    assert(uri.path == '/foo/bar');
    assert(uri.fragment == 'frag');
    assert(uri.origin == 'http://example.org:8080');
    
See the Uri API docs for more URI components that you can get.

### Building URIs

You can build up a URI from individual parts using the `Uri()` constructor:

    var uri = new Uri(
        scheme: 'http',
        host: 'example.org',
        path: '/foo/bar',
        fragment: 'frag');
    assert(
        uri.toString() == 'http://example.org/foo/bar#frag');

## dart:core Dates and times

A DateTime object is a point in time. The time zone is either UTC or the local time zone.

You can create DateTime objects using several constructors:

    // Get the current date and time.
    var now = new DateTime.now();

    // Create a new DateTime with the local time zone.
    var y2k = new DateTime(2000); // January 1, 2000

    // Specify the month and day.
    y2k = new DateTime(2000, 1, 2); // January 2, 2000

    // Specify the date as a UTC time.
    y2k = new DateTime.utc(2000); // 1/1/2000, UTC

    // Specify a date and time in ms since the Unix epoch.
    y2k = new DateTime.fromMillisecondsSinceEpoch(946684800000,
        isUtc: true);

    // Parse an ISO 8601 date.
    y2k = DateTime.parse('2000-01-01T00:00:00Z');

The millisecondsSinceEpoch property of a date returns the number of milliseconds since the “Unix epoch”—January 1, 1970, UTC:

    // 1/1/2000, UTC
    var y2k = new DateTime.utc(2000);
    assert(y2k.millisecondsSinceEpoch == 946684800000);

    // 1/1/1970, UTC
    var unixEpoch = new DateTime.utc(1970);
    assert(unixEpoch.millisecondsSinceEpoch == 0);

Use the `Duration` class to calculate the difference between two dates and to shift a date forward or backward:

    var y2k = new DateTime.utc(2000);

    // Add one year.
    var y2001 = y2k.add(const Duration(days: 366));
    assert(y2001.year == 2001);

    // Subtract 30 days.
    var december2000 =
        y2001.subtract(const Duration(days: 30));
    assert(december2000.year == 2000);
    assert(december2000.month == 12);

    // Calculate the difference between two dates.
    // Returns a Duration object.
    var duration = y2001.difference(y2k);
    assert(duration.inDays == 366); // y2k was a leap year.

> Warning: Using a Duration to shift a DateTime by days can be problematic, due to clock shifts (to daylight saving time, for example). Use UTC dates if you must shift days.

Refer to the API docs for DateTime and Duration for a full list of methods.

## dart:core Utility classes

The core library contains various utility classes, useful for sorting, mapping values, and iterating.

### Comparing objects

Implement the Comparable interface to indicate that an object can be compared to another object, usually for sorting. The compareTo() method returns < 0 for smaller, 0 for the same, and > 0 for bigger.

    class Line implements Comparable<Line> {
      final int length;
      const Line(this.length);

      @override
      int compareTo(Line other) => length - other.length;
    }

    void main() {
      var short = const Line(1);
      var long = const Line(100);
      assert(short.compareTo(long) < 0);
    }

### Implementing map keys

Each object in Dart automatically provides an integer hash code, and thus can be used as a key in a map. However, you can override the hashCode getter to generate a custom hash code. If you do, you might also want to override the == operator. Objects that are equal (via ==) must have identical hash codes. A hash code doesn’t have to be unique, but it should be well distributed.

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

### Iteration

The Iterable and Iterator classes support for-in loops. `Extend (if possible)` or `implement` Iterable whenever you create a class that can provide Iterators for use in for-in loops. Implement Iterator to define the actual iteration ability.

    class Process {
      // Represents a process...
    }
    
    class ProcessIterator implements Iterator<Process> {
      @override
      Process get current => ...
      @override
      bool moveNext() => ...
    }
    
    // A mythical class that lets you iterate through all
    // processes. Extends a subclass of [Iterable].
    class Processes extends IterableBase<Process> {
      @override
      final Iterator<Process> iterator = new ProcessIterator();
    }
    
    void main() {
      // Iterable objects can be used with for-in.
      for (var process in new Processes()) {
        // Do something with the process.
      }
    }
## dart:core Exceptions
The Dart core library defines many common exceptions and errors. Exceptions are considered conditions that you can plan ahead for and catch. Errors are conditions that you don’t expect or plan for.

A couple of the most common errors are:

### NoSuchMethodError
Thrown when a receiving object (which might be null) does not implement a method.

### ArgumentError
Can be thrown by a method that encounters an unexpected argument.

Throwing an application-specific exception is a common way to indicate that an error has occurred. You can define a custom exception by implementing the Exception interface:

    class FooException implements Exception {
      final String msg;

      const FooException([this.msg]);

      @override
      String toString() => msg ?? 'FooException';
    }
    
For more information, see Exceptions and the Exception API docs.

## dart:async Future

Future objects appear throughout the Dart libraries, often as the object returned by an asynchronous method. When a future completes, its value is ready to use.

### Using await
Before you directly use the Future API, consider using await instead. Code that uses await expressions can be easier to understand than code that uses the Future API.

Consider the following function. It uses Future’s then() method to execute three asynchronous functions in a row, waiting for each one to complete before executing the next one.

    runUsingFuture() {
      // ...
      findEntryPoint().then((entryPoint) {
        return runExecutable(entryPoint, args);
      }).then(flushThenExit);
    }
    
The equivalent code with await expressions looks more like synchronous code:
    
    runUsingAsyncAwait() async {
      // ...
      var entryPoint = await findEntryPoint();
      var exitCode = await runExecutable(entryPoint, args);
      await flushThenExit(exitCode);
    }

An async function can catch exceptions from Futures. For example:

    var entryPoint = await findEntryPoint();
    try {
      var exitCode = await runExecutable(entryPoint, args);
      await flushThenExit(exitCode);
    } catch (e) {
      // Handle the error...
    }

> Important: Async functions return Futures. If you don’t want your function to return a future, then use a different solution. For example, you might call an async function from your function.

For more information on using await and related Dart language features, see Asynchrony support.

### Basic usage
You can use then() to schedule code that runs when the future completes. For example, HttpRequest.getString() returns a Future, since HTTP requests can take a while. Using then() lets you run some code when that Future has completed and the promised string value is available:

    HttpRequest.getString(url).then((String result) {
      print(result);
    });
    Use catchError() to handle any errors or exceptions that a Future object might throw.

    HttpRequest.getString(url).then((String result) {
      print(result);
    }).catchError((e) {
      // Handle or ignore the error.
    });
    
The `then().catchError()` pattern is the asynchronous version of `try-catch`.

Important: Be sure to invoke catchError() on the result of then()—not on the result of the original Future. Otherwise, the catchError() can handle errors only from the original Future’s computation, but not from the handler registered by then().

### Chaining multiple asynchronous methods

The then() method returns a Future, providing a useful way to run multiple asynchronous functions in a certain order. If the callback registered with then() returns a Future, then() returns an equivalent Future. If the callback returns a value of any other type, then() creates a new Future that completes with the value.

    Future result = costlyQuery(url);
    result
        .then((value) => expensiveWork(value))
        .then((_) => lengthyComputation())
        .then((_) => print('Done!'))
        .catchError((exception) {
      /* Handle exception... */
    });
    
In the preceding example, the methods run in the following order:

1. costlyQuery()
1. expensiveWork()
1. lengthyComputation()

Here is the same code written using await:

    try {
      final value = await costlyQuery(url);
      await expensiveWork(value);
      await lengthyComputation();
      print('Done!');
    } catch (e) {
      /* Handle exception... */
    }

### Waiting for multiple futures

Sometimes your algorithm needs to invoke many asynchronous functions and wait for them all to complete before continuing. Use the Future.wait() static method to manage multiple Futures and wait for them to complete:

    Future deleteLotsOfFiles() async =>  ...
    Future copyLotsOfFiles() async =>  ...
    Future checksumLotsOfOtherFiles() async =>  ...
    
    await Future.wait([
      deleteLotsOfFiles(),
      copyLotsOfFiles(),
      checksumLotsOfOtherFiles(),
    ]);
    print('Done with all the long steps!');
    
### Stream
Stream objects appear throughout Dart APIs, representing sequences of data. For example, HTML events such as button clicks are delivered using streams. You can also read a file as a stream.

### Using an asynchronous for loop
Sometimes you can use an `asynchronous for loop (await for)` instead of using the Stream API.

Consider the following function. It uses Stream’s listen() method to subscribe to a list of files, passing in a function literal that searches each file or directory.

    void main(List<String> arguments) {
      // ...
      FileSystemEntity.isDirectory(searchPath).then((isDir) {
        if (isDir) {
          final startingDir = new Directory(searchPath);
          startingDir
              .list(
                  recursive: argResults[recursive],
                  followLinks: argResults[followLinks])
              .listen((entity) {
            if (entity is File) {
              searchFile(entity, searchTerms);
            }
          });
        } else {
          searchFile(new File(searchPath), searchTerms);
        }
      });
    }

The equivalent code with await expressions, including an asynchronous for loop (await for), looks more like synchronous code:

    Future main(List<String> arguments) async {
      // ...
      if (await FileSystemEntity.isDirectory(searchPath)) {
        final startingDir = new Directory(searchPath);
        await for (var entity in startingDir.list(
            recursive: argResults[recursive],
            followLinks: argResults[followLinks])) {
          if (entity is File) {
            searchFile(entity, searchTerms);
          }
        }
      } else {
        searchFile(new File(searchPath), searchTerms);
      }
    }
    
>Important: Before using await for, make sure that it makes the code clearer and that you really do want to wait for all of the stream’s results. For example, you usually should not use await for for DOM event listeners, because the DOM sends endless streams of events. If you use await for to register two DOM event listeners in a row, then the second kind of event is never handled.

### Listening for stream data
To get each value as it arrives, either use await for or subscribe to the stream using the listen() method:

    // Find a button by ID and add an event handler.
    querySelector('#submitInfo').onClick.listen((e) {
      // When the button is clicked, it runs this code.
      submitData();
    });
    
In this example, the onClick property is a Stream object provided by the “submitInfo” button.

If you care about only one event, you can get it using a property such as first, last, or single. To test the event before handling it, use a method such as `firstWhere(), lastWhere(), or singleWhere()`.

If you care about a subset of events, you can use methods such as `skip(), skipWhile(), take(), takeWhile(), and where()`.

### Transforming stream data
Often, you need to change the format of a stream’s data before you can use it. Use the transform() method to produce a stream with a different type of data:

var lines = inputStream
    .transform(utf8.decoder)
    .transform(new LineSplitter());

This example uses two transformers. First it uses utf8.decoder to transform the stream of integers into a stream of strings. Then it uses a LineSplitter to transform the stream of strings into a stream of separate lines. These transformers are from the dart:convert library (see the dart:convert section).

### Handling errors and completion
How you specify error and completion handling code depends on whether you use an asynchronous for loop (await for) or the Stream API.

If you use an asynchronous for loop, then use try-catch to handle errors. Code that executes after the stream is closed goes after the asynchronous for loop.

    Future readFileAwaitFor() async {
      var config = new File('config.txt');
      Stream<List<int>> inputStream = config.openRead();

      var lines = inputStream
          .transform(utf8.decoder)
          .transform(new LineSplitter());
      try {
        await for (var line in lines) {
          print('Got ${line.length} characters from stream');
        }
        print('file is now closed');
      } catch (e) {
        print(e);
      }
    }
    
If you use the Stream API, then handle errors by registering an onError listener. Run code after the stream is closed by registering an onDone listener.

    var config = new File('config.txt');
    Stream<List<int>> inputStream = config.openRead();

    inputStream
        .transform(utf8.decoder)
        .transform(new LineSplitter())
        .listen((String line) {
      print('Got ${line.length} characters from stream');
    }, onDone: () {
      print('file is now closed');
    }, onError: (e) {
      print(e);
    });
    
## dart:math - math and random
    
### Trigonometry
The Math library provides basic trigonometric functions:

    // Cosine
    assert(cos(pi) == -1.0);

    // Sine
    var degrees = 30;
    var radians = degrees * (pi / 180);
    // radians is now 0.52359.
    var sinOf30degrees = sin(radians);
    // sin 30° = 0.5
    assert((sinOf30degrees - 0.5).abs() < 0.01);

>Note: These functions use radians, not degrees!

### Maximum and minimum
The Math library provides max() and min() methods:

    assert(max(1, 1000) == 1000);
    assert(min(1, -1000) == -1000);
### Math constants
Find your favorite constants—pi, e, and more—in the Math library:

    // See the Math library for additional constants.
    print(e); // 2.718281828459045
    print(pi); // 3.141592653589793
    print(sqrt2); // 1.4142135623730951
### Random numbers
Generate random numbers with the Random class. You can optionally provide a seed to the Random constructor.

    var random = new Random();
    random.nextDouble(); // Between 0.0 and 1.0: [0, 1)
    random.nextInt(10); // Between 0 and 9.

You can even generate random booleans:

    var random = new Random();
    random.nextBool(); // true or false

## dart:convert - decoding and encoding JSON, UTF-8, and more
The dart:convert library (API reference) has converters for JSON and UTF-8, as well as support for creating additional converters. JSON is a simple text format for representing structured objects and collections. UTF-8 is a common variable-width encoding that can represent every character in the Unicode character set.

The dart:convert library works in both web apps and command-line apps. To use it, import dart:convert.

    import 'dart:convert';
    
### Decoding and encoding JSON
Decode a JSON-encoded string into a Dart object with jsonDecode():

    // NOTE: Be sure to use double quotes ("),
    // not single quotes ('), inside the JSON string.
    // This string is JSON, not Dart.
    var jsonString = '''
      [
        {"score": 40},
        {"score": 80}
      ]
    ''';

    var scores = jsonDecode(jsonString);
    assert(scores is List);

    var firstScore = scores[0];
    assert(firstScore is Map);
    assert(firstScore['score'] == 40);
    
Encode a supported Dart object into a JSON-formatted string with jsonEncode():

    var scores = [
      {'score': 40},
      {'score': 80},
      {'score': 100, 'overtime': true, 'special_guest': null}
    ];

    var jsonText = jsonEncode(scores);
    assert(jsonText ==
        '[{"score":40},{"score":80},'
        '{"score":100,"overtime":true,'
        '"special_guest":null}]');
        
Only objects of type int, double, String, bool, null, List, or Map (with string keys) are directly encodable into JSON. List and Map objects are encoded recursively.

You have two options for encoding objects that aren’t directly encodable. 
* The first is to invoke encode() with a second argument: a function that returns an object that is directly encodable. 
* Your second option is to omit the second argument, in which case the encoder calls the object’s `toJson()` method.

### Decoding and encoding UTF-8 characters
Use `utf8.decode()` to decode UTF8-encoded bytes to a Dart string:

    List<int> utf8Bytes = [
      0xc3, 0x8e, 0xc3, 0xb1, 0xc5, 0xa3, 0xc3, 0xa9,
      0x72, 0xc3, 0xb1, 0xc3, 0xa5, 0xc5, 0xa3, 0xc3,
      0xae, 0xc3, 0xb6, 0xc3, 0xb1, 0xc3, 0xa5, 0xc4,
      0xbc, 0xc3, 0xae, 0xc5, 0xbe, 0xc3, 0xa5, 0xc5,
      0xa3, 0xc3, 0xae, 0xe1, 0xbb, 0x9d, 0xc3, 0xb1
    ];

    var funnyWord = utf8.decode(utf8Bytes);

    assert(funnyWord == 'Îñţérñåţîöñåļîžåţîờñ');
    
To convert a stream of UTF-8 characters into a Dart string, specify `utf8.decoder` to the Stream `transform()` method:

    var lines = inputStream
        .transform(utf8.decoder)
        .transform(new LineSplitter());
    try {
      await for (var line in lines) {
        print('Got ${line.length} characters from stream');
      }
      print('file is now closed');
    } catch (e) {
      print(e);
    }

Use `utf8.encode()` to encode a Dart string as a list of UTF8-encoded bytes:

    List<int> encoded = utf8.encode('Îñţérñåţîöñåļîžåţîờñ');

    assert(encoded.length == utf8Bytes.length);
    for (int i = 0; i < encoded.length; i++) {
      assert(encoded[i] == utf8Bytes[i]);
    }
    
Other functionality
The dart:convert library also has converters for ASCII and ISO-8859-1 (Latin1). For details, see the API docs for the dart:convert library.

