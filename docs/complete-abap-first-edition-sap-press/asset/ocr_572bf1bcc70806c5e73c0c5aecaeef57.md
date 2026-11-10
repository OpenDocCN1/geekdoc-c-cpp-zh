# 8.4.4　Interfaces

Similar to Java, ABAP Objects only supports single inheritance and don't support multiple inheritance as in C++. *Single inheritance* means a class can have multiple subclasses but only one superclass. Many subclasses can use the same class as their superclass, but each subclass can only have a single superclass.

Modern programming languages didn't add support for multiple inheritance (having multiple superclasses) in order to avoid ambiguity. One of the common problems with multiple inheritance is called the *diamond problem*. For example, as depicted in Figure 8.12, assume you have two subclasses B and C inheriting from the same superclass A and that both classes B and C have redefined a method XYZ of class A in their implementation. Now, if a new subclass D is defined as having both class B and class C as its superclasses then which superclass method will it use?

![](bbox=[0.148, 0.409, 0.811, 0.666])

**Figure 8.12** Diamond Problem with Multiple Inheritance

One way of implementing multiple inheritance is to use interfaces. Interfaces provide all the advantages of multiple inheritance while avoiding all the problems.

Interfaces are defined similarly to classes via the `INTERFACE` statement. An interface only contains a definition for which the implementation is maintained in the class that uses the interface. If you need a common definition in multiple classes, then you can create an interface and use it in multiple classes.