# Chapter 19 Bits, Characters, C Strings and structs

+   19.1 Introduction
+   19.2 Structure Definitions
+   19.3 Initializing Structures
+   19.4 Using Structures with Functions
+   19.5 typedef
+   19.6 Example: High-Performance Card Shuffling and Dealing Simulation
+   19.7 Bitwise Operators
+   19.8 Bit Fields
+   19.9 Character-Handling Library
+   19.10 Pointer-Based String-Conversion Functions
+   19.11 Search Functions of the Pointer-Based String-Handling Library
+   19.12 Memory Functions of the Pointer-Based String-Handling Library
+   19.13 Wrap-Up

# 19.1 Introduction

We now discuss structures and the manipulation of bits, characters and C-style strings. Many of the techniques we present here are included for the benefit of the C++ programmer who will work with legacy C and C++ code.

The designers of C++ evolved structures into the notion of a class. Like a class, C++ structures may contain access specifiers, member functions, constructors and destructors. In fact, the only differences between structures and classes in C++ is that structure members default to public access and class members default to private access when no access specifiers are used, and that structures default to public inheritance, whereas classes default to private inheritance. Classes have been covered thoroughly in the book, so there is really no need for us to discuss structures in detail. Our presentation of structures in this chapter focuses on their use in C, where structures contain only public data members. This use of structures is typical of the legacy C code and early C++ code you’ll see in industry.

We discuss how to declare structures, initialize structures and pass structures to functions. Then, we present a high-performance card shuffling and dealing simulation in which we use structure objects and C-style strings to represent the cards. We discuss the bitwise operators that allow programmers to access and manipulate the individual bits in bytes of data. We also present bitfields—special structures that can be used to specify the exact number of bits a variable occupies in memory. These bit manipulation techniques are common in C and C++ programs that interact directly with hardware devices that have limited memory. The chapter finishes with examples of many character and C-style string manipulation functions—some of which are designed to process blocks of memory as arrays of bytes.

# 19.2 Structure Definitions

Structures are *aggregate data types*—that is, they can be built using elements of several types including other structs. Consider the following structure definition: