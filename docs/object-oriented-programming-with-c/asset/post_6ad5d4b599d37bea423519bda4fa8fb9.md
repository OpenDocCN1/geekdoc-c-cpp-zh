
## Review Questions

1.1 What do you think are the major issues facing the software industry today?

1.2 Briefly discuss the software evolution during the period 1950 - 1990.

1.3 What is procedure-oriented programming? What are its main characteristics?

1.4 Discuss an approach to the development of procedure-oriented programs.

1.5 Describe how data are shared by functions in a procedure-oriented program.

1.6 What is object-oriented programming? How is it different from the procedure-oriented programming?

1.7 How are data and functions organized in an object-oriented program?

1.8 What are the unique advantages of an object-oriented programming paradigm?

1.9 Distinguish between the following terms:

(a) Objects and classes

(b) Data abstraction and data encapsulation

(c) Inheritance and polymorphism

(d) Dynamic binding and message passing

1.10 What kinds of things can become objects in OOP?

1.11 Describe inheritance as applied to OOP.

1.12 What do you mean by dynamic binding? How is it useful in OOP?

1.13 How does object-oriented approach differ from object-based approach?

1.14 List a few areas of application of OOP technology.

1.15 State whether the following statements are TRUE or FALSE.

(a) In procedure-oriented programming, all data are shared by all functions.

(b) The main emphasis of procedure-oriented programming is on algorithms rather than on data.

(c) One of the striking features of object-oriented programming is the division of programs into objects that represent real-world entities.

(d) Wrapping up of data of different types into a single unit is known as encapsulation.

(e) One problem with OOP is that once a class is created it can never be changed.

(f) Inheritance means the ability to reuse the data values of one object by another object.

(g) Polymorphism is extensively used in implementing inheritance.

(h) Object-oriented programs are executed much faster than conventional programs.

(i) Object-oriented systems can scale up better from small to large.

(j) Object-oriented approach cannot be used to create databases.

## Beginning with C++

The most important facilities that C++ adds on to C are classes, inheritance, function overloading, and operator overloading. These features enable creation of abstract data types, inherit properties from existing data types and support polymorphism, thereby making C++ a truly object-oriented language.

The object-oriented features in C++ allow programmers to build large programs with clarity, extensibility and ease of maintenance, incorporating the spirit and efficiency of C. The addition of new features has transformed C from a language that currently facilitates top-down, structured design, to one that provides bottom-up, object-oriented design.

## 2.2 Applications of C++

C++ is a versatile language for handling very large programs. It is suitable for virtually any programming task including development of editors, compilers, databases, communication systems and any complex real-life application systems.

- Since C++ allows us to create hierarchy-related objects, we can build special object-oriented libraries which can be used later by many programmers.
- While C++ is able to map the real-world problem properly, the C part of C++ gives the language the ability to get close to the machine-level details.
- C++ programs are easily maintainable and expandable. When a new feature needs to be implemented, it is very easy to add to the existing structure of an object.
- It is expected that C++ will replace C as a general-purpose language in the near future.

## A Simple C++ Program

The double slash comment is basically a single line comment.
Multiline comments can be written as follows:

```cpp
// This is an example of
// C++ program to illustrate
// Some of its features
```

The C comment symbols /*, */ are still valid and are more suitable for multiline comments. The following comment is allowed:

```cpp
/* This is an example of
   C++ program to illustrate
   some of its features
*/
```

We can use either or both styles in our programs. Since this is a book on C++, we will use only the C++ style. However, remember that we can not insert a // style comment within the text of a program line. For example, the double slash comment cannot be used in the manner as shown below:

```cpp
for(j=0; j<n; /* loops n times */ j++)
```

## Output Operator

The only statement in Program 2.1 is an output statement. The statement

```cpp
cout << "C++ is better than C."
```

causes the string in quotation marks to be displayed on the screen.
This statement introduces two new C++ features, cout and <<. The identifier cout (pronounced as ‘C out’) is a predefined object that represents the standard output stream in C++. Here, the standard output stream represents the screen. It is also possible to redirect the output to other output devices. We shall later discuss streams in detail.

The operator << is called the *insertion* or *put to* operator. It inserts (or sends) the contents of the variable on its right to the object on its left (Fig 2.1).

The object **cout** has a simple interface. If string represents a string variable, then the following statement will display its contents:

```cpp
cout << string;
```

You may recall that the operator << is the bit-wise left-shift operator and it can still be used for this purpose. This is an example of how one operator can be used for different purposes, depending on the context. This concept is known as *operator overloading*, an important aspect of polymorphism. Operator overloading is discussed in detail in Chapter 7.

## Table of Standard Library Header Files

| Header file | Contents and purpose |
|---|---|
| `<utility>` | Contains classes and functions that are used by many standard library header files. |
| `<vector>`, `<list>`, `<deque>`, `<queue>`, `<set>`, `<map>`, `<stack>`, `<bitset>` | The header files contain classes that implement the standard library containers. Containers store data during a program’s execution. We discuss these header files in Chapter 14. |
| `<functional>` | Contains classes and functions used by algorithms of the standard library. |
| `<memory>` | Contains classes and functions used by the standard library to allocate memory to the standard library containers. |
| `<iterator>` | Contains classes for manipulating data in the standard library containers. |
| `<algorithm>` | Contains functions for manipulating data in the standard library containers. |
| `<exception>`, `<stdexcept>` | These header files contain classes that are used for exception handling. |
| `<string>` | Contains the definition of class string from the standard library. Discussed in Chapter 15. |
| `<sstream>` | Contains function prototypes for functions that perform input from strings in memory and output to strings in memory. |
| `<locale>` | Contains classes and functions normally used by stream processing to process data in the natural form for different languages (e.g., monetary formats, sorting strings, character presentation, etc.). |
| `<limits>` | Contains a class for defining the numerical data type limits on each computer platform. |
| `<typeinfo>` | Contains classes for run-time type identification (determining data types at execution time). |

