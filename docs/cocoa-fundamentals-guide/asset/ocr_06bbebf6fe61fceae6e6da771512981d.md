# CHAPTER 4
Cocoa Design Patterns

# NSProxy

The NSProxy class defines the interface for objects that act as surrogates for other objects, even for objects that do not exist. A proxy object typically forwards a message sent to the object that it represents, but it can also respond to the message by loading the represented object or transforming itself into. Although NSProxy is an abstract class, it is, in fact, the root class of hierarchy just as the NSObject protocol and other fundamental methods of a root object;

Concrete subclasses of NSProxy can accomplish the stated goals of the Proxy pattern, such as instantiation of expensive objects or acting as sending proxies for security. NSDistantObject, a concrete subclass of NSProxy in the Foundation framework, implements a proxy for transparent distributed messaging. NSDistantObject objects are part of the architecture for distributed objects. By acting as proxies for other processes or threads, they help enable communication between objects in those threads or processes.

NSInvocation objects, which are adaptation of the Command pattern, are also part of the distributed objects architecture ("Invocation Objects" (page 142)).

# Uses and Limitations

Cocoa employs NSProxy only in distributed objects. The NSProxy objects are specifically instances of the concrete subclasses NSDistantObject and ProtocolChecker. You can use distributed objects not only for interprocessing (on the same or different computers) but you can also use it to implement distributed computing or parallel processing. If you want to use objects for other purposes, such as the creation of expensive resources or security, you have to implement your own concrete subclass of NSProxy.

> Further Reading: To learn more about Cocoa proxy objects and the role they play in distributed messaging, read Distributed Objects Grouping Topics.

# Receptionist

The Receptionist design pattern addresses the general problem of redirecting an event occurring in one execution context of an application to another execution context. It is a hybrid. Although it doesn't appear in the "Gang of Four" book, it combines the elements of the Command, Memo, and Proxy patterns described in that book. It is a variation of the Trampoline pattern (which also doesn't appear in the book); in this pattern, an event is initially received by a trampoline object, so-called it immediately redirects, or reverts, to a target object for handling.

You can adopt the Receptionist pattern whenever you need to bounce off to another execution context for handling. When you observe an notification, or implementation or a block handler, or respond to an action message and want to ensure that your code executes in the appropriate execution context, you can implement the Receptionist pattern to redirect the work that must be done to that execution context. With the Receptionist pattern, you might even perform some filtering or coalescing of the incoming data before you bounce a task to process the data. For example, you could collect data into batches, and then at intervals dispatch those batches for processing.

One common situation where the Receptionist pattern is useful-key-value observing. In key-value observing, changes to the value of a model object's property are communicated to observers via KVO notifications. However, changes to a model object can occur on a background thread. This results in a thread mismatch,

How Cocoa Adapts Design Patterns
2010-12-13 | © 2010 Apple Inc. All Rights Reserved.

155