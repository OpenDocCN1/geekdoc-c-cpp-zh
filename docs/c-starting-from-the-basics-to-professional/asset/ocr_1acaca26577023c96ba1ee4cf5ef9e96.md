The prefixes u8, u, and U to the literals indicate that they are UTF-8, UTF-16, and UTF-32, respectively. If your editor and compiler have the capability to process Unicode characters, and you know how to type such letters on your keyboard, you can define Unicode character variables without using the escape sequences as well (see Chapter 1):

```
wchar_t cc {L'¢'};
char8_t yen {u8'¥'};
char16_t delta {u'δ'};
char32_t ya {U'Я'};
```

Because UTF-8 and UTF-16 are variable-width encodings, not all letters can be represented by a single character. The Greek letter Δ, for instance, needs a sequence of two bytes to be encoded in UTF-8.

```
char8_t delta8 {u8'Δ'};  /* Error: Δ (code point U+0394) encoded as 2 UTF-8 code units */
```

> **Note**  The `char8_t` type was introduced in C++20. Most legacy code and libraries will therefore still use `char` to represent UTF-8 encoded letters. This can be confusing, at times, because the same type is used to store narrow (generally ASCII-encoded) letters. New code should therefore shift toward using `char8_t` as much as possible.

The Standard Library provides standard input and output streams `wcin` and `wcout` for reading and writing characters of type `wchar_t`, but there is no provision with the library for handling `char8_t`, `char16_t`, or `char32_t` character data. We briefly return to processing Unicode characters in Chapter 7, where we discuss strings.

# The auto Keyword

You use the `auto` keyword to indicate that the compiler should deduce the type of a variable. Here are some examples:

```
auto m {10};                 // m has type int
auto n {200uL};              // n has type unsigned long
auto p {std::numbers::pi};   // p has type double
```

The compiler will deduce the types for m, n, and p from the initial values you supply. You can use functional or assignment notation with `auto` for the initial values as well:

```
auto m = 10;                 // m has type int
auto n = 200uL;              // n has type unsigned long
auto p(std::numbers::pi);    // p has type double
```

Having said that, this is not really how the `auto` keyword is intended to be used. When defining variables of fundamental types, you often might as well specify the type explicitly. You’ll meet the `auto` keyword again later in the book where it is more appropriately and much more usefully applied.