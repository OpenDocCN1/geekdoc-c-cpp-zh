know whether your data needs to remain fixed throughout program execution or whether it should change.

# NAMED CONSTANTS

Some data must stay the same throughout a program. For example, the conversion formula that converts inches into centimeters is fixed, because 1 inch is always equal to 2.54 centimeters. When stored in memory, this type of data needs to be protected from accidental changes during program execution. In C++, you can use a **named constant** to instruct a program to mark those memory locations in which data is fixed throughout program execution.

**Named constant:** A memory location whose content is not allowed to change during program execution.

To allocate memory, we use C++’s declaration statements. The syntax to declare a named constant is:

```
```cpp
const dataType identifier = value;
```
```

In C++, **const** is a reserved word. It should be noted that a named constant is initialized and declared all in one statement and that it *must* be initialized when it is declared because from this statement on the compiler will reject any attempt to change the value.

# EXAMPLE 2-11

Consider the following C++ statements:

```
```cpp
const double CONVERSION = 2.54;
const int NO_OF_STUDENTS = 20;
const char BLANK = ' ';
```
```

The first statement tells the compiler to allocate memory (eight bytes) to store a value of type *double*, call this memory space CONVERSION, and store the value 2.54 in it. Throughout a program that uses this statement, whenever the conversion formula is needed, the memory space CONVERSION can be accessed. The meaning of the other statements is similar.

Note that the identifier for a named constant is in uppercase letters. Even though there are no written rules, C++ programmers typically prefer to use uppercase letters to name a named constant. Moreover, if the name of a named constant is a combination of more than one word, called a *run-together word*, then the words are typically separated using an underscore. For example, in the preceding example, NO_OF_STUDENTS is a run-together word. (Also see the section Program Style and Form, later in this chapter, to properly structure a program.)