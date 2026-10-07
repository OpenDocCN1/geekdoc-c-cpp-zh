# 8.2 std::filesystem

TODO:

# Further Readings

# Chapter 09 Minor Features

# 9.1 New Type

long long int

long long int is not the first to be introduced in C++11. In fact, as early as C99, long long int has been included in the C standard, so most compilers already support it. C++11 formally incorporate it into the standard library, specifying a long long int type with at least 64 bits.

# 9.2 noexcept and Its Operations

One of the big advantages of C++ over C is that C++ itself defines a complete set of exception handling mechanisms. However, before C++11, almost no one used to write an exception declaration after the function name. Starting from C++11, this mechanism was deprecated, so we will not discuss or introduce the previous mechanism. How to work and how to use it, you should not take the initiative to understand it.

C++11 simplifies exception declarations into two cases:

+   1. The function may throw any exceptions
2. The function can't throw any exceptions

And use noexcept to limit these two behaviors, for example:

```
void may_throw();      // May throw any exception
void no_throw() noexcept; // Cannot throw any exception
```

If a function is modified with noexcept, the compiler will use std::terminate() to immediately terminate the program.

noexcept can also be used as an operator to manipulate an expression. When the expression has no exception, it returns true, otherwise it returns false.

```
#include <iostream>
void may_throw() {
    throw;
```