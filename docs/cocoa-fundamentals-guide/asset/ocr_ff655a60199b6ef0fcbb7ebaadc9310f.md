# CHAPTER 2

Cocoa Objects

> Further Reading: For a more detailed discussion of issues relating to the allocation and initialization of Cocoa objects, see "The Runtime System" in The Objective-C Programming Language.

# Introspection

# Evaluating Inheritance Relationships

Once you know the class an object belongs to, you probably know a bit about the object. You know its capabilities, and what kinds of messages it can respond to. Even after introspection you are unfamiliar with the class to which an object belongs, you now know enough to send it messages.

The NSObject declares methods for determining an object's position in the class hierarchy. These methods operate at different granularities. The class and superclass instance methods, for example, return the Class objects representing the class and superclass, respectively, of the receiver. These methods require you to compare one Class object with another. Listing 2-7 gives a simple (one might say trivial) example of their use.

+   Listing 2-7 Using the class and superclass methods

```
while (id anObject = [objectEnumerator nextObject]) {
  if ([self class] == [anObject superclass]) {
    // do something appropriate...
  }
}
```

> Note: Sometimes you use the class or superclass methods to obtain an appropriate receiver for a class message.

More commonly, to check an object's class affiliation, you would send it a isKindOfClass: or isMemberOfClass: The message returns whether the receiver inherits from an instance of a class or an instance of any class that inherits from that class. A isMemberOfClass: message, on the other hand, tells you if the receiver is an instance of the specified class. The isKindOfClass: method is generally more useful because it you can know at once the complete range of messages you can send to an object. Consider the snippet in Listing 2-