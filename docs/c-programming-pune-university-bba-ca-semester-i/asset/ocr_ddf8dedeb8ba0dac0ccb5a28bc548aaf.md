+   1. **The documentation section** consists of only comments.

This section is also called the comment section. It is not compiled by the compiler. It is a user section.

Use of comments

The Single line comment can be written by // (**double slash**) and

Multi line comment

comment can be written by

```
~~~
/* --------
   ---------- */
~~~
```

Comments (remarks) may appear anywhere within a program, as long as they are placed within the delimiters /* and */ (e.g., /* this is a comment */). Such comments are helpful in identifying the program's principal features or in explaining the underlying logic of various program features.

+   2. **Definition Section:** All the symbolic constants are written in definition section. Macros are known as symbolic constants.

+   3. The **Link section** provides instruction to the compiler to take function from system library. E.g., To use the input & output functions we use `#include<stdio.h>`, this is a link file. Please note that the character (#) should be in the first column and there is no semicolon at the end of this line.

+   4. In the **Global Declaration section** the variable used in more than one function can be declared in Global section. Functions can be declared in this section.

+   5. Every C program consist of one or more function, one of which must be called the main( ) function. The program will always begin by executing the main( ) function, which may access other functions. Any other function definitions must be defined separately, either ahead of or after main( ) function.

**Each function must contain:**

+   1. A function heading, which consists of the function name, followed by an optional list of arguments, enclosed in parentheses.

+   2. A list of argument declarations, if arguments are included in the heading.

+   3. A compound statement, which comprises the remainder of the function.

The arguments are symbols that represent information being passed between the function and other parts of the program. (Arguments are also referred to as parameters.)

Each compound statement is enclosed within a pair of braces, i.e., { }. The braces may contain one or more elementary statements (called expression statements) and other compound statements. Thus compound statements may be nested, one within another.

Each expression statement must end with a semicolon (;).

The C program may contain one or more sections

Both the parts must be placed between opening and closing braces. The program execution begins with the opening braces of main( ) function. Thus the closing brace of main( ) function is the logical end of the program.