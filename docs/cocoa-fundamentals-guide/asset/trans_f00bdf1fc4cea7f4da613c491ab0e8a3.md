

# CHAPTER 1

# What Is Cocoa?

representing system entities such as ports, threads, and processes. The class hierarchy charts in Figure 1-7 (for printing purposes, in three parts) depict the logical groups these classes form as well as their inheritance relationships. Classes in blue-shaded areas are present in both the Mac OS and iOS versions of Foundation; classes in gray-shaded areas are present only in the Mac OS version.

# Figure 1-7 The Foundation class hierarchy

![](img/0c5ea7638a6e08e6bdc6bc222975f6ee_31_0.png)

# CHAPTER 1

# What Is Cocoa?

## Objective-C Foundation Continued

| Operating-System Services |
|--- |
| NSError |
| NSHost |
| NSService |
| NSNetworkBrowser |
| NSPhotography |
| NSProcessInfo |
| NSLoop |
| NSSpellServer |
| NSTextCheckingResult |
| NSTimer |
| NSUserDefaults |
| NSBundle |
| NSFileHandle |
| NSFileManager |
| NSMetadata |
| NSMetadataQuery |
| NSMetadataQueryAttributeValueTuple | NSStream |
| NSMetadataQueryResultGroup | OutputStream |

| NSObject |
| URL |
| NSCHTTPURLResponse |
| NSHTTPCookie |
| NSHTTPCookieStorage |
| NSURL | NSURLAuthorizationChallenge |
| NSCache |
| NSConnection |
| NSCredential |
| NSDataStorage |
| NSURLDownload |
| NSURLProtectionSpace |
| NSProtocol | NSMutableURLRequest |
| NSRequest |
| NSResponse | NSHTTPURLResponse |

| Interprocess Communication |
|--- |
| NSPipe | NSMachPort |
| NSPort | NSMessagePort |
| NSPortMessage | NSocketPort |
| NSPortNameServer | NSMachBootstrapNameServer | NSocketPortNameServer |

| Locking/Threading |
|--- |
| NSConditionLock |
| NSDistributedLock |
| NSLock |
| NSOperation | NSBlockOperation |
| NSOperationQueue | NSInvocationOperation |
| NSRecursiveLock |
| NSTask |
| NSThread |

The Cocoa Frameworks 2010-12-13 | © 2010 Apple Inc. All Rights Reserved.

# CHAPTER 1

What Is Cocoa?

## Objective-C Foundation Continued

| Notifications | |
| --- | --- |
| NSNotification | NSDributedNotificationCenter |
| NSNotificationCenter | |
| NSNotificationQueue | |

| Archiving and Serialization | |
| --- | --- |
| NSCoder | NSArchiver |
| NSPropertyListSerialization | NSKeyArchiver |
| | NSKeyedUnarchiver |
| | NSPortCommand |
| | NSDataArchiver |

| Objective-C Languages | |
| --- | --- |
| NSAssertionHandler | |
| NSAutoreleasePool | |
| NSClassDescription | |
| NSException | |
| NSGarbageCollector | |
| NSInvocation | |
| NSMethodSignature | |
| NSUndoManager | |

| Scripting | |
| --- | --- |
| NSApplicationEventDescriptor | NSScriptClassDescription |
| NSApplicationEventManager | NSCCommand |
| NSScript | NSCountCommand |
| | NSCreateCommand |
| NSPitionalSpecifier | NSSelectCommand |
| NSCoercionHandler | NSMoveCommand |
| NSScriptCommand | NSSetCommand |
| NSScriptDescription | NSIndexSpecifier |
| NSScriptExecutionContext | NSNameSpecifier |
| | NSPropertySpecifier |
| NSObjectSpecifier | NSRandomSpecifier |
| NSRangeSpecifier |
| | NSValueSpecifier |
| NSiteRegistry | NSUniqueSpecifier |
| NSWhitelistTest | NSProxyTest |
| | NSLogicalTest |
| | NSSpecifiedTest |

| Distributed Objects | |
| --- | --- |
| NSConnection | |
| NSDistantObjectRequest | |
| NSDistantObject | |
| NSProtocolChecker | |

These diagrams logically group the classes of the Foundation framework in categories (with other associations pointed out). Of particular importance are the classes whose instances are value objects and collections.

## Value Objects

Value objects encapsulate values of primitive types, including strings, numbers (integers and floating-point values), dates, and even structures. They mediate access to these values and manipulate them in suitable ways. When you compare value objects of the same class, it is their encapsulated values that are compared, not their pointer values. Value objects are the attributes of other objects, including custom objects.

Of course, you may choose to use scalars and other primitives directly in your program—after all, Objective-C—and in many cases using scalars is a reasonable thing to do. But in other situations, wrapping these values in objects is either advantageous or required. For example, because value objects are objects, you, at runtime, can detect their class, determine the messages that be sent to, and perform other tasks that can be done with objects. The elements of collection objects such as arrays and dictionaries must be objects. Many if not most methods of the Cocoa frameworks take and return values as strings, and dates require that these values be encapsulated in objects. (With strings, in particular, you should always use NSString objects and not C-strings).

Some classes for value objects are mutable and immutable variants—for example, there are the NSData and NSString classes. The values encapsulated by immutable objects cannot be modified after they are created, whereas the values encapsulated by mutable objects can be modified. (Object Mutability (page 90) discusses mutable and immutable objects in detail.)

The following are what the most important value objects do:

- Instances of NSString encapsulates a single value—example, scalar types as floating-point values as points and structures.
- NSNumber (a subclass of NSString) instantiates objects that contain numeric values such as integers, floats, and doubles.
- NSData provides object-oriented storage for streams of bytes (example, image data). The class has methods for writing data to the file and reading them back.
- Date class, along with supporting NSTZone, DateComponents, and NSLocale, provide objects for calculating time, for displaying dates in many formats, and for adjusting dates based on location.
- NSCharacterSet represents a set of characters—a type of value object that provide object-oriented storage for strings such as UTF-8 which are typically presented in the user interface.

# Collections

Collections are objects that store other objects in a particular ordering for later retrieval. Foundation defines three major collection classes that are common to both iOS and Mac: NSArray, NSDictionary, and Set. As many value classes, these collections have immutable and mutable variants. For example, once you create an NSArray that holds a certain number of elements, you cannot add new elements or remove existing ones; for that purpose you need NSMutableArray.

Objects of the major collection classes have common characteristics and requirements. The items they contain must be objects, but the objects can be of any type. Collection objects, as with value objects, are essential components of property lists and, like all objects, can be achieved and distributed. Moreover, collection objects automatically retain—that is, keep a strong reference to—any object that if you remove from a mutable collection, it is released, which results in the object being freed if no other object claims it. Note: "Retain," "release," and related terms refer to memory management of objects. To learn about this topic, see "Object Retention" (page 70).

The collection classes provide methods to access specific objects. In addition, there are special enumerator objects (NSEnumerator) and language-level support to iterate through collections and access each element in sequence.

The major collection classes are differentiated by the ordering they use:

- Arrays (NSArray) are ordered collections that use zero-indexing for accessing the elements of the collection.
- Dictionaries (NSDictionary) are collections managing keys and values; the key is an object that identifies the value, which is also an object. Because of this key-value scheme, the elements in a dictionary are unordered. Within a dictionary, the keys must be unique. Although they are typically strings, any key can be any type of object.
- Sets (NSSet) are similar to arrays, but they provide unordered storage of their elements instead of ordered storage. In other words, the order of elements in a set is not important. In an NSSet must be distinct from each other; however, an instance of NSCountedSet (a subclass of NSMutableSet) may include the same object more than once.

In Mac OS, the Foundation framework includes several additional classes. NSMapTable is a mutable dictionary-like class; however, NSDictionary can hold pointers as well as objects and maintains weak references to its contents and NULL values can maintain either strong or weak references. NSPPointerArray is an array that can hold pointers to them. NSHashTable is modeled after NSSet but it can store pointers to functions and provides different options, in particular to support weak relationships in a garbage-collected environment.

For more classes and objects, see Collections Programming Topics.

# Other Categories of Foundation Classes

The remaining classes of the Foundation framework fall into various categories, as indicated by the diagram in Figure 1-7 (page 32). The major categories of classes, shown in Figure 1-7, are described here:

- Operating-system bytes. Many Foundation classes facilitate access to various lower-level services of the operating system and, at the same time, insulate you from operating system idiosyncrasies. For example, NSProcessInfo lets you query the environment in which an application runs and NSHost yields the names and addresses of host systems on a network. You can use NSTimer object to send a message to another object at specific intervals, and NSRunLoop lets you manage the input sources of an application or other type of program. NSUserDefaults provides a programmatic interface to a system database of global (per-host) and per-user default values (preferences).

