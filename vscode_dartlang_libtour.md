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
    Use contains() and containsAll() to check whether one or more objects are in a set:

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

You add, get, and set map items using the bracket syntax. Use remove() to remove a key and its value from a map.

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

Use isEmpty or isNotEmpty to check whether a list, set, or map has items:

    var coffees = [];
    var teas = ['green', 'black', 'chamomile', 'earl grey'];
    assert(coffees.isEmpty);
    assert(teas.isNotEmpty);

To apply a function to each item in a list, set, or map, you can use forEach():

    var teas = ['green', 'black', 'chamomile', 'earl grey'];

    teas.forEach((tea) => print('I drink $tea'));
    
When you invoke forEach() on a map, your function must take two arguments (the key and value):

    hawaiianBeaches.forEach((k, v) {
        print('I want to visit $k and swim at $v');
        // I want to visit Oahu and swim at
        // [Waikiki, Kailua, Waimanalo], etc.
    });
    
Iterables provide the map() method, which gives you all the results in a single object:

var teas = ['green', 'black', 'chamomile', 'earl grey'];

    var loudTeas = teas.map((tea) => tea.toUpperCase());
    loudTeas.forEach(print);

>Note: The object returned by map() is an Iterable that’s lazily evaluated: your function isn’t called until you ask for an item from the returned object.

To force your function to be called immediately on each item, use map().toList() or map().toSet():

    var loudTeas =
        teas.map((tea) => tea.toUpperCase()).toList();

Use Iterable’s where() method to get all the items that match a condition. Use Iterable’s any() and every() methods to check whether some or all items match a condition.

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

