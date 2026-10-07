
# CHAPTER 5

Communicating with Objects

A notification center delivers notifications to observers synchronously. In other words, the poster of the notification doesn't regain control until all observers have received and processed the notification. To send notifications asynchronously, use a notification queue, which is described in "Notification Queues" (page 194).

In a multithreaded application, notifications are always delivered in the thread in which the notification was posted, which may not be the same thread as an observer registered.

## NSDistributedNotificationCenter

Each task has a default notification center that you access with the `NSDistributedNotificationCenter` class method. This default notification center handles notifications that can be sent between tasks on a single computer. For communication between tasks on different computers, use distributed objects (*Distributed Objects Programming Topics*).

Posting a distributed notification is an expensive operation. The notification gets to a systemwide server that then distributes it to all tasks that have registered for distribution. The latency between posting and the observer's arrival in task is unbounded. In fact, if many notifications are posted and the server's queue fills, notifications might be dropped.

Distributed notifications are delivered via a task's run loop. A task must be running a run loop in common modes, such as `DefaultRunLoopMode`, to receive a notification. If the receiving task is multithreaded, do depends on the notification arriving on the main thread. The notification is usually delivered to the main thread's run loop, but other threads could also receive the notification.

Whereas a regular notification center allows any object to be the notification object (that is, the object encapsulated by the notification), a distributed notification center is restricted to having an `NSString` object as its notification object. Because the posting object and the observer may be in different tasks, notifications cannot contain pointers to arbitrary objects. Therefore a distributed notification center requires a string to use as the notification object. Notification matching is based on this string, rather than based on an object pointer.

## Notification Queues

NSNotificationQueue (or simply, notification queues) act as buffers for notification centers (instances of `NSNotificationCenter`). A notification queue maintains notifications (instances of `NSNotification`) generally in a First In First Out (FIFO) order. When a notification rises to the front of the queue, the queue dispatches the notification to all objects registered as observers.

Every thread has a default notification queue, which is associated with the default notification center for the task. Figure 5-7 illustrates this association. You can create your own notification queues and have multiple queues per center and thread.

# CHAPTER 5

Communicating with Objects

Figure 5-7 A notification queue and notification center

![](img/0c5ea7638a6e08e6bdc6bc222975f6ee_194_0.png)

## Coalescing Notifications

The NotificationQueue class introduces two important features to the Foundation framework's notification mechanism: the coalescing of notifications and asynchronous posting. Coalescing is a process that removes notifications in the queue that are similar to the notification just queued. If the new item is similar to a notification already queued, the new one isn't queued and all notifications (except the first in the queue) are removed. However, you should not depend on this particular coalescing behavior.

You indicate the criteria for similarity in notifications by specifying one or more of the following constants in the third parameter of the `enqueueNotification:postingStyle:coalesceMask:forModes:` method.

```
NSNotificationNoCoalescing
NSNotificationCoalescingName
NSNotificationCoalescingOnSender
```

You can perform a bitwise-OR operation with the NSNotificationCoalescingOnName and NSNotificationCoalescingOnSender to specify coalescing using both the notification name and notification object. In this case, all notifications having the same name and sender as the one enqueued are coalesced.

## Asynchronously Posting Notifications

With the NotificationCenter method `postNotification:` and its variants, you can post a notification immediately to a notification center. However, the invocation of the method is synchronous: Before the posting object can return its thread of execution, it must wait until the notification center dispatches the notification to all observers and returns. With the NotificationQueue methods `enqueueNotification:postingStyle:` and `enqueueNotification:postingStyle:coalesceMask:forModes:`, however, you can post a notification asynchronously by putting it in a queue. These methods immediately return to the invoking object after putting the notification in the queue.

# CHAPTER 5

Communicating Objects

The notification queue is emptied and its notifications are posted based on the posting style and runloop mode specified in the encoding method. The mode specifies the run loop mode in which the queue is emptied. For example, if you specify NSModalPanelRunLoopMode, the notifications are posted only when the run loop is in this mode. If the run loop is not in this mode, the notifications wait until the next time that is mode.

Posting to a notification queue can occur in one of three styles: NSPostASAP, NSPostWhenIdle, and NSPostNow. These styles are described in the following sections.

## Posting As As Possible

Any notification queued with the NSPostASAP style is posted to the notification center when the iteration of the run loop completes, assuming the current run loop matches the requested mode. If the requested and current modes are different, the notification is posted when the requested mode is entered. Because the run loop can make multiple calls during each iteration, the notification may or not be delivered as soon as the current event exits and returns to the run loop. Other calls may place it first, such as a source firing or the delivery of any asynchronous notifications.

You typically use the NSPostASAP style for an expensive resource, such as the server display. Many clients draw on the window during a buffer call from the run loop, it is expensive to flush the buffer after every draw. In this situation, draw methods such as `FlushTheServer` with coalescing on object and specified and with a posting style of NSPostASAP. As a result, only one of notifications is dispatched at the end of the run loop and the window buffer is flushed only once.

## Posting When Idle

A notification queued with the NSPostWhenIdle style is posted only when the run loop is in a wait state. In this state, there's nothing the run loop's input channels, including timers or other asynchronous events. Note that a run loop is about to exit (which occurs when all the input channels have expired) is in a wait state and does not post a notification.

## Posting Immediately

A notification queued with NSPostNow is posted immediately after coalescing to the notification center. You queue a notification with NSPostNow(or post one with the NotificationCenter method postNotification:) when you do not require asynchronous calling behavior. For many programming situations, synchronous is not only desirable but desirable: You want the notification center to return after dispatching so you can see that objects have received and processed the notification. Of course, you should use `enqueueNotification:...with NSPostNow` rather than `postNotification:` when there are similar notifications in the queue that you want to remove coalescing.

## Ownership of Delegates, Observers, and Targets

Delegating objects are not considered to own their delegates or data sources. Similarly, controls and cells are not considered to own their targets, and the notification center does not own the observers of notifications. For memory-managed code these framework objects follow the convention of not retaining their targets, delegates, observers, and data sources; instead, they store a pointer to the object.
