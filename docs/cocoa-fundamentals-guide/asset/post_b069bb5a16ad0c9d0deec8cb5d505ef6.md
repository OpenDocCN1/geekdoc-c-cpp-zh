
## CHAPTER 3
Adding Behavior to a Cocoa Program

With Boolean attributes a variation of the form for getter methods is acceptable. In this case it would take the form isAttribute. For example, a Boolean instance variable hidden would have a isHidden getter method and setHidden setter method.

If an instance variable is a scalar type, such as int or float, the implementations of accessor methods tend to be simple. An instance variable named currentRate, of type float, Listing 3-5 shows how to implement the accessor methods.

### Listing 3-5 Implementing accessors for a scalar instance variable

```
(float)currentRate {
    return currentRate;
}
```

```
(void)setCurrentRate:(float)newRate {
    currentRate = newRate;
}
```

If garbage collection is enabled, implementation of the setter accessor method for properties with object values is also a matter of simple assignment. Listing 3-6 shows how you would implement such methods.

### Listing 3-6 Implementing accessors for an object instance variable (garbage collection enabled)

```
(NSString*)jobTitle {
    return jobTitle;
}
```

```
(void)setJobTitle:(NSString*)newTitle {
    jobTitle = newTitle;
}
```

When instance variables hold objects and garbage collection is not enabled, the situation becomes nuanced. Because these objects must be persistent and must be created, copied, or retained when they are assigned. When a setter accessor changes the value of an instance variable, it is responsible only for ensuring persistence but for properly disposing of the old value. The getter lends the value of the instance variable to the object requested. The operations of both types of accessors have implications for memory management given two assumptions from the Cocoa object-ownership policy:

- Objects returned from methods (such as from getter access) are valid in the scope of the invoking object. In other words, it is guaranteed that the object will not be released or change value within that scope
- When an invoking object receives an object from a method as an accessor, it should not release the object unless it has explicitly retained (or copied) it

With these two assumptions in mind, let's look at two possible implementations of a getter and setter accessor for an NSString instance variable named title. Listing 3-7 shows the first.

### Listing 3-7 Implementing accessors for an object instance variable—good technique

```
(NSString*)jobTitle {
    return jobTitle;
}
```

```
(void)setTitle:(NSString*)newTitle {
if (title != newTitle) {
    title autorelease;
    title = [newTitle copy];
}
}
```

Note that the getter accessor simply returns the instance variable. The setter accessor, on the other hand, is busy. After verifying the passed-in value for the instance variable isn't the same as the current value, it autoreleases the current value before copying the new value. (Sending autorelease to the object is "more thread-safe than sending it to release") However, there is still a potential danger with this approach. If a client is using the object returned by the getter and whilst the setter accessor autoreleases the NSString object and then, soon after, the object is released and destroyed. The client's reference to the instance variable would no longer be valid.

Listing 3-8 shows implementation of the accessor methods that works around this problem by retaining and autoreleasing the instance variable in the getter.

### Listing 3-8 Implementing accessors for an object variable—better technique

```
(NSString *)title {
    return [[self retain] autorelease];
}
(void)setTitle:(NSString *)newTitle {
    if (title != newTitle) {
        [title autorelease];
        title = [newTitle copy];
    }
}
```

In both examples of the setter method above (Listing 3-5 and Listing 3-7), the new NSString variable is copied rather than retained. The general rule is: if it isn't retained, you should copy it. When an instance is a value object—that is, an object that represents something such as a string, date, number, or record—you should copy it. In other words, you want your own copy of the object.

However, if the object to be stored and accessed is an object entity, such as a UIView or NSWindow, you should retain it. Entities are more costly and relational, and copying them can be expensive. One way to determine whether an object is a value object or entity is to decide whether you're interested in the value of the object or the object itself. If you're interested in the value, a value object and should copy it (assuming, of course, the object conforms to the NSCopy protocol).

Another way to decide whether to retain or copy an instance variable in the setter is to determine whether the instance is an attribute or a relationship. This is especially useful for model objects, where objects are objects that represent the data of an application. An attribute is essentially the same as a value object: object that is a defining characteristic of the object that encapsulates it, such as a color (NSColor) or title. A relationship on the other hand is just that: to retain a relationship (with a reference to) one or more objects. Generally, in setter methods you copy the values of attributes and you retain relationships. However, relationships have a cardinality; they can be one-to-one or one-to-many. One-to-many relationships, which are typically represented by collection objects such as NSArray instances, may require setter methods to do something else than simply retain the instance variable. See Model Object Implementation Guide for details. For on object properties as attributes or relationships, see "Key-Value Mechanisms" (page 128).
