
## Creating Custom Work Queues

pushed, but they may complete in an arbitrary order, and any number of them might be running at once.

There is also one special queue, which is intended to run on the main thread. You can get a reference to this with dispatch_get_main_queue(). This queue is used on OS X 10.6 to implement the run loop. This queue is a FIFO queue, and you may wish to create similar queues. A FIFO queue is similar to a lightweight thread. It executes sequentially, one block at a time. The relationship between threads and queues is variable. All of your queues may end up running concurrently on separate threads, or all may be executed on a single OS thread, depending on various factors.

You create a new FIFO queue by calling dispatch_queue_create(). This is useful when you have a number of things that need to execute in a defined order, but are largely independent of the rest of the program. This helps reduce the need for explicit synchronization.

The example at the start of this chapter pushed three blocks that incremented a counter and one that printed its final value into a new queue. These blocks are all related; executing them in the wrong order is a very bad idea. With this approach, they all execute in a guaranteed order with respect to each other, but not with regard to the rest of the program. This means that you don’t need to put any lock around the counter variable, unless you plan on accessing it from outside of the queue.

## Notifications

Objective-C encourages loose coupling, and nothing in the Foundation framework better epitomizes this than the notification* mechanism. Notifications are a simple way of implementing callbacks for arbitrary numbers of listeners.

You can listen for notifications with a specific name, from a specific object, or both. The notification itself has a sender, a name, and a dictionary associated with it, so objects can pass arbitrary amounts of information to things that are listening for notifications.

If you use notifications, you make it very easy to reuse your classes. Rather than expecting every class that wants to listen for events from your classes to implement a particular interface, you just post notifications. Any number of classes can listen for notifications from the same object, and your class doesn’t have to implement any of the logic for storing references to them.

## Requesting Notifications

```objectivec
-(void)notify:(NSNotification*)note {
    NSLog("Received %@", note);
}
-(void)registerListener {
    NSNotificationCenter *nc =
        [NSNotificationCenter defaultCenter];
    [nc addObserver:self
          selector:@selector(notify:)
          name:"Example"
          object:nil];
}
-(void)dealloc {
    NSNotificationCenter *nc =
        [NSNotificationCenter defaultCenter];
    [nc removeObserver:self];
    [super dealloc];
}
```

From: notify.m To listen for notifications, you need to register an interest for them with the NSNotificationCenter object for your thread. This is the routing point for notifications. When a notification is posted, it is sent to the notification center and the notification center forwards it to all of the interested parties. Most of the time, you will be using the default notification center. It is possible to create different notification centers for different uses, but most commonly you will use the standard one. This is obtained by sending a +default message to NSNotificationCenter.

To register for a notification, you then send an -addObserver:selector:name:object: message to the center. Note the selector argument in this message. A single object may receive different notifications on different methods. This is quite useful, because it means you don't need to test what kind of notification you've received and can cleanly separate out different event handlers into different methods.

Either the object or the notification name can be nil when registering an observer. This lets you register either to receive all messages sent by a specific object, or all notifications of a specific type, irrespective of their sender.

These are more useful for debugging than anything else. You can, for example, write a logging aspect that listens for all notifications of a particular type and logs the sender.

One important thing to remember when you listen for a notification is that the notification center does not retain your object. If your object is still registered to receive notifications when it is destroyed, then your program will crash the next time one of these notifications is sent.

To avoid this, make sure that you send a -removeObserver: message in your -dealloc method. If you forget this, the crash will not be obvious. You will see a lot of strange things in the back trace, including the notification center.

## Sending Notifications

```objectivec
NSNotificationCenter *nc = 
[NSNotificationCenter defaultCenter];
[nc postNotificationName:@"Example" 
object:@"sender" 
userInfo:nil];
```

From: notify.m Posting notifications is even easier than registering to listen for them. The canonical way of posting a notification object is to construct an NSNotification object and then send it.

In practice, I don't think that I've ever seen code that does this. The notification center has some convenience methods that construct and post notifications in a single operation.

The most common way of sending a notification is the -postNotificationName:object:userInfo method. There is also a simplified version of this that omits the userInfo: parameter and is equivalent to passing nil as the final parameter.

Note that the object--the sender of the notification—is specified as a parameter. That means that it is possible to send notifications claiming to be from another object. This means that, for example, façades or C code can send notifications on behalf of other objects.

## Enqueuing Notifications

```objectivec
NSNotificationQueue *ng = [NSNotificationQueue defaultQueue];
NSNotification *note = [NSNotification notificationWithName:@"Example" object:@"sender"];
[ng enqueueNotification:note postingStyle:NSPostWhenIdle];
[NSRLoop currentRunLoop run];
```

From: notify.m

Sometimes, your code might be generating a lot of notifications, or may be generating ones that do not need to be handled immediately. The NSNotificationQueue class solves both of these problems.

Notification queues can both defer delivery of notifications and can coalesce them. Unlike NSNotificationCenter, the queue does not have convenience methods for constructing the notifications, you must do this yourself. The notification is then posted with one of three posting styles.

In this example, the notification's delivery is deferred until there are no other events in the run loop. Timers and data becoming ready on file descriptors take priority. Alternatively, you can post in the next run loop iteration or immediately.

If you send a lot of notifications of the same type then it is a good idea to cache the notification object. Passing the same object to the notification queue repeatedly is quite cheap, and it can automatically send the notification just once.

If you use the longer method for queuing notifications, one of the parameters is coalesceMask:, which determines how notifications should be combined. You can combine notifications with the same name, notifications with the same sender, or both. Coalescing is most useful with the NSPostWhenIdle posting style. This is ideal for bits of code that trigger some low-priority bookkeeping work.

## Sending Notifications Between Applications

```objectivec
[c
 addObserver:self
 selector:@selector(newCopyStarted:)
 name:ProcessDidStart
 object:nil
 suspensionBehavior:NotificationSuspensionBehaviorHold];
```

From: distributedNotify.m The loose coupling provided by notifications is so useful that it is extended within the Foundation framework to provide a (simple) mechanism for communication between applications. The NSDistributedNotificationCenter class is a subclass of NSNotificationCenter that broadcasts notifications to other applications. This extension requires some changes. A normal notification has a sender associated with it, which is a pointer to some object. A pointer to an object is not particularly useful in a process with another address space, so distributed notifications use a string as the sender. This can be anything that you like, but it is usually the application name. Notifications can have dictionaries associated with them. Within an application, these dictionaries can contain any objects, but for broadcast they are restricted to objects that can be stored in property lists (see Chapter 9).
