
## Chapter 8: Other Language Features

In C++17, there are a couple of minor or small changes to the C++ core language, which are described in this chapter.

### 8.1 Nested Namespaces

Proposed in 2003 for the first time, the C++ standards committee has finally enabled to specify nested namespaces as follows:

```
namespace A::B::C {
    ...
}
```

which is equivalent to:

```
namespace A {
    namespace B {
        namespace C {
            ...
        }
    }
}
```

Note that there is no support for nesting inline namespaces (yet). This is simply because it is not obvious whether the inline applies to the last or to all namespaces (both could equally be useful).

Another application of the new expression evaluation order is the function that inserts a space before passed arguments.

### Backward Incompatibilities

The new guaranteed evaluation order might impact the output of existing programs. This is not just theory. Consider, for example, the following program:

lang/evalexcept.cpp

```
#include <iostream>
#include <vector>

void print10elems(const std::vector<int>& v) {
    for (int i=0; i<10; ++i) {
        std::cout << "value: " << v.at(i) << '\n';
    }
}

int main()
{
    try {
        std::vector<int> vec{7, 14, 21, 28};
        print10elems(vec);
    }
    catch (const std::exception& e) {    // handle standard exception
        std::cerr << "EXCEPTION: " << e.what() << '\n';
    }
    catch (...) {                        // handle any other exception
        std::cerr << "EXCEPTION of unknown type\n";
    }
}
```

Because the vector<> in this program has only four elements, the program throws an exception in the loop in print10elems() when calling at() as part of an output statement for an invalid index:

```
std::cout << "value: " << v.at(i) << "\n";
```

Before C++17, the output could be:

```
value: 7
value: 14
value: 21
value: 28
EXCEPTION: ...
```

because at() was allowed to be evaluated before "value:  " was written, so that for the wrong index, the output was skipped completely.[^2]

Since C++17, the output is guaranteed to be:

```
value: 7
value: 14
value: 21
value: 28
value: EXCEPTION: ...
```

because the output of "value:  " has to be performed before at() is evaluated.

### 8.3 Relaxed Enum Initialization from Integral Values

For enumerations with a fixed underlying type, since C++17, you can use an integral value of that type for direct list initialization. This applies to unscoped enumerations with a specified type and all scoped enumerations because they always have an underlying default type:

```
// unscoped enum with underlying type:
enum MyInt : char { };
MyInt i1{42};        // OK since C++17 (ERROR before C++17)
MyInt i2 = 42;      // still ERROR
MyInt i3(42);       // still ERROR
MyInt i4 = {42};    // still ERROR
```

```
// scoped enum with default underlying type:
enum class Weekday { mon, tue, wed, thu, fri, sat, sun };
Weekday s1{0};      // OK since C++17 (ERROR before C++17)
Weekday s2 = 0;     // still ERROR
Weekday s3(0);      // still ERROR
Weekday s4 = {0};   // still ERROR
```

The same applies if Weekday has a specified underlying type:

```
// scoped enum with specified underlying type:
enum class Weekday : char { mon, tue, wed, thu, fri, sat, sun };
Weekday s1{0};      // OK since C++17 (ERROR before C++17)
Weekday s2 = 0;     // still ERROR
Weekday s3(0);      // still ERROR
Weekday s4 = {0};   // still ERROR
```

For unscoped enumerations (enum without class) with no specified underlying type, you still cannot use list initialization for numeric values:

```
enum Flag { bit1=1, bit2=2, bit3=4 };
Flag f1{0};         // still ERROR
```

Note also that list initialization still does not allow narrowing, which means that you cannot pass a floating-point value:

```
enum MyInt : char { };
MyInt i5{42.2};    // still ERROR
```

This feature was motivated to support the trick of defining new integral types just by defining an enumeration type that maps to an existing integral type as done here with MyInt. Without the feature, there is no way to initialize a new object without a cast.

In fact, since C++17, the C++ standard library also provides std::byte, which uses this feature directly.

### 8.4 Fixed Direct List Initialization with auto

After the introduction of uniform initialization with braces in C++11, it turned out that there were some unfortunate and non-intuitive inconsistencies when using auto instead of a specific type:

```
int x{42};      // initializes an int
int y{1,2,3};    // ERROR
auto a{42};      // initializes a std::initializer_list<int>
auto b{1,2,3};   // OK: initializes a std::initializer_list<int>
```

These inconsistencies were fixed for direct list initialization (brace initialization without =) so that we now have the following behavior:

```
int x{42};      // initializes an int
int y{1,2,3};    // ERROR
auto a{42};      // initializes an int now
auto b{1,2,3};   // ERROR now
```

Note that this is a breaking change that might even silently result in a different program behavior (e.g., when printing a). Therefore, compilers that adopt this change usually also adopt it even in C++11 mode. For the major compilers, the fix was adopted for all modes with Visual Studio 2015, g++ 5, and clang 3.8.

Note also that copy list initialization (brace initialization with =) still has the behavior to initialize a std::initializer_list<> when auto is used:

```
auto c = {42};      // still initializes a std::initializer_list<int>
auto d = {1,2,3};    // still OK: initializes a std::initializer_list<int>
```

Thus, we now have another significant difference between direct initialization (without =) and copy initialization (with =):

```
auto a{42};      // initializes an int now
auto c = {42};    // still initializes a std::initializer_list<int>
```

This is one additional reason by default to prefer direct list initialization (brace initialization without =) when initializing variables and objects.

### 8.5 Hexadecimal Floating-Point Literals

C++17 standardizes the ability to specify hexadecimal floating-point literals (which some compilers supported even before C++17). This notation is especially useful when an exact floating-point representation is desired (for decimal floating-point values there is no general guarantee that the exact value exists).

For example:

lang/hexfloat.cpp

```
#include <iostream>
#include <iomanip>

int main()
{
    // init list of floating-point values:
    std::initializer_list<double> values {
        0x1p4,      // 16
        0xA,        // 10
        0xAp2,      // 40
        5e0,        // 5
        0x1.4p+2,   // 5
        1e5,        // 100000
        0x1.86Ap16, // 100000
        0xC.68p+2,  // 49.625
    };

    // print all values both as decimal and hexadecimal value:
    for (double d : values) {
        std::cout << "dec: " << std::setw(6) << std::defaultfloat << d
                  << "  hex: " << std::hexfloat << d << '\n';
    }
}
```

The program defines different floating-point values by using different existing notations and the new hexadecimal floating-point notation. The new notation is a base-2 scientific notation:

- The significand/mantissa is written in hexadecimal format.
- The exponent is written in decimal format and interpreted with respect to base 2.

For example, 0xAp2 is a way to specify the decimal value 40 (10 multiplied by “2 to the power of 2”). The value could also be expressed as 0x1.4p+5, which is 1.25 multiplied by 32 (0.4 is a hexadecimal quarter and 2 to the power of 5 is 32).

The program has the following output:

```
dec:      16  hex: 0x1p+4
dec:      10  hex: 0x1.4p+3
dec:      40  hex: 0x1.4p+5
dec:       5  hex: 0x1.4p+2
```

[^2]: This was, for example, the behavior of older GCC or Visual C++ versions.
