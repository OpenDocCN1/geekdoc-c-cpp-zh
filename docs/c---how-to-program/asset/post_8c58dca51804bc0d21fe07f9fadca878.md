
```cpp
// use square brackets to create lvalue
cout << "\n\nAssigning 1000 to integers1[5]" << endl;
integers1[ 5 ] = 1000;
cout << "integers1:" << endl;
outputVector( integers1 );

// attempt to use out-of-range index
try
{
    cout << "\nAttempt to display integers1.at( 15 )" << endl;
    cout << integers1.at( 15 ) << endl; // ERROR: out of range
}
catch ( out_of_range &ex )
{
    cout << "An exception occurred: " << ex.what() << endl;
}
}

// output vector contents
void outputVector( const vector< int > &array )
{
    size_t i; // declare control variable

    for ( i = 0; i < array.size(); ++i )
    {
        cout << setw( 12 ) << array[ i ];

        if ( ( i + 1 ) % 4 == 0 ) // 4 numbers per row of output
            cout << endl;
    }

    if ( i % 4 != 0 )
        cout << endl;
}

// input vector contents
void inputVector( vector< int > &array )
{
    for ( size_t i = 0; i < array.size(); ++i )
        cin >> array[ i ];
}
```

```text
Size of vector integers1 is 7
vector after initialization:
0       0       0       0
0       0       0

Size of vector integers2 is 10
vector after initialization:
0       0       0       0
0       0       0       0
0       0

Enter 17 integers:
1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17

After input, the vectors contain:
integers1:
   1       2       3       4
   5       6       7
integers2:
   8       9      10      11
  12      13      14      15
  16      17

Evaluating: integers1 != integers2
integers1 and integers2 are not equal

Size of vector integers3 is 7
vector after initialization:
   1       2       3       4
   5       6       7

Assigning integers2 to integers1:
integers1:
   8       9      10      11
  12      13      14      15
  16      17
integers2:
   8       9      10      11
  12      13      14      15
  16      17

Evaluating: integers1 == integers2
integers1 and integers2 are equal

integers1[5] is 13

Assigning 1000 to integers1[5]
integers1:
   8       9      10      11
  12    1000      14      15
  16      17

Attempt to display integers1.at( 15 )
An exception occurred: invalid vector<T> subscript
```

*Fig. 15.14 | Demonstrating C++ Standard Library class template vector. (Part 4 of 4.)*

### Creating vector Objects

Lines 13–14 create two vector objects that store values of type int—integers1 contains seven elements, and integers2 has 10 elements. By default, all the elements of each vector object are set to 0. Note that vectors can be defined to store any data type, by replacing int in vector<int> with the appropriate data type. This notation, which specifies the type stored in the vector, is similar to the template notation that Section 15.13 introduced with function templates.

### vector Member Function size; Function outputVector

Line 17 uses vector member function size to obtain the size (i.e., the number of elements) of integers1. To invoke a member function, you access it with the dot (.) operator, just as you do with struct and union members. Line 19 passes integers1 to function outputVector (lines 88–102), which uses square brackets, [] (line 94), to obtain the value in each element of the vector for output. Note the resemblance of this notation to that used to access the value of an array element. Lines 22 and 24 perform the same tasks for integers2. Member function size of class template vector returns the number of elements in a vector as a value of type size_t (which represents the type unsigned int on many systems). As a result, line 90 declares the control variable i to be of type size_t, too. On some compilers, declaring i as an int causes the compiler to issue a warning message, since the loop-continuation condition (line 92) would compare a signed value (i.e., int i) and an unsigned value (i.e., a value of type size_t returned by function size).

### Function inputVector

Lines 28–29 pass integers1 and integers2 to function inputVector (lines 105–109) to read values for each vector’s elements from the user. The function uses square brackets [] to form lvalues that are used to store the input values in each vector element.

### Comparing vector Objects for Inequality

Line 40 demonstrates that vector objects can be compared with one another using the != operator. If the contents of two vectors are not equal, the operator returns true; otherwise, it returns false.

### Initializing One vector with the Contents of Another

The C++ Standard Library class template vector allows you to create a new vector object that is initialized with the contents of an existing vector. Line 45 creates a vector object integers3 and initializes it with a copy of integers1. This invokes vector’s so-called copy constructor to perform the copy operation. You’ll learn how to create copy constructors in Chapter 18. Lines 47–49 output the size and contents of integers3 to demonstrate that it was initialized correctly.

### Assigning vectors and Comparing for Equality

Line 53 assigns integers2 to integers1, demonstrating that the assignment (=) operator can be used with vector objects. Lines 55–58 output the contents of both objects to show that they now contain identical values. Line 63 then compares integers1 to integers2 with the equality (==) operator to determine whether the contents of the two objects are equal after the assignment in line 53 (which they are).

### Using the [] Operator to Access and Modify vector Elements

Lines 67 and 71 use square brackets ([]) to obtain a vector element as an rvalue and as an lvalue, respectively. An rvalue cannot be modified, but an lvalue can. As is the case with C-style pointer-based arrays, C++ does not perform any bounds checking when vector elements are accessed with square brackets. Therefore, you must ensure that operations using [] do not accidentally attempt to manipulate elements outside the bounds of the vector. Standard class template vector does, however, provide bounds checking in its member function at, which we use at line 79 and discuss shortly.

### 15.15.3 Exception Handling: Processing an Out-of-Range Index

An exception indicates a problem that occurs while a program executes. The name “exception” suggests that the problem occurs infrequently—if the “rule” is that a statement nor

### Summary of This Example

In this section, we demonstrated the C++ Standard Library class template vector, a robust, reusable class that can replace C-style pointer-based arrays. In Chapter 18, you'll see that vector achieves many of its capabilities by "overloading" C++'s built-in operators, and you'll learn how to customize operators for use with your own classes in similar ways. For example, we create an Array class that, like class template vector, improves upon basic array capabilities. Our Array class also provides additional features, such as the ability to input and output entire arrays with operators `>>` and `<<`, respectively.

## 15.16 Wrap-Up

In this chapter, you learned several of C++'s enhancements to C. We presented basic C++-style input and output with cin and cout and overviewed the C++ Standard Library header files. We discussed inline functions for improving performance by eliminating the overhead of function calls. You learned how to use pass-by-reference with C++'s reference parameters, which enable you to create aliases for existing variables. You learned that multiple functions can be overloaded by providing functions with the same name and different signatures; such functions can be used to perform the same or similar tasks, using different types or different numbers of parameters. We then demonstrated a simpler way of overloading functions using function templates, where a function is defined once but can be used for several different types. You learned the basic terminology of object technology and were introduced to the UML—the most widely used graphical representation scheme for modeling OO systems. In Chapter 16, you will learn how to implement your own classes and use objects of those classes in applications.

## Summary

### Section 15.2 C++

- C++ improves on many of C's features and provides object-oriented-programming (OOP; p. 582) capabilities that increase software productivity, quality and reusability.
- C++ was developed by Bjarne Stroustrup at Bell Labs and was originally called "C with classes."

### Section 15.3 A Simple Program: Adding Two Integers

- C++ filenames can have one of several extensions, such as `.cpp`, `.cxx` or `.C` (uppercase).
- C++ allows you to begin a comment with `//` and use the remainder of the line as comment text. C++ programmers may also use comments delimited by `/* and */`.
- The input/output stream header file `<iostream>` (p. 584) must be included for any program that outputs data to the screen or inputs data from the keyboard using C++-style stream input/output.
- As in C, every C++ program begins execution with function `main`. Keyword `int` to the left of `main` indicates that `main` "returns" an integer value.
- In C, you need not specify a return type for functions. However, C++ requires you to specify the return type, possibly `void`, for all functions; otherwise, a syntax error occurs.
- Declarations can be placed almost anywhere in a C++ program, but they must appear before their corresponding variables are used in the program.
- The standard output stream object (`std::cout`; p. 584) and the stream insertion operator (`<<`; p. 584) are used to display text on the screen.
