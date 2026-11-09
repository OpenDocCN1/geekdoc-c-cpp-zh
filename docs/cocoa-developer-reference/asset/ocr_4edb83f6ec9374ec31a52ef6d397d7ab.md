# ## Using NSOperationQueue

To run an NSOperation object, create an instance of NSOperationQueue, a queue manager object. Create as many instances of NSOperation as you need. Queue them with

```
`[aQueue addOperation: anInstance];`
```

This adds the operation to the queue. The queue runs the operation when it has a free execution slot, and manages objects before they’re executed. Sample code that runs up to four instances simultaneously follows:

```
```objective-c
#import "NSOperationAppDelegate.h"
#import "BackgroundTask.h"
@implementation NSOperationAppDelegate
@synthesize window;
static NSOperationAppDelegate *sharedInstance;
+ (id) shared {
    //Other objects can use shared to get a pointer to this object
    return sharedInstance;
}
- (void)applicationDidFinishLaunching:(NSNotification *) aNotification {
    sharedInstance = self;
    NSOperationQueue *theQueue = [[NSOperationQueue alloc] init];
    //[theQueue setMaxConcurrentOperationCount:1];
    // When set to 1, dispatches tasks sequentially
    [theQueue setMaxConcurrentOperationCount:4];
    // When set to 4, dispatches up to 4 tasks concurrently
    BackgroundTask *task1 =
    [[BackgroundTask alloc] initWithInt:1000];
    [theQueue addOperation:task1];
    BackgroundTask *task2 =
    [[BackgroundTask alloc] initWithInt:2000];
    [theQueue addOperation:task2];
    BackgroundTask *task3 =
    [[BackgroundTask alloc] initWithInt:500];
    [theQueue addOperation:task3];
}
- (void) taskDidFinish: (id) sender {
    NSLog(@"Task %@ finished", sender);
}
@end
```
```

![](bbox=[0.103, 0.818, 0.171, 0.873])

# ### CAUTION

You can use a suspend method to control the queue. It doesn't suspend execution, as you might expect; it suspends dispatch. When the queue is suspended, no more tasks are queued until the suspension is cancelled.

The +(id) shared method is a convenient way to give other objects a pointer to the App Delegate when they need to message it. It’s not obligatory, but is a simple way to allow tasks to “call home” if they need to.