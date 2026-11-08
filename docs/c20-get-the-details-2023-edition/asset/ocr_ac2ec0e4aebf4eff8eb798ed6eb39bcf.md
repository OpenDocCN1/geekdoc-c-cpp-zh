```
```cpp
X1* x1 = new X4;
std::cout << "x1->f(): " << x1->f() << '\\n';

X4 x4;
X1& x2 = x4;
std::cout << "x2.f(): " << x2.f() << '\\n';
}
```
```

Line 24 uses virtual dispatch (late binding) via a pointer, line 28 uses virtual dispatch via a reference.

```
```text
X1->f(): 4
X2.f(): 4
```
```

Use of virtual constexpr functions

# 4.9.4 The new Character Type of UTF-8 Strings: `char8_t`

In addition to the character types `char16_t` and `char32_t` from C++11, C++20 gets the new character type `char8_t`. Type `char8_t` is large enough to represent any UTF-8 code unit (8 bits). It has the same size, signedness, and alignment as an unsigned char, but is a distinct type.

![](bbox=[0.117, 0.535, 0.179, 0.582])

# char versus char8_t

A char has one byte. In contrast to a char8_t, the number of bits of a byte and hence of a char is not defined. Nearly all implementations use 8 bits for a byte. The `std::string` is an alias for a `std::basic_string` of chars.

# `std::string` and a `std::string` literal

```
```cpp
std::string std::basic_string<char>
"Hello World's"
```
```

Consequently, C++20 has a new typedef for the character type `char8_t` (line 1) and a new UTF-8 string literal (line 2).

# A new `char8_t` character type and an UTF-8 string literal

```
```cpp
std::u8string std::basic_string<char8_t>
u8"Hello World"
```
```

The program char8Str.cpp shows the straightforward usage of the new character type char8_t.