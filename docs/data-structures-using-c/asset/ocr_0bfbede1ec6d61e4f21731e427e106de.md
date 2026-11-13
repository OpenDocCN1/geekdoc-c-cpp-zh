# **Basic Concepts of Object-oriented Programming**

We shall discuss some of the basic concepts of OOP.

**Objects** Objects are the basic runtime entities in an object-oriented system. A programming problem is analysed in terms of objects and the nature of communication between them. Each object contains data and code to manipulate the data.

**Classes** Object-oriented programming encapsulates data (attributes) and functions (behaviour) into packages called as classes. A class is a user-defined data type.

**Data abstraction and encapsulation** Combining a number of variables and functions into a single package, such as an object of some class, is called as encapsulation. Abstraction refers to the act of representing essential features without including the details of implementation. Generally, data members are made private and are accessible to only class member functions. This insulation of data from direct access by the program is called data hiding or information hiding.

**Inheritance** Inheritance is a process by which the objects of one class inherit the properties of another class. Classes in C++ support the concept of hierarchical classification.

**Reusability** The concept of inheritance provides the feature of reusability by additional features to the existing class without modifying the existing one leads to a new class.

**Polymorphism** Polymorphism means the ability to take more than one form. Polymorphism is a means by which we can request an object to do something without knowing exactly what kind of object it is, and the object will figure out how to process the request appropriately.

**Dynamic binding** Binding refers to the linking of a procedure call to the code to be executed in response to the call. Dynamic binding means that the code associated with a given procedure call is not known until the time of call at runtime. This is associated with polymorphism and inheritance.

**Message passing** An OOP consists of a set of objects that communicate with each other. Message for an object is a request for execution of a procedure and therefore will invoke a function in the receiving object that generates the desired result. Message passing involves specifying the name of the object, the name of the function (message), and the information to be sent.

# *List Abstract Data Type*

We have studied about ADTs. An ADT consists of a data type and operations that manipulate the data. From the application program’s perspective, it is also independent of the data structure used to implement it. The user while using the list ADT is not aware of the implementation of how the data is manipulated and what data structure is used. Hence, we could implement the list using either an array or a linked list. Further, linked list can be realized using array or using pointers and dynamic memory management. Thus, if we implement a list using linked list, we could change the implementation from a linked