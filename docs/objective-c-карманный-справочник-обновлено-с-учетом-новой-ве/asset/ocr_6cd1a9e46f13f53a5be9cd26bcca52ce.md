# Comparing Strings

Objective-C runtime or Foundation framework to be linked in order to work. They also have a flags field, allowing their internal representation to be either UTF-8 or UTF-16, depending on which is more efficient for their contents.

Constant Objective-C strings are created by prefixing a constant C string literal with an symbol, as in "@string". You also create constant Core Foundation strings by using the CFSTR macro, in both C and Objective-C code. This macro calls a compiler built-in function which generates a constant string object.

# Comparing Strings

```
NSString *twelve = @"12";nNSString *twelveFromInt =
[NSString stringWithFormat:@"%d", 12];
NSNumber *numberTwelve =
[NSNumber numberWithInt:12];

if ([twelve isEqualToString:twelveFromInt])
    NSLog(@"Both strings are equal");
if (twelve == twelveFromInt)
    NSLog(@"Both strings are identical");
if (twelve == @"12")
    NSLog(@"Constant strings are identical");
if ([twelve isEqual:numberTwelve])
    NSLog(@"String is equal to number");
```

From: CompareStrings.m The simplest and most obvious way of comparing strings for equality is the C