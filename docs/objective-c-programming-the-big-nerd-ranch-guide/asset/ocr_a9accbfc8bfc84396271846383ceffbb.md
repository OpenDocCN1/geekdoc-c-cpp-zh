common proper names that are also regular words. For example, “Glen” is a guy’s name, and “glen” is a narrow valley. In the word files, proper names are capitalized.

When a computer orders strings, it typically considers uppercase letters as coming before lowercase letters. To do a comparison that ignores the case, use the method `caseInsensitiveCompare:`.

```
```objectivec
NSString *a = @"ABC";
NSString *b = @"abc";
if ([a caseInsensitiveCompare:b] == NSOrderedSame) {
    NSLog(@"a and b are equal");
}

if ([a caseInsensitiveCompare:b] == NSOrderedAscending) {
    NSLog(@"a comes before b");
}

if ([a caseInsensitiveCompare:b] == NSOrderedDescending) {
    NSLog(@"b comes before a");
}
```
```