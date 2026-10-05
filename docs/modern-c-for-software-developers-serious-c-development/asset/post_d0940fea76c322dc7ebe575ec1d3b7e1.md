
```cpp
int y = 5;
if (auto x = test(y); x != -1)
    std::cout << "x = " << x << std::endl;
else
    std::cout << "x = " << x << std::endl;
```

```cpp
// output
x = 1
```

**Note:** Compound initialization is prohibited:

```cpp
if (int y = -2; auto x = test(y); x + y != -1) {....} // error
```

## Switch Statement With Initialization

Using an initialization clause in a switch statement allows us to initialize a variable for the scope of the switch:

```cpp
#include <iostream>
int test(int x)
{
    if (x == 0) return 0;
    else if (x > 1) return 1;
    else if (x <= 1) return -1;
    return 0;
}
int main()
{
    switch(int x = -5; x = test(x))
    {
    case -1:
        std::cout << "switch = " << -1 << std::endl;
        break;
    case 1:
        std::cout << "switch = " << 1 << std::endl;
        break;
    default:
        std::cout << "switch = " << 0 << std::endl;
    }
}
```

```cpp
// output
switch = -1
```

## Modern C++: Inline Variables (C++17)

One of the best features of C++ is its support for header-only libraries. In a header-only library, the header definitions as well as the implementation are all contained in a single header file. However, up to C++17, a header only library could not be created if the library had global variables or objects. This restriction was a consequence of the one definition rule.

According to the one definition rule (ODR), a variable or entity must be defined only once. That is, the variable must be defined in only one translation unit. Thus if a header-only library defines a global variable, then this global variable will be included in all of the implementation files (.cpp) that include the single header library. In other words, we will have multiple definitions of the global variable. This is an error. For the same reason, a static member variable in a class will potentially have multiple definitions unless it is also declared as a const. The inline variable attribute in C++17 solves this problem by ensuring that a global variable in a header file is defined only once.

Beginning with C++17, we can define a global variable in a header file to be inline. Then if this header file is used in multiple translation units, the compiler will ensure that there is only one unique definition of the inline variable. The syntax for an inline variable is:

```cpp
inline int x = 0;
class Foo {
public:
    static std::string greet = "hello world";
};
inline class Foo foo;
```

## Using Inline Variables

In C++17, the **inline** keyword permits us to define a global variable in a header file, even though this header file might be included in multiple implementation (.cpp) files. The inclusion of the header file a multiple number of times does not create multiple definitions of the global variable.

Any initialization of an inline variable will be performed by the first translation unit that includes the header file.

```cpp
// some header file
class Foo {
public:
    // OK since C++17
    inline static std::string greet = "hello world";

// OK even if included in multiple implementation (.cpp) files
inline Foo foo;
```

## Modern C++: Lambda Extensions (C++17)

C++17 expands the use of lambdas as follows:

- lambdas can be constexpr
- a lambda can access the this pointer of an object

## constexpr Lambdas

C++17 permits a lambda to be used in a compile-time context, provided that it can be evaluated at compile-time.

To specify that a lambda can be evaluated at compile-time, we declare it with the constexpr attribute:

```cpp
// OK since C++17
auto squared = [](auto val) constexpr {
    return val*val;
}
```

constexpr lambdas cannot have any static variables, try/catch blocks or allocate memory.

A compiler error will occur if this constexpr lambda cannot be evaluated at compile-time. The following example demonstrates this:

```cpp
#include <iostream>
#include <string>

int main()
{
    int value = 9;
    auto summand = [](int val) constexpr {
        static int multiplier = 2;
        return val*multiplier;
    };
    std::cout << summand(value) << std::endl;
}
```
```text
// output (error)
error: 'multiplier' declared 'static' in 'constexpr' function
```

## Accessing This Pointer In Lambda

Prior to C++17, a lambda declared in a member function did not have access to the this pointer. C++17 rectifies this:

```cpp
#include <iostream>
#include <string>

class Foo
{
    std::string name;
public:
    Foo(const std::string& nm) : name(nm) {}

    void bar(){
        auto print = [this] { std::cout << name << std::endl; };
        print();
    }
};

int main() {
    Foo foo("test");
    foo.bar();
}
```
```text
// output
test
```
In the example above, this pointer to the object is captured in the lambda. A lambda can also capture this, which means that a copy of the current object is passed to the lambda.

## Modern C++: Type Exception Spec (C++17)

Since C++17, exception specifications have become part of the function. That is, the following two declarations are now different types:

```cpp
void foo(int);
void foo(int) noexcept; // different type
```

Prior to C++17, both functions would have been the same type. The compiler will enforce exception semantics for function pointers:

```cpp
// Note: we cannot define f1 and f2 together in the same namespace
// f1 and f2 have the same signatures though they are different types
void f1();
void f2() noexcept;

// define a pointer to a function that doesn't throw an exception
void (*funcptr)() noexcept; // Error C++17, the pointer is trying to point to a different type
fp = f1;
```

We cannot overload a function name with the same signature and different exception semantics in the same scope:

```cpp
void f3(int x);
void f3() noexcept; // Compiler Error
```

Consider this example:

```cpp
int func(int a, int b)
{
    return a + b;
}
int func(int a, int b) noexcept
{
    return a + b;
}
int main()
{
    func(1, 3);
    return 0;
}
```
```text
// error: redefinition of 'int func(int, int)'
```

## Modern C++: Empty Enum Initialization (C++17)

C++11 implements strong enum safety with scoped enums (enum class). A scoped enum is a distinct type that does not implicitly convert to an integer.

C++17 permits empty braced initialization for scoped enums. These enums do not have any enumerators.

```cpp
#include <iostream>
#include <string>

int main()
{
    // scoped enum does not declare any enumerators
    enum class CAPITAL { };

    // initialize
    CAPITAL capital{ 3000 };
    CAPITAL capital2{ 5000 };

    if (capital == capital2)
        std::cout << "capital = 5000" << std::endl;
    else
        std::cout << "capital != 5000" << std::endl;

    return 0;
}
```
```text
// output
capital != 5000
```

Braced initialization always prohibits narrowing conversions for any type:

```cpp
#include <iostream>
#include <string>

int main()
{
    enum class CAPITAL:int { };

    // cannot convert long int to int
    CAPITAL capital{ 30000000000000000 }; // error
    CAPITAL kapital{ 5000 };

    if (capital == kapital)
        std::cout << "capital = 5000" << std::endl;
    else
        std::cout << "capital = 3000" << std::endl;
}
```
```text
// output: narrowing conversion of '30000000000000000' from 'long int' to 'int'
```

## Modern C++: Fold Expressions (C++17)

A fold expression applies a binary operator to all of the elements of a parameter pack. Consequently, we can perform binary operations on the elements of a parameter pack without having to resort to recursion.

We can use all of the binary operators with fold expressions except for: ~, ->, and [].

In the following example, the function foldSum receives a parameter pack argument and returns the sum of all of its arguments:

```cpp
#include <iostream>
#include <string>
template<class Ttype>
auto sum(Ttype ... args) {
    auto sum = (... + args);
    std::cout << "sum = " << sum << std::endl;
    return sum;
}

int main() {
    sum(1, 5, 11, 18, 9);
}
```
```text
// output
sum = 44
// (Wait, the text says 44)
```
`(... args)` is called a fold expression, it applies the + operator to all of the parameter pack arguments starting from the left.

The parentheses around the fold expression is mandatory.

## Using Fold Expressions

Let operator be some binary operator, then:
