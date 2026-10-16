
| Method | Purpose |
|---|---|
| +stringWithContentsOfURL:encoding:error: | Constructs a new string containing the contents of the resource specified by the URL. The resource will be downloaded using the specified protocol, and decoded using the provided encoding. This call will block while the resource is downloading. |
| +stringWithContentsOfFile:usedEncoding:error: | Constructs a new string containing the contents of the file specified. Will attempt to automatically detect the type of file encoding used and inform the caller of the type of encoding detected via the usedEncoding out parameter. |
| +stringWithContentsOfURL:usedEncoding:error: | Constructs a new string containing the contents of the resource specified by the provided URL. Will download the resource, and attempt to detect the type of file encoding used and inform the caller of the encoding type via the usedEncoding out parameter. |

Each of these also has an initializer version that can be used if you prefer to create your strings that way.

## NOTE

The term “factory method” refers to class methods that can be used to construct an object using particular arguments.

## Using format strings

One of the more commonly used factory methods is the +stringWithFormat: factory method, which utilizes a printf style format string and a list of arguments to construct the string. (I use format strings in many of the examples of this book. Every time you see a call to NSLog, you see an instance of a format string.) Listing 12.3 shows an example of a format string used with a call to NSLog.

## Listing 12.3

### The format string in NSLog

```
NSLog(@"The age of the employee named %@ is %ld", [employee name], [employee age]);
```

The use of @"" indicates the format string is an instance of NSString. When creating a format string, you use a special combination of percent signs and characters to indicate particular

parameters that will be substituted into the string when it is passed to the object that is using the string. The format string contains three kinds of components, the first is the format specifiers. A format specifier is a special combination of characters, beginning with a %, followed by one or more numbers and letters specifying the format of the argument to be substituted into the format string at runtime. You can use a format specifier to insert anything from an object, to an integer, or a float. A format specifier can also specify how the argument is formatted when placed into the string. For example, to construct a format specifier to insert a floating-point value with two decimal places after it, you use a format specifier, such as %.2f. The different characters used for the format specifiers are extensive and comprehensive, and could probably fill a book this size with their complexity and quirks. Therefore, I won’t go into a great amount of detail about all of them. I encourage you to read the Apple documentation on format strings.

That said, however, there is one format specifier which I would like to address specifically. It is the format specifier %@. This specifier is special to Objective-C. It is intended to be used in conjunction with object arguments. What it does is cause the format string to take the object passed as an argument for that format specifier and call the method -description on that object in order to get a string representation of that object. Most foundation classes have a -description method that returns something sensible for the class in question. NSString’s -description method actually returns the string itself. NSArray’s -description method returns a string that shows a stringified representation of the contents of the array. The default NSObject implementation of -description returns a string, which shows the pointer address of the object. If you create a custom class, and you want to use this feature of format strings with your class, be sure to override the -description method accordingly.

The second type of component that can be used in a format string is called an escape sequence. You use escape sequences to insert special, nonstandard characters into the string. The first letter of an escape sequence is always a backslash character followed by a character that tells the compiler what type of special character you wish to insert. For example, to insert a carriage return character into the string, you use the escape sequence \r.

The most commonly used escape sequences are \n to insert a newline, \r for a carriage return, \" for a double quote, and \t for a tab character. Because of the use of the \ character to begin an escape sequence, the escape sequence \\ also inserts just a \ character.

Finally, the third type of component you can use in a format string is essentially anything that doesn’t fall into the first two component categories. These characters are simply passed straight through into the final result.

When a format string is interpreted, it goes through the format string, and for each format specifier that it encounters, it looks for a following argument to the function for which this format string is an argument itself. It then substitutes the value of that argument into the result string and performs whatever conversion the format specifier indicates. To give you an idea of exactly how this works, take a look at Listing 12.4.

## Listing 12.4

### Using format strings

```
NSString *str;

NSString *cardName = @"Ace";
NSString *cardSuit = @"Spades";

str = [NSString stringWithFormat:@"The winning card is %@ of %@.",
    cardName, cardSuit];
// str is "The winning card is Ace of Spades."

str = [NSString stringWithFormat:@"You have %ld gold!",
    [player goldAmount]];
// str is "You have 1000 gold!"

str = [NSString stringWithFormat:@"Your change is: $%.2f.", change];
// str is "Your change is $2.43
```

Notice that the arguments passed when working with format strings are passed using an unusual syntax. The format string allows you to pass a variadic argument list to the +stringWithFormat method. The count of arguments is determined by how many format specifiers are provided.

## NOTE

To ensure your code is 64-bit safe, it's generally considered a best practice to use the %ld format specifier when working with integers. When using NSInteger as the type for your integers, it will automatically change with the architecture from 32-bit to 64-bit. Using %ld for your format specifier insures that the format string will work with either 32-bit or 64-bit NSIntegers, regardless of their size.

## Working with Other NSString Methods

Using format strings allows you to create strings in a much more flexible fashion than if you simply had to append them together. Various applications for format strings are available aside from simply constructing new strings. For example, you can also append a formatted string, as shown in Listing 12.5.

## Listing 12.5

### Appending a formatted string

```
NSMutableString *str = [...] ;

[str appendFormat:@"Your change is: %.2f.", change];
```

You can also split a string into separate components by using the method -componentsSeparatedByString:. This method will search for instances of the given string within the receiver, and then returned and NSArray containing the parts of the string separated by that string. Listing 12.6 shows example of this.

## Listing 12.6

### Splitting a string into its components

```
NSString *str = @"This is a string of words.";

NSArray *words = [str componentsSeparatedByString:@" "];

// words is now [@"This", @"is", ... ]
```

Similarly, the corollary to this is the NSArray method -componentsJoinedByString: which will do the opposite operation. It will take an array of strings and combine them into a single string with each component separated by the given string.

You can perform string searching and replacement using methods like -rangeOfString: to find the range of a given string within the receiver, or -stringByReplacingOccurrencesOfString:withString: to do string replacement. NSString even has some limited regular expression matching support as well.

Overall, NSString is an amazingly powerful and comprehensive class with a lot of functionality much more than can be covered here. My advice is to visit the NSString documentation, and review all the methods it provides you.
