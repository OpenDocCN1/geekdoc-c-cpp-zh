The key difference between an object created using the alloc (or new) keyword and one created using a convenience method is that of ownership, as the following example shows:

```
NSString *str1 = [[NSString alloc] initWithFormat:@"%d", 4];
[str1 release]; //---this is ok because you own str1---
NSString *str2 = [NSString stringWithFormat:@"%d", 4];
[str2 release]; //---this is not ok because you don't own str2---
//---str2 will be removed automatically when the autorelease pool is activated---
```

If you want to take ownership of an object when using a convenience method, you can do so using the retain keyword:

```
NSString *str2 = [[NSString stringWithFormat:@"%d", 4] retain];
```

To release the object, you can use either the autorelease or release keyword. You learned earlier that the release keyword immediately decreases the reference count by 1 and that the object is immediately de-allocated from memory when the reference count reaches 0. In contrast, the autorelease keyword promises to decrease the reference count by 1, not immediately, but sometime later. It is like saying, "Well, I still need the object now, but later I can let it go." The following code makes it clear:

```
NSString *str = [[NSString stringWithFormat:@"%d", 4] retain];
[str autorelease]; // you don't own it anymore; still available
NSLog(str);       // still accessible for now
```

> NOTE After you have autoreleased an object, do not release it anymore.

Note that the statement

```
NSString *str2 = [NSString stringWithFormat:@"%d", 4];
```

has the same effect as

```
NSString *str2 = @"4";
```

Although autorelease objects seem to make your life simple by automatically releasing objects that are no longer needed, you have to be careful when using them. Consider the following example:

```
for (int i=0; i<=99999; i++){
    NSString *str = [NSString stringWithFormat:@"%d", i];
    //...
    //...
}
```

You are creating an NSString object for each iteration of the loop. Because the objects are not released until the function exits, you may well run out of memory before the autorelease pool can kick in to release the objects.

One way to solve this dilemma is to use an autorelease pool, as discussed in the next section.