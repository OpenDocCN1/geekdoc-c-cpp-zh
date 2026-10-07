# CHAPTER 1

# Is Cocoa?

+   **File system and URL.** NSFileManager provides a consistent interface for file operations such as creating, deleting, and moving files, NSFileHandle permits file operations at a lower level (for example, seeking within a file), NSBundle finds resources in bundles and dynamically load some of them (for example, nib files and code). You use NSURL... to represent, access, and manage URL sources of data.

+   **Concurrency.** NSThread creates multithreaded programs, and various lock classes for controlling access to resources by threads. You use NSOperation and NSOperationQueue to perform multiple operations (concurrent or nonconcurrent) in priority and dependence order. With NSTask, your program can fact off a process to perform and monitor its progress.

+   **Interprocess communication.** Most of the classes in this category represent various kinds of system ports, sockets, and servers are useful for implementing low-level IPC. NSPipe represents a BSD pipe, a unidirectional communication channel between processes.

> Note: The name classes are not in the iOS version.

+   **Networking.** The NSSystemService and NSServiceBrowser classes support the zero-configuration networking architecture Bonjour. Bonjour is a powerful system for publishing and browsing for services on IP network.

+   **Notifications.** See the summary of the notification classes in "Foundation Paradigms and Policies" (page 31).

+   **Archiving and serialization.** The classes in this category make object distribution and persistence possible. NSCoder and its subclasses, using the NSCoding protocol, represent the data object in an architecture-independent way using class information to store with the data. NSKeyedarchiver and NSKeyedunarchiver offer methods for encoding objects and values and decoding them in a way that is not dependent on the order of encoding methods.

+   **Objective-C classes.** NSException and NSAssertion provide an object-oriented way of making assertions and handling exceptions in code. NSInvocation is a static representation of an Objective-C message that you can store and later invoke a message in another object; it is used by the undo manager (UndoManager) and by the distributed objects system. NSMethodSignature records the type of information and is used in method forwarding. ClassDescription is an abstract class for decoding and querying the relationships and properties of a class.

+   **XML processing.** Foundation on platforms has the XMLParser class, which is an object-oriented implementation of a string parser that enables you to process XML data in an event-driven way.

+   **Predicates and expressions.** The predicate classes—NPredicate, NSCompoundPredicate, and NSComparisonPredicate encapsulate the logic conditions to fetch a or filter object. NSPredression objects represent expressions in a predicate.