# Trimming Strings

# Trimming Strings

```
NSString *str =
@" a String with leading spaces"
str = [str
stringByTrimmingCharactersInset:
[CharacterSet whitespaceCharacterSet]];
str = [str substringFromIndex:2];
NSAssertisEqualTo:
@"String with leading spaces"],
"Trimming failed");
```

From: trim.m
Often, when you have a string, you want to trim the ends, removing either a fixed number of characters or characters from a particular set. A common example of the second case is removing leading and trailing whitespace from a string.
Objective-C string objects support quite a few methods for doing this. If you just want to remove the trailing or leading characters from a string, the -substringWithRange: method on NSString is the most useful. This will create a new string object containing a range of characters in another string. This is a very cheap operation on immutable strings; it just returns a string object that references the data in the original string, it doesn't copy the string. When you call it on a mutable string, however, it must copy the characters. remove characters from a particular set, you need to understand NSCharacterSet objects. As its name implies, this class encapsulates a set of