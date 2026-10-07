# OBJECT-ORIENTED PROGRAMMING

that work individually or in combination to carry out a specific task. These objects are designed by first creating an abstract conceptualization of some aspect of a problem and formalizing the notion in a computer code construct called a class. An instance of a class is created inside a program is called an object. It encapsulates its own internal data and the methods/functions/subroutines that are appropriate for use with the data it contains. This "encapsulation" feature has the benefit of providing a mechanism for data protection. The object-oriented framework is also amenable to design and reuse in that the creation of objects tends to enforce modularity

As one might expect, problem deconstruction in functional programming involves the creation of a set of functions that work in tandem to find a solution. Under strict adherence to the functional programming philosophy, functions can only take inputs and outputs; they are not allowed to make changes in the data to the program. Instead, each function operates on its output providing the source of input for another function or functions along the solution path. Disallowing changes in input data functional programming represents a kind of counterpoint to the object-oriented approach where the creation and alteration of objects is the focus of a program.

# 1.2 Object-oriented programming

This section gives a high-level introduction to the object-oriented programming (OOP) concept. These ideas recur in later chapters and will be helpful to have a common technical dialect with which to discuss them.

The focus of OOP is creation of classes. A class provides an abstract description of a concept through specification of its attributes and its behavior. For scientific computing the "concept" will usually represent a mathematical operation as solving a system of equations, generating a random number or finding the minimum of a given function. In this respect a class should be designed with a single meta-task in mind. For example, a class for linear algebra probably not contain methods for checking that an integer is a prime number. The construction of focused classes has the benefit of simplifying development as well as enhancing the opportunities for code reuse.

The attributes of a class are its members and its member functions. Methods often belong to primitive data types in the sense of being integer, floating-point or other types of variables that are inherent to the programming language. However, they can be more abstract in the sense of deriving from other user-created types or classes. As noted in the previous section, an instance of a class for which members have been given specific values is called an object.

The behavior of a class depends on the class methods that determine the type of actions it can perform as well as the ways the object can be altered. In combination the data and function methods provide answer to the essential questions

+   - What are objects of the class supposed to do?

+   - What data or object will be provided with different levels of protection. Specifically, class members can be classified as private, public or protected. The private designation has the consequence that such members and methods can be used only within the class itself. Members and methods are open to use outside the class by other functions and objects. Protected class member and methods are only available to derived class objects that inherit from the class in a sense to be described shortly.

The OOP approach provides us with various types of polymorphism. The word "polymorphism" means that a single thing can take different forms. In the context of OOP this translates to functions and classes that act or behave in different ways depending on