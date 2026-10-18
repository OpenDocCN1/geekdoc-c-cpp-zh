Sometimes, the default arguments may be used instead of overloading. This may reduce the number of functions to be defined.

Overloaded functions are extensively used for handling class objects. They will be illustrated later when the classes are discussed in the next chapter.

# 4.11 Friend and Virtual Functions

C++ introduces two new types of functions, namely, friend function and virtual function. They are basically introduced to handle some specific tasks related to class objects. Therefore, discussions on these functions have been reserved until after the class objects are discussed. The friend functions are discussed in Sec. 5.15 of the next chapter and virtual functions in Sec. 9.5 of Chapter 9.

# 4.12 Math Library Functions

The standard C++ supports many math functions that can be used for performing certain commonly used calculations. Most frequently used math library functions are summarized in Table 4.1.

**Table 4.1** *Commonly used math library functions*

![](bbox=[0.138, 0.709, 0.204, 0.761])

> **NOTE:** *The argument variables **x** and **y** are of type **double** and all the functions return the data type **double**.*

To use the math library functions, we must include the header file **math.h** in conventional C++ and **cmath** in ANSI C++.

# Program 4.6