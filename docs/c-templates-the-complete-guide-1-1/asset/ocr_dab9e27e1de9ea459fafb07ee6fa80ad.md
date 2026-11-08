becomes a run-time error because for C-strings, `max(a, b)` creates a new, temporary local value that is returned by reference, but that temporary value expires as soon as the return statement is complete, leaving a dangling reference. Unfortunately, the error is quite subtle and may not manifest itself in all cases.

Note: in contrast, the first call to `max()` in `main()` doesn't suffer from the same issue. These temporaries are created for the arguments (7, 42, and 68), but those temporaries are created in `main()` where they persist until the statement is done.

This is only one example of code that might behave differently than expected as a result of the overloaded resolution rules. In addition, ensure that all overloaded versions of a function are declared before the function is called. This is because the fact that all overloaded functions are visible when a corresponding function call is made may matter. For example, defining a three-argument version of `max()` without having seen the declaration of a special two-argument version of `max()` for `int` causes the two-argument template to be used by the three-argument version.

`basics/max.cpp`

# Click here to view code image

```
```cpp
#include <iostream>

// maximum of two values of any type:
template<typename T>
T max (T a, T b)
{
    std::cout << "max(T,T) \\n";
    return b < a ? a : b;
}

// maximum of three values of any type:
template<typename T>
T max (T a, T b, T c)
{
    return max(max(a,b), c);        // use the two-argument version
                                      // because the two-argument
                                      // is too late!
}

// maximum of two int values:
int max (int a,
         int b)
{
    std::cout << "max(int,int) \\n";
    return b < a ? a : b;
}

int main()
{
    max(7, 42, 68); // error: case max(T,T) isn't instantiated
}
```
```

We discuss details in Section 13.2 on page 317.

# 1.6. BUT, SHOULDN'T WE ...?

Probably, even these simple function template examples might raise fair questions. Three questions are probably so common that we should discuss them here briefly.

# 1.6.1 Pass by Value or by Reference?

You might wonder, why in general declare the functions to pass the arguments by value instead of using references. In general, passing by reference is recommended for types other than those that have only one value type such as `std::string_view`, because unnecessary copies are created.

However, for an example of reasons, passing by value in general is often better.