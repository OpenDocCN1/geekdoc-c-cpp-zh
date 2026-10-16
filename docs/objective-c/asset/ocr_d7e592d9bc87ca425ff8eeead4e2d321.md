# Listing 12.5

# Appending a formatted string

```
NSMutableString *str = [...] ;

[str appendFormat:@"Your change is: %.2f.", change];
```

You can also split a string into separate components by using the method -components SeperatedByString:. This method will search for instances of the given string within the receiver, and then returned and NSArray containing the parts of the string separated by that string. Listing 12.6 shows example of this.

# Listing 12.6

# Splitting a string into its components

```
NSString *str = @"This is a string of words.";

NSArray *words = [str componentsSeperatedByString:@" "];

// words is now [@"This", @"is", ... ]
```

Similarly, the corollary to this is the NSArray method -componentsJoinedByString: which will do the opposite operation. It will take an array of strings and combine them into a single string with each component separated by the given string.

You can perform string searching and replacement using methods like -rangeOfString: to find the range of a given string within the receiver, or -stringByReplacingOccurrences OfString:withString: to do string replacement. NSString even has some limited regular expression matching support as well.

Overall, NSString is an amazingly powerful and comprehensive class with a lot of functionality much more than can be covered here. My advice is to visit the NSString documentation, and review all the methods it provides you.