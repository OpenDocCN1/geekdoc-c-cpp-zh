# CHAPTER 6: Manipulating Strings

```
int main(int argc, char **argv) {
    [NSAutoreleasePool new];
    MutableString *str =
        [MutableString stringWithFormat:"%d arguments: %s", argc];
    for (int i=0; i<argc; i++) {
        [str appendFormat:"%s \ argv[i]];
    }
    NSLog("%%@", str);
    return 0;
}
```

From: formatstring.m

start of this program. Using format strings creates some temporary autoreleased. If you don’t have an autorelease pool, you will get a warning that these objects are leaked. In this trivial program, they are leaked anyway; there’s no point in telling the autorelease pool to collect them because the operating system will reclaim the memory when the process exits anyway.

This example first a mutable string containing the number of arguments passed to the program. It then loops over the remaining arguments, appending each (as a C string) to the mutable string. Finally, it passes the result to NSLog().

The NSLog() function also uses format strings. It’s tempting to just pass str as the first