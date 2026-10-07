
# Cocoa Design Patterns

> Further Reading: See Archives and Serializations Programming Guide for further information about archiving.

# Property List Serialization

A property list is a simple, structured serialization of an object graph that uses only objects of the following classes: NSDictionary, NSArray, NSString, NSData, NSDate, and NSNumber. These objects are commonly referred to as property list objects. Several Cocoa framework classes offer methods to serialize these property lists and define special formats for the data stream recording the contents of the objects and their hierarchical relationship. The NSPropertyListSerialization class provides methods that serialize property list objects to and from XML format or unnamed binary format.

# Uses and Limitations

If the object in an object graph is simple, property list serialization is a flexible, portable, and adequate method to capture and externalize an object and its state. However, form of serialization has its limitations. It does not preserve the full identity of objects, only the general kind (array, dictionary, string, and so on). Thus an object restored from a property list might be of a different class than original class, and so is an issue when the mutability of an object can vary. Property list serialization also doesn't keep track of objects that are referenced multiple times in an object, potentially resulting in multiple instances upon deserialization when a single instance was in the original object graph.

> Further Reading: See Archives and Serializations Programming Guide for further information on property list serialization.

# Core Data

Core Data is a Cocoa framework that defines an architecture for managing object graphs and making them persistent. It is this capability—object persistence—that Core Data an adaptation of the Memento pattern.

In the Core Data architecture, a central object called the managed object context manages the various objects in an application's graph. Below the managed object context is the persistence stack for that graph—a collection of framework objects that mediate between model objects and external data, such as XML files or relational databases. The persistence-stack objects map data between the store and corresponding objects in the managed data context, and when there are multiple data stores, present them to the managed object context as a single aggregate store.

The design of Core Data is also heavily influenced by the Model-View-Controller and object modeling patterns.

# Uses and Limitations

Core Data is practically useful in the development of enterprise applications where complex graphs of model objects must be defined, managed, and transparently archived and unarchived to and from data stores. The Xcode environment includes project templates and design tools that reduce the programming effort required to create the two types of Core Data applications, those that are document-based and those that are not document-based. The Interface Builder application also includes Core framework objects in its library.

Further Reading: To learn more about Core Data, read Core Data Programming Guide. The tutorials NSPersistentDocument Core Data Tutorial and Core Data Utility Tutorial step you through the basic for creating document-based and non-document-based Core Data applications.

# Observer

The Observer design pattern defines a one-to-many dependency between objects so that when one object changes state, all its dependents are notified and updated automatically. The Observer pattern is essentially publish-and-subscribe model where the subject and its observers are loosely coupled. Communication can take place between the observer and observed objects without needing to know much about the other.

# Notifications

The notification mechanism of Cocoa implements one-to-many broadcast of messages by the Observer pattern. Objects in a program add themselves or other objects to a list of one or more notifications, each of which is identified by a global string (the notification name). The object that wants to notify other object—creates a notification and posts it to a notification center. The notification center determines the observers of a particular and sends the notification to them as a message. The methods invoked by the notification center must conform to a single-parameter signature. The pattern of the method is the notification object, which contains the notification name, the observed object, and a dictionary containing any supplemental information.

Posting a notification is a synchronous process. The posting object doesn't regain control until the notification center has broadcast to all observers. For any asynchronous behavior, you can put a notification in a notification queue; control returns immediately to the posting object and the notification center broadcasts when it reaches the top of the queue.

Regular notifications—that is, broadcast by the notification center—are intraprocess. If you want broadcast to across processes, use the distributed notification center and its related API.

# Uses and Limitations

You can use notifications for a variety of reasons. For example, you could broadcast a notification to change user-interface elements display information based on a center event else in the program. Or you could use notifications as a way to ensure that objects in a document save their state before the document window is closed. The general purpose of notifications is to inform other objects of program events so they respond appropriately.

But receiving notifications react react after the event has occurred. This is a significant difference from delegation. delegation is given a chance to reject or modify the operation proposed by the delegating object. Observing objects, on the other hand, cannot directly affect an impending operation.

The notification classes are NSNotification (for notification objects), NSNotificationCenter (to post notifications and add observers), NSNotificationQueue (to enqueue notifications), and NSistributedNotificationCenter. Many Cocoa frameworks publish and post notifications by the delegating any object can observe.

# CHAPTER 4

# Cocoa Design Patterns

> Further Reading: "Notifications" (page 190) describes the notification mechanism in greater detail and offers guidelines for its use.

# Key-Value Observing

Key-value observing is a mechanism that allows objects to be notified of changes to specific properties of other objects. It is called NSKeyValueObserving informal protocol. Observed properties can be simple attributes, to-one relations, or to-many relations. In the context of the Model-View-Controller pattern, key-value observing is especially important because it enables objects to observe—via the controller layer—see "Controller Classes in the AppKit Framework" (page 149).

Cocoa provides a default "automatic" implementation of many NSKeyValueObserving methods that give complying objects a proxy-observing capability.

# Uses and Limitations

Key-value observing is similar to the notification mechanism but is different in many respects. In key-value observing there is no central object that provides change notification for all observers. Instead, notifications of changes are directly transmitted to observed objects. Key-value observing is also directly tied to the values of specific object properties. The notification mechanism, on the other hand, is more broadly concerned with program events.

Objects that participate in key-value observing (KVO) must be KVO-compliant—that is, comply with certain requirements. Automatic observing requires compliance with the requirements of key-value coding (KVC-compliance) and using the KVC-compliance methods (that is, accessor methods). Key-value coding is a related mechanism (based on a related informal protocol) for automatically getting and setting the values of a related property.

You can refine KVO objects by disabling automatic observer notifications and implementing manual notifications using the methods of the NSKeyValueObserving protocol and associated categories.

> Further Reading: Key-Value Observing Programming Guide to learn more about the mechanism and underlying protocol. Also see the related documents Key-Value Coding Programming Guide and Cocoa Bindings Programming Topics.

# Proxy

The proxy design pattern provides a surrogate, or placeholder, for another object in order to control access to that object. You use this pattern to create a representative, or proxy, object that controls access to another object, which may be remote, expensive, or in need of securing. This pattern is structurally similar to the Decorator pattern but it serves a different purpose; Decorator adds behavior to an object whereas Proxy controls access to an object.
