# CHAPTER 7: Working with Collections

Objective-C collections are higher-level constructs. Each Objective-C collection, like most of the other additions made by Objective-C, is an object. You communicate with them by sending them messages.

The Foundation framework includes a number of collection classes for storing ordered and unordered data, as well as maps or sets of indexes. Most of the collection classes in Objective-C store objects. Unlike C++ STL collections, which need refining for the types they may contain, Objective-C collections are heterogeneous. They may store any kind of Objective-C object.

Most Objective-C collections, like strings, use the *mutable subclass pattern*, where the superclass implements behavior for an immutable collection and a subclass provides a mutable version.

All of the classes that follow this pattern implement the `NSMutableCopying` protocol, meaning that you can send a `-mutableCopy` message to a collection and get a copy that is mutable, even if the original isn’t.

Most collections are also *clusters*. When you create one, you will get some private subclass abstract. The public classes are typically abstract. The user-friendly methods are all implemented in terms of a small number of primitive methods. If you create your own subclass, you will need to implement these methods yourself.