> > As stated and restated throughout this chapter, our primary goal is to develop abstract object-oriented classes to be used as both a foundation and a reusable base that will move us into the higher levels of programming. Therefore, our development of classes must include completely abstracted versions of both member functions and their variables, so that base classes are capable of adapting to a host of scenarios such as calculating either whole or floating-point values, defining Boolean types, and referencing characters without the need to revise our coding. This should be a sustained goal as both a student of C# and throughout your future as a programmer.

![](bbox=[0.808, 0.101, 0.928, 0.191])

# Abstract

Another useful feature when dealing with inheritance is the ability to declare a class using an *abstract* modifier, which is a modifier that alters the application of a class by allowing it to be used as a reference only by other inheriting classes. The practical application of abstract modifiers becomes obvious as we restrict base references in order to produce a large base of generic classes. Abstract classes cannot be instantiated, nor can they be modified with a sealed modifier (sealed modifiers are defined later in this chapter). Only abstract classes may use abstract methods and abstract accessors, but all nonabstract classes derived from such classes must include implementations of the abstract references to guarantee that those methods will be referenced from the derived class. Abstract methods are also implicitly virtual, thus, that distinction need not be declared. Inheriting classes wishing to duplicate static methods referenced from within an abstract base must also include an *overriding* modifier.

> > Individual properties declared with an abstract modifier reference cannot also contain a static modifier (see Example 5.38).

![](bbox=[0.811, 0.704, 0.928, 0.798])