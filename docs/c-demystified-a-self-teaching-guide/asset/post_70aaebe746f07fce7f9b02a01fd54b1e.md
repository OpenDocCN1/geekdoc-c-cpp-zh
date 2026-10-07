
statements. In the "Hello World" program, main is the name of a function. A program may have many functions, and in Chapter 9 I will show you how to create and use functions. However, a program must have one main function, and only one main function. The reason is that the main function is the starting point for every C++ program. If there was no main function, the computer would not know where to start the program. If there was more than one main function, the program would not know whether to start at one or the other.

Note: The main function is preceded by it and followed by void in parentheses. It will cover the meaning of both in Chapter 9.

## The Function Body

Each of the related instructions, or statements, which belong to the main function are contained within the body of that. A function starts with a left brace, {, and ends with a right brace, }.

Each statement usually ends with a semicolon. The main function has two statements:

```cpp
cout << "Hello World";
return 0;
```

Statements are executed in order, from top to bottom. Don't worry, the term "executed" doesn't mean the statement is put to down. Rather, it means that the statement is carried out, or executed, by the computer.

## cout

The first statement is:

```cpp
cout << "Hello World";
```

cout is pronounced "C-out". The "out" refers to the direction in which cout sends a stream of data.

A data stream may flow in one of directions. One direction is input—into your program from an outside source such as a file or keyboard input. The other direction is output—out from your program to an outside source such as a monitor, printer, or file.

cout concerns the output stream. The standard output device is usually your monitor, though it could be something else, such as a printer or a file on your hard drive.

The << following is an operator. You likely used operators before, such as the arithmetic operators +, -, *, and /, for addition, subtraction, multiplication, and division, respectively.

The << operator is known as the stream insertion operator. It inserts the information immediately to it—the text "Hello World!" into the data stream. The cout object sends that information to the standard output device—in this case, the monitor.

Note: In Chapter 3, you will learn about the counters to use cout and the << operator, the cin object, which concerns the input stream, and the >> operator with the cin object.

## The return Statement

The second and final statement returns a value of zero to the computer's operating system, whether that Windows, UNIX, or another. This tells the operating system that the program ended normally. Some programs do not end, but instead crash, such as if you ran out of memory during the running of the program. The operating system may need to handle this abnormal program termination differently than normal termination. That is why your program tells the system that it ended normally.

## #include Directive

Your C++ program "knows" to start at the main function because the main function is part of the core of the C++ language. We certainly did not write any code that told the C++ program to start at main.

Similarly, your C++ program seems to know that the count object, in conjunction with the stream insertion outputs information to the monitor. We did not write any code to have the count object and the << operator achieve this result.

However, the count is not part of the C++ core language. Rather, it is defined elsewhere, in a standard library file. C++ has a number of standard library files, each defining commonly used objects. Outputting information to the monitor certainly is a common task. While you could go to the trouble of writing your own function that outputs to the screen, a standard library file implementation saves you the trouble of "reinventing the wheel."

While C++ has already implemented the count object for a standard library file, you still have to tell the program to include that standard library file in your application. You do so with the #include directive, followed by the name of the library file. If the library is a standard library file, as opposed to one you wrote (you create), then the file name is enclosed in angle brackets, < and >.

The count object is defined in the standard library file iostream. The "io" in iostream refers to input and output—stream—to a stream of data. To use the count, we need to include the iostream standard library file in our application. We do so with the following:

```cpp
#include <iostream>
```

The include directive is called a preprocessor directive. The preprocessor, together with the compiler and linker, are discussed later in this chapter "Translating the Code for the Computer." The preprocessor directive, unlike statements, is not ended by a semicolon.

## Namespace

The final statement to be discussed in the Hello World! example is using namespace std;

C++ uses namespaces to organize different names in programs. Every time you use the iostream standard library file is part of a namespace called std. Consequently, the count object is called std::count. Using the namespace statement avoids the need for every reference to count, so we can use count in our code.

## Anatomy of a C++ Program

## Translating the Code for the Computer

While you now understand the "Hello World", the computer won't. Computers don't understand C++ or any other programming language. They understand only machine language.

Three programs are used to translate your source code into an executable file the computer can run. These programs are, in their order of appearance:

1. Preprocessor
2. Compiler
3. Linker

## Preprocessor

The preprocessor is a program that scans the source code for preprocessor directives such as include directives. The preprocessor inserts into the source code all files included by include directives.

In this example, the iostream standard library file is included by an include directive. Therefore, the preprocessor inserts the contents of that library file, including its definition of the cout object, into the source code.

## Compiler

The compiler is another program that translates the preprocessed source code (the source code after the insertions by the preprocessor) into corresponding machine language instructions, which are stored in a separate file, called an object file, having an extension. There are different compilers for different programming languages, but the purpose of the compiler is essential same, the translation of a programming language into machine language, no matter which programming language involved.

The compiler can understand your code and translate it into machine language only if your code is in proper syntax for that language. C++, like other programming languages, and indeed most languages, has rules for the spelling of words and for grammar of statements. If there is a syntax error, then the compiler cannot translate your code into machine language instructions, and instead will call your attention to the syntax errors. Thus, in a sense, the compiler acts as a spell checker and grammar checker.

## Linker

While the object file has machine language instructions, the computer cannot run the object file as a program. The reason is that C++ also needs to use other code library, called the run-time library, for common operations, such as the translation of keyboard input or the ability to interact with external hardware to display a message.

The run-time library files may already be installed as part of your operating system. If not, you can download the run-time library files from Microsoft or another vendor. Finally, if you install an IDE as discussed in the next section, the run-time library files are included with the installation.

Note: The linker is a third program that combines the object file with the necessary parts of the run-time library. The result is the creation of an executable file with an .exe extension. The computer runs this file to display “Hello World!” on the screen.
