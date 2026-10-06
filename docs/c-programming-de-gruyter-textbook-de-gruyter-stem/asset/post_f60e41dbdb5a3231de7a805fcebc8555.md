
# 3 Functions

from the same company, if they are in different versions, provide different system functions. So programmers must consult the manual of the system library or the online help of the compiler, to check the functionality, parameters, return value, and usage of system functions.

Make clear which header file contains the declaration of the system function you want to use. This can also be found in the manual of the system library or in the online help.

For example, the way to find the category list of system functions of VC++6.0 from MSDN Visual Studio 6.0 is: First select "Visual C++ Documentation" in "Activity Subset"; then go through the following path: Visual C++ Documentation -> Using Visual C++ -> C++ Programmer's Guide -> Run-Time Library Reference -> Run-Time Routines by Category -> Run-Time Routines by Category, The helping system lists the functions in the following groups: as shown in Figure 3.6.

- Argument access
- Floating-point support
- Buffer manipulation
- Input and output
- Byte classification

![](img/5618306d085ac1bac8275d6c4c5bbf2a_125_0.png)

Fig. 3.6: MSDN Library in Visual Studio 6.0.

- Internationalization
- Character classification
- Memory allocation
- Data conversion
- Process and environment control
- Debugging
- Searching and sorting
- Directory control
- String manipulation
- Error handling
- System calls
- Exception handling
- Time management
- File handling

# 3.6 Summary

In-oriented programming, the function is the basic unit of functionality abstraction.

A complex system usually needs to be divided into several subsystems, which then are developed and debugged separately. Subprograms are embodied as functions in C++. The abstraction of objects is also implemented through functions. Functions can be reused once completed. We can use a function only knowing its behavior and usage, without the development efficiency and the reliability of the program can be improved, without the need to know its implementation. In this way, codes can be reused, and collaboration, modification, and maintenance can be realized more easily.

C++ modification may consist of a main function and several subfunctions. The main function is the entry point of the program execution. The main function may call sub-functions, and subfunctions may call other subfunctions.

Function overloading allows functions with similar operations to share the same name. It is easy to use and can make the code more readable. The overloaded functions are discriminated by their formal parameters, and functions with the same name must have differences in the number of parameters or in the types of parameters, or in both.

In addition, the C++ system library provides hundreds of functions for programmers to use. The declarations of system function prototypes have all been provided in the C++ system library, which sorts and stores them in different header files. Programs need to use include to embed the related files into their code, and then they can use the system functions.

# Exercises

3.1 What is a function in C++? What is a calling function, and what is a called function? What is the relationship between them? How does one make a function call?

3.2 Look at the running result of the following program. Is there any difference between what you presumed? Think over the usage of references.

Source code:

```
#include <iostream>
using namespace std;
int main() {
    int intOne;
    int &rSomeRef = intOne;

    intOne = 5;
    cout << "&intOne:\\t" << intOne << endl;
    cout << "&rSomeRef:\\t" << rSomeRef << endl;
    cout << "&intOne:\\t" << &intOne << endl;
    cout << "&rSomeRef:\\t" << &rSomeRef << endl;

    int intTwo = 8;
    rSomeRef = intTwo; //not what you think!
    cout << "\intOne:\\t" << intOne << endl;
    cout << "&intTwo:\\t" << intTwo << endl;
    cout << "&rSomeRef:\\t" << rSomeRef << endl;
    cout << "&intOne:\\t" << &intOne << endl;
    cout << "&intTwo:\\t" << &intTwo << endl;
    cout << "&rSomeRef:\\t" << &rSomeRef << endl;
}
```

3.3 Compare Call-by-Value and Call-by-Reference, and list their similarities and differences.

3.4 What is an inline function? What are its characteristics?

3.5 Must the following three names be the same: the formal parameter name in the function prototype, the formal parameter name in the function definition, and the actual parameter name in the function call?

3.6 How does one differentiate overloaded functions?

3.7 Write a function that contains two unsigned short int parameters. When the second parameter is nonzero, it returns the result of the first parameter dividing by the second parameter, and the result is of the short int type; otherwise, it returns -1. Realize input and output in the main function.

3.8 Write a function to convert Fahrenheit degrees to Celsius degrees. The formula is: C = (F - 32) * 5/9. In the main function, prompt users to input a Celsius degree, convert it into the corresponding Fahrenheit degree, and output the result.

3.9 Write a function to judge whether a number is prime or not. Realize input and output in the main function.

3.10 Write a function to get the greatest common divisor and the least common multiple of two integers.

3.11 What is a nested call? What is a recursive call?

3.12 Input an integer n in the main function, and write a function to calculate 1 + 2 + ... + n in a recursive way.

3.13 Write a recursive function Power(int x, int y) to calculate the y-th power of x. Realize input and output in the main function.

3.14 Write a function to calculate Fibonacci numbers in a recursive way.

fib(n) = fib(n-1) + fib(n-2), n > 2 ; fib(1) = fib(2) = 1

Observe the procedure of making a recursive call.

3.15 Write a function to calculate the n-th Legendre Polynomial in a recursive way. Realize input and output in the main function. The recursion formula of the n-th Legendre Polynomial is:

```
p_n(x) = \begin{cases} 1 & (n = 0) \\ x & (n = 1) \\ ((2n-1) \times x \times p_{n-1}(x) - (n-1) \times p_{n-2}(x))/n & (n > 1) \end{cases}
```

# 4 Class and Object

Everything in the real world we are familiar with is an object. Objects can not only be visible, as houses, cars, airplanes, animals and plants, but also be invisible, as a plan. Objects can be a simple unit, like a person; and they can also be a combination of several objects; for example, there are multiple departments in a company, and each department has staff members. A class can be formed based on common attributes abstracted from similar objects. These are the concepts and methods we are familiar with the real world. The aim of programming is to describe and solve problems in the real world, the first step is to describe objects and classes faithfully in programs. C++, an object-oriented programming language, supports this kind of abstraction. A class in C++ is formed by the encapsulation of abstracted data and functions.

In this chapter, we will first introduce the main features of object-oriented design: abstraction, encapsulation, and polymorphism. We then focus on the core concept of object-oriented design – class, which includes how to define and implement a class, and how to use classes to solve problems.

# 4.1 Basic Features of Object-Oriented Design

## 4.1.1 Abstraction

As a fundamental way to understand problems, abstraction is not new to us. Abstraction in the object-oriented method is a procedure in which specific issues (objects) are summarized and abstracted into the common attributes of a class of objects; it also includes the procedure of describing these attributes. The procedure of abstraction is also a procedure of analyzing and understanding problems. In the development of object-oriented software, we should find the specific procedure to solve it. Generally, the abstraction of a problem includes two types: abstraction of data and abstraction of behavior (or code). The former describes the attributes or states of a class of objects, i.e., the characteristics used to distinguish this class of objects from other classes; the latter describes the common behavior or functional characteristics of a class of objects.

Let us see two simple examples: first we implement a simple clock program on a computer. From the analysis of the clock can we see that we need three integers to store time, which represent the hour, minute, and second respectively. This is an abstraction of the data that a clock possesses. In addition, a clock needs some simple functions, such as time display and time setup. This is an abstraction of the behavior of the clock. Using variables and functions in C++, we can describe the abstracted attributes of a clock like:

https://doi.org/10.1515/9783110471977-004
