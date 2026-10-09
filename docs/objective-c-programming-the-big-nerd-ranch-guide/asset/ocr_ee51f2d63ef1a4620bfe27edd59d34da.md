```
[anObject release]; // anObject loses an owner
[anObject retain]; // anObject gains an owner
```

You would see these sorts of calls primarily in accessor methods (where the new value was retained and the old value was released) and in dealloc methods (where all the previously retained objects were released). The setHolder: method for Asset would have looked like this:

```
- (void)setHolder:(Employee *)newEmp
{
    [newEmp retain];
    [holder release];
    holder = newEmp;
}
```

The dealloc method would have looked like this:

```
- (void) dealloc
{
    [label release];
    [holder release];
    [super dealloc];
}
```

What about the description method? It creates and returns a string. Should Asset claim ownership of it? That wouldn't make sense; the asset is giving away the string it created. When you autorelease an object, you are marking it to be sent release in the future. Before ARC, the description method for Asset would look like this:

```
- (NSString *)description
{
    NSString *result = [[NSString alloc] initWithFormat:@"<%@: $%d >",
                     [self label], [self resaleValue]];
    [result autorelease];
    return result;
}
```

When would it be sent release? When the current autorelease pool was drained:

```
// Create the autorelease pool
NSAutoreleasePool *arp = [[NSAutoreleasePool alloc] init];
Asset *asset = [[Asset alloc] init];

NSString *d = [asset description];
// The string that d points to is in the autorelease pool

[arp drain]; // The string is sent the message release
```

ARC uses the autorelease pool automatically, but you must create and drain the pool. When ARC was created, we also got a new syntax for creating an autorelease pool. The code above now looks like this:

```
// Create the autorelease pool
@autoreleasepool {
    Asset *asset = [[Asset alloc] init];

    NSString *d = [asset description];
    // The string that d points to is in the autorelease pool
}
// The pool is drained
```