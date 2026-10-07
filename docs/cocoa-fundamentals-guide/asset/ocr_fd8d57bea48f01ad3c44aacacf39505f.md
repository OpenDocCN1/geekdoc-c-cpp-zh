# CHAPTER 2
Cocoa Objects

either do nothing or return some reasonable default value as self. These default implementations make it possible to send messages such as init to any Cocoa object—even to any class that does not override—without risking a runtime exception. It is not necessary to check (using respondsTo:) before sending the message. More importantly, the "placeholder" methods of NSObject define a common structure for Cocoa objects and establishes conventions that, when followed by all classes, make object interactions more reliable.

# Instance and Class Methods

The runtime system methods defined in the root class are in a special way. Instance methods defined in a root class can be performed by both instances and classes. Therefore, all classes have access to the instance methods defined in the root class. Any object can perform any instance method, provided it doesn't have a class with the same name.

For example, a class could be sent messages to perform the NSObject instance methods respondsToSelector:performSelector:withObject: as in this example:

```
SEL method = @selector(riskAll:);
if ([MyClass respondsToSelector:method])
[MyClass performSelector:method withObject:self];
```

Note that the only instance methods allowed to a class object are defined in its root class. In if MyClass implemented either respondsToSelector: or performSelector:withObject, these new versions would be only available to instances. The object for MyClass implemented respondsToSelector: or performSelector:withObject: as class methods rather than instance methods, the class would perform these new versions.

# Object Retention and Disposal

Objective-C gives you two ways to ensure that objects persist when they are needed and when they are no longer needed, the preferred approach is to use the technology of garbage collection: The runtime detects objects that are no longer needed and disposes of them automatically. (The preferred approach is the simpler in most cases.) The second approach, called memory management, is based on reference counting: An object carries with a numerical value when this value reaches zero, the object is deallocated.

The amount of work you do, as a developer writing Objective-C code, to take advantage of garbage collection or memory management varies.

+   - Garbage Collection. To enable garbage collection, turn on the Objective-C Garbage Collection flag building in Xcode. For each of your custom classes, you might also have to implement the finalize method to remove instances as notification observers and to free any resources that are not instance variables. Also, ensure that in your nib the object acting as File's Owner maintains an outlet connection to that top-level object you want to persist.

> iOS Note: Garbage collection is not supported in iOS.