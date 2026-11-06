
## Outline

- 1. **6.1 Introduction**
- 2. **6.2 Program Components in C++**
- 3. **6.3 Math Library Functions**
- 4. **6.4 Function Prototypes**
- 5. **6.5 Function-Prototype and Argument-Coercion Notes**
  - **6.5.1 Function Signatures and Function Prototypes**
  - **6.5.2 Argument Coercion**
  - **6.5.3 Argument-Promotion Rules and Implicit Conversions**
- 6. **6.6 C++ Standard Library Headers**
- 7. **6.7 Case Study: Random-Number Generation**
  - **6.7.1 Rolling a Six-Sided Die**
  - **6.7.2 Rolling a Six-Sided Die 60,000,000 Times**
  - **6.7.3 Randomizing the Random-Number Generator with srand**
  - **6.7.4 Seeding the Random-Number Generator with the Current Time**
  - **6.7.5 Scaling and Shifting Random Numbers**
- 8. **6.8 Case Study: Game of Chance; Introducing Scoped enums**
- 9. **6.9 C++11 Random Numbers**
- 10. **6.10 Scope Rules**
- 11. 6.11 Function-Call Stack and Activation Records
- 12. 6.12 Inline Functions
- 13. 6.13 References and Reference Parameters
- 14. 6.14 Default Arguments
- 15. 6.15 Unary Scope Resolution Operator
- 16. 6.16 Function Overloading
- 17. 6.17 Function Templates
- 18. 6.18 Recursion
- 19. 6.19 Example Using Recursion: Fibonacci Series
- 20. 6.20 Recursion vs. Iteration
- 21. 6.21 Wrap-Up

- 1. Summary
- 2. Self-Review Exercises
- 3. Answers to Self-Review Exercises
- 4. Exercises
- 5. Making a Difference

## 6.1 Introduction

In this chapter, we take a deeper look at functions. Most computer programs that solve real-world problems are much larger than the programs presented in the first few chapters of this book. Experience has shown that the best way to develop and maintain large programs is to construct them from small, simple pieces, or components. This technique is called **divide and conquer**.

We’ll overview a portion of the C++ Standard Library’s math functions. We’ll introduce function prototypes and discuss how the compiler uses them, if necessary, to convert the type of an argument in a function call to the type specified in a function’s parameter list.

Next, we’ll take a brief diversion into simulation techniques with random number generation and develop a version of a popular casino dice game that uses most of the programming techniques you’ve learned.

We then present C++’s scope rules, which determine where identifiers can be referenced in a program. You’ll learn how C++ keeps track of which function is currently executing, how parameters and other local variables of functions are maintained in memory and how a function knows where to return after it completes execution. We discuss topics that help improve program performance—inline functions that can eliminate the overhead of a function call and reference parameters that can be used to pass large data items to functions efficiently.

Many of the applications you develop will have more than one function of the same name. This technique, called function overloading, is used to implement functions that perform similar tasks for arguments of different types or different numbers of arguments. We consider function templates—a mechanism for concisely defining a family of overloaded functions. The chapter concludes with a discussion of functions that call themselves, either directly, or indirectly (through another function)—a topic called recursion.

## 6.2 Program Components in C++

C++ programs are typically written by combining “prepackaged” functions and classes available in the C++ Standard Library with new functions and classes you write. The C++ Standard Library provides a rich collection of functions for common mathematical calculations, string manipulations, character manipulations, input/output, error checking and many other useful operations.

Functions allow you to modularize a program by separating its tasks into self-contained units. You’ve used a combination of library functions and your own functions in almost every program you’ve written.

There are several motivations for modularizing a program with functions:

- Software reuse. For example, in earlier programs, we did not have to define how to read a line of text from the keyboard—C++ provides this capability via the `getline` function of the `<string>` header.
- Avoiding code repetition.
- Dividing a program into meaningful functions makes the program easier to test, debug and maintain.

### Observation 6.1

*To promote software reusability, every function should be limited to performing a single, well-defined task, and the name of the function should express that task effectively.*

As you know, a function is invoked by a function call, and when the called function completes its task, it either returns a *result* or simply returns *control* to the caller. An analogy to this program structure is the hierarchical form of management ([Figure 6.1](#)).

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_702_0.png)

**Fig. 6.1 Hierarchical boss-function/worker-function relationship.**

A boss (similar to the calling function) asks a worker (similar to a called function) to perform a task and report back (i.e., return) the results after completing the task. The boss function does *not* know how the worker function performs its designated tasks. The worker may also call other worker functions, unbeknownst to the boss. This *hiding of implementation details* promotes good software engineering. **Figure 6.1** shows the `boss` function communicating with several worker functions. The `boss` function divides the responsibilities among the `worker` functions, and `worker1` acts as a “boss function” to `worker4` and `worker5`. The relationship does not need to be hierarchical, but often it is, which makes it easier to test, debug, update and maintain programs.

## 6.3 Math Library Functions

Some functions, such as `main`, are **not** members of a class. These functions are called **global functions**. We introduce various functions from the `<cmath>` header here to present the concept of global functions that do not belong to a particular class.

The `<cmath>` header provides a collection of functions that perform common mathematical calculations. For example, you can calculate the square root of `900.0` with the function call

```cpp
sqrt(900.0);
```

This expression evaluates to `30.0`. Function `sqrt` takes an argument of type `double` and returns a `double` result. There’s no need to create any objects before calling function `sqrt`. Also, *all* functions in the `<cmath>` header are *global functions*—therefore, each is called simply by specifying the name of the function followed by parentheses containing the function’s arguments.

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_704_0.png)

### Error-Prevention Tip 6.1

*Do not call `sqrt` with a negative argument. For industrial-strength code, always check that the arguments you pass to math functions are valid.*

Function arguments may be constants, variables or more complex expressions. If `c = 13.0`, `d = 3.0` and `f = 4.0`, then the statement

```cpp
cout << sqrt(c + d * f) << endl;
```

displays the square root of `13.0 + 3.0 * 4.0 = 25.0`—namely, `5.0`. Some math library functions are summarized in **Fig. 6.2**. In the figure, the variables `x` and `y` are of type `double`.

**Fig. 6.2 Math library functions.**

| Function | Description | Example |
|---|---|---|
| `ceil(x)` | rounds *x* to the smallest integer not less than *x* | `ceil(9.2)` is `10.0`<br>`ceil(-9.8)` is `-9.0` |
| `cos(x)` | trigonometric cosine of *x* (*x* in radians) | `cos(0.0)` is `1.0` |
| `exp(x)` | exponential function *e*<sup>*x*</sup> | `exp(1.0)` is `2.718282`<br>`exp(2.0)` is `7.389056` |
| `fabs(x)` | absolute value of *x* | `fabs(5.1)` is `5.1`<br>`fabs(0.0)` is `0.0`<br>`fabs(-8.76)` is `8.76` |
| `floor(x)` | rounds *x* to the largest integer not greater than *x* | `floor(9.2)` is `9.0`<br>`floor(-9.8)` is `-10.0` |
| `fmod(x, y)` | remainder of *x/y* as a floating-point number | `fmod(2.6, 1.2)` is `0.2` |
| `log(x)` | natural logarithm of *x* (base *e*) | `log(2.718282)` is `1.0`<br>`log(7.389056)` is `2.0` |
| `log10(x)` | logarithm of *x* (base 10) | `log10(10.0)` is `1.0`<br>`log10(100.0)` is `2.0` |
| `pow(x, y)` | *x* raised to power *y* (*xʸ*) | `pow(2, 7)` is `128`<br>`pow(9, .5)` is `3` |
| `sin(x)` | trigonometric sine of *x* (*x* in radians) | `sin(0.0)` is `0` |
