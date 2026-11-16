# Abstract Data Types

# Fundamental Data Types

A data type provides a description of its variables that tells the computer such things as:

+   - how much memory to allocate for a variable
+   - how to interpret the data in that memory
+   - what range of values can be assigned to a variable
+   - what operations are permissible on that data

We do not have to write a description for the `int` or `float` data type. The author of the compiler did that for us and built it into the compiler. Data types that are built in to a compiler in this way are known as *fundamental data types*.

# Abstract Data Types

Some programming languages have features that allow us to effectively extend the language by adding our own data types. A programmer-defined data type is called an *abstract-data type* (ADT) to distinguish it from a fundamental data type.

The term abstract refers to the way in which a programmer abstracts some concepts from a mass of programming detail and unifies these concepts to create a new data type.

# ADT's in C++

In C++ we can implement our own abstract data types by declaring C++ classes and we can operate on them as if they had been built into the C++ language. This language feature of C++ allows programmers to become, in effect, language designers.

Being able to design and implement our own data types gives us lots of power that we can use to cope with programming large, complicated applications.