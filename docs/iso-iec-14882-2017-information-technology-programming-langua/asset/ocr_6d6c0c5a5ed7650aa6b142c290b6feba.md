# ISO/IEC 14882:2017(E)

# 6.9.2 Compound types

[basic.compound]

+   Compound types can be constructed in the following ways:
- arrays of a given type, 11.3.4;
- functions, which have parameters of given type and return void or references to objects of a given type, 11.3.5;
- pointers to void or objects or functions (including static members of classes) of a given type, 11.3.1;
- references to objects of a given type, 11.3.2. There are two types of references:
  - value reference
  - reference reference
- classes containing a sequence of objects (Clause 12), a set of types, enumerations and functions for manipulating these objects (12.2.1), and a set of restrictions on the access to these entities (Clause 14);
- unions, which are capable of containing objects of different types at different times, 12.3;
- enumerations, which are set of constant values. Each distinct enumeration constitutes a different enumerated type, 10.2;
- pointers to non-static members,53 which identify members of a given type within objects of a given class, 11.3.3.

These methods of construction can be applied recursively; restrictions are mentioned in 11.3.1, 11.3.4, 11.3.5. If the number of bytes in an object exceeds the maximum value representation in the type size_t (2.1) it is ill-formed.

The type of pointer to void or a pointer to an object is called an object pointer type. [Note: A pointer does not have a pointer-to-pointer object, because a pointer to object is not an object type - end note]. The type of a pointer that can designate a function is called a function pointer type. A pointer to object is referred to as pointer to class X. [Example: A pointer to object of type X is referred to as "pointer to X", and a pointer to an object is referred to as "pointer to void" - example end]. For pointers to static members, text referring to "pointers" also applies to pointers to members. Pointer to incomplete types are allowed although there are restrictions on what can be done with them (6.11). Every value of pointer type is one of the following:

+   - a pointer to an object or function (the pointer is said to point to the object or function),
- a pointer past the end of an object (8.7), or
- the null pointer (7.11) for that type, or
- an invalid pointer value.

A value of a pointer to or past an object represents the address of the first byte in memory (4.1) occupied by the object54 or the first byte in memory after the end of the storage occupied by the object. [Note: A pointer past the end of an object (8.7) is not considered to point to an unaltered object of the object's type that might exist at address. A value becomes invalid when the storage reaches the end of its storage; see 6.7 - end note]. For pointers in arithmetic (7.8) or comparison (8.10), a pointer past the end of an array is allowed to point to an element of the same type or beyond. The value representation of pointer types is implementation-defined. Pointers to layout-compatible types have the same value representation and alignment requirements (6.11). [Note: Pointers to over-aligned types but their range of valid values is restricted by the extended

> 53 Static class members are objects or functions, and pointers to them are ordinary pointers to objects or functions.
54 For an object that is not within its lifetime, this is the first byte in memory that it will occupy or use to occupy.