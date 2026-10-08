
## 2.5.8 What does the following program output and why?

```cpp
#include <iostream>
#include <cmath>
using namespace std;

int main() {
    int a = -1;
    unsigned int b = 0;
    if (a < b) {
        cout << "a is smaller\n";
    }
    else {
        cout << "a is bigger\n";
    }
    cout << "Because we're interpreting a to equal ";
    unsigned int castValue = (unsigned int)a;
    cout << castValue;
    cout << "\n";
}
```

## 2.5.9 Write the bell character to cout. If your computer loudspeaker is working, it should beep at you.

# 2.6 Summary

We have learned about the useful data types int, double, char, and bool. We have also learned some technical facts about other data types that we will not use often in this book.

We have learned how to cast between data types and the potential pitfalls.

We have learned about various C++ operators, including arithmetic operators, comparison operators, logical operators, and assignment operators.

We have learned the extreme importance of enabling compiler warnings. If you do not do this, you will write bugs that take you an eternity to find.

# Chapter 3 Functions

A function in C++ is a piece of code that you can call to perform some task. We have already seen the function `pow` that raises one number to a given power. The cmath library (`http://www.cplusplus.com/reference/cmath/`) contains various other mathematical functions.

As we shall see, functions in C++ are used for much more than just computing mathematical formulae. In C++ all software should be divided into functions, each of which performs a particular task. One builds up complex functions by calling simpler functions. For example, you will write a `blackScholesCallPrice` function which will price a Call option using the Black-Scholes formula (Equation (A.6)). This in turn will call a `normcdf` function to compute the cumulative distribution function of the normal distribution.

On a larger scale, a bank's trading system will contain a function to value the bank's portfolio. This will call functions to: read the current trading position from a database; extract current market data from some source such as Bloomberg or Reuters; price the many different types of traded product. Each of these tasks is itself very complex and is coded by breaking it down into lots of small specialist functions.

In the introduction to this book we discussed the need to write scalable and maintainable programs. One of the key ingredients is the technique of breaking a problem into simpler pieces, each represented by its own function.

## 3.1 The C++ function syntax

Consider the mathematical function:

$compoundInterest : \mathbb{R} \times \mathbb{R} \times \mathbb{Z} \rightarrow \mathbb{R}$

given by

$compoundInterest(P, i, n) = P (1 + i/100)^n - P.$

Here *P* is the principal, *i* is the annual percentage rate, and *n* is the number of years. To formally specify a mathematical function, you need to provide the domain and the codomain as well as the formula to use.

One provides very similar information when writing a C++ function. First one gives the name of the function and describes the type of data it can be applied to and the type of data it returns. Next one specifies the actual formulae needed for the function.

In C++ one would write the **compoundInterest** function as follows.

```cpp
double compoundInterest(double P, double i, int n) {
    double interest = P * pow(1 + 0.01*i, n) - P;
    return interest;
}
```

On the first line we first provide the type of data the function computes. In this case it computes a *double*. Next we give the name of the function. In this case the name is **compoundInterest**. We then list the names of all the parameters and their types. In this example we have said that the name of the function is **compoundInterest**. We have said that it takes 3 parameters named $P$, $i$ and $n$. We have said that the variable $P$ is of type *double*. $i$ is also of type *double* and $n$ is an integer.

The actual code for the function is written between a pair of curly brackets. You can write any collection of statements you like inside the curly brackets—perhaps assigning several variables and some *if* statements, for example. When the computation is complete, the code uses the **return** keyword to say what the result of the computation is.

In summary, the syntax for defining a function is:

```cpp
ReturnType functionName( ParameterType1 parameterName1,
                        ParameterType1 parameterName2,
                        ...
                        ParameterTypeN parameterNameN ) {
    ... statements ...
}
```

In any code written after this function has been defined, you can just call the function exactly as though it was a built in function like *sin* or *pow*. So for example we can rewrite our first example program as follows:

```cpp
#include <iostream>
#include <cmath>
using namespace std;

double compoundInterest(double P, double i, int n) {
    double interest = P * pow(1 + 0.01*i, n) - P;
    return interest;
}

int main() {
    int principal;
    double interestRate;
    int numberOfYears;
    cout << "How much are you investing ?\n";
    cin >> principal;
    cout << " What’s the annual interest rate(%)?\n";
    cin >> interestRate;
    cout << "How long for ( years )?\n";
    cin >> numberOfYears;
    double interest
        = compoundInterest(principal,
            interestRate,
        numberOfYears);
    cout << "You will earn ";
    cout << interest;
    cout << "\n";
    return 0;
}
```

In this example, we have replaced the computation of the compound interest with a call to the compoundInterest function.

Note that the file contains two function definitions, one for a function called compoundInterest and another for a function called main. In fact our very first program contained a function called main as well, we just didn’t discuss it at the time.

Every C++ application for the “console” must contain a function called main. A console application is just a program that reads and writes text to the screen as though it was still 1973. When the user asks to run your program, the operating system will make sure that the function main is called. There are many other kinds of applications, for example, web applications, windows applications, and mobile phone apps. If you’re writing a console application, you need a main function. The rules for other kinds of application are different and beyond the scope of this book.

Here are some things to notice in our example:

- The definitions of the functions are written sequentially in the file. We first define compoundInterest completely, then we define main completely.
- The variable names used when we call the function can be completely different from those used in the definition of the function. When we choose the names of parameters and variables in a function, those names have no meaning outside of the function.
- There is a return statement at the end of each function. When a function has computed the desired value, it sends it back to the caller using the return keyword.

What does using a function actually buy us? In this case, the code is a little bit longer than it was before, but does precisely the same thing. So what are the advantages?

- Reuse. Every time we want to compute compound interest, we can simply call the **compoundInterest** function. We never have to write it again.
- Division of labour. The person who writes the main body of the code only has to be an expert in asking the user for input and output. They don’t need to understand how **compoundInterest** is actually computed to write the main chunk of code. If you scale this up to an iPad user interface to price a knock-out option, you realise why you might need to divide the task between different team members.
- Modularity. We have broken our problem into distinct simpler pieces. Just as a theorem is easier to follow when broken into lemmas, a program is easier to understand when broken down into functions.
- Testability. In Chapter 6 we’ll see how using functions makes our code easier to test.

# Tip: Once and only once

You should never write the same code twice. If you want to perform the same task twice, write a function that carries out that task.

A good programmer will avoid using cut and paste. If you copy code from one place to another, you are just increasing the number of lines of code in your program and hence increasing the amount of code you will need to debug.

**Example 1:** Write a function to compute the kinetic energy of a body of given mass and velocity using the formula: *E* = 1/2 *mv*².

*Solution:*

```cpp
double kineticEnergy(double mass, double velocity) {
    return 0.5 * mass * velocity * velocity;
}
```

As this example demonstrates, you can return complex expressions as well as the value of a single variable.

One thing to observe is that this function doesn’t print anything using **cout**. Instead it quietly returns the answer using **return**. Using **cout** to print things is great for your first few programs, but we now want to start writing functions that operate silently. As an example, consider the built-in function
