# Chapter 11

647 Class Inheritance

# Point of Information

**Object-Based Versus Object-Oriented Languages**

In an object-based language, data and operations can be incorporated together in such a way that data values can be isolated and accessed through the specified class functions. The capability to bind data members with operations in a single unit is referred to as encapsulation. In C++, encapsulation is provided by its class capability.

For a language to be classified as object-oriented it must also provide inheritance and polymorphism. As discussed, inheritance is the ability to derive one class from another. A derived class incorporates all the data members and member functions of the parent class and can add its own data and function members. Polymorphism permits using the same function name to call one operation in a parent class's objects and a different operation in a derived class's objects.

C++, provides encapsulation, inheritance, and polymorphism, which is a true object-oriented language. Because C, is C++s predecessor, doesn't provide these features, it is not an object-based or object-oriented language.

Except for the access-specifier after the colon and the base class name, there is nothing new or complicated about the construction of the Cylinder class. Before providing a description of the Circle class adding data and function members to the Cylinder class, you need to reexamine access specifiers and how they relate to derived classes.

# Access Specifications

Now you use only private and public access specifiers in a class. Giving all data members status ensures that they can be accessed by class member functions or friends. This restricted access prevents access by nonclass functions (except friends) is sensible because without it, anyone could bypass the private restriction by deriving a class.

To retain access across derived classes, C++ provides a third specification—protected. A **protected** access behaves as private access, in that it permits access only to class member functions, but it permits any derived class to inherit this restriction. The derived class then defines what type of inheritance it's taking on, subject to the base class access specifier. This is is done by the class member specifier, which is listed at the start of the class declaration section. Table 11.3 lists the derived class member resulting from the base class member specifications and the derived class-access specifier.

The shaded region in Table 11.3 shows that if the base class has a protected and the derived class member is protected to its class. Similarly, if the base class has a public access and the derived class-access specifier is public. These specifications for base class data members are the most commonly used, so are the ones used in this section. For all classes intended for use as a base class, a protected member access is used instead of a private designation.