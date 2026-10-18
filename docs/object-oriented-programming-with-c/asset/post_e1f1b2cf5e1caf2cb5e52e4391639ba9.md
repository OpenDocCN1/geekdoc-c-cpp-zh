
```cpp
//Destructor code
throw;
}
catch (...)
{
//Exception handling code
}
```

We may incorporate exception handling mechanism in an operator overloaded function definition to handle system generated or user specified exceptions. Recall Program 7.2 in which we had overloaded the + binary operator to compute the sum of two complex numbers. The following code depicts the handling of user-specified exception of adding a zero to the complex number object.

```cpp
class complex
{



public:
class FLAG{}; //Abstract class FLAG


};
complex complex :: operator+ (complex c)
```

- We can place two or more catch blocks together to catch and handle multiple types of exceptions thrown by a try block.
- It is also possible to make a catch statement to catch all types of exceptions using ellipses as its argument.
- We may also restrict a function to throw only a set of specified exceptions by adding a throw specification clause to the function definition.

## Key Terms

**abort()** function | asynchronous exceptions | bugs | **catch** block | **catch(...)** statement | catching mechanism | errors | exception handler | exception handling mechanism | exception specifying | exceptions | logic errors | multiple catch | out-of-range index | overflow | rethrowing exceptions | synchronous exceptions | syntactic errors | **throw** | throw point | **throw** statement | **throw()** | throwing mechanism | **try** block

## Review Questions

- 13.1 What is an exception?
- 13.2 How is an exception handled in C++?
- 13.3 What are the advantages of using exception handling mechanism in a program?
- 13.4 When should a program throw an exception?
- 13.5 When is a **catch(...)** handler used?
- 13.6 Can we throw class types as exceptions? Explain with the help of an example.
- 13.7 What is an exception specification? When is it used?
- 13.8 What should be placed inside a **try** block?
- 13.9 What should be placed inside a **catch** block?
- 13.10 When do we use multiple **catch** handlers?
- 13.11 State what will happen in the following situations:

```cpp
{
    switch(age)
    {
        case 10:
            throw "Child";
        case 20:
            throw "Student";
            break;
        case 30:
            throw "Employee";
            break;
    }
}
}
void operator ++()
{
    age+=10;
}
};
void main()
{
    Person objPerson(10);
    objPerson.getOccupation();
    ++objPerson;
    objPerson.getOccupation();
    ++objPerson;
    objPerson.getOccupation();
}
```

### 13.2 Identify the error in the following program.

```cpp
#include <iostream.h>

void callFunction(int i)
{
    if(i)
        throw 1;
    else
        throw 0;
}
void callFunction(char *n)
{
    try
    {
    if(n)
    throw "StringOK";
    else
    throw "StringError";
    }
    catch(char* name)
    {
    cout << name << " ";
    }
}
void main()
{
    try
    {
    callFunction("testString");
    callFunction(1);
    callFunction(0);
    }
    catch(int i)
    {
    cout << i << " ";
    }
    catch(char *name)
    {
    cout << name << " ";
    }
}
```

### 13.3 Identify the error in the following program.

```cpp
#include <iostream.h>
class Mammal
{
public:
Mammal()
{
}
class Human
{
};
class Student : virtual public Human
{
};
class Employee : virtual public Human
{
};
void getObject()
{
throw Employee();
}
};
void main()
{
Mammal m;
try
{
m.getObject();
}
catch(Mammal::Human&)
{
cout << "Human ";
}
catch(Mammal::Student&)
{
    cout << "Student ";
}
catch(Mammal::Employee&)
{
    cout << "Employee ";
}
catch(...)
{
    cout << "All";
}
}
```

### 13.4 Identify the error in the following program:

```cpp
#include <iostream>
#include <conio.h>
using namespace std;

class Error
{
    int err_code;
public:
    Error(int c)
    {
        err_code = c;
    }
    void err_display(void)
    {
        cout << "\nerror Code: " << err_code << "\n";
    }
};

int main()
{
    try
    {
        cout << "Press any key to throw a test exception..";
        getch();
        throw Error();
    }
    catch(Error e)
    {
        cout << "\nException caught successfully..";
        e.err_display();
    }
    getch();

    return 0;
}
```

### 13.5 Identify errors, if any, in the following statements.

- (a) `catch(int a, float b)`
- (b) `try {throw 100;}`
- (c) `try {fun1()}`
- (d) `throw a, b;`
- (e) `void divide(int a, int b) throw(x, y) {.....}`
- (f) `catch(int x, ..., float y) {.....}`
- (g) `try {throw x/y;}`
- (h) `try {if(!x) throw x;} catch(x) {cout << "x is zero \n";}`

## Programming Exercises

- 13.1 Write a program containing a possible exception. Use a try block to throw it and a catch block to handle it properly.
- 13.2 Write a program that illustrates the application of multiple catch statements.
- 13.3 Write a program which uses catch(…) handler.
- 13.4 Write a program that demonstrates how certain exception types are not allowed to be thrown.
- 13.5 Write a program to demonstrate the concept of rethrowing an exception.
- 13.6 Write a program with the following:
  - (a) A function to read two double type numbers from keyboard.
  - (b) A function to calculate the division of these two numbers.
  - (c) A try block to throw an exception when a wrong type of data is keyed in.
  - (d) A try block to detect and throw an exception if the condition "divide-by-zero" occurs.
  - (e) Appropriate catch block to handle the exceptions thrown.
- 13.7 Write a main program that calls a deeply nested function containing an exception. Incorporate necessary exception handling mechanism.

## Introduction to the Standard Template Library

We have seen how templates can be used to create generic classes and functions that could extend support for generic programming. In order to help the C++ users in generic programming, Alexander Stepanov and Meng Lee of Hewlett-Packard developed a set of general-purpose templatized classes (data structures) and functions (algorithms) that could be used as a standard approach for storing and processing of data. The collection of these generic classes and functions is called the _Standard Template Library (STL)_. The STL has now become a part of the ANSI standard C++ class library.

STL is large and complex and it is difficult to discuss all of its features in this chapter. We therefore present here only the most important features that would enable the readers to begin using the STL effectively. Using STL can save considerable time and effort, and lead to high quality programs. All these benefits are possible because we are basically "reusing" the well-written and well-tested components defined in the STL.

STL components which are now part of the Standard C++ Library are defined in the **namespace std.** We must therefore use the **using namespace** directive

using namespace std;

to inform the compiler that we intend to use the Standard C++ Library. All programs in this chapter use this directive.

### 14.2 **Components of STL**

The STL contains several components. But at its core are three key components. They are:

- containers,
- algorithms, and
- iterators.

These three components work in conjunction with one another to provide support to a variety of programming solutions. The relationship between the three components is shown in [Fig. 14.1](#fig-14-1). *Algorithms* employ *iterators* to perform operations stored in *containers*.

![](img/62b7c32e48e4f960a8dc2825a7119fb2_590_0.png)

**Fig. 14.1** *Relationship between the three STL components*

A *container* is an object that actually stores data. It is a way data is organized in memory. The STL containers are implemented by template classes and therefore can be easily customized to hold different types of data.
