
## Points to Remember

The proverb *practice makes man perfect* is to be always remembered by all the initial learners of C programming. Along with lot of practice, we need to remember the points mentioned in the following paragraph to reduce the mistakes committed during programming:

1. All needed header files should be included before declaring the main( ) function.
2. An executable C program should always contain only one main( ) function.
3. Two functions with the same name are not allowed in C program.
4. Normally, C programs are written using lower case letters, but upper case can also be used.
5. Identifiers are case sensitive.
6. There should be at least one blank space between two C tokens.
7. Usually, C statements end with a semi colon.
8. Comment can be inserted anywhere in the C program as per the need of the programmers.
9. Always write a proper comment before writing a function.
10. Every opening curly bracket should have a corresponding closing curly bracket.
11. Meaningful name should be given to a variable name used in C program. For example, if a variable is supposed to store student name, then it should be defined as studentname or student_name.

## Summary

In this chapter, we have learned about the basics of C programming. The emphasis was to understand the elementary components required for C programming. We also learned about the need of a programming language and generations of programming. A brief look at the history of C language was taken, and then we devised our first C program. We then understood the structure of a C program along with the usage of each of the segments used in the structure. Then, the C character set was discussed with the emphasis on type of reserved words and concept of variables and constants that can be used in C language. Finally, the steps to create and execute a C program in Linux environment are shown.

## Review Questions

- Q1. Explain the terms system software and application software.
- Q2. Write a brief note on generation of languages.
- Q3. Draw the block diagram of C program structure.
- Q4. What is the use of comments in a C program?
- Q5. What is the purpose of the global variable declaration section?
- Q6. Differentiate between keyword and variable in C language.
- Q7. State the rules used to define a variable name in C language.
- Q8. Differentiate between the following:
    - i. Integer constant and Real constant
    - ii. Character constant and String constant
- Q9. Write the steps used to create and execute a C program.
- Q10. State whether true or false:
    - i. C statements end with a comma.
    - ii. FLOAT is a valid variable name.
    - iii. `#include <define.h>` includes a file named `define` in C program.
    - iv. V is a valid single character constant.
    - v. The extension of C executable program is .exe.
    - vi. "Glisc1" is a valid string constant.
    - vii. To include symbolic constants in C program, we use documentation section.
    - viii. To insert a tab key in the output, the back slash character \t is used.
    - ix. 0x55 is a valid hexadecimal number.
    - x. The identifier add() represents a variable name.

## Practical Exercises

- Q1. Write a program to convert the given centimeters into kilometers and millimeters.
- Q2. Write a program that accepts value of pi, radius, and height. Then find the volume of a cylinder using the formula $V = \pi$ * square of radius * height.
- Q3. Write a program to accept a number N and find its square.
- Q4. Write a program to accept a number of days and convert it into number of weeks.
- Q5. Write a program to accept a temperature value in centigrade and convert it to Fahrenheit, where $F = (5/9) * (C - 32)$.

# 03 C Data Types

## OBJECTIVES

- Understanding Data Type
- Explain Data Types in C
- Explain User-Defined Data Type
- Describe Derived Data Type
- Describe Void Pointers

In the previous chapter, we have discussed about a C token called *identifier*. Identifiers are integral part of any C program. For example, assume that in our program, we have defined an identifier named *joining_month*, which is used to store the numeric value of month in which an employee has joined the organization. This identifier can then store any value between number 1 and 12, as we only have 12 months in the calendar year. It is not possible here to store a value such as 1.8, as the value will be inappropriate. This example suggests that the type of values stored in an identifier also has significance. C language uses certain reserved words to identify the type of data value that can be stored in an identifier. As the reserved word associates a data value type with the identifier, it is known as data type. In this chapter, we will understand and discuss in detail about different data types available in C and their usage. We will also learn about user-defined data type and enumerated data type.

## 3.1 Understanding Data Type

The type of data value that can be stored in an identifier is known as its data type. If an identifier *joining_month* is assigned a data value 8, then we would say that the identifier is capable of storing an integer data. This in turn states that the data type of the identifier *joining_month* is an integer. Similarly, if an identifier *total_marks* is assigned a data value 95.75, then we would say that it is capable of storing real data; hence, its data type has to be real.

Reserved words of C are used to associate two entities with an identifier. First is the type of value that can be stored in the identifier, and second is the memory space required for storage by the identifier. The compiler designers associate a pre-allocated fixed memory space with a data type. Thus, it becomes easier for the compiler to handle different identifiers used in C. The basic unit of memory space is byte, and 8 bits makes 1 byte. The data types in C are classified as primitive and derived. The next section discusses the basic data types available in C.

## 3.2 Data Types in C

As discussed earlier, the identifiers defined in C store a predefined type of value. To implement this feature, C language supports two categories of data types, namely, primitive and derived. Figure 1 shows the data types that fall under each of these categories:

![](img/5d422ba7108ffdf64376be51eaf0c459_57_0.png)

The primitive data types form the basic building block for defining an identifier. C language supports four primitive or basic data types, namely, integer, decimal, character, and empty. These data types are represented by using keywords *int, float, char, and void*, respectively. To associate an identifier with its data type, the following syntax is used:

```
Data Type identifier 1[, identifier 2, identifier 3, ..., identifier n];
```

The preceding syntax is known as a declaration statement in C language, where the identifier 2, identifier 3, ...., identifier n are all optional. It means that they may be present or absent in the definition. In case these identifiers are present, it means that we have multiple identifiers of the same type. In this chapter, we are going to have a look at primitive data types in detail. The derived data types, except for enum and pointer, are discussed later in separate chapters.

### Integer

Many numeric operations involve a positive or a negative integer number. To store integer numbers in an identifier, we need to define the identifier of type *int*. In this case, int is a C reserved word, which indicates that the identifier is capable of storing an integer data value. To declare a variable of type integer, we use the following syntax:

```
int identifier1[, identifier 2, identifier 3, ..., identifier n];
```

Some examples of declaring an integer identifier are as follow:

```
int i_joining_month;
int i_age, i_basic_salary;
```

In the preceding examples, the first statement declares an identifier with a name *i_joining_month* capable of storing integer value that represents the numeric value of month of joining for an employee in an organization. The second statement declares two identifiers, namely, *i_age* and *i_basic_salary*, capable of storing integer values that represent age and basic salary of an employee.
