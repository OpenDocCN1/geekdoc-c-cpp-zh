
Next, we discussed pure `virtual` functions and abstract classes (classes with one or more pure `virtual` functions). You learned that abstract classes cannot be used to instantiate objects, while concrete classes can. We demonstrated using abstract classes in an inheritance hierarchy. You learned how polymorphism works “under the hood” with *vtables* created by the compiler.

We used runtime type information (RTTI) and dynamic casting to determine the type of an object at execution time and act on that object accordingly. We used the `typeid` operator to get a `type_info` object containing a given object’s type information.

In the next chapter, we discuss many of C++’s I/O capabilities and demonstrate several stream manipulators that perform various formatting tasks.

## Summary

## Section 12.1 Introduction

- **Polymorphism** (p. [532](#)) enables us to write programs that process objects of classes that are part of the same class hierarchy as if they were all objects of the hierarchy’s base class.
- With polymorphism, we can design and implement systems that are easily extensible—new classes can be added with little or no modification to the general portions of the program. The only parts of a program that must be altered to accommodate new classes are those that require direct knowledge of the new classes that you add to the hierarchy.

## Section 12.2 Introduction to Polymorphism: Polymorphic Video Game

- With polymorphism, one function call can cause different actions to occur, depending on the type of the object on which the function is invoked.
- This makes it possible to design and implement more extensible systems. Programs can be written to process objects of types that may not exist when the program is under development.

## Section 12.3 Relationships Among Objects in an Inheritance Hierarchy

- C++ enables polymorphism—the ability for objects of different classes related by inheritance to respond differently to the same member-function call.

## Section 12.4.2 Declaring `virtual` Functions

- Polymorphism is implemented via `virtual` **functions** (p. **540**) and **dynamic binding** (p. **541**).

## Section 12.4.3 Invoking a `virtual` Function Through a Base-Class Pointer or Reference

- When a base-class pointer or reference is used to call a `virtual` function, C++ chooses the correct overridden function in the appropriate derived class associated with the object.

## Section 12.4.4 Invoking a `virtual` Function Through an Object’s Name

- If a `virtual` function is called by referencing a specific object by name and using the dot member-selection operator, the reference is resolved at compile time (this is called **static binding**; p. 541); the `virtual` function that’s called is the one defined for the class of that particular object.
- Derived classes can override a base-class `virtual` function if necessary, but if they do not, the base class’s implementation is used.

## Section 12.4.5 `virtual` Functions in the `CommissionEmployee` Hierarchy

- To help prevent errors, apply C++11’s `override` **keyword** (p. 542) to the prototype of every derived-class function that overrides a base-class virtual function. This enables the compiler to check whether the base class has a `virtual` member function with the same signature. If not, the compiler generates an error.

## Section 12.4.6 `virtual` Destructors

- Declare a `virtual` **base-class destructor** (p. 546) if the class contains `virtual` functions. This makes all derived-class destructors virtual, even though they do not have the same name as the base-class destructor. If an object in the hierarchy is destroyed explicitly by applying the `delete` operator to a base-class pointer to a derived-class object, the destructor for the appropriate class is called. After a derived-class destructor runs, the destructors for all of that class’s base classes run all the way up the hierarchy.
- In C++11, you can tell the compiler to explicitly generate the default version of a default constructor, copy constructor, move constructor, copy assignment operator, move assignment operator or destructor by following the special member function’s prototype with `= default` (p. 546).

## Section 12.4.7 C++11: `final` Member Functions and Classes

- In C++11, a base-class virtual function that's declared `final` (p. [546](#)) in its prototype cannot be overridden in any derived class.
- In C++11, you can **declare a class as `final`** (p. [547](#)) to prevent it from being used as a base class.
- Attempting to override a `final` member function or inherit from a `final` base class results in a compilation error.

## Section 12.5 Type Fields and `switch` Statements

- Polymorphic programming with `virtual` functions can eliminate the need for `switch` logic. You can use the `virtual` function mechanism to perform the equivalent logic automatically, thus avoiding the kinds of errors typically associated with `switch` logic.

## Section 12.6 Abstract Classes and Pure `virtual` Functions

- **Abstract classes** (p. **547**) are typically used as base classes, so we refer to them as **abstract base classes** (p. **547**). No objects of an abstract class may be instantiated.
- Classes from which objects can be instantiated are **concrete classes** (p. **547**).

## Section 12.6.1 Pure Virtual Functions

- You create an abstract class by declaring one or more **pure virtual functions** (p. 548) with pure specifiers (`= 0`) in their declarations.
- If a class is derived from a class with a pure `virtual` function and that derived class does not supply a definition for that pure `virtual` function, then that `virtual` function remains pure in the derived class. Consequently, the derived class is also an abstract class.
- Although we cannot instantiate objects of abstract base classes, we can declare pointers and references to objects of abstract base classes. Such pointers and references can be used to enable polymorphic manipulations of derived-class objects instantiated from concrete derived classes.

## Section 12.8 (Optional) Polymorphism, Virtual Functions and Dynamic Binding “Under the Hood”

- Dynamic binding requires that at runtime, the call to a virtual member function be routed to the `virtual` function version appropriate for the class. A `virtual` function table called the *vtable* (p. 563) is implemented as an array containing function pointers. Each class with `virtual` functions has a *vtable*. For each `virtual` function in the class, the *vtable* has an entry containing a function pointer to the version of the `virtual` function to use for an object of that class. The `virtual` function to use for a particular class could be the function defined in that class, or it could be a function inherited either directly or indirectly from a base class higher in the hierarchy.
- When a base class provides a `virtual` member function, derived classes can override the `virtual` function, but they do not have to override it.
- Each object of a class with `virtual` functions contains a pointer to the *vtable* for that class. When a function call is made from a base-class pointer to a derived-class object, the appropriate function pointer in the *vtable* is obtained and dereferenced to complete the call at execution time.
- Any class that has one or more `nullptr` pointers in its *vtable* is an abstract class. Classes without any `nullptr` *vtable* pointers are concrete classes.
- New kinds of classes are regularly added to systems and accommodated by dynamic binding.

## Section 12.9 Case Study: Payroll System Using Polymorphism and Runtime Type Information with `dynamic_cast`, `typeid` and `type_info`

- Operator `dynamic_cast` (p. 567) checks the type of the object to which a pointer points, then determines whether the type has an *is-a* relationship with the type to which the pointer is being converted. If so, `dynamic_cast` returns the object’s address. If not, `dynamic_cast` returns `nullptr`.
- Operator `typeid` (p. 570) returns a reference to a `type_info` object (p. 570) that contains information about the operand’s type, including the type name. To use `typeid`, the program must include header `<typeinfo>` (p. 570).
- When invoked, `type_info` member function `name` (p. 570) returns a pointer-based string that contains the name of the type that the `type_info` object represents.
- Operators `dynamic_cast` and `typeid` are part of C++’s **runtime type information (RTTI; p. 567)** feature, which allows a program to
