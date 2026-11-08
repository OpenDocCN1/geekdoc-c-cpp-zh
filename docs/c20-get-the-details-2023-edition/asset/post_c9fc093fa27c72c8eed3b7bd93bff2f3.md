
If you want to know all the sophisticated details, I strongly suggest you watch the CppCon 2019 talk “Deprecating volatile” from JF Bastien. Here are a few examples from his talk. Additionally, I fixed a few typos in the source code. The numbers in the following code snippets refer to the three deprecations listed earlier.

### Deprecated use case for volatile

```cpp
// (1)
int neck, tail;
volatile int brachiosaur;
brachiosaur = neck;      // OK, a volatile store
tail = brachiosaur;      // OK, a volatile load

// deprecated: does this access brachiosaur once or twice
tail = brachiosaur = neck;

// deprecated: does this access brachiosaur once or twice
brachiosaur += neck;

// OK, a volatile load, an addition, a volatile store
brachiosaur = brachiosaur + neck;

***********************************************
// (2)
// deprecated: a volatile return type has no meaning
volatile struct amber jurassic();

// deprecated: volatile parameters aren't meaningful to the
//             caller, volatile only applies within the function
void trex(volatile short left_arm, volatile short right_arm);

// OK, the pointer isn't volatile, the data it points to is
void fly(volatile struct pterosaur* pteranodon);

***********************************************
(3)
struct linhenykus { volatile short forelimb; };
void park(linhenykus alvarezsauroid) {
    // deprecated: does the binding copy the forelimbs?
    auto [what_is_this] = alvarezsauroid; // structured binding
    // ...
}
```

![](img/c60a87adb7f61e2e82071d081bbb389a_231_0.png)

### volatile and Multithreading Semantics

volatile is typically used to denote objects that can change independently of the regular program flow. These are, for example, objects in embedded programming that represent an external device (memory-mapped I/O). Because these objects can change independently of the regular program flow and their value is directly written to main memory, no optimized storing in caches takes place. In other words, volatile avoids aggressive optimization and has no multithreading semantics.

## 4.9.2 Range-based for loop with Initializers

With C++20, you can directly use a range-based for loop with an initializer.

Range-based for loop with initializer

```cpp
// rangeBasedForLoopInitializer.cpp

#include <iostream>
#include <string>
#include <vector>

int main() {

    for (auto vec = std::vector{1, 2, 3}; auto v : vec) {
        std::cout << v << " ";
    }

    std::cout << "\n\n";

    for (auto initList = {1, 2, 3}; auto e : initList) {
        e *= e;
        std::cout << e << " ";
    }

    std::cout << "\n\n";

    using namespace std::string_literals;
    for (auto str = "Hello World"s; auto c : str) {
        std::cout << c << " ";
    }

    std::cout << '\n';
}
```

The range-based for loop uses in line 9 a `std::vector`, in line 15 a `std::initializer_list`, and line 23 a `std::string`. Furthermore, in line 9 and line 15 I apply automatic type deduction for class templates, which we had since C++17. Instead of `std::vector<int>`, I just write `std::vector`.

![](img/c60a87adb7f61e2e82071d081bbb389a_232_0.png)

Use of a range-based for loop with initializers

## 4.9.3 Virtual constexpr function

A constexpr function has the potential to run at compile time but can also be executed at run time. Consequently, you can make a constexpr function with C++20 virtual. Both directions are possible. A virtual constexpr function can override a non-constexpr function, and a virtual non-constexpr function can override a virtual constexpr function. I want to emphasize that override implies that the relevant function of a base class is virtual.

Program virtualConstexpr.cpp shows both combinations:

```cpp
// virtualConstexpr.cpp

#include <iostream>

struct X1 {
    virtual int f() const = 0;
};

struct X2: public X1 {
    constexpr int f() const override { return 2; }
};

struct X3: public X2 {
    int f() const override { return 3; }
};

struct X4: public X3 {
    constexpr int f() const override { return 4; }
};

int main() {
    X1* x1 = new X4;
    std::cout << "x1->f(): " << x1->f() << '\n';

    X4 x4;
    X1& x2 = x4;
    std::cout << "x2.f(): " << x2.f() << '\n';
}
```

Line 24 uses virtual dispatch (late binding) via a pointer, line 28 uses virtual dispatch via a reference.

```text
X1->f(): 4
X2.f(): 4
```

Use of virtual constexpr functions

## 4.9.4 The new Character Type of UTF-8 Strings: `char8_t`

In addition to the character types `char16_t` and `char32_t` from C++11, C++20 gets the new character type `char8_t`. Type `char8_t` is large enough to represent any UTF-8 code unit (8 bits). It has the same size, signedness, and alignment as an unsigned char, but is a distinct type.

![](img/c60a87adb7f61e2e82071d081bbb389a_233_0.png)

### char versus char8_t

A char has one byte. In contrast to a char8_t, the number of bits of a byte and hence of a char is not defined. Nearly all implementations use 8 bits for a byte. The `std::string` is an alias for a `std::basic_string` of chars.

### `std::string` and a `std::string` literal

```cpp
std::string std::basic_string<char>
"Hello World"s
```

Consequently, C++20 has a new typedef for the character type `char8_t` (line 1) and a new UTF-8 string literal (line 2).

### A new `char8_t` character type and an UTF-8 string literal

```cpp
std::u8string std::basic_string<char8_t>
u8"Hello World"
```

The program char8Str.cpp shows the straightforward usage of the new character type char8_t.

### Intuitive usage for the new character type char8_t

```cpp
// char8Str.cpp

#include <iostream>
#include <string>

int main() {

    const char8_t* char8Str = u8"Hello world";
    std::basic_string<char8_t> char8String = u8"helloWorld";
    std::u8string char8String2 = u8"helloWorld";

    char8String2 += u8".";

    std::cout << "char8String.size(): " << char8String.size() << '\n';
    std::cout << "char8String2.size(): " << char8String2.size() << '\n';

    char8String2.replace(0, 5, u8"Hello");

    std::cout << "char8String2.size(): " << char8String2.size() << '\n';
}
```

Without further ado, here is the output of the program:

```
char8String.size(): 10
char8String2.size(): 11
char8String2.size(): 12
```

Use of the new character type char8_t

C++20 does not have the output operator for char8_t strings. Consequently, a convenient way is to apply reinterpret_cast<const char*>(...) to a char8_t string.

### Output of a char8_t string

```cpp
// char8StrOutput.cpp

#include <iostream>
#include <string>

int main() {

    std::cout << '\n';

    const char8_t* char8Str = u8"Dollar: \u20AC";
    std::basic_string<char8_t> char8String = u8"Euro: \u0024";
    std::u8string char8String2 = u8"Pound: \u00A3";

    std::cout << reinterpret_cast<const char*>(char8Str) << '\n';
    std::cout << reinterpret_cast<const char*>(char8String.c_str()) << '\n';
    std::cout << reinterpret_cast<const char*>(char8String2.c_str()) << '\n';

    std::cout << '\n';
}
```

The program displays the Dollar (line 14), Euro (line 15), and Pound (line 16) sign.

![](img/c60a87adb7f61e2e82071d081bbb389a_235_0.png)

Output of a char8_t string

## 4.9.5 using enum in Local Scopes

A using enum declaration introduces the enumerators of the named enumeration in the local scope.

### Introducing enumerators in the local scope

```cpp
// enumUsing.cpp

#include <iostream>
#include <string_view>

enum class Color {
    red,
    green,
    blue
};

std::string_view toString(Color col) {
    switch (col) {
        using enum Color;
        case red: return "red";
        case green: return "green";
        case blue: return "blue";
    }
    return "unknown";
}

int main() {

    std::cout << '\n';

    std::cout << "toString(Color::red): " << toString(Color::red) << '\n';

    using Color::green;

    std::cout << "toString(green): " << toString(green) << '\n';

    using enum Color;

    std::cout << "toString(blue): " << toString(blue) << '\n';

    std::cout << '\n';

}
```

The using enum declaration (lines 14 and 32) introduces the enumerators of the scoped enumerations Color into the local scope. From that point on, the enumerators can be used unscoped (lines 15 - 17 and line 34). Additionally, you can also apply a using declaration for a specific enumeration value (line 28).

![](img/c60a87adb7f61e2e82071d081bbb389a_236_0.png)

## 4.9.6 Default Member Initializers for Bit Fields

First of all, what is a bit field? Here is the definition from Wikipedia⁸⁰: “A bit field is a data structure used in computer programming. It consists of a number of adjacent computer memory locations which have been allocated to hold a sequence of bits, stored so that any single bit or group of bits within the

⁸⁰https://en.wikipedia.org/wiki/Bit_field
