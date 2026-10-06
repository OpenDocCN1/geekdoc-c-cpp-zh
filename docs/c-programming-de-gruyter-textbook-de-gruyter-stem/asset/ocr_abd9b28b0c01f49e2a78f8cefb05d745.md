# 2 Elementary C++ Programming

```
int i;
and,
int i;
and
i
;
```

However, it is strongly recommended to write programs with clearness and readability. This is because programs not only need to be executed by machines, but also need to be revised and maintained by programmers.

Comments in a program are used to explain and interpret the program to improve its readability. When the compiling system compiles the source program, it first strips the comments. Thus comments have no effect on the realization of a program’s functions. In addition, since they are stripped by the compiler code generation, will not increase the size of the final executable program. Comments, if used properly, can make a program more readable.

There are two ways to add comments in C++. One follows the C language, using "/*" and "//" to enclose comments as follows:

```
/* This is
 a comment.
*/
int i; /* i is an integer */
```

Here all the symbols between "/*" and "*/" are to be recognized as comments. Starting from "//" and the other way using "//" to delimit a single-line comment. Starting from "//" until the finishing point of that line, all the characters are viewed as comments.

```
// This is a comment.
int i; // i is an integer
```

# 2.2 Basic Data Types and Expressions

Data are the objects process. They can be classified according to their characteristics. For example, in mathematics there are concepts like integers, real numbers, etc.; in daily life we need character strings to denote a person’s names and addresses; the answers of some questions can only be “yes” or “no” (i.e., “true” or “false” in logic). Different types of data have different processing methods. For example, both integers and real numbers can participate in arithmetical operations, while real numbers differ from integers in that they have to retain a certain part of decimal fractions; character