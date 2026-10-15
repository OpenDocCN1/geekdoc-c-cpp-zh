```
Enter a number between 0 and 2, 3 to end: 2
You entered 2 so function2 was called

Enter a number between 0 and 2, 3 to end: 3
Program execution completed.
```

Fig. 8.28 | Array of pointers to functions. (Part 3 of 3.)

# 8.13 Introduction to Pointer-Based String Processing

In this section, we introduce some common C++ Standard Library functions that facilitate string processing. The techniques discussed here are appropriate for developing text editors, word processors, page layout software, computerized typesetting systems and other kinds of text-processing software. We have already used the C++ Standard Library string class in several examples to represent strings as full-fledged objects. For example, the GradeBook class case study in Chapters 3–7 represents a course name using a string object. In Chapter 18 we present class string in detail. Although using string objects is usually straightforward, we use null-terminated, pointer-based strings in this section. Many C++ Standard Library functions operate only on null-terminated, pointer-based strings, which are more complicated to use than string objects. Also, if you work with legacy C++ programs, you may be required to manipulate these pointer-based strings.

# 8.13.1 Fundamentals of Characters and Pointer-Based Strings

Characters are the fundamental building blocks of C++ source programs. Every program is composed of a sequence of characters that—when grouped together meaningfully—is interpreted by the compiler as a series of instructions used to accomplish a task. A program may contain character constants. A character constant is an integer value represented as a character in single quotes. The value of a character constant is the integer value of the character in the machine’s character set. For example, 'z' represents the integer value of z (122 in the ASCII character set; see Appendix B), and '\n' represents the integer value of new-line (10 in the ASCII character set).

A string is a series of characters treated as a single unit. A string may include letters, digits and various special characters such as +, -, *, / and $. String literals, or string constants, in C++ are written in double quotation marks as follows:

```
"John Q. Doe"          (a name)
"9999 Main Street"     (a street address)
"Maynard, Massachusetts" (a city and state)
"(201) 555-1212"        (a telephone number)
```

A pointer-based string in C++ is an array of characters ending in the null character ('\0'), which marks where the string terminates in memory. A string is accessed via a pointer to its first character. The value of a string is the address of its first character, but the sizeof a string literal is the length of the string including the terminating null character. In this sense, strings are like arrays, because an array name is also a pointer to its first element.

A string literal may be used as an initializer in the declaration of either a character array or a variable of type char *. The declarations