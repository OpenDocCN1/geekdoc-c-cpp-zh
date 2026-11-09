Here’s how we register our Display to listen for changes in the count property of the UpOrDown object. We’ll register when the Display object awakes from nib.

```
```objc
-(void) awakeFromNib {
    [counter addObserver:self
              forKeyPath:@"count"
                 options:NSKeyValueObservingOptionNew
                 context:NULL];
}
```
```

All objects inherit addObserver:forKeyPath:options:context: from NSObject so the Display object can send that message to the UpOrDown object to register itself as an observer of the count property.

Don’t forget to clean up after yourself. You need to unregister your observers when the observer is being released. When we managed memory by reference counting, we released resources in the dealloc method. Now, with automatic garbage collection turned on, we instead use the finalize method as dealloc is never called.

```
```objc
-(void) finalize {
    [counter removeObserver:self forKeyPath:@"count"];
    [super finalize];
}
```
```

That’s all there is to responsibly registering an observer.

# 20.5 Making Changes Observable

We’ve seen so much magic in Cocoa that it seems as if you should just be able to set the value of UpOrDown’s ivar count like this and have the change get picked up by Display.

```
```objc
-(void) step: (id) sender {
    //not good enough
    count = [NSNumber numberWithInteger:[sender integerValue]];
}
```
```

Unfortunately, when you set a variable directly, you need to bracket the change with a signal that an observed value is about to change and another signal that the observed value did change.