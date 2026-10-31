an input with Standard.Event.replyEvent(). An Event can be sent to a destination other than its default destination with a call to Standard.Event.routeTo(<destination>).

# Preprocessing Behavior

The default preprocessing behavior is shown in Figure 5-21. An external event source generates a message, which is received by the channel and processed by the channel thread. The channel thread creates the event from the incoming message and places it on a shared queue.

![](bbox=[0.17, 0.5, 0.8, 0.9])

Actions that assert events and concepts into working memory do not take effect until this thread runs the RTC.

Locking occurs if RTC is configured for single-threaded operation.

Figure 5-21: Default Preprocessing Behavior