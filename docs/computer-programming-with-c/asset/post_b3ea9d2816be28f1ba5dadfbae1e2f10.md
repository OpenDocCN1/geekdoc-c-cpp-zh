
## Chapter 2 | Fundamentals

### 2.1 Overview

C++ is an extension of C. This means that all the features of C are also available in C++. Furthermore, C++ has certain additional features of object-oriented programming, which makes it superior to the conventional C language. The details of object orientation and other features of C++ are covered in the later chapters of this text book.

In this chapter, we will study some fundamentals, which build the foundation to understand the advanced features of C and various object-oriented features supported by C++.

### 2.2 The First C/C++ Program

Recall from Chapter 1 that every C/C++ program has to be compiled and linked so as to convert the high-level language into the machine code. All the instructions written in the program are executed one-by-one by the processor in a sequence as they appear in the program file. Therefore, it is the job of the programmer to inform the processor about the exact starting point from which the execution of the program should begin. The main() function in C/C++ is used to represent the start and end points of the program execution. Hence, every program must have exactly one main() function, which is shown in Figure 2.1.

CPU will execute all the instructions where we write inside the body of the main() function in a sequence as they appear. The presence of empty round parenthesis after a special word main() informs the compiler that the function main() does not take any arguments. By default, every function in C/C++ is expected to return a value to the one who invokes the function. We can use a keyword void if we do not want to return any value to the calling function. The complete details on functions with arguments and return values are discussed in Chapter 7 of this text book and hence the details about ‘function arguments’ and ‘return types’ can be ignored at this point of time.

At this stage, we need to understand that a main() function is to be created using a template shown in Figure 2.1. The function main() defines the ‘start point’ and the ‘end point’ of the program, as the execution of any program starts from a point where the main() function begins and the execution of the program terminates at a point where the

As stated before, execution of any program always starts from main() function. Given that this program has only one statement in the main() function (which is the printf() statement), the output of the program is shown below.

```
I like Computer Programming
```

NOTE: Following is applicable to C++ and not to C

The program shown in Figure 2.2 executes in C as well as C++. This is because the printf() function is supported by both the languages. Along with support to printf() statement, C++ supports another way to print a message on the computer screen. cout is a built-in object available in C++ but not in C, which is used to stream messages on an output device. The program written in Figure 2.3 shows the usage of cout object to print the message on the computer screen.

![](img/57c0d966bb33c67a5a188e6bf39e4e02_40_0.png)

**Figure 2.3:** Source code to print a message on the computer screen

The statement

```
cout<<"I like Computer Programming";
```

is used to print a message I like Computer Programming on the computer screen. Note that every statement ends with a semicolon. The operator << is called as an insertion operator, which actually inserts a text message on the computer screen. We have also explained in Chapter 4 of this text book that the operator << is also used as 'left shift operator', which can be used to shift the bits of a binary number in the left direction. However, in this case, we have used the operator <<, which acts as an insertion operator and prints a message on the screen because it is internally overloaded by C++ in one of the built-in classes which is named as ostream. The class ostream is fully defined inside the header file iostream.h. Also, cout is an object of class ostream, which is created inside the file iostream.h. Therefore, we have written the first statement of the C++ program as,

```
#include <iostream.h>
```

The statement includes the contents of the header file `iostream.h` into the program, so as to facilitate the programmer to use the built-in object of class `ostream`, which is named as `cout` directly in the code. Remember, `#include` is a pre-processor directive, which is used to include the contents of a particular header file into the C++ program before the compilation of the code starts. This ensures that the complete definition of the class `ostream` and the insertion operator `<<` is included in the program before the compilation. Details about classes and objects are discussed in Chapter 11 of this text book. **The only point we must understand at this stage is that the statement**

`cout<<"I like Computer Programming";`

*is used to print a message as I like Computer Programming on the computer screen as shown in Figure 2.4. And we must include the contents of header file `iostream.h` before making use of `cout` in our program.*

![](img/57c0d966bb33c67a5a188e6bf39e4e02_41_0.png)

**Figure 2.4:** Usage of cout

C++ supports *streaming outputs*, which are not supported by C. In general, the word *stream* refers to the flow of data in the computer system. The *output stream* of C++ allows the programmer to perform a ‘write’ operation on the output devices such as ‘screen’, ‘file’, and ‘disk’. The header file `iostream.h` defines the necessary classes and functions to support the streaming input and output. We will discuss the *input streams* of C++ in the later sections of this chapter. As we have written the `cout` instruction inside the main function, the processor will now execute the instruction after translating the instruction into a machine code, thereby printing a message specified on the computer screen as seen in the output of the program.

### NOTES

The program given in Figure 2.2 uses `printf()` statement to print a message on the computer screen. The `printf()` function is declared in header file `stdio.h` which is included in the program. The program using `printf()` works with C as well as C++ because the header file `stdio.h` and `printf()` function are supported by both the languages. However, the program using `cout` shown in Figure 2.3 works with C++ but not with C. This is because the object `cout` and header file `iostream.h` are only supported by C++ and not by C. This clearly means that C++ supports streaming output operations whereas C does not. We will learn more about streams supported by C++ in Chapter 15.

### Can I write C/C++ programs in upper case?

![](img/57c0d966bb33c67a5a188e6bf39e4e02_42_0.png)

The answer is NO, because C/C++ is a case sensitive language. This means that upper case and lower case characters have different meaning for the language. For example, `printf()` and `PRINTF()` will be considered as two different identifiers by the compiler. `stdio.h` declares the function `printf()` in lower case and hence compiler will not be able to recognize a symbol `PRINTF()`. Therefore, we cannot just write the complete C/C++ program in the upper case, rather we have to preserve the syntax of the language along with the case. Syntax of C/C++ is such that most of the built-in keywords and reserved words are in lower case. There are still some built-in macros which are to be written in upper case.

### 2.3 Writing Comments

Comment is a part of the code, which is ignored by the compiler. However, programmers may still write comments in the program to give documentation for the complex logic implemented using a particular piece of code. Although, comments do not contribute in generating the output of the program (comments are not even compiled), it is always recommended to comment the source code wherever possible. This makes the code easy to read and understand if any part of the code is to be referred in future for editing or debugging purpose. There are two different types of commenting styles that can be applied to the program:

- 1. Single line comments (only supported by C++ and not by C)
- 2. Multi-line comments (supported by both C and C++)

A single line comment starts with two slash symbols written back to back without any space in between two slash symbols as shown below:

```cpp
// This is a single line comment
```

The compiler will ignore any text that is written within the line after two slash (`//`) symbols. Note that, a single line comment can be stretched until the end of current line only. This means that, if we wish to write a comment across multiple lines then we must begin each of the lines by the two slash symbols as shown below:

```cpp
// This is the first line of the comment
// This is the second line of the comment
// This is the third line of the comment
```

Along with a support to `//` symbol for single line comments, compiler also ignores any text which is written in between `/*` and `*/` so as to support creation of multiline comments in the program. Hence, we can write a multiline comment in the code, such that, it begins with a token `/*` and ends with a token `*/` as shown below:

```cpp
/*This is the first line of the comment
This is the second line of the comment
This is the third line of the comment*/
```
