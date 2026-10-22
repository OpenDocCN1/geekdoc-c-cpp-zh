
## Feedback

We welcome your constructive input—both the negative and the positive. We worked very hard to bring you what we hope you’ll find to be an excellent book. However, at some point we had to stop writing, reviewing, and tweaking so we could “release the product.” You may therefore find errors, inconsistencies, and presentations that could be improved, or topics that are missing altogether. Your feedback gives us a chance to inform all readers through the book’s Web site and to improve any subsequent editions.

The best way to reach us is by email. You will find the email address at the Web site of this book: http://www.tmplbook.com Please, be sure to check the book’s Web site for the currently known errata before submitting reports. Many thanks.

> ¹ Note that in C++, a type definition defines a “type alias” rather than a new type (see Section 2.8 on page 38).

For example:

```
typedef int Length; // define Length as an alias for int
int i = 42;
Length l = 88;
i = l; // OK
l = i; // OK
```

> ² The committee now aims at issuing a new standard roughly every 3 years. Clearly, that leaves less time for massive additions, but it brings the changes more quickly to the broader programming community. The development of larger features, then, spans time and might cover multiple standards.

## Part I
## The Basics

This part introduces the general concepts and language features of C++ templates. It starts with a discussion of the general goals and concepts by showing examples of function templates and class templates. It continues with some additional fundamental template features such as nontype template parameters, variadic templates, the keyword `typename`, and member templates. Also it discusses how to deal with move semantics, how to declare parameters, and how to use generic code for compile-time programming. It ends with some general hints about terminology and regarding the use and application of templates in practice both as application programmer and author of generic libraries.

## Why Templates?

C++ requires us to declare variables, functions, and most other kinds of entities using specific types. However, a lot of code looks the same for different types. For example, the implementation of the algorithm *quicksort* looks structurally the same for different data structures, such as arrays of `int`s or vectors of strings, as long as the contained types can be compared to each other.

If your programming language doesn’t support a special language feature for this kind of genericity, you only have bad alternatives: 1. You can implement the same behavior again and again for each type that needs this behavior. 2. You can write general code for a common base type such as `Object` or `void*`. 3. You can use special preprocessors.

If you come from other languages, you probably have done some or all of this before. However, each of these approaches has its drawbacks: 1. If you implement a behavior again and again, you reinvent the wheel. You make the

2. If you write general code for a common base class, you lose the benefit of type checking. In addition, classes may be required to be derived from special base classes, which makes it more difficult to maintain your code.

3. If you use a special preprocessor, code is replaced by some “stupid text replacement mechanism” that has no idea of scope and types, which might result in strange semantic errors. Templates are a solution to this problem without these drawbacks. They are functions or classes that are written for one or more types not yet specified. When you use a template, you pass the types as arguments, explicitly or implicitly. Because templates are language features, you have full support of type checking and scope.

In today’s programs, templates are used a lot. For example, inside the C++ standard library almost all code is template code. The library provides sort algorithms to sort objects and values of a specified type, data structures (also called *container classes*) to manage elements of a specified type, strings for which the type of a character is parameterized, and so on. However, this is only the beginning. Templates also allow us to parameterize behavior, to optimize code, and to parameterize information. These applications are covered in later chapters. Let’s first start with some simple templates.

## Chapter 1
## Function Templates

This chapter introduces function templates. Function templates are functions that are parameterized so that they represent a family of functions.

### 1.1 A First Look at Function Templates

Function templates provide a functional behavior that can be called for different types. In other words, a function template represents a family of functions. The representation looks a lot like an ordinary function, except that some elements of the function are left undetermined: These elements are parameterized. To illustrate, let’s look at a simple example.

### 1.1.1 Defining the Template

The following is a function template that returns the maximum of two values:

Click here to view code image

basics/max1.hpp

```
template<typename T>
T max (T a, T b)
{
// if b < a then yield a else yield b
return b < a ? a : b;
}
```

This template definition specifies a family of functions that return the maximum of two values, which are passed as function parameters a and b.¹ The type of these parameters is left open as template parameter T. As seen in this example, template parameters must be announced with syntax of the following form:

Click here to view code image

```
#include "max1.hpp"
#include <iostream>
#include <string>
int main()
{
  int i = 42;
  std::cout << "max(7,i): " << ::max(7,i) << '\n';

  double f1 = 3.4; double f2 = -6.7;
  std::cout << "max(f1,f2): " << ::max(f1,f2) << '\n';

  std::string s1 = "mathematics", std::string s2 = "math";
  std::cout << "max(s1,s2): " << ::max(s1,s2) << '\n';
}
```

Inside the program `max()` is called three times: once for two ints, once for two doubles, and once for two `std::strings`. Each time, the maximum is computed. As a result, the program has the following output: [Click here to view code image](#)

```
max(7,i): 42
max(f1,f2): 3.4
max(s1,s2): mathematics
```

Note that each call of the `max()` template is qualified with `::`. This is to ensure that our `max()` template is found in the global namespace. There is also a `std::max()` template in the standard library, which under some circumstances may be called or may lead to ambiguity.

Templates aren’t compiled into single entities that can handle any type. Instead, different entities are generated from the template for every type for which the template is used. Thus, `max()` is compiled for each of these three types. For example, the first call of `max()`

```
int i = 42;
max(7,i);
```

uses the function template with `int` as template parameter T. Thus, it has the semantics of calling the following code: `int max (int a, int b)`

```
{
  return b < a ? a : b;
}
```

The process of replacing template parameters by concrete types is called *instantiation*. It results in an *instance* of a template.

Note that the mere use of a function template can trigger such an instantiation process. There is no need for the programmer to request the instantiation separately.

Similarly, the other calls of `max()` instantiate the `max` template for `double` and `std::string` as if they were declared and implemented individually:

[Click here to view code image](#)

```
double max (double, double);
std::string max (std::string, std::string);
```

Note also that `void` is a valid template argument provided the resulting code is valid. For example: [Click here to view code image](#)

```
template<typename T>
T foo(T*)
{
}
```

```
void* vp = nullptr;
foo(vp); // OK: deduces void foo(void*)
```

### 1.1.3 Two-Phase Translation

An attempt to instantiate a template for a type that doesn’t support all the operations used within it will result in a compile-time error. For example: [Click here to view code image](#)

```
std::complex<float> c1, c2; // doesn’t provide operator <
...
::max(c1,c2); // ERROR at compile time
```

Thus, templates are “compiled” in two phases: 1. Without instantiation at *definition time*, the template code itself is checked for correctness ignoring the template parameters. This includes:

- Syntax errors are discovered, such as missing semicolons.
- Using unknown names (type names, function names, …) that don’t depend on template parameters are discovered.
- Static assertions that don’t depend on template parameters are checked.

2. At *instantiation time*, the template code is checked (again) to ensure that all code is valid. That is, now especially, all parts that depend on template parameters are double-checked.

For example:

**[Click here to view code image](#)**

```
template<typename T>
void foo(T t)
```
