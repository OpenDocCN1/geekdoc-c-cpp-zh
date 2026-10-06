# Overloaded Operators and Friend Access 5

+   Contents
C5.1 Overloaded Operators 415
C5.1.1 Overloading = for Assignment 417
C5.1.2 Overloading + for Concatenation 419
C5.2 Friend Access and Overloading << 421

# Prerequisites

+   Chapter 4 Link-Based Implementations
Chapter 8 Lists
Chapter 9 List Implementations

> C++ provides many operators, as +, -, =, ==, >, and <<, that are defined for primitive data types. For instance, when working with integers, the symbol + represents the addition operation, = is used for the assignment operation, and == is used for equality comparisons. When we define new C++ data types using classes, these symbols do not have a definition that how to add or compare two objects of the class. This C++ Interlude describes the tools that C++ provides for extending the operators so that they can be applied to classes you have created.

![](bbox=[0.233, 0.743, 0.303, 0.803])

# C5.1 Overloaded Operators

The standard arithmetic operations in C++ actually have multiple meanings. The addition operations in the expressions 2 + 3 and 2.0 + 3.0 appear to be the same, they in fact not. Because integers such as 2 and 3 have internal representations that differ from floating-point numbers as 2.0 and 3.0, the algorithm to add two integers must differ from the algorithm to add two floating-point numbers. C++ could use two different symbols to designate integer addition and floating-point addition, but instead it uses only one symbol, +. The actual meaning of the + operator—that is, the type of addition designates—is implied by the data type of its operands. An operator with more than one meaning is overloaded and it is an example of polymorphism.