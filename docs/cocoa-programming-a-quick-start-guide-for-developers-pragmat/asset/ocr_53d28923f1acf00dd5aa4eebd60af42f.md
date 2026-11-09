# ### 6.9 Cleaning Up in dealloc

When the reference count for an object reaches zero, its `dealloc` is called. This is where you clean up the resources used by your object. For example, in `Greeter` there are two pointers to objects that we own: `name` and `today`. We need to send each a `release` when our `Greeter` object is about to be destroyed. We do this by overriding the `dealloc` method:

Download Memory/Flashlight16/Classes/Greeter.m

```
```objective-c
- (void) dealloc {
    [name release];
    [today release];
    [super dealloc];
}
```
```

Note that in the `init` method we let the superclass do its initialization before we did our custom initialization. Here we clean our custom objects up first and end with a call to `[super dealloc]`.

You can add this line to your `dealloc` to output a quick message to the Console window when your `Greeter` object is being freed.

```
```objective-c
NSLog(@"In Greeter dealloc.");
```
```

If you are a belt and suspenders type of person and want to make sure that there's no chance that you end up sending a message to a freed object, then you may want to set the variables to `nil` after you release them like this:

Download Memory/Flashlight16/Classes/Greeter.m

```
```objective-c
- (void) dealloc {
    [name release];
    name = nil;
    [today release];
    today = nil;
    [super dealloc];
}
```
```

Here you are releasing the instance variable and setting it to `nil`. You can combine these steps using the corresponding property like this:

Download Memory/Flashlight16/Classes/Greeter.m

```
```objective-c
- (void) dealloc {
    self.name = nil;
    self.today = nil;
    [super dealloc];
}
```
```