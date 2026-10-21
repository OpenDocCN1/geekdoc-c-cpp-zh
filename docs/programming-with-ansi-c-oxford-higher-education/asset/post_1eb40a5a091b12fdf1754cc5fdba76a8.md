
# Table 2.1 C++ keywords

| asm | do | if | return | typedef |
| auto | double | inline | short | typeid |
| bool | dynamic_cast | int | signed | typename |
| break | else | long | sizeof | union |
| case | enum | mutable | static | unsigned |
| catch | explicit | namespace | static_cast | using |
| char | export | new | struct | virtual |
| class | extern | operator | switch | void |
| const | false | private | template | volatile |
| const_cast | float | protected | this | wchar_t |
| continue | for | public | throw | while |
| default | friend | register | true |  |
| delete | goto | reinterpret_cast | try |  |

The boldface words are ANSI C keywords. Normal typeface words are original C++ keywords (from Stroustrup), and italic words are ANSI C++ additions to earlier C++ keyword set.

## 2.3 DATA TYPES

The C++ data types in C++ can be divided into three categories. The first category represents the data types borrowed directly from C and forms the largest set. The second category represents the data types that were available in C and are also available in C++, but with extended meanings. The third category represents the new data types that have been introduced in C++ and were not available in C.

### 2.3.1 Borrowed from C

The data types void, int, char, float, and double and the modifiers to these data types, namely, signed, unsigned, long, and short, operate in the same way as in C. Moreover, pointers, except for void pointers, and arrays, unless containing data of newly added data types, also operate in the same manner as in C.

### 2.3.2 Borrowed from C with Modifications

Some data types of C included in C++ have been adapted to be compatible with the features and compiler requirements of C++. These data types are structure, union, enumeration, and pointers.

In C++, struct(structure) is extended to be compatible with the data type class. The class data type and the difference between class and struct in C++ are discussed in Chapter 3. The span of union is also extended in C++ and is discussed in detail in Chapter 3.

In C, enum(enumeration) literals are globally visible even if they are defined locally; however, in C++ these are visible only to the class (or structure) in which they are defined.

Pointer definitions in C++ operate just like those in C, with the exception of void pointers and two new types of pointers, the constant pointer and pointer to constant. Pointers in C++ are discussed in detail in Section 2.4.

### 2.3.3 Newly Added Data Types

Some newly added data types in C++ are described in this section. Classes are the central constructs in C++. A class has the capability to represent an entity of the real world in a true sense. Classes are discussed in detail in Chapter 3.

Strings in C++ are much simpler to use than in C. In C, they are treated as character arrays, but C++ has a special string class for defining strings. Strings are used throughout this book and have been discussed in detail in Chapter 15. Strictly speaking, a string is still an outside entity for a C++ program and the <string> file needs to be included to provide operations on strings. There are a few other classes such as queue and vector, which are part of the Standard Template Library (STL). These are covered in Chapter 16.

## Abstract Data Types

One may argue that strings, queues, and stacks are not native or built-in data types but are user-defined. The distinction between a built-in and a user-defined data type, which was clear in C, is quite blurred in C++. Moreover, these data types are given by a standard, and thus, for an end user, they are quite similar to built-in data types. They are sometimes denoted as abstract data types and can only be found in object-based languages.

An interesting new data type added in C++ is bool (Boolean). It can have only two values, true or false, both of which are keywords in C++.

Consider the following program. It tests the input and comes out of the program if the input is zero.

```
//TestBool.cpp
#include <iostream>
using namespace std;
void main()
{
    bool flag;
    flag = true;
    int test;
    while(flag)
    {
        cin >> test;
        if(!test)
            flag = false;
    }
}
```

Notice the use of ‘flag’ as a bool variable. A bool variable can be used where any relational or logical expression is used. Providing a Boolean operation was the additional job assigned

to the integer type variables in C. We can spare integer variables in C++ if our purpose is to test the veracity and nothing else. The use of the bool variable makes this testing easier and also makes the program more readable. It can have either true or false value as shown.

## 2.4 POINTERS

Though pointers are available in C++ also, they have some characteristics that are different from those in C that are discussed in the following sections.

### 2.4.1 Void Pointer

Void pointer is an important type of pointer borrowed from C. One may question the need for void pointers. As a pointer must point to a variable (i.e., it has an address of some variable), the idea of a void pointer (a pointer pointing to nothing) may sound ironic. However, such pointers are useful in C for returning a pointer value of an unknown type. The malloc() function is an example.

> Note The malloc() function can be used for acquiring memory for any data type. This is why it is designed to return a void pointer which the user cast to whatever required. It is also needed to write a generic algorithm that can accept any pointer type by defining the algorithm to accept a void pointer in the argument.

The essence of the void pointer in C++ is better captured by the term pointer to void. A void pointer points to a value that does not have a type (such as int and float). This means that the value pointed to by the void pointer has an undetermined length and undetermined dereferencing properties. The difference between the definitions of void pointers in C and C++ can be brought out by considering the following code segment:

```
int* FirstPointer;
void* SecondPointer;
```

The statement

```
SecondPointer = FirstPointer;
```

is valid both in C and in C++. However, the reverse, that is,

```
FirstPointer = SecondPointer;
```

does not work in C++ though it works fine in C. This is because C++ is a strictly typed language.

> Note C++ is a strictly typed language. When one writes a function as xyz(); and assuming that it returns an integer, writes the statement int i = xyz(); one relies on xyz() returning int which is not specified explicitly at the time of definition. Such statements rely on the default behaviour of the compiler to consider int even when not specified. When the complier does not default to int, such code results in errors that are hard to debug.

To have the same effect as in C, the second pointer must be explicitly cast in the following manner:

```
FirstPointer = (int*) SecondPointer;
```

The earlier statement produces a compilation error, whereas this one does not.

### 2.4.2 Constant Pointer

A constant pointer is one that cannot point to anything other than what it is pointing to at the time of its definition. It is analogous to the const int or const float types, where the value assigned at the time of definition cannot be changed throughout the program. The value stored in the const pointer is the address of another variable.

When the constant pointer is used, the address itself cannot be changed; however, it must be noted that the content of that address can be changed. So, if we define

```
int * const SecondPointer = &Content1;
```

then the following is allowed:

```
*SecondPointer = AnotherContent;
```

```
// Changing the content of the integer pointed to
```

However, the following is not allowed:

```
SecondPointer++;
```

or

```
SecondPointer = &AnotherContent;
```

```
// Changing the pointer value itself
```

Consider the following code:

```
void main()
int Content1 = 10;
int Content2 = 20;
int *FirstPointer = &Content1;
// Normal pointer; operation is allowed
int *const SecondPointer = &Content2;
// SecondPointer is a constant pointer
*SecondPointer = 100;
// Operation is allowed; contents can be changed
FirstPointer++;
// Normal pointer, operation is allowed
SecondPointer++;
/* Erroneous statement; not allowed as pointer address itself cannot be changed */
// Error: lvalue specifies const object
// lvalue is a variable-like construct, which can be assigned a value
```

When it is not possible to assign a value to a construct such as a const object, it is an error. It is already known from the knowledge of C that a pointer to an integer can be defined as

```
int* FirstPointer = &Content1;
```

C++ allows inserting the keyword const between * and the name of the pointer. Such a pointer then becomes a constant pointer, that is, the address pointed to by it cannot be manipulated. However, the content of that address can be manipulated. So, the following statement is acceptable:

```
SecondPointer = &Content2;
```

The expressions int* const, int* const, and int *const are correct and mean the same. Same is the case with expressions such as int &Name, int & Name, and int& Name.
