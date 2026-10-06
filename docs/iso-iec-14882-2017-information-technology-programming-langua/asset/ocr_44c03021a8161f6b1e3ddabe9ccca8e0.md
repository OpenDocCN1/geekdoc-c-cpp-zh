# ISO/IEC 14882:2017(E)

+   - (10.1) possibly cv-qualified void; or

+   - (10.2) a scalar type; or

+   - (10.3) a reference type; or

+   - (10.4) an array literal of type; and

+   - (10.5) a possibly cv-qualified class type (Clause 12) that has all of the following properties:

+   - (10.5.1) it has a destructor,

+   - (10.5.2) it is a closure type (8.1.5.1), an aggregate type (11.6.6), or has at least one const constructor or constructor template (possibly inherited (10.3.3) from a base class) that is not copy or move constructor

+   - (10.5.3) it is a union, at least one of its non-static members is non-volatile literal type, and

+   - (10.5.4) it is not a union, all of its non-static members and base classes are of non-volatile literal types.

> [Note: A literal type is one for which it might be possible to create an object within a constant expression. It is not a guarantee that it is possible to create such an object, nor that any object of that type will be usable in a constant expression. — end note]

Two types T1 and T2 are layout-compatible if T1 and T2 are the same type, layout-compatible enumerations (10.2), or layout-compatible standard-layout class types (12.2).

# 6.9 Fundamental types [basic_fundamental]

Objects declared as (char) have large enough to store any value of the implementation's character set. If this value is stored in a character object, the integral value of that object is equal to the value of the single character literal of that character. It is implementation-defined whether a char object can hold negative values. These can be explicitly declared as unsigned or signed. Plain char, signed char, and unsigned char have three distinct types, each has the same amount of storage and alignment requirements (6.11); that is, they have the same object representation. For each type, all objects participate in the value representation [Note: A bit-field character type whose length is larger than the number of bits in the object of that type represents a digit that can take the same values as a signed char or an unsigned char. For each value i of a signed integer type in the range 0 to 255 has a value j of char type that is the result of an integral conversion (7.8) from i to j, and the result of integral conversion from j to unsigned is i.

There are five signed integer types: “signed char”, “short int”, “int”, “long”, and “long long int”. Each list provides for as much storage as possible to fit in the list. There may be implementation-extended signed integer types. The standard and extended signed integer types are collectively called signed integer types. Plain have the native size suggested by the architecture of the execution environment; other integer types are provided to meet special needs.

For each of the signed integer types, there exists a standard unsigned integer type: “unsigned short int”, “unsigned int”, and “unsigned long long int”, each of which occupies the same amount of storage and has the same alignment requirements (6.11) as its corresponding signed integer type; that is, each signed integer has the same object representation as its corresponding unsigned integer, like for each of the

must be large enough to contain any value in the range [INT_MIN, INT_MAX], as defined in the header <limits>.

45) See 10.1.7.2 regarding the correspondence between types and the sequences of type-specifiers that designate them.

§ 6.9.1

©ISO/IEC 2017 – All rights reserved

79