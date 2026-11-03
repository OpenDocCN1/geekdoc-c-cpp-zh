+   18.1 Introduction
+   18.2 Using the Overloaded Operators of Standard Library Class string
+   18.3 Fundamentals of Operator Overloading
+   18.4 Overloading Binary Operators
+   18.5 Overloading the Binary Stream Insertion and Stream Extraction Operators
+   18.6 Overloading Unary Operators
+   18.7 Overloading the Unary Prefix and Postfix ++ and -- Operators
+   18.8 Case Study: A Date Class
+   18.9 Dynamic Memory Management
+   18.10 Case Study: Array Class
+   18.10.1 Using the Array Class
+   18.10.2 Array Class Definition
+   18.11 Operators as Member vs. Non-Member Functions
+   18.12 Converting Between Types
+   18.13 explicit Constructors and Conversion Operators
+   18.14 Overloading the Function Call Operator ()
+   18.15 Wrap-Up

Summary | Self-Review Exercises | Answers to Self-Review Exercises | Exercises

# 18.1 Introduction

This chapter shows how to enable C++'s operators to work with class objects—a process called operator overloading. One example of an overloaded operator built into C++ is <<, which is used both as the stream insertion operator and as the bitwise left-shift operator (which we discussed in Chapter 10). Similarly, >> is also overloaded; it's used both as the stream extraction operator and the bitwise right-shift operator. Both of these operators are overloaded in the C++ Standard Library. You've already been using overloaded operators. The overloads are built into the base C++ language itself. For example, C++ overloads the addition operator (+) and the subtraction operator (-) to perform differently, depending on their context in integer, floating-point and pointer arithmetic with data of fundamental types.

You can overload most operators to be used with class objects—the compiler generates the appropriate code based on the types of the operands. The jobs performed by overloaded operators also can be performed by explicit function calls, but operator notation is often more natural.

Our examples start by demonstrating the C++ Standard Library's class string, which has lots of overloaded operators. This enables you to see overloaded operators in use before implementing your own overloaded operators. Next, we create a PhoneNumber class that enables us to use overloaded operators << and >> to conveniently output and input fully formatted, 10-digit phone numbers. We then present a Date class that overloads the prefix and postfix increment (++) operators to add one day to the value of a Date. The class also overloads the += operator to allow a program to increment a Date by the number of days specified on the right side of the operator.