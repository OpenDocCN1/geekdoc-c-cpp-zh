and how a function knows where to return after it completes execution. We discuss two topics that help improve program performance—inline functions that can eliminate the overhead of a function call and reference parameters that can be used to pass large data items to functions efficiently.

Many of the applications you develop will have more than one function of the same name. This technique, called function overloading, is used by programmers to implement functions that perform similar tasks for arguments of different types or possibly for different numbers of arguments. We consider function templates—a mechanism for defining a family of overloaded functions. The chapter concludes with a discussion of functions that call themselves, either directly, or indirectly (through another function)—a topic called recursion.

# 6.2 Program Components in C++

C++ programs are typically written by combining new functions and classes you write with “prepackaged” functions and classes available in the C++ Standard Library. In this chapter, we concentrate on functions.

The C++ Standard Library provides a rich collection of functions for performing common mathematical calculations, string manipulations, character manipulations, input/output, error checking and many other useful operations. This makes your job easier, because these functions provide many of the capabilities programmers need. The C++ Standard Library functions are provided as part of the C++ programming environment.

# Software Engineering Observation 6.1

> Read the documentation for your compiler to familiarize yourself with the functions and classes in the C++ Standard Library.

# 6.3 Math Library Functions

As you know, a class can provide member functions that perform the services of the class. For example, in Chapters 3–5, you have called the member functions of various versions of a GradeBook object to display the GradeBook’s welcome message, to set its course name, to obtain a set of grades and to calculate the average of those grades.

Sometimes functions are not members of a class. Such functions are called global functions. Like a class’s member functions, the function prototypes for global functions are placed in header files, so that the global functions can be reused in any program that includes the header file and that can link to the function’s object code. For example, recall that we used function pow of the <cmath> header file to raise a value to a power in Figure 5.6. We introduce various functions from the <cmath> header file here to present the concept of global functions that do not belong to a particular class. In this chapter and in subsequent chapters, we use a combination of global functions (such as main) and classes with member functions to implement our example programs.

The <cmath> header file provides a collection of functions that enable you to perform common mathematical calculations. For example, you can calculate the square root of 900.0 with the function call

```
sqrt( 900.0 )
```