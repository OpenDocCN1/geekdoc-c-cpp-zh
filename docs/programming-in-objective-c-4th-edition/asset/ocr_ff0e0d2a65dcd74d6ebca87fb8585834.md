```
NSLog("Chars from index 8 through 13:
%@", res);
```

```
// An easier way to do the same thing
```

```
res = [strl] substringWithRange:
NSMakeRange(8, 6]);
NSLog("Chars from index 8 through 13:
%@", res);
```

```
// Locate one string inside another
```

```
subRange = [strl] rangeOfString: "string
A"];
NSLog("String is at index %lu, length
is %lu",
subRange.location, subRange.length);
```

```
subRange = [strl] rangeOfString: "string
B"];
if (subRange.location == NSNotFound)
NSLog("String not found");
else
NSLog("String is at index %lu, length
is %lu",
subRange.location,
subRange.length);
}
return 0;
}
```