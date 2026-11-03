# Chapter 3

# Input-Output In C

There are three main functions of any program- it takes data as input, processes this data and gives the output. The input operation involves movement of data from an input device (generally keyboard) to computer memory, while in output operation the data moves from computer memory to the output device (generally screen). C language does not provide any facility for input-output operations. The input output is performed through a set of library functions that are supplied with every C compiler. These functions are formally not a part of the language but they are considered standard for all input-output operations in C. The set of library functions that performs input-output operations is known as standard I/O library.

There are several header files that provide necessary information in support of the various library functions. These header files are entered in the program using the #include directive at the beginning of the program. For example if a program uses any function from the standard I/O library, then it should include the header file stdio.h as #include <stdio.h>

Similarly there are other header files like math.h, string.h, alloc.h that should be included when certain library functions are used.

In this chapter we'll discuss about the input functions scanf( ) and getchar( ) and the output functions printf( ) and putchar( ). There are several other input-output functions that will be discussed in further chapters.

A simple method for taking the data as input is to give the value to the variables by assignment statement.

```
int basic = 2000;
char ch = 'y';
```

But in this way we can give only particular data to the variables.

The second method is to use the input function scanf( ), which takes the input data from the keyboard. In this method we can give any value to the variables at run time. For output, we use the function printf( ).

# 3.1 Conversion Specifications

The functions scanf( ) and printf( ) make use of conversion specifications to specify the type and size of data. Each conversion specification must begin with a percent sign ( % ). Some conversion specification are given below

+   - %c - a single character