# # Chapter 1 Types

# ## Fundamental Types

C++ contains the same familiar keywords (e.g., `int`) that you recognize from C#. This is unsurprising given that both are C-like languages. There is, however, one potential landmine that can throw you into trouble. While C# explicitly defines the sizes of fundamental types (a `short` is a 16-bit integer, an `int` is a 32-bit integer, a `long` is a 64-bit integer, a `double` is a 64-bit double-precision IEEE 754 floating point number, etc.), C++ makes no such guarantees.

The smallest fundamental unit in C++ is `char`, which only needs to be at least large enough to hold the 96 basic characters that the C++ standard specifies, plus any other characters in the implementation's basic character set. In theory, some implementation of C++ could define a `char` as 7 bits or 16 bits ... almost anything is possible. But in practice you don't need to worry too much about a `char` being anything other than 8 bits (the equivalent of the byte or sbyte type in C#), which is its size in Visual C++.

In C++, `char`, `signed char`, and `unsigned char` are three distinct types. All three are required to take up the same amount of storage in memory. So a `char` in practice is either signed or unsigned. Whether it is signed or unsigned is implementation defined (see the sidebar). In Visual C++ the `char` type is, by default, signed. But you can use a compiler switch to have it treated as unsigned instead. In GCC, whether it is signed or unsigned depends on which CPU architecture you are targeting.

The signed integer types, in size order from smallest to largest, are:

+   1. `signed char`
+   2. `short int`
+   3. `int`
+   4. `long int`
+   5. `long long int`

> > **Implementations**
> > Like many programming languages, there are multiple C++ implementations from various companies and organizations. Two of the most popular C++ implementations are Visual C++ and GCC. The C++ standard leaves some of its details to be defined by the implementer. If you are writing cross-platform code, you need to keep these implementation-defined details in mind, lest you find a program working fine on one OS and failing in weird ways on another.

The only guarantee of the size of each of these integer types is that each one is at least as large as the next smallest integer type. In Visual C++, an `int` and a `long int` are both 32-bit integers. It is only the `long long int` that is a 64-bit integer.

> > **Note:** *You can simply write Long or Long Long; you do not need to write Long Int or Long Long Int, respectively. The same is also true for short int (i.e. you can just write short). The short type is a 16-bit signed integer in Visual C++.*

Each of the integer types has a corresponding unsigned integer type. You just put the keyword `unsigned` in front to get the unsigned version (except for `signed char`, which you change to `unsigned char`).

If you need to ensure that you are using specific sizes, you can include the C++ Standard Library header file `cstdint` (e.g., `#include <cstdint>`), which defines, among other things, the types:

+   - `int8_t`
+   - `int16_t`
+   - `int32_t`