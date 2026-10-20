# 21.1 Introduction

You’ve used existing generic methods and classes in Chapters 7 and 20. In this chapter, you’ll learn how to write your own. You’ll also learn the relationships between generics and other Java features, such as overloading and inheritance.

It would be nice if we could write a single sort method to sort the elements in an Integer array, a String array or an array of any type that supports ordering (i.e., its elements can be compared). It would also be nice if we could write a single Stack class that could be used as a Stack of integers, a Stack of floating-point numbers, a Stack of Strings or a Stack of any other type. It would be even nicer if we could detect type mismatches at compile time—known as compile-time type safety. For example, if a Stack stores only integers, attempting to push a String onto that Stack should issue a compile-time error.

This chapter discusses generics, which provide the means to create the general models mentioned above. Generic methods enable you to specify, with a single method declaration, a set of related methods. Generic classes (and interfaces) enable you to specify, with a single class (or interface) declaration, a set of related types, respectively. Generics also provide compile-time type safety that allows you to catch invalid types at compile time.

We might write a generic method for sorting an array of objects, then invoke the generic method with Integer arrays, Double arrays, String arrays and so on, to sort the array elements. The compiler could perform type checking to ensure that the array passed to the sorting method contains the same type elements. We might write a single generic Stack class that manipulates a stack of objects, then instantiate Stack objects for a stack of Integers, a stack of Doubles, a stack of Strings and so on. The compiler could perform type checking to ensure that the Stack stores elements of the same type.

> Software Engineering Observation 21.1
> Generic methods and classes are among Java’s most powerful capabilities for software reuse with compile-time type safety.

# 21.2 Motivation for Generic Methods

Overloaded methods are often used to perform similar operations on different types of data. To motivate generic methods, let’s begin with an example (Fig. 21.1) containing overloaded printArray methods (lines 21–28, 31–38 and 41–48) that print the String representations of the elements of an Integer array, a Double array and a Character array, respectively. We could have used arrays of primitive types int, double and char. We’re

+   21.1 Introduction
+   21.2 Motivation for Generic Methods
+   21.3 Generic Methods: Implementation and Compile-Time Translation
+   21.4 Additional Compile-Time Translation Issues: Methods That Use a Type Parameter as the Return Type
+   21.5 Overloading Generic Methods
+   21.6 Generic Classes
+   21.7 Raw Types
+   21.8 Wildcards in Methods That Accept Type Parameters
+   21.9 Generics and Inheritance: Notes
+   21.10 Wrap-Up

Summary | Self-Review Exercises | Answers to Self-Review Exercises | Exercises