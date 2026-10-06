```
'X'];
```

```
NSLog("%c", [myNumber charValue]);
```

```
// float value
```

```
floatNumber = [NSNumber numberWithFloat:
100.00];
```

```
NSLog("%g", [floatNumber floatValue]);
```

```
// double
```

```
myNumber = [NSNumber numberWithDouble:
12345e+15];
```

```
NSLog("%lg", [myNumber doubleValue]);
```

```
// Wrong access here
```

```
NSLog("%li", (long) [myNumber
integerValue]);
```

```
// Test two Numbers for equality
```

```
if ([intNumber isEqualTo:
floatNumber] == YES)
```

```
NSLog("Numbers are equal");
```

```
else
NSLog("Numbers are not equal");
```

```
// Test if one Number is <, or =
second Number
```

```
if ([intNumber compare: myNumber] ==
NSOrderedAscending)
```

```
NSLog("First number is less than
second");
```

```
}
```