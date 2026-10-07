# Cocoa Design Patterns

> Further Reading: See Archives and Serializations Programming Guide for further information about archiving.

# Property List Serialization

A property list is a simple, structured serialization of an object graph that uses only objects of the following classes: NSDictionary, NSArray, NSString, NSData, NSDate, and NSNumber. These objects are commonly referred to as property list objects. Several Cocoa framework classes offer methods to serialize these property lists and define special formats for the data stream recording the contents of the objects and their hierarchical relationship. The NSPropertyListSerialization class provides methods that serialize property list objects to and from XML format or unnamed binary format.

# Uses and Limitations

If the object in an object graph is simple, property list serialization is a flexible, portable, and adequate method to capture and externalize an object and its state. However, form of serialization has its limitations. It does not preserve the full identity of objects, only the general kind (array, dictionary, string, and so on). Thus an object restored from a property list might be of a different class than original class, and so is es an issue when the mutability of an object can vary. Property list serialization also doesn't keep track of objects that are referenced multiple times in an object, potentially resulting in multiple instances upon deserialization when a single instance was in the original object graph.

> Further Reading: See Archives and Serializations Programming Guide for further information on property list serialization.

# Core Data

Core Data is a Cocoa framework that defines an architecture for managing object graphs and making them persistent. It is this capability—object persistence—that Core Data an adaptation of the Memento pattern.

In the Core Data architecture, a central object called the managed object context manages the various objects in an application's graph. Below the managed object context is the persistence stack for that graph—a collection of framework objects that mediate between model objects and external data, such as XML files or relational databases. The persistence-stack objects map data between the store and corresponding objects in the managed data context, and when there are multiple data stores, present them to the managed object context as a single aggregate store.

The design of Core Data is also heavily influenced by the Model-View-Controller and object modeling patterns.

# Uses and Limitations

Core Data is practically useful in the development of enterprise applications where complex graphs of model objects must be defined, managed, and transparently archived and unarchived to and from data stores. The Xcode environment includes project templates and design tools that reduce the programming effort required to create the two types of Core Data applications, those that are document-based and those that are not document-based. The Interface Builder application also includes Core framework objects in its library.