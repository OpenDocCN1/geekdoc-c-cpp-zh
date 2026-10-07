# Chapter 13 Class Inheritance

Note that if a function declares an argument as a reference or pointer to const, it cannot pass along argument to another function unless that function also guarantees not to change the argument.

# Public Inheritance Considerations

Naturally, adding inheritance to a program brings up a number of considerations. Let's look at a few.

# Is-a Relationship Considerations

You should be guided by the is-a relationship. If your proposed class is not a particular kind of the base class, you shouldn't use public derivation. For example, you shouldn't derive a Programmer class from a Brain class. If you want to represent the belief that a programmer has a brain, you should use a Brain class object as a member of the class.

In some cases the best approach may be to create an abstract data class with pure functions and to derive other classes from it.

Remember that one expression of the is-a relationship is that a base class pointer point to a derived-class object and that a base-class reference can refer to a derived-class object without an explicit type cast. Also remember that the reverse is not true; thus, you cannot have a derived-class pointer or reference to a base-class object without an explicit type cast. Depending on the class declarations, such an explicit cast (a downcast) may not make sense. (You might want to review Figure 13.4)

# What's Not Inherited

Constructors are not inherited. That is, a derived object requires calling a derived-class constructor. However, derived-class constructors typically use the memberinitializer list to call base-class constructors to construct the base class portion of a derived object. If the derived-class constructor doesn't explicitly call a base-class constructor by using the member-initializer list, it uses the base class's default constructor to pass information to its immediate base class. C++11 adds a mechanism that enables the inheritance of constructors but the default behavior is still that constructors are not inherited.

Destructors are not inherited either. However, when an object is destroyed, the program first calls the derived destructor and then the base destructor. If there is a default base destructor, the compiler generates a default derived class destructor. Generally speaking, if a class serves as a base class, its destructor should be virtual.

Assignment operators are not inherited. The reason is simple. An inherited method has the same function signature in a derived class as it does in the base class. However, an assignment operator has a function signature that changes from class to class because it has a formal parameter that is the class type. Assignment operators do have some interesting properties, which we'll look at next.