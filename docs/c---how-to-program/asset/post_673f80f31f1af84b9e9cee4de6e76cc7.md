
int), each row corresponding to an element in the topics array. When the program runs, it should ask the user to rate each issue. Have your friends and family respond to the survey. Then have the program display a summary of the results, including:

- a) A tabular report with the five topics down the left side and the 10 ratings across the top, listing in each column the number of ratings received for each topic.
- b) To the right of each row, show the average of the ratings for that issue.
- c) Which issue received the highest point total? Display both the issue and the point total.
- d) Which issue received the lowest point total? Display both the issue and the point total.

## 7.33 *(Carbon Footprint Calculator: Arrays of Function Pointers)*

Using arrays of function pointers, as you learned in this chapter, you can specify a set of functions that are called with the same types of arguments and return the same type of data. Governments and companies worldwide are becoming increasingly concerned with carbon footprints (annual releases of carbon dioxide into the atmosphere) from buildings burning various types of fuels for heat, vehicles burning fuels for power, and the like. Many scientists blame these greenhouse gases for the phenomenon called global warming. Create three functions that help calculate the carbon footprint of a building, a car and a bicycle, respectively. Each function should input appropriate data from the user, then calculate and display the carbon footprint. (Check out a few websites that explain how to calculate carbon footprints.) Each function should receive no parameters and return void. Write a program that prompts the user to enter the type of carbon footprint to calculate, then calls the corresponding function in the array of function pointers. For each type of carbon footprint, display some identifying information and the object’s carbon footprint.

## 8

## C Characters and Strings

## Objectives

In this chapter, you'll:

- Use the functions of the character-handling library (`<ctype.h>`).
- Use the string-conversion functions of the general utilities library (`<stdlib.h>`).
- Use the string and character input/output functions of the standard input/output library (`<stdio.h>`).
- Use the string-processing functions of the string-handling library (`<string.h>`).
- Use the memory-processing functions of the string-handling library (`<string.h>`).

![](img/d0d3b7423c2d9e5650be79209ea1885d_366_0.png)

## Outline

- 8.1 Introduction
- 8.2 Fundamentals of Strings and Characters
- 8.3 Character-Handling Library
  - 8.3.1 Functions isdigit, isalpha, isalnum and isxdigit
  - 8.3.2 Functions islower, isupper, isspace, iscntrl, ispunct, isprint and isgraph
- 8.4 String-Conversion Functions
  - 8.4.1 Function strtod
  - 8.4.2 Function strtol
  - 8.4.3 Function strtoul
- 8.5 Standard Input/Output Library Functions
  - 8.5.1 Functions fgets and putchar
  - 8.5.2 Function getchar
  - 8.5.3 Function sprintf
  - 8.5.4 Function sscanf
- 8.6 String-Manipulation Functions of the String-Handling Library
  - 8.6.1 Functions strcpy and strncpy
  - 8.6.2 Functions strcat and strncat
- 8.7 Comparison Functions of the String-Handling Library
- 8.8 Search Functions of the String-Handling Library
  - 8.8.1 Function strchr
  - 8.8.2 Function strcspn
  - 8.8.3 Function strpbrk
  - 8.8.4 Function strrchr
  - 8.8.5 Function strspn
  - 8.8.6 Function strstr
  - 8.8.7 Function strtok
- 8.9 Memory Functions of the String-Handling Library
  - 8.9.1 Function memcpy
  - 8.9.2 Function memmove
  - 8.9.3 Function memcmp
  - 8.9.4 Function memchr
  - 8.9.5 Function memset
- 8.10 Other Functions of the String-Handling Library
  - 8.10.1 Function strerror
  - 8.10.2 Function strlen
- 8.11 Secure C Programming

*Summary | Self-Review Exercises | Answers to Self-Review Exercises | Exercises | Special Section: Advanced String-Manipulation Exercises | A Challenging String-Manipulation Project | Making a Difference*

## 8.1 Introduction

This chapter introduces the C standard library functions that help us process strings and characters. The functions enable programs to process characters, strings, lines of text and blocks of memory. The chapter discusses the techniques used to develop editors, word processors, page-layout software, computerized typesetting systems and other kinds of text-processing software. The text manipulations performed by formatted input/output functions like `printf` and `scanf` can be implemented using the functions discussed in this chapter.

### C11 Annex K Functions

As we discuss in Section 8.11, C11’s optional Annex K describes more secure versions of many functions that we present in this chapter. As with `printf_s` and `scanf_s` for `printf` and `scanf`, the more secure Annex K versions should be used, if available for your compiler.

## 8.2 Fundamentals of Strings and Characters

Characters are the fundamental building blocks of source programs. Every program is composed of a sequence of characters that—when grouped together meaningfully—is interpreted by the computer as a series of instructions used to accomplish a task. A program may contain character constants. A character constant is an int value represented as a character in single quotes. The value of a character constant is the integer value of the character in the machine's character set. For example, 'z' represents the integer value of the letter z, and '\n' the integer value of newline (122 and 10 in ASCII, respectively).

A string is a series of characters treated as a single unit. A string may include letters, digits and various special characters such as +, -, *, / and $. String literals, or string constants, in C are written in double quotation marks as follows:

- "John Q. Doe" (a name)
- "99999 Main Street" (a street address)
- "Waltham, Massachusetts" (a city and state)
- "(201) 555-1212" (a telephone number)

A string in C is an array of characters ending with the null character ('\0'). A string is accessed via a pointer to the first character in the string. The value of a string is the address of its first character. Thus, in C, it's appropriate to say that a string is a pointer—in fact, a pointer to the string's first character. This is just like arrays, because strings are simply arrays of characters.

A character array or a variable of type char * can be initialized with a string in a definition. The definitions

```c
char color[] = "blue";
const char *colorPtr = "blue";
```

each initialize a variable to the string "blue". The first definition creates a 5-element array color containing the characters 'b', 'l', 'u', 'e' and '\0'. The second definition creates pointer variable colorPtr that points to the string "blue" somewhere in read-only memory.

> **Portability Tip 8.1** The C standard indicates that a string literal is immutable (i.e., not modifiable), but some compilers do not enforce this. If you might need to modify a string literal, it must be stored in a character array.

The preceding array definition could also have been written

```c
char color[] = { 'b', 'l', 'u', 'e', '\0' };
```

When defining a character array to contain a string, the array must be large enough to store the string and its terminating null character. The preceding definition automatically determines the size of the array based on the number of initializers (5) in the initializer list.

> **Common Programming Error 8.1** Not allocating sufficient space in a character array to store the null character that terminates a string is an error.

> **Common Programming Error 8.2** Printing a "string" that does not contain a terminating null character is an error. Printing will continue past the end of the "string" until a null character is encountered.
