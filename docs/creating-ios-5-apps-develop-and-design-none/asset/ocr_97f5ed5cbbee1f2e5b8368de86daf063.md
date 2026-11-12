For example, to implement asynchronous saves, we simply need to create two managed object contexts with a simple parent-child relationship. Our application makes all its changes to the child context. When it wants to save, we start by saving the child context on the main thread. This creates a snapshot of our data—pushing our changes up to the parent context. Then we save the parent context on a background thread. As we will see, UIManagedDocument uses this technique when auto-saving document data.

> **NOTE:** In previous Core Data project templates, Xcode’s auto-generated code accessed the managed object context directly from the app delegate. With iOS 5, Apple highly recommends switching to a “pass the baton” approach, where the correct context is handed from object to object along the view controller hierarchy. This is especially true in any applications using multi-layer contexts.

![](bbox=[0.744, 0.378, 1.0, 0.517])

# MANAGED OBJECTS

All Core Data entities are instantiated as an NSManagedObject or one of its subclasses. Each managed object is associated with an entity description. This includes both the object’s metadata and information about the managed object context where our object resides.

In many cases, we can simply use raw managed objects in our project. Each managed object will automatically generate both public and primitive accessors for all the modeled properties. For attributes and other to-one relationships, these follow the standard <key> and set<Key> naming conventions.

For to-many relationships, these accessors can be used to get and set the entire collection (as an NSSet or NSOrderedSet, depending on the type of to-many relationship). However, if we want to simply add or remove individual members, we can request a mutable set using the mutableSetValueForKey: or mutableOrderedSetValueForKey: method. We can then add or remove entities from this set—all changes will be made to the managed object context’s object graph. We can also use the dynamic relationship accessors add<Key>Object: and remove<Key>Object: (insertObject:in<Key>AtIndex: and removeObjectFrom<Key>AtIndex: for ordered to-many relationships).