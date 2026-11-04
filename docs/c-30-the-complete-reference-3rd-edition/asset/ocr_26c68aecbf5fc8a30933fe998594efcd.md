# Interfaces, Structures, and Enumerations

This chapter discusses one of C#'s most important features: the *interface*. An *interface* defines a set of methods that will be implemented by a class. An *interface* does not, itself, implement any method. Thus, an *interface* is a purely logical construct that describes functionality without specifying implementation.

Also discussed in this chapter are two more C# data types: *structures* and *enumerations*. *Structures* are similar to classes except that they are handled as value types rather than reference types. *Enumerations* are lists of named integer constants. Structures and enumerations contribute to the richness of the C# programming environment.

# Interfaces

In object-oriented programming it is sometimes helpful to define what a class must do, but not how it will do it. You have already seen an example of this: the abstract method. An abstract method declares the return type and signature for a method, but provides no implementation. A derived class must provide its own implementation of each abstract method defined by its base class. Thus, an abstract method specifies the *interface* to the method, but not the *implementation*. Although abstract classes and methods are useful, it is possible to take this concept a step further. In C#, you can fully separate a class' *interface* from its implementation by using the keyword *interface*.

Interfaces are syntactically similar to abstract classes. However, in an interface, no method can include a body. That is, an interface provides no *implementation* whatsoever. It specifies what must be done, but not how. Once an interface is defined, any number of classes can implement it. Also, one class can implement any number of interfaces.

To implement an interface, a class must provide bodies (*implementations*) for the methods described by the *interface*. Each class is free to determine the details of its own *implementation*. Thus, two classes might implement the same *interface* in different ways, but each class still supports the same set of methods. Therefore, code that has knowledge of the *interface* can use objects of either class since the *interface* to those objects is the same. By providing the *interface*, C# allows you to fully utilize the “one interface, multiple methods” aspect of polymorphism.