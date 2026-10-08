
# Reading Numbers from Strings

131

same form. They take a pointer to a variable and return a **BOOL**, indicating whether they succeeded. The scanner stores the current scanning index in the string, and only increments it on a successful scan, so you can try parsing the next characters in different ways. You can also implement read-ahead and backtracking easily with **Scanner**. If you send it a `-scanLocation` message, it returns the current index in the string. You can then try scanning a few things, get to an error, and backtrack by sending it a `-setScanLocation:` message, resetting the old index.

One of the most powerful methods in NSScanner is `-scanCharactersFromSet:into:`. This reads a string from the current scanning point until it encounters a character not present in the specified set. As we will see in Chapter 6, you can construct **NSCharacterSet** instances with any arbitrary set of characters, or you can use one of the standard ones.

The example at the start of this section reads a number, then a word, then another number from a string. The number is read using the built-in **-scanInt:** method, but the word is a bit more complex. It uses an **NSCharacterSet**, in this case the set of all letters.

This isn't the only **NSCharacterSet** used in this example. This scanner is also configured to skip whitespace. The **setCharactersToBeSkipped:** message sent to the scanner tells it to ignore any characters in the set passed as the argument. Passing the whitespace character set tells it to skip any whitespace that occurs between calls. If there are characters in this set at the position where the scanner starts reading when you send it a scan message, it will skip past them. It will not skip these characters while parsing a token, so putting “1 2” in the string would be read as two separate numbers, not as 12.

# Manipulating Strings

Objective-C provides two sorts of strings: C strings and Objective-C strings, also called string objects. As a compiler extension, GCC also lets you use Pascal strings, but these are rare and are only supported for compatibility with Pascal libraries.

A string is a very primitive data type. It is an array of characters, terminated by a NULL byte. It has no concept of character encodings, and can be used to store any sequence of bytes that does not contain a zero byte. UTF-8 was specifically designed to be usable with C strings: It is a variable-width encoding that does not use zero bytes, even in multibyte sequences.

An Objective-C string is a higher-level abstraction. It is accessed as a sequence of UTF-16 characters, but its internal representation is private. If you compile Objective-C for the GNU runtime, constant strings are represented by an instance of a class with three instance variables: the isa pointer, a pointer to a C string, and an integer containing the length of the C string. The runtime library will set the isa pointer to the correct class when the module is loaded.

When you access individual characters in Objective-C string, you use the unichar type. This represents a single UTF-16 character. Note that UTF-16 is also a variable-length encoding, and that a single Unicode character may be more than one UTF-16 character. To make matters more confusing, combining marks like accents may mean that more than one Unicode character is used to represent a single glyph.

# Creating Constant Strings

```
const char *cstring = "C string";
NSString *objcstring = @"Objective-C string";
CFNSStringRef cfstring = CFStringCreateWithCString(NULL, "Core Foundation string", kCFStringEncodingASCII);
```
From: constantStrings.m

On OS X, Objective-C strings are toll-free bridged with Core Foundation (CF) strings. Constant CF strings are represented in a similar way to GNU runtime Objective-C strings, but with a few differences. Their isa pointer is present in the Core foundation framework, so they don't require the Objective-C runtime or Foundation framework to be linked in order to work. They also have a flags field, allowing their internal representation to be either UTF-8 or UTF-16, depending on which is more efficient for their contents.

Constant Objective-C strings are created by prefixing a constant C string literal with an symbol, as in "@". You also create constant Core Foundation strings by using the CFSTR macro, in both C and Objective-C code. This macro calls a compiler built-in function which generates a constant string object.

# Comparing Strings

```
NSString *twelve = @"12";
NSString *twelveFromInt = [NSString stringWithFormat:@"%d", 12];
NSNumber *numberTwelve = [NSNumber numberWithInt:12];

if ([twelve isEqualToString:twelveFromInt])
    NSLog(@"Both strings are equal");
if (twelve == twelveFromInt)
    NSLog(@"Both strings are identical");
if (twelve == @"12")
    NSLog(@"Constant strings are identical");
if ([twelve isEqual:numberTwelve])
    NSLog(@"String is equal to number");
```
From: CompareStrings.m The simplest and most obvious way of comparing strings for equality is the C comparison operator, ==. Unfortunately, this actually does work sometimes, which can lead to some subtle bugs. It will test whether two objects are identical, rather than equal. It will test whether they are the same object, not whether they are objects with equal values. Comparing two pointers is much faster than comparing two strings, and even faster than sending a message. In some cases, it may be faster to try a pointer comparison first. The result of the pointer comparison is the knowledge that the two strings are the same or that they might be the same. It won't ever tell you that they are definitely different. This can make code faster, if you are comparing identical strings a lot, but is usually an example of premature optimization.

If you want to test two strings for equality, you should use the -isEqualToString: method. Note that this expects the argument to be another Objective-C string. You can compare any two Objective-C objects by sending them -isEqualTo: messages, but it is up to the receiver to decide which objects it considers to be equal.

In the sample at the start of this section, the compiler will typically combine the constant strings, so that twelve and the literal @"12" will be the same object. This is not guaranteed, but there is no good reason for the compiler not to do it.

The comparison between the string and the NSNumber instance is more interesting. You’d expect this to compare the string to the result of sending -stringValue to the number, but it doesn’t.

This is important, because equality has to be commutative. If [a isEqual:b], then a lot of code will assume [b isEqual:a]. This is especially true in collection classes. If you insert two objects into an NSMutableSet, for example, where the equality holds in one direction but not the other, then the result is undefined.

Often, when you want to compare strings—or indeed, any objects—you want to find out not whether they are equal, but their ordering. This is where things start to get complicated for strings. Given two numbers, there is a single canonical ordering between them. For strings, there are several well-defined orderings. Which order should “etoile,” “Étoilé,” and “Eile” be arranged in?

If you are doing a case-insensitive comparison, the first and last ones will have equal rank. Whether accented letters come immediately before or after their unaccented variants, or before after all unaccented letters, depends on your locale. When you have a list of files, the user might get irritated if you sort “file10” before “file2,” even though that’s the dictionary order of the filenames.

For simple comparisons, based solely on the character values, you can use the -compare method. This, like all other comparison results, returns an NSComparisonResult, an enumerated type with three possible values: NSOrderedAscending, NSOrderedSame, and NSOrderedDescending. If you are presenting data to the user, you should use -localizedCompare: instead. This will return the ordering of the strings according to the rules defined for the user’s chosen language. Both of these are wrappers around this general comparison method:

+   - (NSComparisonResult)
  compare: (NSString*)aString
  options: (NSStringCompareOptions)mask
  range: (NSRange)range
  locale: (id)locale;

This allows you to specify a set of options, such as NSNumericSearch for sorting 10 after 9, and NSCaseInsensitiveSearch for ignoring case. Passing a range as the third parameter allows you to restrict the comparison to a substring in the receiver, and passing a locale lets you specify the ordering rules for non-ASCII characters. It’s worth noting that normally passing nil as a locale means either use the current locale or the canonical locale. In this case, passing nil means use the canonical locale and perform numeric comparisons on the character values.
