# Listing 8.8 *(continued)*

```
```objc
@end

@implementation NSMutableDictionary (SortedKeys)

-(void)generateSortedKeys;
{
    NSMutableArray *keys = [NSMutableArray arrayWithArray:[self allKeys]];
    [keys sortUsingSelector:@selector(compare:)];
    objc_setAssociatedObject(self, @"KEYS", keys, OBJC_ASSOCIATION_RETAIN);
}

-(NSArray *)sortedKeys;
{
    return objc_getAssociatedObject(self, @"KEYS");
}

-(void)dropSortedKeys;
{
    objc_setAssociatedObject(self, @"KEYS", nil, OBJC_ASSOCIATION_RETAIN);
}

@end
```
```

As you can see, when the sorted keys array is created, it’s stored as an associative reference on self, or that is, the dictionary upon which we are operating, this is shown in -generateSortedKeys. When finished with the sorted keys, the associative reference can be removed using the -dropSortedKeys method.

Because you’re not subclassing, you do need to make sure you explicitly call the -dropSortedKeys (or whatever your cleanup method is) in order to release the memory associated with the object before deallocating it.

> **NOTE**
> 
> If you use the newer LLVM 1.5 compiler and the modern runtime, they include the ability to declare instance variables in class extensions, so you can avoid most of this rigmarole. To do so, you simply declare them as part of your extension interface, just like if you were declaring them in a class. See the LLVM documentation for the flags required to enable this behavior.

> **NOTE**
> 
> You can use `NSString` constants (as I have used here) for keys, because they are defined by the language to be static references to each other when defined inline like I have done here.