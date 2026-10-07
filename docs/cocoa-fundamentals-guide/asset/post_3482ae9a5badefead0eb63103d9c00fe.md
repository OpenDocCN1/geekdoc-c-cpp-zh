
# Cocoa Objects

- *If the value of the instance variable frequently changes but you rarely return it to clients in getter methods, you can make the instance variable mutable but return an immutable copy of it in your accessor method; in memory-managed programs, this object would be autoreleased (Listing 2-13).*

**Listing 2-13** Returning an immutable copy of a mutable instance variable

```objc
@Interface MyClass : NSObject {
// ...
  NSMutableSet *widgets;
}
// ...
@end
```

```objc
@implementation MyClass
  - (NSSet *)widgets {
    return [(NSSet *widgets copy] autorelease];
  }
@end
```

One sophisticated approach for handling mutable collections that are returned to clients is to maintain a flag that records whether the object is currently mutable or immutable. If there is a change, make the object mutable and apply the change. When handing out the collection, make the object immutable (if necessary) before returning it.

# Receiving Mutable Objects

The invoker of a method is interested in the mutability of a returned object for two reasons:

- It wants to know if it can change the object’s value.
- It wants to know if the object’s value will change unexpectedly while it has a reference to it.

# Use Return Type, Not Introspection

To determine whether a client can receive an object, the receiver of a message must rely on the formal type of the return value. If it receives, for example, an array typed as immutable, it should not attempt to mutate it. It is not an acceptable programming practice to determine if an object is mutable based on its class membership—for example—

```objc
if ([array isKindOfClass:[NSMutableArray class]]) {
  // remove objects from array
}
```

For reasons related to implementation, `kindOfClass:` returns in this case may not be accurate. For other reasons this, you should not make assumptions about whether an object is mutable based on class membership. Your decision should be guided solely by what the signature of the method vending the object says about its mutability. If you are not sure an object is mutable or immutable, assume it’s immutable.

A couple of examples might help clarify why this guideline is important:

# CHAPTER 2

# Cocoa Objects

- You read a property list from a file. When the Foundation framework processes the list, it notices that various subsets of the property list are identical, so it creates a set of objects that it shares among all subsets. After you use the created property list objects and decide to mutate one subset. Suddenly, without being aware of it, you've changed the tree in multiple places.

- You ask NSView for its subviews (with the subviews method) and it returns an object that is declared to be an NSArray but could be an NSMutableArray internally. You then pass that array to other code that, through introspection, it determines to mutate and changes it. By changing this, the code is mutating data structures of the NSView class.

Don't make an assumption about object mutability based on what introspection tells you about an object. Treat objects as mutable or not based on what you receive at the API boundaries (that is, based on the return type). If you want to unambiguously mark an object as mutable or immutable when you pass it to clients, pass that information as a flag along with it.

# Make Snapshots of Received Objects

If you want to ensure that a supposedly immutable object received from a method does not mutate your knowing about it, you can make snapshots of the object by copying it. Then compare the stored version of it with the most recent version. If the object has mutated, you can adjust anything in your program that is dependent on the version of the object. Listing 2-14 shows a possible implementation of this technique.

# Listing 2-14 Making a potentially mutable object

```objc
static NSArray *snapshot = nil;
(void)myFunction {
    NSArray *thingArray = [otherObj objects];
    if (snapshot) {
        if (![thingArray isEqual:snapshot]) {
            [self updateStateWith:thingArray];
        }
    }
    snapshot = [thingArray copy];
}
```

A problem with making snapshots of objects for later comparison is that it is expensive. You're required to make multiple copies of the same object. A more efficient alternative is to use key-value observing. See "Key-Value Observing" (page 154) for an overview of this protocol.

# Mutable Objects in Collections

Storing mutable objects in collections can cause problems. Certain collections can become invalid or even corrupt if they contain mutable objects, by mutating, these objects can affect the way they are placed in the collection. First, the properties of objects are keys in collections such as NSDictionary objects or NSMutable objects will, if changed, the collection if the changes affects the results of the object's hash or isEqual (the hash method of the objects in the collection does not depend on their internal state, correction is less likely). Second, if an object in an ordered collection as a sorted array has its properties changed, this might affect how the object compares to other objects in the array, rendering the ordering invalid.

# CHAPTER 2
Cocoa Objects

# Class Clusters

Class clusters are a design pattern that the Foundation framework makes extensive use of. Class clusters a group of private concrete subclasses under a public abstract superclass. The grouping of classes in this way simplifies the publicly visible architecture of an object-oriented framework without reducing its functional richness. Class clusters are based on the Abstract Factory design pattern discussed in “Cocoa Design Patterns” (page 137).

# Without Class Clusters: Simple Concept but Complex Interface

To illustrate the class architecture and its benefits, consider the problem of constructing objects of different types (char, int, float, double). In the Foundation framework, you generally create an object by invoking a className method or the `alloc`... `init`... methods. Taking the Foundation framework's `NSNumber` class as an example, you could send these messages to create number objects:

```objc
NSNumber *Char = [NSNumberWithChar:'a'];
NSNumber *Int = [NSNumberWithInt:1];
NSNumber *float = [NSNumberWithFloat:1.0];
NSNumber *Double = [NSNumberWithDouble:1.0];
```

You are responsible for releasing the objects returned from the factory method; see [Class Factory Methods](#(page 86) for more. Many classes also use the standard `alloc`... and `init`... methods to create objects that require you to manage their deallocation.

Each object returned—`char`, `int`, `float`, and `double`—may belong to a different subclass (and in fact). Each object's method is hidden, it is public, the interface declared by the abstract subclass, `NSNumber`. Although it is not precisely correct, it's convenient to consider the `char`, `int`, `float`, and `double` objects to be instances of the `NSNumber` class, because they're created by `NSNumber` class and accessed through instance methods declared by `NSNumber`.

The abstract class in class cluster must declare methods for creating instances of its private subclasses. It's the subclass's responsibility to instantiate an object of the proper subclass based on the creation method that you invoke—you can't choose the class of the instance.

# Class Clusters with Multiple Public Superclasses

In the example below, one abstract public class declares the interface for multiple private subclasses. This is a class cluster in the purest sense. It is also possible, and often desirable, to have two (or more) abstract public classes that declare the interface for the cluster. This is what in the Foundation framework, which includes the clusters listed in Table 2-3.

**Figure 2-10** A simple hierarchy for number
img/0c5ea7638ae08e6bc22975f6ee_94

**Figure 2-11** A more complete number hierarchy
img/0c5ea7638ae08e6bc22975f6ee_94_1

**Figure 2-12** Class cluster applied to number classes
img/0c5ea7638ae08e6bc22975f6ee_95_0

# With Class Clusters: Simple Concept and Simple Interface

Applying the class cluster design pattern to this problem yields the class hierarchy in 2-12 (private classes are in gray).
