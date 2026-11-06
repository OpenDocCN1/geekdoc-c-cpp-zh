
## 21 Bits, Characters, C Strings and structs

> *The same old charitable lie*
> *Repeated as the years scoot by*
> *Perpetually makes a bit—*
> *“You really haven’t changed a bit!”*
> —*Margaret Fishback*

> *The chief defect of Henry King*
> *Was chewing little bits of string.*
> —*Hilaire Belloc*

> *Vigorous writing is concise. A*
> *sentence should contain no*
> *unnecessary words, a paragraph*
> *no unnecessary sentences.*
> —*William Strunk, Jr.*

### Objectives

In this chapter you’ll learn:

- To create and use **structs**.
- To pass structs by value and by reference.
- To use **typedef** to create aliases for previously defined data types and structs.
- To manipulate data with the bitwise operators and to create bit fields for storing data compactly.
- To use the functions of the character-handling library `<cctype>`.
- To use the string-conversion functions of the general-utilities library `<cstdlib>`.
- To use the string-processing functions of the string-handling library `<cstring>`.

![](img/023f159fdd47d944d48e08843cea732d_888_0.png)

### Outline

- 21.1 Introduction
- 21.2 Structure Definitions
- 21.3 Initializing Structures
- 21.4 Using Structures with Functions
- 21.5 typedef
- 21.6 Example: Card Shuffling and Dealing Simulation
- 21.7 Bitwise Operators
- 21.8 Bit Fields
- 21.9 Character-Handling Library
- 21.10 Pointer-Based String Manipulation Functions
- 21.11 Pointer-Based String-Conversion Functions
- 21.12 Search Functions of the Pointer-Based String-Handling Library
- 21.13 Memory Functions of the Pointer-Based String-Handling Library
- 21.14 Wrap-Up

*Summary* | *Terminology* | *Self-Review Exercises* | *Answers to Self-Review Exercises* | *Exercises* | *Special Section: Advanced String-Manipulation Exercises* | *Challenging String-Manipulation Projects*

### 21.1 Introduction

We now discuss structures and the manipulation of bits, characters and C-style strings. Many of the techniques we present here are included for the benefit of those who will work with legacy C and C++ code.

C++'s designers evolved structures into the notion of a class. Like a class, C++ structures may contain access specifiers, member functions, constructors and destructors. In fact, the only differences between structures and classes in C++ is that structure members default to public access and class members default to private access when no access specifiers are used, and that structures default to public inheritance, whereas classes default to private inheritance. Classes have been covered thoroughly in the book, so there is really no need for us to discuss structures in detail. Our presentation of structures in this chapter focuses on their use in C, where structures contain only public data members. This use of structures is typical of the legacy C code and early C++ code you'll see in industry.

We discuss how to declare, initialize and pass structures to functions. Then, we present a high-performance card shuffling and dealing simulation in which we use structure objects and C-style strings to represent the cards. We discuss the bitwise operators that allow you to access and manipulate the individual bits in bytes of data. We also present bitfields—special structures that can be used to specify the exact number of bits a variable occupies in memory. These bit manipulation techniques are common in C and C++ programs that interact directly with hardware devices that have limited memory. The chapter finishes with examples of many character and C string manipulation functions—some of which are designed to process blocks of memory as arrays of bytes. The detailed C string treatment in this chapter is mostly for reasons of legacy code support and because there are still remnants of C string use in C++, such as command-line arguments (Appendix F). New development should use C++ string objects rather than C strings.

### 21.2 Structure Definitions

Structures are aggregate data types—that is, they can be built using elements of several types including other structs. Consider the following structure definition:

```
struct Card
{
   string face;
   string suit;
}; // end struct Card
```

Keyword **struct** introduces the definition for structure Card. The identifier Card is the structure name and is used in C++ to declare variables of the structure type (in C, the type name of the preceding structure is struct Card). In this example, the structure type is Card. Data (and possibly functions—just as with classes) declared within the braces of the structure definition are the structure's members. Members of the same structure must have unique names, but two different structures may contain members of the same name without conflict. Each structure definition must end with a semicolon.

> **Common Programming Error 21.1**
>
> *Forgetting the semicolon that terminates a structure definition is a syntax error.*

Card’s definition contains two string members—face and suit. Structure members can be variables of the fundamental data types (e.g., int, double, etc.) or aggregates, such as arrays, other structures and classes. Data members in a single structure definition can be of many data types. For example, an Employee structure might contain character-string members for the first and last names, an int member for the employee’s age, a char member containing 'M' or 'F' for the employee’s gender, a double member for the employee’s hourly salary and so on.

A structure cannot contain an instance of itself. For example, a structure variable Card cannot be declared in the definition for structure Card. A pointer to a Card structure, however, can be included. A structure containing a member that is a pointer to the same structure type is referred to as a self-referential structure. We used a similar construct—self-referential classes—in Chapter 20, Data Structures, to build various kinds of linked data structures.

The Card structure definition does not reserve any space in memory; rather, it creates a new data type that is used to declare structure variables. Structure variables are declared like variables of other types. The following declarations

```
Card oneCard;
Card deck[ 52 ];
Card *cardPtr;
```

declare oneCard to be a structure variable of type Card, deck to be an array with 52 elements of type Card and cardPtr to be a pointer to a Card structure. Variables of a given structure type can also be declared by placing a comma-separated list of the variable names between the closing brace of the structure definition and the semicolon that ends the structure definition. For example, the preceding declarations could have been incorporated into the Card structure definition as follows:

```
struct Card
{
   string face;
   string suit;
} oneCard, deck[ 52 ], *cardPtr;
```

The structure name is optional. If a structure definition does not contain a structure name, variables of the structure type may be declared only between the closing right brace of the structure definition and the semicolon that terminates the structure definition.

> **Software Engineering Observation 21.1**
>
> *Provide a structure name when creating a structure type. The structure name is required for declaring new variables of the structure type later in the program, declaring parameters of the structure type and, if the structure is being used like a C++ class, specifying the name of the constructor and destructor.*

The only valid built-in operations that may be performed on structure objects are assigning one structure object to another of the same type, taking the address (`&`) of a structure object, accessing the members of a structure object (in the same manner as members of a class are accessed) and using the `sizeof` operator to determine the size of a structure. As with classes, most operators can be overloaded to work with objects of a structure type.

Structure members are not necessarily stored in consecutive bytes of memory. Sometimes there are “holes” in a structure, because some computers store specific data types only on certain memory boundaries for performance reasons, such as half-word, word or double-word boundaries. A word is a standard memory unit used to store data in a computer—usually two bytes or four bytes and typically four bytes on today’s popular 32-bit systems. Consider the following structure definition in which structure objects `sample1` and `sample2` of type `Example` are declared:

```
    struct Example
    {
       char c;
       int i;
    } sample1, sample2;
```

A computer with two-byte words might require that each of the members of `Example` be aligned on a word boundary (i.e., at the beginning of a word—this is machine dependent). Figure 21.1 shows a sample storage alignment for an object of type `Example` that has been assigned the character `'a'` and the integer `97` (the bit representations of the values are shown). If the members are stored beginning at word boundaries, there is a one-byte hole (byte 1 in the figure) in the storage for objects of type `Example`. The value in the one-byte hole is undefined. If the member values of `sample1` and `sample2` are in fact equal, the structure objects are not necessarily equal, because the undefined one-byte holes are not likely to contain identical values.

![](img/023f159fdd47d944d48e08843cea732d_891_0.png)

**Fig. 21.1** | Possible storage alignment for a variable of type `Example`, showing an undefined area in memory.

> **Common Programming Error 21.2**
>
> *Comparing variables of structure types is a compilation error.*
