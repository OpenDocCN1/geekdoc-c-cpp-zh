# CHAPTER 3
Adding Behavior to a Cocoa Program

Each thread has its own call stack and is therefore responsible instead catching any local exceptions and cleaning up them. The exception cannot be thrown to the main thread or any other thread for handling. Failure to catch and handle an exception may result in the termination of the thread or the owning process.

+   - volatile variables in protected code.

The additional guidelines for Cocoa programs are few:

+   - Deal with immutable objects in your code as you may please, especially across interface boundaries.

Objects whose value or content cannot be modified—immutable objects—are thread safe. Mutable objects are often not. As a corollary to this guideline, respect the declared mutability status of objects returned from method; if you receive an object declared as immutable it is mutable and you modify it, you can cause behavior that is catastrophic to the program.

The main thread of a Cocoa application is responsible for receiving and dispatching events. Although your application can handle events on a secondary thread of the main thread, it must keep all event-handling code on that thread. If you spin off the events to different threads, user events (such as the letters typed on the keyboard) can occur out of sequence.

 a secondary thread is to draw a view in a Cocoa application on Mac OS, ensure that all drawing code falls between calls to the NS methods `lockFocusIfNeeded` and `unlockFocus`.

> Note: You can learn more about these guidelines in Threading Programming Guide.

# The Cocoa Frameworks Thread Safe?

Before you can make your program thread safe, it is essential to know the thread safety of the frameworks your program relies on. The core Cocoa frameworks, Foundation and AppKit, have parts that are thread safe and parts that are not.

Generally, the classes of Foundation objects are immutable collections (NSArray, NSDictionary, and so on) as those immutable objects encapsulate primitive values or constructs (for example, NSString, NSNumber, NSException) are thread safe. Conversely, the mutable versions of these collection and primitive-value classes are not thread safe. Classes of objects represent system-level—NSTask, NSRunLoop, NSQueue, NSHost, and NSPort,among others—are not thread safe (NSThread and the classes, on the other hand, are safe).

In AppKit, (UIView objects) are generally thread safe in that you you can create and manage them on a secondary thread. Events (NSEvent) are, however, are safe handled only on the main thread or a secondary thread; otherwise you run the risk of having events get out of sequence. Drawing and views (NSView objects) are generally thread safe, although operations on views as creating, resizing, and moving should happen on the main thread.

All UIKit objects should be used on the main thread.

For information on the thread safety of the Cocoa frameworks, see “Thread Safety” in Threading Programming Guide.

136  Multithreaded Cocoa Programs
2010-12-13 | © 2010 Apple Inc. All Rights Reserved.