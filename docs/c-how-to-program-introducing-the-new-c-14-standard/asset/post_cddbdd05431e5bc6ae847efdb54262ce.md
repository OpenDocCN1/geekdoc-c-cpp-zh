
## 9.16 Wrap-Up

This chapter deepened our coverage of classes, using a `Time` class case study to introduce several new features. We showed how to engineer a class to separate its interface from its implementation. We used an include guard to prevent the code in a header (`.h`) file from being included multiple times in the same source code (`.cpp`) file.

You created formatted `string`s using `ostringstream` objects. You learned how to use the arrow operator to access an object’s members via a pointer of the object’s class type. You learned that member functions have class scope—the member function’s name is known only to the class’s other members unless referred to by a client of the class via an object name, a reference to an object of the class, a pointer to an object of the class or the scope resolution operator. We also discussed access functions (commonly used to retrieve the values of data members or to test the truth or falsity of conditions), and utility functions (`private` member functions that support the operation of the class’s `public` member functions).

You learned that a constructor can specify default arguments that enable it to be called in a variety of ways. You also learned that any constructor that can be called with no arguments is a default constructor and that there can be at most one default constructor per class. We discussed destructors for performing termination housekeeping on an object of a class before that object is destroyed, and demonstrated the order in which an object’s constructors and destructors are called.

We demonstrated the problems that can occur when a member function returns a reference or a pointer to a `private` data member, which breaks the encapsulation of the class. We also showed that objects of the same type can be assigned to one another using default memberwise assignment—in [Chapter 10](#), we’ll discuss how this can cause problems when an object contains pointer members.

You learned how to specify `const` objects and `const` member functions to prevent modifications to objects, thus enforcing the principle of least privilege. You also learned that, through composition, a class can have objects of other classes as members. We demonstrated how to declare and use `friend` functions.

You learned that the `this` pointer is passed as an implicit argument to each of a class’s non-`static` member functions, allowing them to access the correct object’s data members and other non-`static` member functions. We used the `this` pointer explicitly to access the class’s members and to enable cascaded member-function calls. We motivated the notion of `static` data members and member functions and demonstrated how to declare and use them.

In [Chapter 10](#), we continue our study of classes and objects by showing how to enable C++’s operators to work with class-type objects—a process called operator overloading. For example, you’ll see how to overload the `<<` operator so it can be used to output a complete array without explicitly using an iteration statement.

## Summary

### Section 9.2 `Time` Class Case Study: Separating Interface from Implementation

- Placing a complete class definition in a header reveals the entire implementation of the class to the class’s clients—a header is simply a text file that anyone can open and read.
- Conventional software engineering wisdom says that to use an object of a class, the client code needs to know only: what member functions to call, what arguments to provide to each member function and what return type to expect from each member function. The client code does not need to know how those functions are implemented.

### Section 9.2.1 Interface of a Class

- **Interfaces** (p. 388) define and standardize the ways in which things such as people and systems interact with one another.
- The interface of a class describes what services a class’s clients can use and how to request those services, but not how the class carries out the services.
- A class’s `public` interface consists of the class’s `public` member functions (also known as the class’s `public` services).
- You can specify a class’s interface by writing a class definition that lists only the class’s member-function prototypes and the class’s data members.

### Section 9.2.2 Separating the Interface from the Implementation

- To separate the class’s interface from its implementation, we break up the class into two files—a header in which the class is defined and a source-code file in which the class’s member functions are defined.
- By convention, member-function definitions are placed in a source-code file of the same base name as the class’s header but with a `.cpp` filename extension (some compilers support other filename extensions as well).

### Section 9.2.3 `Time` Class Definition

- A class definition that contains function prototypes rather than definitions describes the class’s `public` interface without revealing the class’s member-function implementations.
- The class’s header still specifies the class’s `private` data members as well—the compiler must know the data members of the class to determine how much memory to reserve for each object of the class.
- Including the class’s header in the client code provides the compiler with the information it needs to ensure that the client code calls the class’s member functions correctly.
- An **include guard** (p. 389)—consisting of `#ifndef`, `#define` and `#endif`—prevents a header from being `#include`d multiple times in the same source-code file.
- Attempts to include a header multiple times (inadvertently) typically occur in large programs with many headers that may themselves include other headers.

### Section 9.2.5 Scope Resolution Operator (`::`)

- When member functions are defined outside a class’s definition, each member function’s name must be preceded by the class name and the scope resolution operator (`::`). This “ties” each member function to the class definition, which declares the class’s members, telling the compiler that each member function is within that **class’s scope** (p. 391).

### Section 9.2.6 Including the Class Header in the Source-Code File

- The source-code file containing a class’s member-function definitions must include the class’s header. This enables the compiler to ensure that the first line of each member function matches its prototype in the class’s header and that each member function knows about the class’s data members and other member functions.

### Section 9.2.7 `Time` Class Member Function `setTime` and Throwing Exceptions

- A function can **throw an exception** (p. **392**) of type `invalid_argument` (p. **392**) to notify the client code that an invalid argument was received.
- A `throw` **statement** (p. **392**) creates and throws an object of the type specified to the right of the `throw` keyword.
- After an exception object is created, the `throw` statement immediately terminates the function and the exception is returned to the calling function.

### Section 9.2.8 `Time` Class Member Function `toUniversalString` and String Stream Processing

- Objects of class `ostringstream` (p. 392; from the header `<sstream>`) provide the same functionality as `cout`, but write their output to `string` objects in memory.
- Class `ostringstream`’s `str` (p. 392) member function returns the `string` created by an `ostringstream`.
- Parameterized stream manipulator `setfill` (p. 392) specifies the **fill character** (p. 392) that’s displayed when an integer is output in a field wider than the number of digits in the value.
- The fill characters appear to the *left* of the digits in the number for a right-aligned value—for left-aligned values, the fill characters appear to the right.
- Once the fill character is specified with `setfill`, it applies for all subsequent values that are displayed in fields wider than the value being displayed—this is a sticky setting.
