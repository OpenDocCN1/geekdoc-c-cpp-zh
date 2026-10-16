Ideal scenario, they will be deleted the next time the runtime exits its run loop. In practice, of course it’s not always quite that simple. Because of this, you want to avoid creating large amounts of objects using the autorelease pool. On platforms with especially strict memory limitations, it is even possible to exhaust your memory without having any memory leaks. Take, for example, the code shown in Listing 4.9.

# Listing 4.9

# Leaving many objects on the autorelease pool

```
```objective-c
-(void)inflateMemoryUsage
{
for(NSUInteger n = 0; n < 100000; ++n)
{
// this object is autoreleased
NSData *data = [self getBigBlobOfData];
// do something with data...
[self doStuff:data];
}
// all 100,000 data objects are still alive here.
}
```
```

In this case, the code seems simple enough. Notice, however, that I am executing a tight loop wherein objects are being allocated and being left on the autorelease pool to be released later. Because this code is looping, the execution flow is not exiting the current stack. The autorelease pool is never being drained. Thus, memory use continues to simply climb.

You can resolve this problem several different ways. The first, of course, is to simply release the objects instead of using autoreleased objects. For example, if you rewrote the code in Listing 4.9 to be like Listing 4.10, the problem would go away.

# Listing 4.10

# Releasing the objects inside the loop

```
```objective-c
-(void)inflateMemoryUsage
{
for(NSUInteger n = 0; n < 100000; ++n)
{
// this object is autoreleased
NSData *data = [self getBigBlobOfData];
// do something with data...
[self doStuff:data];
}
}
```
```