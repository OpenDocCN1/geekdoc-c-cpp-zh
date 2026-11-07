![](bbox=[0.0, 0.126, 0.093, 0.3])

+   - **10.1** Introduction
+   - **10.2** Using the Overloaded Operators of Standard Library Class `string`
+   - **10.3** Fundamentals of Operator Overloading
+   - **10.4** Overloading Binary Operators
+   - **10.5** Overloading the Binary Stream Insertion and Stream Extraction Operators
+   - **10.6** Overloading Unary Operators
+   - **10.7** Overloading the Unary Prefix and Postfix `++` and `--` Operators
+   - **10.8** Case Study: A Date Class
+   - **10.9** Dynamic Memory Management
+   - **10.10** Case Study: Array Class
+     - 10.10.1 Using the Array Class
+     - 10.10.2 Array Class Definition
+   - **10.11** Operators as Member vs. Non-Member Functions
+   - **10.12** Converting Between Types
+   - **10.13** `explicit` Constructors and Conversion Operators
+   - **10.14** Overloading the Function Call Operator `()`
+   - **10.15** Wrap-Up
+   
+   *Summary | Self-Review Exercises | Answers to Self-Review Exercises | Exercises*

# 10.1 Introduction

This chapter shows how to enable C++’s operators to work with class objects—a process called **operator overloading**. One example of an overloaded operator built into C++ is `<<`, which is used both as the stream insertion operator and as the bitwise left-shift operator (which is discussed in Chapter 22). Similarly, `>>` also is overloaded; it’s used both as the stream extraction operator and the bitwise right-shift operator. Both of these operators are overloaded in the C++ Standard Library. You’ve been using overloaded operators since early in the book. The overloads are built into the base C++ language itself. For example, C++ overloads the addition operator (`+`) and the subtraction operator (`-`) to perform differently, depending on their context in integer, floating-point and pointer arithmetic with data of fundamental types.

You can overload *most* operators to be used with class objects—the compiler generates the appropriate code based on the *types* of the operands. The jobs performed by overloaded operators also can be performed by explicit function calls, but operator notation is often more natural.

Our examples start by demonstrating the C++ Standard Library’s class `string`, which has lots of overloaded operators. This enables you to see overloaded operators in use before implementing your own overloaded operators. Next, we create a `PhoneNumber` class that enables us to use overloaded operators `<<` and `>>` to conveniently output and input fully formatted, 10-digit phone numbers. We then present a `Date` class that overloads the prefix and postfix increment (`++`) operators to add one day to the value of a `Date`. The class also overloads the `+=` operator to allow a program to increment a `Date` by the number of days specified on the right side of the operator.

Next, we present a capstone case study—an `Array` class that uses overloaded operators and other capabilities to solve various problems with pointer-based arrays. This is one of the most important case studies in the book. Many of our students have indicated that the `Array` case study is their “light bulb moment” in truly understanding what classes and object technology are all about. As part of this class, we’ll overload stream insertion, stream extraction, assignment, equality, relational and subscript operators. Once you master this