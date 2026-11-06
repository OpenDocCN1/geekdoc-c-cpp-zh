which constructors and destructors are called for objects of classes that are part of an inheritance hierarchy. Finally, we explained the three types of inheritance—public, protected and private—and the accessibility of base-class members in a derived class when using each type.

In Chapter 13, Object-Oriented Programming: Polymorphism, we build on our discussion of inheritance by introducing polymorphism—an object-oriented concept that enables us to write programs that handle, in a more general manner, objects of a wide variety of classes related by inheritance. After studying Chapter 13, you’ll be familiar with classes, objects, encapsulation, inheritance and polymorphism—the essential concepts of object-oriented programming.

# Summary

# *Section 12.1 Introduction*

+   - Software reuse reduces program development time and cost.

# *Section 12.2 Base Classes and Derived Classes*

+   - Inheritance is a form of software reuse in which you create a class that absorbs an existing class’s data and behaviors and enhances them with new capabilities. The existing class is called the base class, and the new class is referred to as the derived class.
+   - A direct base class is the one from which a derived class explicitly inherits. An indirect base class is inherited from two or more levels up the class hierarchy.
+   - With single inheritance, a class is derived from one base class. With multiple inheritance, a class inherits from multiple (possibly unrelated) base classes.
+   - A derived class represents a more specialized group of objects. Typically, a derived class contains behaviors inherited from its base class plus additional behaviors. A derived class can also customize behaviors inherited from the base class.
+   - Every object of a derived class is also an object of that class’s base class. However, a base-class object is not an object of that class’s derived classes.
+   - The *is-a* relationship represents inheritance. In an *is-a* relationship, an object of a derived class also can be treated as an object of its base class.
+   - The *has-a* relationship represents composition—an object contains one or more objects of other classes as members, but does not disclose their behavior directly in its interface.
+   - A derived class cannot access the private members of its base class directly. A derived class can access the public and protected members of its base class directly.
+   - A derived class can effect state changes in private base-class members, but only through non-private member functions provided in the base class and inherited into the derived class.
+   - A base-class member function can be redefined in a derived class.
+   - Single-inheritance relationships form treelike hierarchical structures.
+   - It’s possible to treat base-class objects and derived-class objects similarly; the commonality shared between the object types is expressed in the base class’s data members and member functions.

# *Section 12.3 protected Members*

+   - A base class’s public members are accessible anywhere that the program has a handle to an object of that base class or to an object of one of that base class’s derived classes—or, when using the binary scope resolution operator, whenever the class’s name is in scope.