
## Chapter 1 Types

### Fundamental Types

C++ contains the same familiar keywords (e.g., `int`) that you recognize from C#. This is unsurprising given that both are C-like languages. There is, however, one potential landmine that can throw you into trouble. While C# explicitly defines the sizes of fundamental types (a `short` is a 16-bit integer, an `int` is a 32-bit integer, a `long` is a 64-bit integer, a `double` is a 64-bit double-precision IEEE 754 floating point number, etc.), C++ makes no such guarantees.

The smallest fundamental unit in C++ is `char`, which only needs to be at least large enough to hold the 96 basic characters that the C++ standard specifies, plus any other characters in the implementation's basic character set. In theory, some implementation of C++ could define a `char` as 7 bits or 16 bits ... almost anything is possible. But in practice you don't need to worry too much about a `char` being anything other than 8 bits (the equivalent of the byte or sbyte type in C#), which is its size in Visual C++.

In C++, `char`, `signed char`, and `unsigned char` are three distinct types. All three are required to take up the same amount of storage in memory. So a `char` in practice is either signed or unsigned. Whether it is signed or unsigned is implementation defined (see the sidebar). In Visual C++ the `char` type is, by default, signed. But you can use a compiler switch to have it treated as unsigned instead. In GCC, whether it is signed or unsigned depends on which CPU architecture you are targeting.

The signed integer types, in size order from smallest to largest, are:

- `signed char`
- `short int`
- `int`
- `long int`
- `long long int`

> **Implementations**
> Like many programming languages, there are multiple C++ implementations from various companies and organizations. Two of the most popular C++ implementations are Visual C++ and GCC. The C++ standard leaves some of its details to be defined by the implementer. If you are writing cross-platform code, you need to keep these implementation-defined details in mind, lest you find a program working fine on one OS and failing in weird ways on another.

The only guarantee of the size of each of these integer types is that each one is at least as large as the next smallest integer type. In Visual C++, an `int` and a `long int` are both 32-bit integers. It is only the `long long int` that is a 64-bit integer.

> **Note:** You can simply write `long` or `long long`; you do not need to write `long int` or `long long int`, respectively. The same is also true for `short int` (i.e., you can just write `short`). The `short` type is a 16-bit signed integer in Visual C++.

Each of the integer types has a corresponding unsigned integer type. You just put the keyword `unsigned` in front to get the unsigned version (except for `signed char`, which you change to `unsigned char`).

If you need to ensure that you are using specific sizes, you can include the C++ Standard Library header file `cstdint` (e.g., `#include <cstdint>`), which defines, among other things, the types:

- `int8_t`
- `int16_t`
- `int32_t`
- `int64_t`
- `uint8_t`
- `uint16_t`
- `uint32_t`
- `uint64_t`

These types have their use, but you will find that most APIs do not use them; instead, they use the fundamental types directly. This can make your programming confusing, as you constantly need to check the underlying fundamental type to ensure you do not end up with unintended truncation or expansion.

These types might come into use more, so I recommend checking for their usage in major libraries and APIs from time to time and adjusting your code accordingly if they become widely adopted. Of course, if you absolutely need a variable to be, for example, an unsigned 32-bit integer, you certainly should make use of `uint32_t` and make any adjustments for API calls and portability as needed.

Floating-point numbers are the same as far as size order rules. They go from float to double to long double. In Visual C++, float is a 32-bit floating-point number and double and long double are both 64-bit floating point numbers (long double is not larger than double, in other words).

C++ does not have any native type that is comparable to C#'s decimal type. However, one of the nice things about C++ is there are typically a large number of free or inexpensive libraries that you can license. For example, there's the decNumber library, the Intel Decimal Floating Point Math Library, and the GNU Multiple Precision Arithmetic Library. None are exactly compatible with C#'s decimal type, but if you are writing for Windows systems only, then you can use the DECIMAL data type to get that compatibility if needed, along with the Decimal Arithmetic Functions and the Data Type Conversion Functions.

There is also a Boolean type, bool, which can be true or false. In Visual C++, a bool takes up a byte. Unlike in C#, a bool can be transformed into an integer type. When false, it has an integer-equivalent value of 0, and when true, it has a value of 1. So the statement `bool result = true == 1;` will compile and result will evaluate to true when the statement has been executed.

Then there is the `wchar_t` type, which holds a wide character. A wide character's size varies based on the platform. On Windows platforms, it is a 16-bit character. It is the equivalent of C#'s `char` type. It is frequently used to construct strings. We will discuss strings in another chapter since many variants can be used for strings.

Lastly, there is the `void` type, which is used the same way it is in C#. And there is a `std::nullptr_t` type, which is messy to explain properly, but basically is there to be the type of the `nullptr` literal, which is what you should use instead of `NULL` or a literal 0 (zero) to check for null values.

### Enumerations

Enumerations are fairly similar to each other in C++ and C#. C++ has two types of enums: scoped and un-scoped.

A scoped enumeration is defined as either an `enum class` or an `enum struct`. There is no difference between the two. An un-scoped enumeration is defined as a plain `enum`. Let's look at a sample:

**Sample: EnumSample\EnumSample.cpp**

```cpp
#include <iostream>
#include <ostream>
#include <string>
#include "../pchar.h"

enum class Color
{
    Red,
    Orange,
    Yellow,
    Blue,
    Indigo,
    Violet
};

// You can specify any underlying integral type you want, provided it fits.
enum Flavor : unsigned short int
{
    Vanilla,
    Chocolate,
    Strawberry,
    Mint,
};

int _pmain(int /*argc*/, _pchar* /*argv*/[])
{
    Flavor f = Vanilla;
    f = Mint; // This is legal since the Flavor enum is an un-scoped enum.

    Color c = Color::Orange;
    //c = Orange; // This is illegal since the Color enum is a scoped enum.

    std::wstring flavor;
    std::wstring color;

    switch (c)
    {
    case Color::Red:
        color = L"Red";
        break;
    case Color::Orange:
        color = L"Orange";
        break;
    case Color::Yellow:
        color = L"Yellow";
        break;
    case Color::Blue:
        color = L"Blue";
        break;
    case Color::Indigo:
        color = L"Indigo";
        break;
    case Color::Violet:
        color = L"Violet";
        break;
    default:
        color = L"Unknown";
        break;
    }

    switch (f)
    {
    case Vanilla:
        flavor = L"Vanilla";
        break;
    case Chocolate:
        flavor = L"Chocolate";
        break;
    case Strawberry:
        flavor = L"Strawberry";
        break;
    case Mint:
        flavor = L"Mint";
        break;
    default:
        break;
    }

    std::wcout << L"Flavor is " << flavor.c_str() << L" (" << f <<
        L"). Color is " << color.c_str() << L" (" <<
        static_cast<int>(color) << L")." << std::endl;
    std::wcout << L"The size of Flavor is " << sizeof(Flavor) <<
        L"." << std::endl;
    std::wcout << L"The size of Color is " << sizeof(Color) <<
        L"." << std::endl;

    return 0;
}
```

> **Note:** In C++, the scope resolution operator is `::`. We’ll discuss this in more detail later on. For now, just think of it as serving many of the same purposes as the `.` operator in C#.

This code will give the following output:

```text
Flavor is Mint (3). Color is Orange (1).
The size of Flavor is 2.
The size of Color is 4.
```

As you can see in the sample, the scoped Color enumeration requires you to access its members in the same way as C# by prefixing the enumeration member with the enumeration’s name and the scope resolution operator. By contrast, the un-scoped Flavor enumeration allows you simply to specify the members without any prefix. For this reason, I think it’s better practice to prefer scoped enumerations: You minimize the risks of naming collisions and lessen namespace pollution.

Notice that there is another difference with scoped enumerations: When we wanted to output the numerical value of the scoped Color enum, we had to use the static_cast operator to convert it to an int, while we did not need to do any casting for the un-scoped Flavor enumeration.

For the Flavor enumeration, we specified the underlying type as being an unsigned short int. You can also specify the underlying type for scoped enumerations. Specifying the underlying type is optional, but is mandatory if you wish to use forward declaration with an un-scoped enumeration. Forward declaration is a way to speed up program compile times by only telling the compiler what it needs to know about a type rather than forcing it to compile the whole header file the type is defined in.

We will look at this later on. For now, just remember that an un-scoped enumeration must have its underlying type explicitly specified in order to use a forward declaration of it; a scoped enumeration does not require specification of its underlying type to use a forward declaration of it (the underlying type will be int if none is specified).
