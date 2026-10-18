
The output of the previous code looks like this:

```
A1 = 541.326
sizeof( SimpleCircle ) = 8
A2 = 541.601
sizeof( PrecCircle ) = 8
```

It is interesting to observe that in all cases, the size of each object is just large enough to accommodate the fRadius member from the base. This is one of the main benefits of static polymorphism, as compared to the dynamic version.

## 4.14 (✕) Mixin Classes

An interesting topic related to the CRTP is the mixin class pattern (https://www.fluentcpp.com/2017/12/12/mixin-classes-yang-crtp). Its general scheme is shown in Listing 4.30.

**Listing 4.30** General scheme of a mixin class MMixin. The key idea is to provide the base class as a template parameter to MMixin (in CppBookCode/VirtualMechanisms.cpp).

```cpp
template < typename Base >
class MMixin : public Base
{
    // Can use members of Base ...
};
```

Mixin resembles an inverted CRTP pattern. It lets us compose new components from existing simpler ones, as in the example in Listing 4.31.

**Listing 4.31** Example of mixin classes to display the date in different formats (in CppBookCode/VirtualMechanisms.cpp).

```cpp
struct TDate
{
    int             fDay    {};
    std::string     fMonth  {};
    int             fYear   {};
};
```

The following MPrint_Date_US mixin displays TDate in the US format:

```cpp
template < typename B >
struct MPrint_Date_US : public B
{
    // US date print format
    void Print( void )
    {
        std::cout << fMonth << "/" << fDay << '/' << fYear << '\n';
    }
};
```

On the other hand, the MPrint_Date_Eu mixin knows how to display TDate in the European format:

```cpp
template < typename B >
struct MPrint_Date_Eu : public B
{
    // European date print format
    void Print( void )
    {
        std::cout << fDay << "/" << fMonth << '/' << fYear << '\n';
    }
};
```

Finally, the MixinTest function shows the two mixins in action:

```cpp
void MixinTest( void )
{
    // Alias is useful with mixins
    using Date_US = MPrint_Date_US< TDate >;
    using Date_Eu = MPrint_Date_Eu< TDate >;

    Date_US dus { 9, "Nov", 2019 };
    dus.Print();

    Date_Eu deu { 9, "Nov", 2019 };
    deu.Print();
}
```

The result of running MixinTest is as follows:

> Nov/9/2019
> 9/Nov/2019

A unique key associated with each record is a requirement when building database systems with classes that represent personal data such as first and last names, address, age, etc. In Poland, each individual has a personal identification number called the PESEL ID (https://en.wikipedia.org/wiki/PESEL; similar to a US Social Security number) consisting of exactly 11 digits that are unique to the person and that also convey encoded information about their date of birth and sex. For this example, we decided to include this information in each person’s record. Listing 4.32 shows our first attempt to define the TPerson class.

Here is our first attempt to set fID with an 11-digit PESEL:

```
fID = 94120612345;    // try to write the PESEL id
```

This results in a nasty error, which we will see when we try to display fID. In systems where unsigned int objects are stored in four bytes, the following result appears:

> fID = 3926299129

**Listing 4.32** First definition of the `TPerson` class. The type chosen to represent fID is inappropriate here since it cannot reliably convey an 11-digit value; it must be replaced.

```cpp
class TPerson
{
private:

    std::wstring          fFirstName;
    std::wstring          fLastName;

    unsigned char         fAge {};

    unsigned int          fID {};          // PESEL id

public:

    // ...
};
```

We discussed this problem when we introduced various data types in Section 3.1. Listing 3.2 computed the minimum number of bits for a value representation. However, such details are easy to overlook during design and can result in malfunctioning software. To measure if, for example, `unsigned long` would be sufficient, we can modify the code from Listing 3.2 as follows:

```cpp
// Test PESEL ID stored in ID_TYPE
using ID_TYPE = unsigned long;
ID_TYPE          fID {};             // PESEL id

std::cout << "sizeof( ID_TYPE ) = " << sizeof( ID_TYPE ) << std::endl;
std::cout << "Bits to store 11 digits = " << (int)( log( 99999999999.0 ) / log( 2.0 ) + 1 ) << std::endl;
```

We obtained the following output on our system:

```text
sizeof( ID_TYPE ) = 4
Bits to store 11 digits = 37
```

Hence, even `unsigned long`, which offers 4·8 = 32 bits, is much too short, since at least 37 bits are necessary to store 11 digits. Since computer memory is byte-addressable, this means using at least five bytes; but an odd number is also not appealing, for performance reasons (Patterson and Hennessy 2018). The 11 digits are nothing to quarrel about – we can put `std::array<unsigned char, 11>` or another `wstring` in the `TPerson` class, and the problem is solved. However, when we consider storing thousands of such `TPerson` objects in a database, then the extra bytes do not add to software quality. So, in this section, we will show how to design a class to store digits optimally using a *binary-coded decimal* (BCD) representation, which entails only four bits per digit. Then we will scrutinize various ways of designing a special class to represent PESEL IDs. We will consider embedding an 11-digit object, as well as deriving from it. We will also compare their properties and size.

In this example project, we will learn about a number of useful programming techniques:

- BCD data format
- Endianness
- Efficient storage of long numbers

## 4.15.2 Endianness

Endianness defines a way to store multibyte words in the computer’s memory (Section 2.1). There are two variants:

- ***Big endian*** – Most significant byte at the lowest address
- ***Little endian*** – Most significant byte at the highest address

Figure 4.21 illustrates two possible types of endianness for the two-byte value 0xABCD.

![](img/31dee73f41f3d43a1f2e2b4eaffa2afd_337_0.png)

**Figure 4.21** Storing a two-byte value 0xABCD with big and little endianness.

Byte order is defined by the microprocessor architecture standard, and manufacturers usually have their own preferences. For example, little endian was employed in x86 and new RISC-V architectures (Patterson and Hennessy 2018). But the 68k series of Motorola processors operated in big-endian mode. There are even some microprocessors for which endianness can be programmatically set (e.g. PowerPC). But big endian dominates in networking protocols (e.g. TCP/IP). In C++, it is not defined and should not pose a problem on a given platform. However, endianness conversion may be necessary when e.g. sending data structures over different systems. To revert the byte order in a word, the RevertEndianness function from Section 3.13.2.2 can be used.

In our project, endianness needs to be considered when converting strings, such as “12345,” into a series of BCD-organized values. For this purpose, big endian seems to be appropriate, as we will discuss.

## 4.15.3 Definition of the *TLongNumberFor* Class

Listing 4.33 shows the definition of the TLongNumberFor class that will be used to represent numbers of any length efficiently. As usual, on lines [1–6], the STL headers are included. The last header, i.e. the *exception* header, contains definitions of the `std::exception` class hierarchy, which will be used to represent exceptions that may occur in our code.

**Listing 4.33** Annotated definition of the `TLongNumberFor` class (in LongNumber/LongNumberFor.h).

```cpp
#include <cassert>
#include <string>
#include <array>
#include <iostream>
#include <algorithm>
#include <exception>

using std::string;
using std::istream, std::ostream;

// This class efficiently stores a series of numbers, such as 12345678901234567890
// of a given length. Each number is stored in a nibble (i.e. 4 bits).
//
// The auto keyword in a template parameter -
// the type is deduced at the point of instantiation.
//
template < auto MAX_NUMBERS >
class TLongNumberFor
{
public:

    inline static const auto kMaxNumbers { MAX_NUMBERS };

private:

    // ------------------------------
    // A class can define another class
    // This class is just a placeholder
    struct NibblePair
    {
        unsigned char fFirst     : 4;       // define two bit fields
        unsigned char fSecond    : 4;              // of a total size of 1 byte

        NibblePair() : fFirst( 0 ), fSecond( 0 ) {}
    };
    // ------------------------------
```

Then, on lines [9–10], the useful `std` classes are introduced. As a result, the `std::` prefix can be omitted for these explicitly listed classes from `std`, as discussed in Section 3.14.6.

The definition of the `TLongNumberFor` template class starts on line [20] and spans to line [158]. This is an example of a template class with the `auto` keyword in front of the `MAX_NUMBERS` parameter. The `auto` keyword allows for correct type deduction based on the type of the argument passed during template class instantiation.

On line [25], the template parameter is copied into the local `kMaxNumbers` inline static constant object. As a result, this object is defined only once for the class and does not occupy memory in objects of the `TLongNumberFor` type. If necessary, information about the maximum number of digits can be accessed from a concrete instantiation of `TLongNumberFor`.
