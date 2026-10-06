as one of the first lines in your program. More information on the C++ class string is in Section A.7
of Appendix A.

**Constants.** Constants in Java are declared within a class or method using the syntax

```
public static final int MAX_SIZE = 20;
```

which creates a publicly accessible constant MAX_SIZE with the value 20. A similar statement in C++nuses the keyword const to indicate a constant value:

```
const int MAX_SIZE = 20;
```

Constants in C++ are available anywhere within the scope of their declaration. If a constant
declared outside of a class or file, that is available to any function or class defined after it is
file and is said to be **global**, even though it is restricted to that file.

Java has a null null that is used to indicate that an object has not been assigned to a variable.
C++ uses nullptr for this purpose.

**Arrays.** You declare and reference arrays in Java and C++ using similar statements, their
imlements are very different. Arrays in Java and C++ have a public field length thatncontains the number of locations in the array. If a program attempts to access a position beyond
tend of the array, an exception is thrown.

C++ arrays are not objects, but are sequences of memory locations of the data type declared for
try. In C++ arrays are accessed using [ ], just as they are in Java. C++ arrays have no
data field that tracks the positions in the array that do, and most importantly, C++ permits the
rogrammer to access positions in the array that do not exist. This is a very common source of errors
a a C++ program and is one of the areas where you must take care. The STL class vector,
which is discussed in Section A.6 of Appendix A, is an alternative to C++ arrays that providesnsome of the features of the Java array.

The following declares an array of 20 integers in Java:

```
int[] myArray = new int[MAX_SIZE];
```

This statement does the same thing in C++:

```
int myArray[MAX_SIZE];
```

You can also declare a C++ array by using syntax similar to that of Java:

```
int myArray[] = new int[MAX_SIZE];
```

One difference is the location of the square brackets, but you must also take responsibility for de-leting the array when you are finished with. You do so with the delete statement:

```
delete[] myArray;
```

Notice the [ ] following the delete operator to indicate that myArray is an array. In C++ Interude 2,
we discuss the use of the operators new and delete in C++.

# K.3 Flow Control and Functions

**Flow control.** The syntax of flow is derived from C++, the structure of flow-control
stements in C++ is the same as those you are familiar with Java. This is true for the selection
statements if, if-else, and switch. It is also true for loop statements while, do-while, and for.
significant differences in C++ are related to the test expression that controls the selection or
petition.