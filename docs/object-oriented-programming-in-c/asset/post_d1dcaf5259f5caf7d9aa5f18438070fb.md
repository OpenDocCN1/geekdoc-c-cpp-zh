
- All ANSI C++ programs must include **using namespace std** directive.
- A typical C++ program would contain four basic sections, namely, include files section, class declaration section, member function section and main function section.
- Like C programs, C++ programs can be created using any text editor.
- Most compiler systems provide an integrated environment for developing and executing programs. Popular systems are UNIX AT&T C++, Turbo C++ and Microsoft Visual C++.

## Key Terms

- #include
- a.out
- Borland C++
- cascading
- cin
- class
- client
- comments
- cout
- edlin
- extraction operator
- float
- free-form
- get from operator
- input operator
- insertion operator
- int
- iostream
- iostream.h
- keyboard
- main()
- member functions
- MS-DOS
- namespace
- object
- operating systems
- operator overloading
- output operator
- put to operator
- return ()
- screen
- server
- Simula67
- text editor
- Turbo C++
- Unix AT&T C++
- using
- Visual C++
- Windows
- Zortech C++

## Review Questions

2.1 State whether the following statements are TRUE or FALSE.

- (a) Since C is a subset of C++, all C programs will run under C++ compilers.
- (b) In C++, a function contained within a class is called a member function.
- (c) Looking at one or two lines of code, we can easily recognize whether a program is written in C or C++.
- (d) In C++, it is very easy to add new features to the existing structure of an object.
- (e) The concept of using one operator for different purposes is known as operator overloading.
- (f) The output function printf() cannot be used in C++ programs.

2.2 Why do we need the preprocessor directive #include <iostream> ?

2.3 How does a main() function in C++ differ from main() in C?

2.4 What do you think is the main advantage of the comment // in C++ as compared to the old C type comment?

2.5 Describe the major parts of a C++ program.

## Debugging Exercises

2.1 Identify the error in the following program.

```cpp
#include <iostream.h>
void main()
{
int i=10, j=5;
int modResult=0;
int divResult=0;

modResult = i%j;
cout << modResult << " ";

divResult = i/modResult;
cout << divResult;
}
```

2.4 Find errors, if any, in the following C++ statements.

- (a) cout << "x=" x;
- (b) m = 5; // n = 10; // s = m + n;
- (c) cin >>x; >>y;
- (d) cout << \n "Name:" << name;
- (e) cout <<"Enter value:"; cin >> x;
- (f) /*Addition*/ z = x + y;

## Programming Exercises

2.1 Write a program to display the following output using a single cout statement.
Maths = 90
Physics = 77
Chemistry = 69

2.2 Write a program to read two numbers from the keyboard and display the larger value on the screen.

2.3 Write a program to input an integer value from keyboard and display on screen "WELL DONE" that many times.

2.4 Write a program to read the values of a, b and c and display the value of x, where
x = a / b - c
Test your program for the following values:
(a) a = 250, b = 85, c = 25
(b) a = 300, b = 70, c = 70

2.5 Write a C++ program that will ask for a temperature in Fahrenheit and display it in Celsius.

2.6 Redo Exercise 2.5 using a class called temp and member functions.

## 3 Tokens, Expressions and Control Structures

### Key Concepts

- Tokens
- Keywords
- Identifier
- Data types
- User-defined types
- Derived types
- Symbolic constants
- Declaration of variables
- Initialization
- Reference variables
- Type compatibility
- Scope resolution
- Dereferencing
- Memory management
- Formatting the output
- Type casting
- Constructing expressions
- Special assignment expressions
- Implicit conversion
- Operator overloading
- Control structures

### 3.1 Introduction

As mentioned earlier, C++ is a superset of C and therefore most constructs of C are legal in C++ with their meaning unchanged. However, there are some exceptions and additions. In this chapter, we shall discuss these exceptions and additions with respect to tokens and control structures.

### 3.2 Tokens

As we know, the smallest individual units in a program are known as tokens. C++ has the following tokens:

- Keywords
- Identifiers
- Constants
- Strings
- Operators

A C++ program is written using these tokens, white spaces, and the syntax of the language. Most of the C++ tokens are basically similar to the C tokens with the exception of some additions and minor modifications.

### 3.3 Keywords

The keywords implement specific C++ language features. They are explicitly reserved identifiers and cannot be used as names for the program variables or other user-defined program elements.

Table 3.1 gives the complete set of C++ keywords. Many of them are common to both C and C++. The ANSI C keywords are shown in boldface. Additional keywords have been added to the ANSI C keywords in order to enhance its features and make it an object-oriented language. ANSI C++ standards committee has added some more keywords to make the language more versatile. These are shown separately. Meaning and purpose of all C++ keywords are given in Appendix D.

### 3.4 Identifiers and Constants

Identifiers refer to the names of variables, functions, arrays, classes, etc. created by the programmer. They are the fundamental requirement of any language. Each language has its own rules for naming these identifiers. The following rules are common to both C and C++:

- Only alphabetic characters, digits and underscores are permitted.
- The name cannot start with a digit.
- Uppercase and lowercase letters are distinct.
- A declared keyword cannot be used as a variable name.

A major difference between C and C++ is the limit on the length of a name. While ANSI C recognizes only the first 32 characters in a name, ANSI C++ places no limit on its length and, therefore, all the characters in a name are significant.

Care should be exercised while naming a variable which is being shared by more than one file containing C and C++ programs. Some operating systems impose a restriction on the length of such a variable name.

Constants refer to fixed values that do not change during the execution of a program.

Like C, C++ supports several kinds of literal constants. They include integers, characters, floating point numbers and strings. Literal constants do not have memory locations. Examples:

```
123                // decimal integer
12.34              // floating point integer
037                // octal integer
0X2                // hexadecimal integer
"C++"             // string constant
'A'                // character constant
L'ab'              // wide-character constant
```

The wchar_t type is a wide-character literal introduced by ANSI C++ and is intended for character sets that cannot fit a character into a single byte. Wide-character literals begin with the letter L.

**Table 3.1 C++ keywords**

|    |    |    |    |
|----|----|----|----|
| asm | double | new | switch |
| auto | else | operator | template |
| break | enum | private | this |
| case | extern | protected | throw |
| catch | float | public | try |
| char | for | register | typedef |
| class | friend | return | union |
| const | goto | short | unsigned |
| continue | if | signed | virtual |
| default | inline | sizeof | void |
| delete | int | static | volatile |
| do | long | struct | while |
| Added by ANSI C++ |  |  |  |
| bool | export | reinterpret_cast | typename |
| const_cast | false | static_cast | using |
| dynamic_cast | mutable | true | wchar_t |
| explicit | namespace | typeid |  |

Note: The ANSI C keywords are shown in bold face.
