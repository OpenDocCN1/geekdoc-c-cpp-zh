On my laptop the performance is even better than before. The time for the minimum width of two has gone from around twenty seconds to less than five. The time for a width of one is now around twenty seconds. Next, we'll start to wrap the calculations in queues that don't execute on the main thread.

# 26.6  Global Concurrent Queues

This next change is striking. You'll get a little performance improvement, but the main difference is that the drawing will begin right away, and the image will update until it is finished.

When you don't need to integrate with the main GUI thread, you should look to see whether you can safely spin off an operation to another thread. When you can, you should use a global concurrent queue. You get a handle to one by calling the function dispatch_get_global_queue(). The first argument specifies the priority of the queue. Your choices are DISPATCH_QUEUE_PRIORITY_DEFAULT, DISPATCH_QUEUE_PRIORITY_LOW, and DISPATCH_QUEUE_PRIORITY_HIGH. The docs explain that the second argument should be 0 for now because that slot is being reserved for future expansion.

Soon we'll use lots of these concurrent queues. For now we'll just send the calls to spawn off the four subtile s to a concurrent queue inside the split method. Use the default priority level.

```
```objc
-(void) split {
    CGFloat size = (self.frame.size.width)/2;
    CGFloat x = self.frame.origin.x;
    CGFloat y = self.frame.origin.y;
    dispatch_async(
        dispatch_get_global_queue(DISPATCH_QUEUE_PRIORITY_DEFAULT, 0), ^{
            [self tileWithX:x Y:y size:size];
            [self tileWithX:x Y:y+size size:size];
            [self tileWithX:x+size Y:y size:size];
            [self tileWithX:x+size Y:y+size size:size];
        });
    [self.grid.tiles removeObject:self];
}
```
```

The result is much more satisfying. You should quickly see some of the larger squares displayed, and then you should see the fractal animate a bit as the image is refined. Try this with different values for the