
### Fig. 10.3 Hierarchy of classes defining different types of errors

![](img/0da15892b2796544fb447dc5727e9ab4_455_0.png)

### PROGRAM 10.8 Invoking the pure virtual function statically

```cpp
//StaticInvocation.cpp
#include <iostream>
using namespace std;

class Error
{
private:
    int ErrorCode;
    string Description;
public:
    virtual void PossibleSolutions() const = 0;
};

// Body of the virtual function defined outside the class
void Error::PossibleSolutions() const
{
    cout << "Generic error\n";
}

// Derived class SyntaxError
class SyntaxError : public Error
{
public:
    void PossibleSolutions() const
    {
        Error::PossibleSolutions();
        cout << "Check the syntax\n";
    }
};

// Derived class LogicalError
class LogicalError : public Error
{
public:
    void PossibleSolutions() const
    {
        Error::PossibleSolutions();
        cout << "Logic is erroneous\n";
    }
};

// Class CompilerError is derived from SyntaxError
class CompilerError : public SyntaxError
{
public:
    void PossibleSolutions() const
    {
```

Also shows how one can define `PossibleSolutions()` as a pure virtual function, as all classes inherited from it must define it. The `Error` class (the base class) must also have generic solutions using `PossibleSolutions()`, and so must have a body. As explained earlier, the body is defined outside the `Error` class.

### Calling a pure virtual function

If the `PossibleSolutions()` function of any class is called, it will call the `PossibleSolutions()` function for only that case. For example, consider the following statements:

```cpp
Error *pError = new InitializationError;
pError->PossibleSolutions();

Error *qError = new LinkerError;
qError->PossibleSolutions();
```

This code will only display the possible solutions for initialization errors and linker errors. The need here is that it should also display errors related to their base classes. In case of initialization errors, it should also display the possible solutions for logical errors as well as general errors. In case of linker error, it should display possible solutions for linker errors, syntax errors, and general errors.

### Need for static invocation

This can be achieved by statically invoking `PossibleSolutions()` function for all the base classes, such as the `PossibleSolutions()` function of `LinkerError` in turn calls syntax errors as well as generic errors.

It can be seen that the function contains a call to the `PossibleSolutions()` function of the `SyntaxError` class, which in turn calls the `Error::PossibleSolutions()`; thus, one can get all possible solutions related to the error.

`SyntaxError::PossibleSolutions()` and `Error::PossibleSolutions()` are calls to virtual functions. They are different though. They are known as statically invoked calls to virtual functions.

Why is the static invocation needed? A linker error is also a syntax error, which in turn is an error. We need to print the description given by every class. Why a pure virtual function? We want programmers to implement `PossibleSolutions()` for every error that is a part of the hierarchy.

## Recapitulation

- Run-time polymorphism is an important feature of OO programming.
- C++ achieves run-time polymorphism using virtual functions.
- Run-time polymorphism adds overhead to the run-time system. Thus, it is not made a default. We have run-time polymorphism only when a function is defined as virtual.
- Run-time polymorphism is different from compile-time polymorphism.
- In the case of a normal function being overloaded by the derived class, a base class pointer will always execute the function defined in the base class irrespective of where it is pointing to.
- The pointer, if pointing to a derived class object, executes a derived class function; otherwise, it executes the base class function.
- When a base class pointer is made to point to a derived class object, it can access only the base class subobject buried within the derived class object.
- Whenever a function is defined as virtual, a special pointer is embedded in every object. This pointer points to a table consisting of pointers to virtual functions that the object is capable of invoking.
- Virtual functions are normally linked at run-time.
- The compiler statically binds the virtual function when it can decide the call at compile time.
- Default arguments to virtual functions refer to the pointer type and not the actual function called. Virtual functions are very useful in flexible OO programming.
- Pure virtual functions are virtual functions with `= 0` in the place of the body in the class definition.
- A class with a pure virtual function becomes an abstract class.

## Keywords

**Access method** — This refers to a function written to return the value of a private variable of a class. When we need to provide read-level access of private variables to objects, access methods are used.

**Base class subobject** — In C++ object model, when a class is derived into another, the base class object is embedded within the derived class. This embedded base class object is known as the base class subobject in the derived object.

**Compile-time polymorphism** — Polymorphism achieved using operator overloading and function overloading is known as compile-time polymorphism.

**Dynamic binding** — Linking the function at run-time is known as dynamic binding. Virtual functions are dynamically bound. However, it is possible for the compiler to statically bind the static invocations of virtual functions and also in the case where it is possible to decide at compile time. In such cases, the virtual functions are also statically bound.

**Polymorphism** — The ability of an object to behave differently in different contexts given the same message is known as polymorphism.

**Pure virtual function** — A virtual function with `= 0` in place of the body in the class. It may not have a body; it is also possible to have the body of a pure virtual function defined outside the class.

**RTTI** — Run-time type information is a mechanism to decide the type of the object at run-time.

**Run-time polymorphism** — Polymorphism achieved using virtual functions is known as run-time polymorphism.

**Static binding** — Linking a function during linking phase is known as static binding. Normal functions are statically bound.

**Static invocation of virtual function** — When a virtual function is invoked using a pointer directly, the virtual function is dynamically invoked. It is possible to call a virtual function using an object of the class or using a scope resolution operator. In such a case, the virtual function is statically linked. This is known as static invocation of the virtual function.

**Virtual function** — A function defined with the keyword `virtual` in the base class is known as a virtual function. The compiler will decide the exact class pointed to by the base class pointer and call the respective function of that class if the function is defined as virtual.

**Virtual table** — This is a table consisting of pointers to all virtual functions of the class. Every class with at least one virtual function will have one copy of the virtual table.

## Exercises

### Multiple Choice Questions

1. What does the following syntax show? `virtual void show() = 0;`
   (a) Member function
   (b) Friend function
   (c) Virtual function
   (d) Pure virtual function

2. The two different types of polymorphism are ______.
   (a) compile time and run-time
   (b) compile time and link time
   (c) compile time and load time
   (d) load time and link time

3. When a programmer does not want a class to be instantiated, it can be achieved by ______.
   (a) defining a member function inside that class
   (b) defining a friend function inside that class
   (c) defining a virtual function inside that class
   (d) defining a pure virtual function inside that class

4. When we write a pure virtual function in any class, ________.
   (a) the class becomes an abstract class
   (b) the class cannot be inherited
   (c) the class becomes a virtual class
   (d) the class becomes a pure virtual base class

5. Pure virtual functions can be invoked statically like normal virtual functions only if the function is defined ________.
   (a) outside the class with empty body
   (b) inside the class with empty body
   (c) outside the class with some body
   (d) inside the class with some body

6. Every class with at least one virtual function ________.
   (a) has multiple copies of virtual functions
   (b) has single copy of the virtual table
   (c) has multiple copies of virtual table
   (d) None of the above

7. The ________ is used to get the address of an object.
   (a) address operator
   (b) address function
   (c) address-of operator
   (d) address-of function

8. What should be used to execute a derived class function using a pointer to base class pointing to a derived class object?
   (a) this pointer should be used
   (b) Virtual function should be used
   (c) Virtual pointer should be used
   (d) None of the above

9. ________ cannot help in achieving run-time polymorphism.
   (a) Normal objects
   (b) Pointers to objects
   (c) Virtual functions
   (d) All of the above

10. The ________ manages the pointer to point to the respective subobject in case two or more classes inherit into a single derived class.
    (a) compiler
    (b) linker
    (c) loader
    (d) programmer

### Conceptual Exercises

1. What is polymorphism? What is the difference between compile-time and run-time polymorphism?
2. What is the importance of `this` pointer in the call to the function using base class pointer?
3. Consider base class B and derived class D. Assume pB is a pointer to base class and pD is a pointer to derived class. Differentiate between these two pointers in terms of accessing the derived class object.
4. What is a subobject concept? What is its importance in the case of a base class pointer accessing a derived class object?
5. Why is a non-virtual member function of a base class always called even when the base class pointer is pointing to the derived class object?
6. What is the difference between a normal member function and a virtual function?
7. Explain static binding. How do virtual functions enable dynamic binding?
8. What is the problem of default arguments of the virtual function? How can that be solved?
9. What is the requirement of virtual functions in OO programming?
10. Why virtual constructors are not possible but a virtual destructor is a good idea?
11. Differentiate between virtual functions and pure virtual functions.
12. What is the need for statically invoking pure virtual or virtual functions?

### Practical Exercises

1. Define the `Time` class described in Chapter 9. Inherit Indian Standard Time (IST) and Greenwich Meridian Time (GMT) from it. Write routines that convert from one type of time to another (IST and GMT).
2. Define a class `Stack`. Inherit it into `VariableStack`. Now, inherit this class into `SystemVariableStack` and `UserVariableStack`. Provide constructors and destructors for all the classes.
3. Define a class `Student`. Inherit it into engineering, arts, commerce, and science students. Inherit engineering student into computer science, electronics and communication, and information technology students. Provide constructors for all the classes.
4. For the `Student` class given in Exercise 3, write a program to use a pointer to the `Student` class to access a record of the computer science student. It can be seen that the part defined in computer science is not accessible. Then, define a pointer to computer science student. Now, it can be seen that the part is accessible. Cast the original pointer-to-
