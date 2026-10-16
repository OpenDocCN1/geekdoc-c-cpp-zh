# Listing 5.8 (continued)

```
}
-(void)doSomethingWithBlock;
-(void)setMyBlock:(void (^)(NSString *))inBlock;
@end;

@implementation Foo

-(void)dealloc
{
    [myBlock release];
    [super dealloc];
}

-(void)setMyBlock:(void (^)(NSString *))inBlock
{
    myBlock = [inBlock copy];
}

-(void)doSomethingWithBlock
{
    myBlock(@"foo");
    // ...
}
@end
```

As you can see, all of the standard Objective-C reference counting memory management methods work with blocks just like any other Objective-C object. Although you should use -copy instead of -retain for the block object that is passed in since it’s allocated on the stack and you’ll want to be sure to get a copy on the heap if you want to keep it around.

The way this works is that the runtime will make a const copy of any external variables that the block uses and the self object to the heap. This way you have access to those variables and all of the member variables of the object within which the block is created. Any variables marked with the __block directive are bit-copied to the heap, and the block is responsible for any additional memory management involved in working with those variables.

All this said, if your application uses garbage collection, instead of reference counted memory management, copying, retaining, and releasing are all done for you.