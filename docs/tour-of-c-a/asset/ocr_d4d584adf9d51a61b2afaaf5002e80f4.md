# # 3

# # Modularity

> > Mind your own business.
> Traditional

+   * Introduction
* Separate Compilation Header Files; Modules
* Namespaces
* Function Passing and Return Values Argument Passing; Value Return; Return Type Deduction; Suffix Return Type; Structured Binding
* Advice

# ## 3.1 Introduction

A C++ program consists of many separately developed parts, such as functions (1.2.1), defined types (Chapter 2), class hierarchies (5.5), and templates (Chapter 7). The key to managing a multitude of parts is to clearly define the interactions among those parts. The first and most important step is to distinguish between the interface to a part and its implementation. At the language level, C++ represents interfaces by declarations. A declaration specifies all that's needed to use a function or part.

Click here to view code image

```
double sqrt(double);    // The square root function takes a double and returns a double
```

```
class Vector {
public:
    Vector(int s); // Il what is needed to use a Vector
```