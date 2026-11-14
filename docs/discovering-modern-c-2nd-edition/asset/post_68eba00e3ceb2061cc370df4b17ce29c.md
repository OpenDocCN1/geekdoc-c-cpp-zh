
integral or floating-point types respectively. Conversions to `int` and `double` are preferred (over longer types) when possible as these are considered to have the "natural" size in arithmetic operations (i.e., being best supported by hardware). The integral promotions are, in detail:

- A `char`, `signed char`, `unsigned char`, `short int`, or `unsigned short int` is converted to an `int` if it can represent all source type values; otherwise, it is converted to `unsigned int`.

- A `char8_t`, `char16_t`, `char32_t`, `wchar_t`, or plain `enum` is converted to the first of the following types that is able to hold all source type values: `int`, `unsigned int`, `long`, `unsigned long`, `unsigned long long`.

- A bit-field is converted to an `int` if it can represent all values of the former; otherwise to an `unsigned int` under the same conditions. Otherwise, no promotion applies.

- A `bool` is converted to an `int`: `false` becomes `0` and `true` turns into `1`.

Promotions are used as part of arithmetic conversions (§C.3.3). Source: [62, §10.5.1].

## C.3.2 Other Conversions

C++ performs the following potentially narrowing conversions implicitly:³

3. Modern compilers often give warnings about it.

- Integer and plain `enum` types can be converted to any integer type. If the target type is shorter, leading bits are cut off.

- Floating-point values can be converted to shorter floating-point types. If the source value lies between two destination values, the result is one of them; otherwise, the behavior is undefined.

- Pointers and references: Any pointer to object to `void*` (evil old-style hacking, though). In contrast, pointers to functions or members cannot be converted to `void*`. Pointers/references to derived classes can be implicitly converted to pointers/references to (unambiguous) base classes. `0` (or an expression yielding `0`) can be converted to any pointer type, resulting in a null pointer. `nullptr` is preferable. `T*` can be converted to `const T*`, likewise `T&` to `const T&`.

- bool: Pointers, integral, and floating-point values can be converted to `bool`: zero values become `false`, all others `true`. Remark: None of these conversions contributes to understanding programs better.

- Integer<=>floating-point: When a floating-point is converted to an integer, the fractional part is discarded (rounding toward 0). If the value is too large to be represented, the behavior is undefined. The conversion from integer to a floating-point type is exact when the former is representable in the target type. Otherwise, the next lower or higher floating-point value is taken (which one is implementation-dependent). In the unlikely case that it is too large for the floating-point type, the behavior is undefined.

Source: [62, §10.5.2] and standard.

## C.3.3 Usual Arithmetic Conversions

These conversions are performed on operands of a binary operator to turn them into a common type which is then used as a result type:

- If either operand is `long double`, the other is converted to `long double`;

- Otherwise, if either operand is `double`, the other is converted to `double`;

- Otherwise, if either operand is `float`, the other is converted to `float`;

- Otherwise, integral promotion from Section C.3.1 is performed on both operands.

- Otherwise, if either operand is `unsigned long long`, the other is converted to `unsigned long long`;

- Otherwise, if one operand is a `long long` and the other an `unsigned long`, then the `unsigned long` is converted to `long long` if the latter can represent all values of the former; otherwise, both are converted to `unsigned long long`.

- Otherwise, if one operand is a `long` and the other an `unsigned`, then the `unsigned` is converted to `long` if the latter can represent all values of the former; otherwise, both are converted to `unsigned long`.

- Otherwise, if either operand is `long`, the other is converted to `long`;

- Otherwise, if either operand is `unsigned`, the other is converted to `unsigned`;

- Otherwise, both operands are converted to `int`.

As a consequence, programs with mixed `signed` and `unsigned` integers have platform-dependent behavior since the conversion rules depend on the sizes of integer types. Source: [62, §10.5.3].

## C.3.4 Narrowing

A `Narrowing Conversion` is an implicit conversion:

- From a floating-point type to an integer type; or

- From `long double` to `double` or `float`, or from `double` to `float`, except where the source is a constant expression and the actual value after conversion is within the range of values that can be represented (even if it cannot be represented exactly); or

- From an integer type or unscoped enumeration type to a floating-point type, except where the source is a constant expression and the actual value after conversion will fit into the target type and will produce the original value when converted back to the original type; or

- From an integer type or unscoped enumeration type to an integer type that cannot represent all the values of the original type, except where the source is a constant expression and the actual value after conversion will fit into the target type and will produce the original value when converted back to the original type.

Source: ISO standard.

## Bibliography

- [1] David Abrahams and Aleksey Gurtovoy. C++ Template Metaprogramming: Concepts, Tools, and Techniques from Boost and Beyond. Addison-Wesley, 2005.

- [2] Douglas Adams. Life, the Universe and Everything. Pan Macmillan, 1980.

- [3] Bryce Adelstein. “Core C++ 2019 :: Bryce Adelstein :: Modules are Coming.” https://www.youtube.com/watch?v=DtDM6y6fNSU, July 2019.

- [4] Matthew H. Austern. Generic Programming and the STL: Using and Extending the C++ Standard Template Library. Addison-Wesley, 1999.

- [5] Lewis Baker. CppCoro – A coroutine library for C++. https://github.com/lewissbaker/cppcoro.

- [6] John J. Barton and Lee R. Nackman. Scientific and Engineering C++. Addison-Wesley, 1994.

- [7] L. Susan Blackford, Antoine Petitet, Roldan Pozo, Karin Remington, R. Clint Whaley, James Demmel, Jack Dongarra, Iain Duff, Sven Hammarling, Greg Henry, et al. “An updated set of basic linear algebra subprograms (blas).” ACM Transactions on Mathematical Software, 28(2):135–151, 2002.

- [8] Walter E. Brown. “Three "random"-related proposals, v2.” Technical Report N3742, ISO/IEC JTC 1, Information Technology, Subcommittee SC 22, Programming Language C++, August 2013.

- [9] Krzysztof Czarnecki and Ulrich Eisenecker. “Meta-control structures for template metaprogramming.” http://home.t-online.de/home/Ulrich.Eisenecker/meta.htm.

- [10] Krzysztof Czarnecki and Ulrich W. Eisenecker. Generative Programming: Methods, Tools, and Applications. Addison-Wesley, 2000.

- [11] Ionut Danaila, Frédéric Hecht, and Olivier Pironneau. *Simulation Numérique en C++*. Dunod, Paris, 2003.

- [12] Stefanus Du Toit. “Hourglass interfaces for C++ APIs.” http://de.slideshare.net/StefanusDuToit/cpp-con-2014-hourglass-interfaces-for-c-apis, 2014.

- [13] Margaret A. Ellis and Bjarne Stroustrup. *The Annotated C++ Reference Manual*. Addison-Wesley, 1990.

- [14] Andreas Fertig. “C++20: Aggregate, POD, trivial type, standard layout class, what is what.” https://andreasfertig.blog/2021/01/cpp20-aggregate-pod-trivial-type-standard-layout-class-what-is-what/, 2021.

- [15] Andreas Fertig. *Programming with C++20*. Fertig Publications (via Leanpub), 2021.

- [16] Erich Gamma, Richard Helm, Ralph Johnson, and John Vlissides. *Design Patterns: Elements of Reusable Object-Oriented Software*. Addison-Wesley, 1995.

- [17] Bernhard Ganter and Rudolf Wille. *Formal Concept Analysis: Mathematical Foundations*. Springer Science & Business Media, 2012.

- [18] Peter Gottschling. “Fundamental algebraic concepts in concept-enabled C++.” Technical Report 638, Indiana University, 2006.

- [19] Peter Gottschling. *Mixed Complex Arithmetic*. SimuNova, 2011. http://old.simunova.com/docs/mt14/html/mixed_complex.html, Part of Matrix Template Library 4.

- [20] Peter Gottschling. “Code Reuse in Class Template Specialization.” Technical Report N3596, ISO IEC JTC1/SC22/WG21, 2013. http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2013/n3596.pdf.

- [21] Peter Gottschling. *Matrix Template Library 4*. SimuNova, 2014. http://new.simunova.com/index.xhtml#en-mt14-index-html.

- [22] Peter Gottschling and Andrew Lumsdaine. “Integrating semantics and compilation: using C++ concepts to develop robust and efficient reusable libraries.” In *GPCE '08: Proceedings of the 7th International*
