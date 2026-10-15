# Interface Hierarchies

The concept of inheritance can be applied to interfaces as well as classes. That is, one interface can be derived from another interface. These relationships can form an interface hierarchy, which is similar to a class hierarchy. Inheritance relationships between interfaces are shown in UML diagrams using the same connection (an arrow with an open arrowhead) as they are with classes.

When a parent interface is used to derive a child interface, the child inherits all abstract methods and constants of the parent. Any class that implements the child interface must implement all of the methods. There are no visibility issues when dealing with inheritance between interfaces (as there are with protected and private members of a class), because all members of an interface are public.

Class hierarchies and interface hierarchies do not overlap. That is, an interface cannot be used to derive a class, and a class cannot be used to derive an interface. A class and an interface interact only when a class is designed to implement a particular interface.

> KEY CONCEPT
> Inheritance can be applied to interfaces so that one interface can be derived from another.

# SELF-REVIEW QUESTIONS (see answers in Appendix N)

+   SR 9.10 Draw a UML class diagram showing an inheritance hierarchy containing classes that represent different types of food. Show some appropriate variables and method names for at least two of these classes.
+   SR 9.11 What is the significance of the Object class?
+   SR 9.12 Which is the only Java class that does not have a parent class? Explain.
+   SR 9.13 What is the role of an abstract class?
+   SR 9.14 Why is it a contradiction to define a final, abstract class?
+   SR 9.15 What is an interface hierarchy?

# 9.4 Visibility

As we discussed earlier in this chapter, all variables and methods, even private members, that are defined in a parent class are inherited by a child class. They exist for an object of a derived class, even though they can’t be referenced directly. They can, however, be referenced indirectly.

Let’s look at an example that demonstrates this situation. The program shown in Listing 9.10 contains a main method that instantiates a Pizza

> KEY CONCEPT
> Private members are inherited by the child class, but cannot be referenced directly by name. They may be used indirectly, however.