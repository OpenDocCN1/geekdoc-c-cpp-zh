+   - A.8 Classes 711
+     - A.8.1 The Header File 711
+     - A.8.2 The Implementation File 713
+     - A.8.3 Using the Class Sphere 715
+     - A.8.4 Inheritance 716
+   - A.9 Libraries 717

# Prerequisite

Knowledge of a modern programming language

This book assumes that you already know how to write programs in a modern programming language. If that language is C++, you can probably skip this appendix, returning to it for reference as necessary. If instead you know a language such as Java or C, this appendix will introduce you to C++. Also, Appendices K and L cover C++ to Java and Python, respectively.

It isn't possible to cover all of C++ in these pages. Instead this appendix focuses on the parts of the language used in this book. First we look at the basics of data types, variables, expressions, operators, and simple input/output. We continue with functions, decision constructs, looping constructs, arrays, and strings. Various C++ Interludes, which appear throughout the book as needed, will cover classes, pointers, exceptions, and files.

# A.1 Language Basics

Let's begin with the elements of the language that allow you to perform simple computations. For example, the C++ program in Figure A-1 computes the volume of a sphere. Running this program produces the following output, where the user's response appears in blue:

```
Enter the radius of the sphere: 19.1
The volume of a sphere of radius 19.1 is 29186.927734
```

A typical C++ program consists of several modules, some of which you write and some of which you include from standard libraries. C++ provides a source-inclusion facility, which allows the system to include the contents of a file automatically at a specified point in a program before the program is compiled. For example, our sample program uses a standard library to perform input and output operations. The first line of this program is an include directive that names a standard header iostream, which enables the program to use the input/output module. The second line informs the compiler to use the standard namespace (see Section C.1.2 in C++ Interlude 1).

Each C++ program must contain a function main

A C++ program is a collection of functions, one of which must be called main. Program execution always begins with function main. The following paragraphs provide an overview of the basics of C++ and refer to the simple program in Figure A-1 by line number. Note that the only function this simple program contains is main.

# A.1.1 Comments

Each comment line begins with two slashes

Each comment line in C++ begins with two slashes // and continues until the end of the line. You can also begin a multiple-line comment with the characters /* and end it with */. However, a