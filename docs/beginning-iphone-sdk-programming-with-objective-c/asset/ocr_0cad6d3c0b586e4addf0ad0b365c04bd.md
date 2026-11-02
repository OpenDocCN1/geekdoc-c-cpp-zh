Because the values of the property will be retained, it is important that you free it before you exit the application. A good place to do so is in the dealloc method of a class (such as a View Controller):

```
-(void) dealloc {
    [self.name release];    //---release the name property---
    [super dealloc];
}
```

The dealloc method of a class is fired whenever the reference count of its object reaches 0.
Consider the following example:

```
SomeClass *sc1 = [[SomeClass alloc] initWithName:@"Wei-Meng Lee" andRate:35];
//...do something here...
[sc1 release];  //---reference count goes to 0; dealloc will be called---
```

The preceding example shows that when the reference count of sc1 goes to 0 (when the release statement is called), the dealloc method defined within the class will be called. If you do not define this method in the class, its implementation in the base class will be called.

# Memory Management Tips

Memory management is a tricky issue in iPhone programming. Although there are tools that you can use to test for memory leaks, this section presents some simple things you can do to detect memory problems that might affect your application.

First, ensure that you implement the didReceiveMemoryWarning method in your View Controller:

```
- (void)didReceiveMemoryWarning {
    //---insert code here to free unused objects---
    [super didReceiveMemoryWarning];
}
```

The didReceiveMemoryWarning method will be called whenever your iPhone runs out of memory. You should insert code in this method so that you can free resources/objects that you do not need.

In addition, you should also handle the applicationDidReceiveMemoryWarning: method in your application delegate:

```
- (void)applicationDidReceiveMemoryWarning:(UIApplication *)application
{
    //---insert code here to free unused objects---
    [[ImageCache sharedImageCache] removeAllImagesInMemory];
}
```

In this method, you should stop all memory-intensive activities, such as audio and video playback. You should also remove all images cached in memory.