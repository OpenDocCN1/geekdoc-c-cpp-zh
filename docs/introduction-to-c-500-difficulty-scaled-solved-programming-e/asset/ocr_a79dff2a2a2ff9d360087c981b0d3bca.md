# 494 Introduction to C++

One problem that may occur when writing a template that you don't know what type to use in a declaration. Let's change f() to assign the sum of its arguments to a variable:

```
template <typename T1, typename T2> void f(T1 a, T2 b)
{
    auto sum = a+b;
    ...
}
```

What will be the type of sum? Since we do not know in advance how f() will be used we cannot specify the type. If T1 is double and T2 is int, sum must be declared as double. However, if T1 is short and T2 is int, sum must be declared as int. One way to solve this problem is to use the auto specifier. Alternatively, we can use the decltype specifier. For example:

```
template <typename T1, typename T2> void f(T1 a, T2 b)
{
    decltype(a+b) sum;
    sum = a+b;
}
```

The type of sum becomes the same as that of a+b.
The next question is, and what if the function template returns a value whose type depends on the arguments? For example, what should be the return type in case we want to modify the function and return sum? As before, we cannot specify the return type since we do not know which type of arguments will be passed to f(). The solution is to use the auto specifier as we saw in Chapter 11, when we discussed deduction of return types. See the program:

```
#include <iostream> // Example 16.14
template <typename T1, typename T2>
auto f(T1 a, T2 b)
{
    auto sum = a+b;
    return sum;
}

int main()
{
    int a = 1;
    double b = 2.3;

    auto c = f(a, b);
    std::cout << c << c << "\n";
    return 0;
}
```

The word auto is put in the place of the return type. Absolutely fantastic, what a nice feature is the return type deduction! The type will be deduced from the type of sum when the function is called. Thus, the return type becomes double and the program displays 3.3.