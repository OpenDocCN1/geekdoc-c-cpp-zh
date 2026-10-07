# With Class Clusters: Simple Concept and Simple Interface

Applying the class cluster design pattern to this problem yields the class hierarchy in Figure 2-12 (private classes are in gray).

Figure 2-12    Class cluster architecture applied to number classes

![](bbox=[0.18, 0.22, 0.87, 0.31])

Users of this hierarchy see only one public class, Number, so how is it possible to allocate instances of the proper subclass? The answer is in the way the abstract superclass handles instantiation.

# Creating Instances

The abstract superclass in a class cluster must declare methods for creating instances of its private subclasses. It’s the superclass’s responsibility to dispense an object of the proper subclass based on the creation method that you invoke—you don’t, and can’t, choose the class of the instance.

In the Foundation framework, you generally create an object by invoking a +className... method or the alloc... and init... methods. Taking the Foundation framework’s NSNumber class as an example, you could send these messages to create number objects:

```
NSNumber *aChar = [NSNumber numberWithChar:'a'];
NSNumber *anInt = [NSNumber numberWithInt:1];
NSNumber *aFloat = [NSNumber numberWithFloat:1.0];
NSNumber *aDouble = [NSNumber numberWithDouble:1.0];
```

You are not responsible for releasing the objects returned from factory methods; see “Class Factory Methods” (page 86) for more information. Many classes also provide the standard alloc... and init... methods to create objects that require you to manage their deallocation.

Each object returned—aChar, anInt, aFloat, and aDouble—may belong to a different private subclass (and in fact does). Although each object’s class membership is hidden, its interface is public, being the interface declared by the abstract superclass, NSNumber. Although it is not precisely correct, it’s convenient to consider the aChar, anInt, aFloat, and aDouble objects to be instances of the NSNumber class, because they’re created by NSNumber class methods and accessed through instance methods declared by NSNumber.

# Class Clusters with Multiple Public Superclasses

In the example above, one abstract public class declares the interface for multiple private subclasses. This is a class cluster in the purest sense. It’s also possible, and often desirable, to have two (or possibly more) abstract public classes that declare the interface for the cluster. This is evident in the Foundation framework, which includes the clusters listed in Table 2-3.