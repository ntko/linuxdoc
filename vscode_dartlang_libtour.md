<!-- TOC -->

- [Dart lib tour](#dart-lib-tour)
    - [Strings and regular expressions](#strings-and-regular-expressions)
    - [Searching inside a string](#searching-inside-a-string)
    - [Extracting data from a string](#extracting-data-from-a-string)
    - [Converting to uppercase or lowercase](#converting-to-uppercase-or-lowercase)
    - [Trimming and empty strings](#trimming-and-empty-strings)
    - [Replacing part of a string](#replacing-part-of-a-string)
    - [Building a string](#building-a-string)
    - [Regular expressions](#regular-expressions)
    - [More information](#more-information)

<!-- /TOC -->

## Dart lib tour

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

