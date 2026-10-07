# CHAPTER 5

Communicating Objects

The notification queue is emptied and its notifications are posted based on the posting style and runloop mode specified in the encoding method. The mode specifies the run loop mode in which the queue is emptied. For example, if you specify NSModalPanelRunLoopMode, the notifications are posted only when the run loop is in this mode. If the run loop is not in this mode, the notifications wait until the next time that is mode.

Posting to a notification queue can occur in one of three styles: NSPostASAP, NSPostWhenIdle, and NSPostNow. These styles are described in the following sections.

# Posting As As Possible

Any notification queued with the NSPostASAP style is posted to the notification center when the iteration of the run loop completes, assuming the current run loop matches the requested mode. If the requested and current modes are different, the notification is posted when the requested mode is entered. Because the run loop can make multiple calls during each iteration, the notification may or not be delivered as soon as the current event exits and returns to the run loop. Other calls may place it first, such as a source firing or the delivery of any asynchronous notifications.

You typically use the NSPostASAP style for an expensive resource, such as the server display. Many clients draw on the window during a buffer call from the run loop, it is expensive to flush the buffer notification after every draw. In this situation, draw methods such as `FlushTheServer` with coalescing on object and specified and with a posting style of NSPostASAP. As a result, only one of notifications is dispatched at the end of the run loop and the window buffer is flushed only once.

# Posting When Idle

A notification queued with the NSPostWhenIdle style is posted only when the run loop is in a wait state. In this state, there's nothing the run loop's input channels, including timers or other asynchronous events. Note that a run loop is about to exit (which occurs when all the input channels have expired) is in a wait state and does not post a notification.

# Posting Immediately

A notification queued with NSPostNow is posted immediately after coalescing to the notification center. You queue a notification with NSPostNow(or post one with the NSNotificationCenter method postNotification::) when you do not require asynchronous calling behavior. For many programming situations, synchronous is not only desirable but desirable: You want the notification center to return after dispatching so you can see that objects have received and processed the notification. Of course, you should use enqueueNotification:...with NSPostNow rather than postNotification: when there are similar notifications in the queue that you want to remove coalescing.

# Ownership of Delegates, Observers, and Targets

Delegating objects are not considered to own their delegates or data sources. Similarly, controls and cells are not considered to own their targets, and the notification center does not own the observers of notifications. For memory-managed code these framework objects follow the convention of not retaining their targets, delegates, observers, and data sources; instead, they store a pointer to the object.

196
Ownership of Delegates, Observers, and Targets
2010-12-13 | © 2010 Apple Inc. All Rights Reserved.