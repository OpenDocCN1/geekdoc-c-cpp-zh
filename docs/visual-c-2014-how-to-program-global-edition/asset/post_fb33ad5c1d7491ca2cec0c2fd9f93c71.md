
# Chapter 19 Custom Linked Data Structures

b When the right-parenthesis character has not been encountered, read the expression from left to right.
If the current value is a digit, do the following:
- Push its integer value onto the stack (the integer value of a digit character is its value in the computer's character set minus the value of '0' in Unicode).
Otherwise, if the current character is an *operator*,
- Push the top two elements of the stack into variables x and y.
- Calculate *operator* x.
- Push the result of the calculation onto the stack.

c When the right-parenthesis is encountered in the expression, pop the top value of the stack. This is the result of the postfix expression.
[Note: In Part b above (based on the sample expression at the beginning of this exercise), if the operator is '/', the top of the stack is 4 and the next element in the stack is 8, push 4 into x, push 8 into y, evaluate y / x and push the result, 2, back on the stack. This note also applies to operator '-' The arithmetic operations allowed in expression are:

- + addition
- - subtraction
- * multiplication
- / division
- ^ exponentiation
- % modulus

You may want to evaluate the following methods:
a Method EvalPostfixExpression, which evaluates the postfix expression operator op1.
b Method Calculate, which evaluates the expression op1 op2.

19.8 (Level-Order Binary Tree Traversal) The program of Fig. 19.21 introduced recursive methods of traversing a binary tree-- inorder, preorder, and postorder traversals. This exercise presents the level-order traversal of a binary tree, in which the nodes are displayed by level, starting at the root node. Nodes on each level are displayed from left to right. Level order traversal is not a recursive algorithm. It uses a queue object to control the output of the nodes.
The algorithm is as follows:

+ a Insert the root node in the queue.
b While there are nodes left in the queue, do the following:
- Get the next node in the queue.
- Display the node's value.
- If the reference to the left child of the node is not null:
- Insert the left child into the queue.
- If the reference to the right child of the node is not null:
- Insert the right child into the queue.

Modify the program of Fig. 19.21 to use a level-order traversal of a binary tree object. [Note: You will need to use the queue processing methods of Fig. 19.16 in this program]

# Special Section: Building Your Own Compiler

In Exercises 8.31–8.33, we introduced Simpleton Machine Language (SML), and you implemented a Simpleton simulator to execute SMC programs. In Exercises 19.9–19.13, we will build a compiler that converts programs in a high-level programming language to SML. This section "ties" together the programming process. You will write programs in this new high-level language, compile them on the compiler you build and run them on the simulator you built in Exercise 8.32. [Note: Due to the size of the exercises for Exercises 19.29–19.33, we've posted them in a PDF document located at http://www.de1.com/books/CSharpPE6.]

# Generics

# 20

# Objectives

In this chapter you'll:

- Create generic methods that perform identical tasks on arguments of different types.
- Create a generic Stack class that can be used to store objects of a specific type.
- Understand how to overload generic methods with nongeric methods or with other generic methods.
- Understand the kinds of constraints that can be applied to a type parameter.
- Apply multiple constraints to a type parameter.

![](img/57baed2319be0bb1b5f98674846f2711_855_0.png)

# 856 Chapter 20 Generics

| 20.1 Introduction | 20.5 Overloading Generic Methods |
| 20.2 Motivation for Generic Methods | 20.6 Generic Classes |
| 20.3 Generic-Based Implementation | 20.7 Wrap-Up |
| 20.4 Type Constraints | |
| 20.4 Comparable<T> Interface | |
| 20.4 Specifying Type Constraints | |

Summary | Terminology | Self-Review Exercises | Answers to Self-Review Exercises | Exercises

# 20.1 Introduction

Chapter 19 presented data structures that store and manipulate references to objects. Here we continue our multi-chapter data-structures discussion.

# **object-Based Data Structure Disadvantages**

You can store any object in our data structures. One inconvenient aspect of storing object references when retrieving them from a collection. An app normally needs to process specific types of objects. As a result, the object references obtained need to be *downcast* to an appropriate type to allow the process to correct objects. In addition, data values (e.g., int and double) must be *boxed* to be manipulated with object references, which increases the overhead of processing data. Most importantly, processing all data as type limits the C# compiler's ability to perform type checking.

# **Compile-Time Type Safety**

Though we can easily create data structures that manipulate any type of data as objects (as we did in Chapter 19), it would be nice if we could detect mismatches at compile time—this is known as [compile-time type safety](https://example.com). For example, if a Stack should store only int values, a Sort method should be able to compare elements that are guaranteed to have the same type. If we create type-specific versions of class Stack and method Sort, the C# compiler would certainly ensure compile-time type safety. However, this would require that we create many copies of the basic code.

# Generics

This chapter discusses generics, which provide the means to generate the generic models above. [Generic methods](https://example.com) enable you to specify, with a *single method declaration*, a set of related methods. [Generic classes](https://example.com) enable you to specify, with a single class declaration, a set of related classes. Similarly, [generic interfaces](https://example.com) enable you to specify, with a single *interface declaration*, a set of related interfaces. Generics provide compile-time type safety.[Note: You can also implement generics and [delegates](https://example.com). For far in this book, we've used the generic types *List* (Chapter 9) and *Dictionary* (Chapter 17).

We can write a generic method for sorting an array, with an int array, a double array, a string array and so on, to sort each different type of array. The compiler performs [type checking](https://example.com) to ensure that the array passed to the sorting method contains only elements of the correct type. We can write a single

# 20.2 Motivation for Generic Methods 857

generic Stack class, then instantiate Stack objects for a stack of ints, a stack of doubles,
a stack of strings and so on. The compiler performs type checking to ensure the Stack
stores only elements of the correct type.

This chapter presents examples of generic methods and generic classes. Chapter 21,
Generic Collections; Functional Programming with LINQ/PLINQ, discusses the .NET
Framework's generic collections. A collection is a data structure that maintains the
group of related objects or values. The .NET Framework collection uses generics to
allow you to specify the exact types of object that a particular collection will store.

# 20.2 Motivation for Generic Methods

Overloaded methods are often used to perform similar operations on different types ofndata. To understand the motivation for generic methods, let's begin with an example
(Fig. 20.1) that contains three overloaded DisplayArray methods (lines 23–31, lines
34–42 and lines 45–53). These methods display the elements of an int array, a double
array and a char array, respectively. Soon, we'll implement this program more concisely
and using a single generic method.

```
 // Fig. 20.1: OverloadedMethods.cs
// Using overloaded methods to display arrays of different types.
using System;
class OverloadedMethods
{
    static void Main(string[] args)
    {
        // create arrays of int, double and char
        int[] intArray = {1, 2, 3, 4, 5, 6};
        double[] doubleArray = {1.1, 2.2, 3.3, 4.4, 5.5, 6.6, 7.7};
        char[] charArray = {'H', 'E', 'L', 'L', 'O'};

        Console.Write("Array contains: ");
        DisplayArray(intArray); // pass an int array argument
        Console.Write("Array contains: ");
        DisplayArray(doubleArray); // pass a double array argument
        Console.Write("Array contains: ");
        DisplayArray(charArray); // pass a char array argument
    }

    // output array
    private static void DisplayArray(int[] inputArray)
    {
        foreach (var element in inputArray)
        {
            Console.Write($"{element} ");
        }
        Console.WriteLine();
    }
}

```

> Fig. 20.1 | Using overloaded methods to display arrays of different types. (Part I of 2.)
