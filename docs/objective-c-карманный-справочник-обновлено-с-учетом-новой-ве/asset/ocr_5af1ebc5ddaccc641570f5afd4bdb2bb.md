# CHAPTER 16: Notifications

**Note:** On OS X, there is only a single type of distributed notification center, sending notifications to applications owned running with the same user ID as the sender. GNUStep provides two others, one for communicating with all applications on a computer, irrespective of the user, and one for broadcasting notifications across the local network.

The delivery semantics for distributed notifications are also somewhat different. When you post a (normal) notification, it is delivered synchronously. The sending object already has control of the CPU. The stack frame for its method is at the top of the stack and it is free to delegate program flow to the notification center, which then delegates it to the notification listeners.

With a distributed notification, this is not the case. You can't just interrupt whatever process is doing in the middle of a function¹ and you must wait until a convenient point. Distributed notifications handle this by interfacing with the run loop. To receive distributed notifications, you must be using NSRunLoop. The distributedNotify.m example is a simple program that writes a log message whenever a new instance of itself is started.

> ¹Well, you can; signals do exactly that, but the things you can do from a signal handler are quite limited.