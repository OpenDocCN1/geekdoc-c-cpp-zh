
- precision: you can use a period (.) followed by a non-negative decimal number or a replacement field.

A few examples should help you grasp the basics:

### Applying the Width and Precision Specifier

```cpp
// formatWidthPrecision.cpp

#include <format>
#include <iostream>
#include <string>

int main() {

    int i = 123456789;
    double d = 123.456789;

    std::cout << "---" << std::format("{}", i) << "---\n";
    std::cout << "---" << std::format("{:15}", i) << "---\n"; // (w = 15)
    std::cout << "---" << std::format("{:{}}", i, 15) << "---\n"; // (w = 15)

    std::cout << '\n';

    std::cout << "---" << std::format("{}", d) << "---\n";
    std::cout << "---" << std::format("{:15}", d) << "---\n"; // (w = 15)
    std::cout << "---" << std::format("{:{}}", d, 15) << "---\n"; // (w = 15)

    std::cout << '\n';

    std::string s = "Only a test";

    std::cout << "---" << std::format("{:10.50}", d) << "---\n"; // (w = 10, p = 50)
    std::cout << "---" << std::format("{:{}.{}}", d, 10, 50) << "---\n"; // (w = 10, p = 50)
    std::cout << "---" << std::format("{:10.5}", d) << "---\n";  // (w = 10, p = 5)
    std::cout << "---" << std::format("{:{}.{}}", d, 10, 5) << "---\n"; // (w = 10, p = 5)

    std::cout << '\n';

    std::cout << "---" << std::format("{:.500}", s) << "---\n";    // (p = 500)
    std::cout << "---" << std::format("{:.{}}", s, 500) << "---\n"; // (p = 500)
    std::cout << "---" << std::format("{:.5}", s) << "---\n";      // (p = 5)

}
```

The w character in the source code stands for the width; similarly, the p character for the precision. I have a few interesting observations about the program. No extra spaces are added when you specify the width with a replacement field (line 14). When you specify a precision higher than the length of the displayed double (lines 26 and 27), the length of the displayed value reflects the precision. This observation does not hold for a string (lines 35 and 36).

![](img/c60a87adb7f61e2e82071d081bbb389a_359_0.png)

Applying the width and precision specifiers

Additionally, you can also parametrize the width and the precision.

### Applying the Parametrized Width and Precision Specifier

```cpp
// formatWidthPrecisionParameterized.cpp

#include <format>
#include <iostream>

int main() {

    std::cout << '\n';

    double doub = 123.456789;

    std::cout << std::format("{}\n", doub);

    std::cout << '\n';

    for (auto precision: {3, 5, 7, 9}) {
        std::cout << std::format("{:.{}f}\n", doub, precision);
    }

    std::cout << '\n';

    int width = 10;
    for (auto precision: {3, 5, 7, 9}) {
        std::cout << std::format("{:{}.{}f}\n", doub, width, precision);
    }

    std::cout << '\n';

}
```

Program `formatWidthPrecisionParameterized.cpp` displays the double `doub` in various ways. Line 12 applies the default. Line 17 varies the precision from 3 to 9. The last argument of the format string goes into the inner `{}` of the format specifier `{:{}.{}f}`. Finally, line 24 sets the width of the displayed doubles to 10.

![](img/c60a87adb7f61e2e82071d081bbb389a_360_0.png)

Applying the parametrized width and precision specifiers

### 5.5.2.3.4 Type

In general, the compiler deduces the type of the value used. But sometimes, you want to specify the type. These are the most important type specifications:

- Strings: `s`
- Integers:
  - `b`: binary format
  - `B`: same as `b` but base prefix is `0B`
  - `d`: decimal format
  - `o`: octal format
  - `x`: hexadecimal format
  - `X`: same as `x`, but base prefix is `0X`
- `char` and `wchar_t`:
  - `b`, `B`, `d`, `o`, `x`, `X`: such as integers
- `bool`:
  - `s`: `true` or `false`
  - `b`, `B`, `d`, `o`, `x`, `X`: such as integers
- Floating-point:
  - `e`: exponential format
  - `E`: same as `e`, but the exponent is written with `E`
  - `f`, `F`: fixed point; precision is 6
  - `g`, `G`: precision 6 but exponent is written with `E`
- Pointer:
  - `p`: hexadecimal notation of its address

Only `void*`, `const void*`, and `std::nullptr_t` pointer types are valid. If you want to display the address of an arbitrary pointer, you must cast it to `(const) void*`.

#### Output of Pointers

```cpp
double d = 123.456789;

std::format("{}", &d);                          // ERROR
std::format("{}", static_cast<void*>(&d));      // okay
std::format("{}", static_cast<const void*>(&d));// okay
std::format("{}", nullptr);                     // okay
```

When you don't specify the type, the values are displayed as follows. A string is displayed as a string, an integer in decimal format, a character as a character, and a floating-point value with `std::to_chars`[^32].

The type specifiers allow you to easily display an `int` in a different number system.

[^32]: https://en.cppreference.com/w/cpp/utility/to_chars

#### Applying the Type Specifier

```cpp
// formatType.cpp

#include <format>
#include <iostream>

int main() {

    int num{2020};

    std::cout << "default:    " << std::format("{}", num) << '\n';
    std::cout << "decimal:    " << std::format("{:d}", num) << '\n';
    std::cout << "binary:     " << std::format("{:b}", num) << '\n';
    std::cout << "octal:      " << std::format("{:o}", num) << '\n';
    std::cout << "hexadecimal: " << std::format("{:x}", num) << '\n';

}
```

![](img/c60a87adb7f61e2e82071d081bbb389a_362_0.png)

So far, I've formatted basic types and strings. Additionally, you can format user-defined types.

### 5.5.3 User-Defined Types

I have to specialize the class `std::formatter`[^43] for the user-defined type. In particular, I must implement the member functions `parse` and `format`.

- **parse**: This function parses the format string and throws a `std::format_error` in case of an error. The function `parse` should be `constexpr` to enable compile-time parsing. It accepts a parse context (`std::format_parse_context`) and should return the last character for the format specifier (the closing `}`). When you don't use a format specifier, this is also the first character of the format specifier.

  The following lines show a few examples of the first character of the format specifier:

  ```text
  "{}"      // context.begin() points to '}'
  "{:}"     // context.begin() points to '}'
  "{:d}"    // context.begin() points to 'd'
  "{:5.3f}" // context.begin() points to '5.3f'
  "{:x}"    // context.begin() points to 'x'
  "{0} {0}" // context.begin() points to '}'
  ```

  `context.begin()` points to the first character of the format specifier, and `context.end()` to the last character of the entire format string. When you provide a format specifier, you have to parse all between `context.begin()` and `context.end()` and return the position of the closing `}`.

- **format**: This function should be `const`. It gets the value `val` and the `std::format_context` context. `format` formats the value `val` and writes it, according to the parsed format, to `context.out()`. The `context.out()` return value can be directly fed into `std::format_to`. `std::format_to` has to return the new position for further output. It returns an iterator that represents the end of the output.

[^43]: https://en.cppreference.com/w/cpp/utility/format/formatter

Let me apply the theory and start with the first example.

#### 5.5.3.1 A Formatter for a Single Value

```cpp
// formatSingleValue.cpp

#include <format>
#include <iostream>

class SingleValue {
public:
    SingleValue() = default;
    explicit SingleValue(int s) : singleValue(s) {}
    int getValue() const {
        return singleValue;
    }
private:
    int singleValue;
};

template<>
struct std::formatter<SingleValue> {
    constexpr auto parse(std::format_parse_context& context) {
        return context.begin();
    }
};
```
