# Classes

> *Those types are not “abstract”; they are as real as **int** and **float**.*  
> — Doug McIlroy

# 16.1 Introduction

C++ classes are a tool for creating new types that can be used as conveniently as the built-in types. In addition, derived classes (§3.2.4, Chapter 20) and templates (§3.4, Chapter 23) allow the programmer to express (hierarchical and parametric) relationships among classes and to take advantage of such relationships.

A type is a concrete representation of a concept (an idea, a notion, etc.). For example, the C++ built-in type **float** with its operations **+**, **−**, **∗**, etc., provides a concrete approximation of the mathematical concept of a real number. A class is a user-defined type. We design a new type to provide a definition of a concept that has no direct counterpart among the built-in types. For example, we might provide a type **Trunk_line** in a program dealing with telephony, a type **Explosion** for a video game, or a type **list<Paragraph>** for a text-processing program. A program that provides types that closely match the concepts of the application tends to be easier to understand, easier to reason about, and easier to modify than a program that does not. A well-chosen set of user-defined types also makes a program more concise. In addition, it makes many sorts of code analysis feasible. In particular, it enables the compiler to detect illegal uses of objects that would otherwise be found only through exhaustive testing.

The fundamental idea in defining a new type is to separate the incidental details of the implementation (e.g., the layout of the data used to store an object of the type) from the properties essential to the correct use of it (e.g., the complete list of functions that can access the data). Such a separation is best expressed by channeling all uses of the data structure and its internal housekeeping routines through a specific interface.

This chapter focuses on relatively simple “concrete” user-defined types that logically don’t differ much from built-in types:

§16.2 *Class Basics* introduces the basic facilities for defining a class and its members.  
§16.3 *Concrete Classes* discusses the design of elegant and efficient concrete classes. The following chapters go into greater detail and presents abstract classes and class hierarchies:

+   - *Chapter 17*  
+   - *Chapter 18*  
+   - *Chapter 19*  
+   - *Chapter 20*  
+   - *Chapter 21*

*Chapter 22 Construction, Cleanup, Copy, and Move* presents the variety of ways to