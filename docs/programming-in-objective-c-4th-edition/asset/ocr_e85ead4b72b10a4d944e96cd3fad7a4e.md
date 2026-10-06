```
substr];
    NSLog("%@", mstr);
}
```

```
// Set the mutable string directly
```

```
[mstr set: @"This is string A"];
NSLog("%@", mstr);
```

```
// Now let's replace a range of chars
with another
```

```
[mstr replaceCharactersInRange:
NSMakeRange(8, 8)
    withString: @"a
mutable string"];
NSLog("%@", mstr);
```

```
// Search and replace
```

```
search = @"This is";
replace = @"An example of";
```

```
if (substr.location != NSNotFound) {
    [mstr replaceCharactersInRange: substr
    withString:replace];

```

```
NSLog("%@", mstr);
}
```

```
// Search and replace all occurrences
```

```
search = @"a";
replace = @"x";
```