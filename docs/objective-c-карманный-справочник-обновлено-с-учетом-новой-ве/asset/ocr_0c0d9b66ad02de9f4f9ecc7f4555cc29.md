# 146 CHAPTER 6: Manipulating Strings

characters. You can create these from a string, but there are also a number of predefined ones that represent a particular well-defined set of characters.

This class is used in a similar way to the ctype.h functions in C. You can send it a -characterIsMember: message to test whether a single character is a member of the set. Calling ispunct() C library function, for example, is equivalent to sending a -characterIsMember: message to the object obtained by sending a +punctuationCharacterSet message to NSStringSet.

The Objective-C version is more verbose, but is more generic. Character set objects can be passed around your code easily. The NSString class uses them in a number of places. You can ask for the range within a string of characters in a given set, or split a string using a character set to define the separators, for example.

# Splitting Strings

```
NSString *str = @"A String with\twords and spaces";nNSArray *wordsWithTab = [str componentsSeparatedByString:@" "];\NSArray *words = [str componentsSeparatedByCharactersInset:[CharacterSet whitespaceCharacterSet]];
```

From: split.m