
```cpp
// ...
template void f<int>(); // manual instantiation
```

This structure provides some flexibility. One can include only `E.cpp` to get an explicit instantiation. Note also that the object file generated from `E.cpp` can be used to instantiate the templates. The more likely approach is to include `E.hpp` to get an explicit instantiation declaration, or to include `E.cpp` to get an explicit instantiation definition.

### 14.5.2 Explicit Instantiation Declarations

A more targeted approach to the initialization of explicit instantiations is the use of an explicit instantiation declaration, which is also called an extern template. An explicit instantiation declaration suppresses automatic instantiation of the template specialization, whereas an explicit instantiation definition causes instantiation of the template specialization (as for explicit instantiation definitions). We can generally declare but not define explicit instantiation declarations. Such declarations can be more complex than that.

- Inline functions can still be instantiated for the purpose of expanding them inline (but no explicit object code is generated).
- Variables with declared `auto` or `decltype(auto)` types and functions with deduced return types can still be instantiated to determine their types.
- Variables whose values are usable as constant-expressions can still be instantiated to determine their values.
- Variables of reference types can still be instantiated as they would be if they were not templates.
- Class templates and also template functions can still be instantiated to check the resulting types.

Using explicit instantiation declarations, we can provide the template definition for the headers (e.g., `E.hpp`) and suppress automatic instantiation for commonly used specializations, as follows:

[Click here to view code image](#)

```cpp
// e.hpp
extern template void f<int>(); // declaration
```

[Click here to view code image](#)

```cpp
// e.cpp
template void f<int>();        // definition
```

Each explicit instantiation declaration must be paired with a corresponding explicit instantiation definition, which must follow the explicit instantiation declaration. Omitting the definition would result in a linker error.

Explicit instantiation declarations can be used to improve compile time only when certain specializations are used in many different translation units. Unlike with manual instantiation, which requires manually updating the list of explicit instantiation declarations each time a new specialization is used, the compiler automatically performs the declaration as an optimization at any point. However, the compile-time benefits may not be as significant as with manual instantiation, because some redundant automatic instantiation is likely to occur ... and because the template definitions are still parsed as part of the header.

## 14.6 COMPILE-TIME IF STATEMENTS

As introduced in Section 8.5 on page 134, C++17 added a new statement kind that turns out to be remarkably useful when writing templates: compile-time if. It also introduces a new variable in the instantiation process.

[Click here to view code image](#)

```cpp
template<typename T> void f(T p) {
  if constexpr (sizeof(T) <= sizeof(long long)) {
    // ... code for types that fit in a long long
    return p+posnap<0 > 1;
  } else {
    return p+posnap<0 > 1;
  }
}
```

The compile-time if (`if constexpr`) statement, where the `if` keyword is immediately followed by the keyword `constexpr`, behaves in a way similar to an ordinary `if` with a condition that is known at compile time. The parenthesized condition must be a constant expression whose value (converted to `bool`) is not false. The implicit branches whose condition is not selected are the other branches of the `if` statement and are not instantiated. This means that discarded branches of templates (including generic lambdas) are not instantiated. That is necessary for our example to be valid because we are instantiating `f<1>()` with `T=int`, which means that the `else` branch is discarded. If it weren't discarded, it would be instantiated and would probably result in a compile-time error, because `p+posnap<0 > 1;` is not valid for a `long long`.

The example above, in C++14, might be implemented as follows:

[Click here to view code image](#)

```cpp
template<bool b> struct Dispatch { // only be instanti-
  // ated when b is false
  static bool f(T p) {                 // code to meet spe-
    // cialization for true
    return p > 0;
  }
};
```

[Click here to view code image](#)

```cpp
template<> struct Dispatch<true> {
  static bool f(T p) {
    return p > 0;
  }
};
```

[Click here to view code image](#)

```cpp
template<typename T> bool f(T p) {
  return Dispatch<sizeof(T) == sizeof(long long)>::f(p);
}
```

[Click here to view code image](#)

```cpp
bool g(int n) {
  return f(n); // OK
}
```

Clearly, the constexpr if alternative expresses our intention far more clearly and concisely. However, it requires implementations to refine the unit of instantiation: Whereas previously function definitions were always instantiated as a whole, now it must be possible to inhibit the instantiation of parts of them.

Another very handy use of constexpr if is expressing the recursion needed to handle pattern-matching packs. To generalize the example, introduced in Section 8.5, on page 343:

[Click here to view code image](#)

```cpp
template<typename T, typename... Rem>
void f(T&& h, Rem&&... rem) {
  do_something(std::forward<T>(h));
  if constexpr (sizeof...(rem) > 0) {
    // Hand the remainder recursively, perfectly for-
    // warding the arguments:
    do_something(std::forward<Rem>(rem)...);
  }
}
```

Without constexpr if statements, this requires an additional overload of the `f()` template to ensure that recursion terminates.

Even in non-template contexts, constexpr if statements have a somewhat unique effect:

[Click here to view code image](#)

```cpp
void g() {
  if constexpr (sizeof(int) == 1) {
    h();
  }
}
```

On most platforms, the condition in `g()` is false and the call to `h()` is therefore discarded. As a consequence, `h()` need not necessarily be defined at all (unless it is used elsewhere, of course). Had the keyword `constexpr` been omitted in this example, a lack of a definition for `h()` would elicit an error at link time.

## 14.7 IN THE STANDARD LIBRARY

The C++ standard library includes a number of templates that are only commonly used with a few basic types. For example, the `std::basic_string` class template is most commonly used with `char` (because `std::string` is a type alias of `std::basic_string<char>`) or `wchar_t`, although it is possible to instantiate it with other character-like types. Therefore, it is common for standard library implementations to introduce explicit instantiation declarations for these common cases. For example:

[Click here to view code image](#)

```cpp
namespace std {
  template<typename charT, typename traits =
    char_traits<charT>, typename Allocator = allocator<charT>>
  class basic_string;

  extern template class basic_string<char>;
  extern template class basic_string<wchar_t>;
}
```

The source files implementing the standard library will then contain the corresponding explicit instantiation definitions, so that these common implementations can be shared among all users of the standard library. Similar explicit instantiations often exist for the various stream classes, such as `basic_istream`, `basic_ostream`, and so on.

## 14.8 AFTERNOTES

This chapter deals with two related but different issues: the C++ template compilation model and various C++ template instantiation mechanisms.

The compilation model determines the meaning of a template at various stages of the translation of a program. In particular, a template model determines what the various constructs in a template mean when it is instantiated. However, the 1998 and 2003 standards also supported a separation model of template compilation, which allowed a template definition to be written in a different translation unit from its instantiations. These separated templates were only ever implemented once, by the Edison Design Group (EDG). Their implementation offered tremendous insight into (1) implementing the separation model of C++ templates was vastly more difficult and time consuming than had been anticipated, and (2) the preferred benefits of the separation model, such as improved compile times, did not materialize due to complexities of the model. As the development of the 2003 standard was wrapping up, it became clear that other implementers were not going to support the feature, and the C++ standards committee voted to remove exported templates from the language. We refer readers interested in the details of the separation model to the first edition of this book, which describes the behavior of export.

The instantiation mechanisms are the external mechanisms that allow C++ implementations to create instantiations correctly. These mechanisms may be constrained by requirements of the linker and other software building tools. While instantiation mechanisms differ from one implementation to the next (and each has its trade-offs), they generally do not have a significant impact on day-to-day programming in C++.

Shortly after C++11 was completed, Walter Bright, Herb Sutter, and Andrei Alexandrescu proposed a “static if” feature but could not agree (via paper N3329). It has, however, a more general form that could appear even outside of template definitions. (Walter Bright is the principal designer and implementer of the D programming language, which has a similar feature.) For example:

[Click here to view code image](#)

```cpp
template<unsigned long N>
struct X {
  static if (N <= 1) {
    constexpr unsigned long value = 1;
  } else {
    constexpr unsigned long value = N*fact<N-1>::value;
  }
};
```

Note how class-scope declarations are made conditional in this example. This powerful ability was controversial, however, with some committee members fearing that it might be abused and others not liking some technical aspects of the proposal (such as the fact that the top scope is treated by the braces and the discarded branch is not parsed at all).

A few years later, Ville Voutilainen came back with a proposal (P0128) that was mostly what would become constexpr if statements. It went through a few minor design iterations (involving tentative keywords `static_if` and `constexpr_if`), and with the help of Jens Maurer, Ville eventually shepherded the proposal into the language (via paper P0292).

The term instantiation is sometimes misused to refer to the creation of objects from types. In this book, however, it always refers to template instantiation.

- 1. The term instantiation is used in the general sense of an entity that is a specific instance of a template (see Chapter 10). It does not refer to the explicit specialization mechanism described in Chapter 16.
- 2. The term specialization is used in the general sense of an entity that is a specific instance of a template (see Chapter 10). It does not refer to the explicit specialization mechanism described in Chapter 16.
- 3. Anonymous unions are always special in this way: Their members can be considered to be members of the enclosing class. An anonymous union is primarily a construct that says that some class members share the same storage.
- 4. Some compilers, such as GCC, allow zero-length arrays as extensions and may therefore accept this code even when it is not valid in C++.
- 5. Typical examples are smart pointer templates (e.g., the standard `std::unique_ptr<>`).
- 6. Besides two-phase lookup, terms such as two-range lookup or two-phase name lookup are also used.
- 7. Surprisingly, it is not clearly specified in the standard at the time of this writing. However, it is not expected to be a controversial issue.
- 8. The call operator of generic lambda is a subtle exception to that observation.
- 9. In modern compilers the binding of data is typically handled by a mostly language-independent component of the compiler (called the back end or middle end). However, C++ front ends may also have the ability to expand all inline because older back ends were too conservative when considering calls for inline expansion.
- 10. The original C++98 standard also provided a separation model. It never gained popularity and was removed just before publishing the C++11 standard.
- 11. Current systems have grown to detect certain differences, however. For example, they might report if a declaration has associated debugging information and another does not.
- 12. When a compiler is unable to inline every call to a function that you marked with the keyword `inline`, a separate copy of the function is emitted in the object file. This may happen in multiple object files.
- 13. Virtual function calls are usually implemented as indirect calls through a table of pointers to functions. See the discussion of such implementations for a thorough explanation.
