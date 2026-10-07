
Memory Management. In memory-managed code, each call makes a claim of ownership on an object—object allocation and initialization, object copying, and retain—must be balanced with a call that removes claim—release and autorelease. When the object's retain count (reflecting the number of claims on it) reaches zero, the object is deallocated and the memory occupied by the object is freed.

In addition to being easier to implement, garbage-collected code has several advantages over memory-managed code. Garbage collection provides a simple, consistent model for all participating programs while avoiding problems such as retain cycles. It simplifies the implementation of accessor methods and makes it easier to ensure exception safety.

> **Important:** Although memory-managed methods are no-ops in a garbage-collected application, there are still intractable differences between certain programming paradigms and patterns used in the two models. Therefore it is not recommended that you migrate a memory-managed application to a source base that tries to support both memory management and garbage collection. Instead, create a new full-version release that supports garbage collection.

The following sections explore how garbage collection and memory management work by following the lifecycle of objects from their creation to their destruction.

> **Further Reading:** To learn all about the garbage collection feature of Objective-C, read Garbage Collection Programming Guide. Memory management is discussed in detail in Memory Management Programming Guide.

## How the Garbage Collector Works

The work of garbage collection is done by an entity known as the garbage collector. To the garbage collector, objects in a program are either reachable or not reachable. Periodically the collector scans through the objects and those that are reachable. Those objects that aren't reachable—the garbage objects—are finalized (that is, their finalize method is invoked). Subsequently, the memory they had is freed.

The critical notion behind the architecture of the Objective-C garbage collector is the set of factors that constitute a reachable object. These factors start with an initial root set of global variables (including NSApp), stack variables, and external references (that is, outputs). The outputs of the initial root set are never treated as garbage and persist throughout the lifetime of the program. The collector adds to this initial set all objects directly reachable through strong references as well as all possible references in the stack calls of every thread. The garbage collector recursively follows strong references from one object to other objects, and from those objects to other objects, until all reachable objects have been counted (All references from one object to another are considered strong references by default; weak references must be explicitly marked as such). In other words, a nonzero point exists at the end of a cycle if the collector can reach it via root references.

Figure-3 illustrates the general path the collector follows when it looks for reachable objects. But it also shows some important aspects of the garbage collector. The collector scans only a portion of a Cocoa's virtual memory for reachable objects. Scanned memory includes the stacks of threads, global variables, and the auto zone, and an area of memory where all garbage-collected blocks of memory are disposed. The collector does not scan the malloc zone, which is the zone from which blocks of memory are allocated via the `malloc` function.

## CHAPTER 2

### Cocoa Objects

Figure 2-3 Reachable and unreachable objects

![](img/0c5ea7638a6e08e6bdc6bc222975f6ee_71_0.png)

Another thing the diagram illustrates is that objects may have references to other objects, but if there is no chain of strong references that leads back to a root object, the object is considered unreachable and is disposed of at the end of a collection cycle. These references can be circular, but in garbage collection the circular references do not cause memory leaks, as they retain cycles in memory-managed code. All of these objects are disposed of when they are no longer reachable.

The Objective-C garbage collector is request-driven, not demand-driven. It initiates collection cycles only upon request; Cocoa makes requests at intervals optimized for performance or when a certain memory threshold has been exceeded. You can also request collections using methods of the NSGarbageCollector class. The garbage collector is also generational. It makes not only exhaustive, or full, collections of objects periodically, but incremental collections based on the "generation" of objects. An object's generation is determined by when it was allocated. Incremental collections are faster and more frequent than full collections, affect the more recently allocated objects (Most objects are assumed to be "die young"). If an object survives the first collection, it is likely to be intended to have a longer life.

The garbage collector runs on one thread of a Cocoa program. In a collection cycle it will stop threads to determine which objects in those threads are unreachable. It never stops threads at once, and it stops each thread for a short time as much as possible. The collector is also conservative in it never compacts auto-zone memory by relocating blocks of memory or updating pointers; once allocated, an object always stays in its original memory location.

Object Retention and Disposal
2010-12-13 | © 2010 Apple Inc. All Rights Reserved.

## How Memory Management Works

In memory-managed Objective-C code, a Cocoa object exists over a life span which, potentially, has least distinct stages. It is created, initialized, and used (that is, objects send messages to it). It is possibly retained, copied or archived, and eventually it is released and destroyed. The following discussion charts the life of a typical object without needing any detail—yet.

Let's begin at the end, when objects are disposed of by garbage collection is turned off. In this context Cocoa and Objective-C opt for a voluntary, policy-driven procedure for keeping objects around and disposing of them when they're no longer needed.

This procedure policy rest on the notion of reference counting. Each Cocoa object carries with it an indicating number of other objects (or procedural code) that are interested in its persistence. This is referred to as the object's retain count (`retain` is used to avoid overloading the term “reference”). When you create an object, by using a class method or by using the alloc methods, Cocoa does a couple of important things:

- It sets the object's pointer—the NSObject class's instance variable—to point to the object's class, integrating the object into the runtime's view of the class hierarchy. (See “Object Creation” (page 77) for further information.)
- It sets the object's retain count—a kind of instance variable managed by the runtime—to one. (The assumption is that an object is created in its persistence.)

After allocation, you generally initialize an object by setting its instance variables to reasonable initial values (NSNumber declares the init method as the prototype for this purpose). The object is now ready to be used; you send messages to it, pass it to other objects, and so on.

> Note: Because an initializer can return an object other than the one explicitly allocated, the convention is to nest the alloc message in the init message—for example:
`id anObj = [[MyApp alloc] init];`

When you release an object—that is, a release message to it—decrements its retain count. If the retain count falls from one to zero, the object is deallocated. Deallocation takes in two steps: first, the object's dealloc method is invoked to release instance variables and free dynamically allocated memory. The operating system destroys the object itself and reclaims the memory once occupied.

> Important: You should never directly invoke an dealloc method.

What if you don't want an object to go away any too soon? After receiving an object from somewhere you send it a retain message, the object's retain count is incremented to two. Now two release messages are required before deallocation occurs. Figure 2-4 depicts this rather simplistic scenario.
