# Outline

+   - 11.1 Introduction
+   - 11.2 Fundamentals of Operator Overloading
+   - 11.3 Restrictions on Operator Overloading
+   - 11.4 Operator Functions as Class Members vs. Global Functions
+   - 11.5 Overloading Stream Insertion and Stream Extraction Operators
+   - 11.6 Overloading Unary Operators
+   - 11.7 Overloading Binary Operators
+   - 11.8 Dynamic Memory Management
+   - 11.9 Case Study: Array Class
+   - 11.10 Converting between Types
+   - 11.11 Building a String Class
+   - 11.12 Overloading ++ and --
+   - 11.13 Case Study: A Date Class
+   - 11.14 Standard Library Class string
+   - 11.15 explicit Constructors
+   - 11.16 Proxy Classes
+   - 11.17 Wrap-Up

Summary | Terminology | Self-Review Exercises | Answers to Self-Review Exercises | Exercises

# 11.1 Introduction

Chapters 9–10 introduced the basics of C++ classes. Services were obtained from objects by sending messages (in the form of member-function calls) to the objects. This function call notation is cumbersome for certain kinds of classes (such as mathematical classes). Also, many common manipulations are performed with operators (e.g., input and output). We can use C++'s rich set of built-in operators to specify common object manipulations. This chapter shows how to enable C++'s operators to work with objects—a process called operator overloading.

One example of an overloaded operator built into C++ is <<, which is used both as the stream insertion operator and as the bitwise left-shift operator (which is discussed in Chapter 21, Bits, Characters, Strings and structs). Similarly, >> is also overloaded; it's used both as the stream extraction operator and as the bitwise right-shift operator. Both of these operators are overloaded in the C++ Standard Library.

Although operator overloading sounds like an exotic capability, most programmers implicitly use overloaded operators. For example, the C++ language overloads the addition operator (+) and the subtraction operator (-). These operators perform differently, depending on their context in integer, floating-point and pointer arithmetic.

C++ enables you to overload most operators to be sensitive to the context in which they're used—the compiler generates the appropriate code based on the context (in particular, the types of the operands). Some operators are overloaded frequently, especially the assignment, relational and various arithmetic operators such as + and -. The jobs performed by overloaded operators can also be performed by explicit function calls, but operator notation is often clearer and more familiar to programmers.

We discuss when to, and when not to, use operator overloading. We create classes PhoneNumber, Array and Date to demonstrate how to overload operators, including the stream insertion, stream extraction, assignment, equality, relational, subscript, logical negation and increment operators. We demonstrate C++'s Standard Library class string, which provides many overloaded operators. In the exercises, we ask you to implement several classes with overloaded operators. The exercises also use classes Complex (for complex numbers) and HugeInt (for integers larger than a computer can represent with type long) to demonstrate overloaded arithmetic operators + and -, and ask you to enhance those