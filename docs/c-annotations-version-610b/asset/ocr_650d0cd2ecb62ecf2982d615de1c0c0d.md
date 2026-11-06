Other operators can easily and analogously be constructed.

Operators like the above were defined for the `ios::openmode` enumeration type, allowing us to specify `ios::in | ios::out` as argument to `open` while specifying the corresponding parameter as `ios::openmode` as well. Clearly, operator overloading can be used in many situations, not necessarily only involving class-types.

# 11.12 User-defined literals (C++11, 4.7)

The C++11 standard offers *user-defined literals*, also known as *extensible literals*. Standard C++ defines various kinds of literals, like numerical constants (with or without suffixes), character constants and string (textual) literals.

A user-defined literal is defined by a function (see also section [22.3](#)) that must be defined at namespace scope. Such a function is called a literal operator. A literal operator cannot be a class member function. Under the C++11 standard the names of a literal operator must start with an underscore, and a literal operator is used (called) by *suffixing* its name (including the underscore) to the argument that must be passed to it. Assuming `_NM2km` (nautical mile to km) is the name of a literal operator, then it could be called as `100_NM2km`, producing, e.g., the value 185.2.

Using `Type` to represent the return type of the literal operator its generic declaration looks like this:

```
Type operator "" _identifier(parameter-list);
```

The blank space trailing the empty string is required. The parameter lists of literal operators can be:

+   - `unsigned long long int`. It is used as, e.g., `123_identifier`. The argument to this literal operator can be decimal constants, binary constants (initial `0b`), octal constants (initial `0`) and hexadecimal constants (initial `0x`);
+   - `long double`. It is used as, e.g., `12.25_NM2km`;
+   - `char const *text`. The text argument is an ASCII-Z string. It is used as, e.g., `1234_pental`. The argument must *not* be given double quotes, and must represent a numeric constant, as also expected by literal operators defining `unsigned long long int` parameters.
+   - `char const *text, size_t len`. Here, the compiler determines `len` as if it had called `strlen(text)`. It is used as, e.g., `"hello"_nVowels`;
+   - `wchar_t const *text, size_t len`, same as the previous one, but accepting a string of `wchar_t` characters. It is used as, e.g., `L"1234"_charSum`;
+   - `char16_t const *text, size_t len`, same as the previous one, but accepting a string of `char16_t` characters. It is used as, e.g., `u"utf 16"_uc`;
+   - `char32_t const *text, size_t len`, same as the previous one, but accepting a string of `char32_t` characters. It is used as, e.g., `U"UTF 32"_lc`;

If literal operators are overloaded the compiler will pick the literal operator requiring the least ‘effort’. E.g., `120` is processed by a literal operator defining a `unsigned long long int` parameter and not by its overloaded version, defining a `char const *` parameter. But if overloaded literal operators exist defining `char const *` and `long double` parameters then the operator defining a `char const *` parameter is used when the argument `120` is provided, while the operator defining a `long double` parameter is used with the argument `120.3`.

A literal operator can define any return type. Here is an example of a definition of the `_NM2km` literal operator:

```
double operator "" _NM2km(char const *nm)
```