# Creating the Source Code

**Source code** is a series of statements or commands used to instruct the computer to perform your wanted tasks. As mentioned, the first step in the Program Development Cycle is to enter source code into an editor. For example, here is a line of C source code:

```
printf("Hello, Mom!");
```

This statement instructs the computer to display the message Hello, Mom! onscreen. (For now, don't worry about how this statement works.)

# Using an Editor

Most programming occurs in an Integrated Development Environment (IDE), which enables you to enter your programs in your editor and compile your programs, as well as debug and build your applications. (Although those concepts you tackle later.) You don't have to use the included editor, but it probably makes the most sense. However, most computer systems include a program that can be used as an editor. If you use a Linux or UNIX system, you can use editors such as ed, ex, emacs, or vi. If you use Microsoft Windows, Notepad or WordPad is available.

Most word processors use special codes to format their documents. These codes can't read correctly by other programs. The American Standard Code for Information Interchange (ASCII) has a specified text format that nearly any program, including C, can use. Many word processors, such as WordPerfect, Microsoft Word, WordPad, and WordStar can save source files in ASCII (as a text file rather than a document file). When you want to save a word processor's file as an ASCII file, select the ASCII or text option when saving.

If none of these editors is what you want to use, you can always use a different editor. These are packages, both commercial and shareware, that have been designed specifically for entering source code.

When you save a source file, you must give it a name. The name should describe what the program does. In addition, when you save C program source files, give the file a .c extension. Although you could give your source file any name and extension, .c is recognized as the appropriate extension to use.

# Compiling the Source Code

Although you might understand C source code (at least after reading this book you will), you can't. A computer requires digital, or binary, instructions in machine language. Before your C program can run on a computer, it must be translated from source code to machine language. This translation, the second step in program