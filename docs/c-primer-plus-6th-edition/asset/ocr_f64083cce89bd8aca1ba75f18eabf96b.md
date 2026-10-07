# Chapter 7 Functions: C++'s Programming Modules

address of an array conveys no information about the size of the array, you normally pass the array size as a separate argument. Alternatively, you can pass pointers to the beginning of the array and to one position the end to indicate range, as do the algorithms in the STL.

C++ provides three ways to represent C-style strings: using a character array, a string constant, or a pointer to char. All are type char* (pointer-to-char), so they are passed to a function as a type char*. C++ uses the null character (\0) to terminate strings, and string functions test the null character to determine the end of any string they are processing.

C++ also provides the string class to represent strings. A function can accept string objects as arguments and use a string as a return value. The string class size() method can be used to determine the length of a stored string.

C++ treats structures as basic types, meaning that you can pass them by value and use them as return types. However, if a structure is large, it might be more efficient to pass a pointer to the structure and let work with the original data. These same considerations apply to class objects.

A C++ function can be recursive; that is, the code for a particular function can include a call of itself.

The name of a C++ function acts as the address of the function. By using an argument that is a pointer to a function, you can pass to a function the name of a second function that the first function will invoke.

# Chapter Review

+   1. What are the three steps in using a function?

+   2. Construct function prototypes that match the following descriptions:

a. igor() takes no arguments and has no return value.
b. tofu() takes an int argument and returns a float.
c. mpg() takes two double arguments and returns a double.
d. summation() takes the name of a long array and an array size as values and returns a long value.
e. doctor() takes a string argument (the string is not to be modified) and returns a double value.
f. ofcourse() takes a boss structure as an argument and returns nothing.
g. plot() takes a pointer to a map structure as an argument and returns a string.