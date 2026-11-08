will output `['1', '2', '1', '4', '5']` for `21.5_B7`.

Note that this technique is only supported for numeric literals that are valid even without the suffix. For example:

Click here to view code image

```
auto a = 01.3_B7;       // OK: deduces <'0', '1', '3'>
auto b = 0.1_B7;        // OK: deduces <'0', '1'>
auto c = 015_B7;        // ERROR: B is no valid octal literal digit
auto d = hello_B7;      // ERROR: identifier hello_B7 is not defined
auto e = hello_B7;      // ERROR: Literal operator _B7 does not exist
```

See Section 23.6 on page 599 for an application of the feature to compute integral literals at compile time.

# 15.6 VALUE REFERENCES

C++11 introduced rvalue references to enable move semantics, including more semantic and perfect forwarding. This section describes their interactions between value references and deduction.

# 15.6.1 REFERENCE COLLAPSING RULES

Programmers are not allowed to directly declare a reference to a reference:

Click here to view code image

```
int const& r = 42;
int const& & r2 = r;  // ERROR: reference to reference is not allowed
```

However, when composing types through the substitution of template parameters, type aliases, or decltype constructs, such situations are permitted. For example:

Click here to view code image

```
using T = int&;
int&& r = 42;
T&& r2 = r;       // T&& is then int&
```

The rules that determine the type resulting from such a composition are known as the reference collapsing rules. If `&` and `&&` are combined in a type, the resulting reference is always an lvalue reference. If two rvalue references are combined, the result is an rvalue reference. Table 15.1, which can be summarized as “if either reference is an lvalue reference, so is the resulting type; otherwise, it is an rvalue reference.”

| Inner reference | Outer reference | Resulting reference |
|---|---|---|
| `&` | `&` | `&` |
| `&` | `&&` | `&` |
| `&&` | `&` | `&` |
| `&&` | `&&` | `&&` |

*Table 15.1. Reference Collapsing Rules*

One more example shows these rules in action:

Click here to view code image

```
using T = int const&;
RVO volatile T& = 42;  // OK: & type int const
using R = int&&;
R& r = 42;
```

Here `volatile` is applied on top of the reference type (`T` alias for `int const`) and is therefore discarded. An rvalue reference is then placed on top of that type, but since the underlying type is an lvalue reference and value references “take precedence” in the reference collapsing rule, the overall type remains `int const&`. (Of course, this is equivalent to applying `const` on top of `r`.) This is discarded, and applying an rvalue reference on top of the resulting value reference type, still leaves `r` with an rvalue reference type in the end (which is able to bind an rvalue like 42).

# 15.6.2 FORWARDING REFERENCES

As introduced in Section 6.6 on page 61, template argument deduction behaves in a special way when a function parameter is a forwarding reference (an rvalue reference to a template parameter of that function template). In this case, template argument deduction considers not just the type of the function call argument but also whether that argument is an lvalue or an rvalue. In the cases where the argument is an lvalue, the type determined by template argument deduction is an lvalue reference to the argument type, and the reference collapsing rules (see above) ensure that the