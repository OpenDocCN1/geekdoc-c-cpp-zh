# ISO/IEC 14882:2017(E)

that is implicitly defined (see 6.3.3).

The function-local defined variable `__func__` is defined as a definition of the form
static char __func__[] = "function-name";
had been provided, where *function-name* is an implementation-defined string. It is unspecified whether
a variable has an address distinct from any other object in the program.[103] [Example:

```
struct S {
    S(): s(__func__) {}      // OK
    const char s;
    void f(const char& s = __func__); // error: __func_ is undeclared
}; // end example
```

# 11.4.2 Explicitly-defined functions

+   A definition of the form:
attribute-specifier-seq_opt dec-specifier-seq_opt declarator virt-specifier-seq_opt
is called an explicitly-defined function. A function that is explicitly defined shall
be a member function,
have the same declared function type (except for possibly different ref-qualifiers and except that
in the case of a constructor or copy assignment operator, the parameter type may be “reference to non-const T”, T is the name of the member function's class) as if it had been declared,
have default arguments.

+   An explicitly-defined function that not default may be declared `constexpr` if only it
have been implicitly declared or explicitly defined on its first declaration, it is
implicit to be `constexpr` if the implicit declaration would be.
If a function that is explicitly defined is declared with a `noexcept`-specification that does not produce the same
exception specification as the implicit declaration (18.4), then
if the function is explicitly defined on its first declaration, it is declared as default;
therwise, the program is ill-formed.

```
Example:
struct S {
    S() = default;              // ill-formed: implicit S is not constexpr
    S(int a = 0) = default;     // ill-formed: default argument
    void operator=(const S&) = default; // ill-formed: non-matching return type
    S() const noexcept(false) = default;  // deleted: exception specification does not match
private:
    int i;
    S(S);\                       // OK: private copy constructor
};
S::S(const S&) = default;      // OK: copy constructor
// end example
```

Explicitly-defined functions and implicitly-declared functions are collectively *defaulted* functions, and
the implementation shall provide implicit definitions for them (15.5.14, 15.8), which might mean defining

[103] Implementations are permitted to provide predefined variables with names that are reserved to the implementations-ion (5.10). If a predefined variable is not od-used (6.6), its string value need not be present in the program image.