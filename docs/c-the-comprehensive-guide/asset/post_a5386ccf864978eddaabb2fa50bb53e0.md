
- `add_1` uses the verbose syntax with `requires` after the template header. Here, the type `T` has a name that you can refer to in the `requires` part.
- `add_2` uses a particularly compact shorthand in the template header that utilizes a previously defined concept.
- `add_3` uses the abbreviated function template with `auto` parameter instead of the template header. You hardly notice that you are defining a template.
- `add_4` compensates for the disadvantage of `add_3`, which is that without a template header, you don’t have a name for the template parameter. However, you can determine the type of the parameter with `decltype` and then restrict it even after the function header with `requires`.

The added value is apparent when you try to call the function with a non-integral. The compiler reports to me at `add_3("text")` (excerpt):

```
error: no matching function for call to 'add_3(const char [5])'
template argument deduction/substitution failed:
required for the satisfaction of 'integral<const char *>'
```

This error message states directly and precisely that `const char*` is not integral and therefore cannot be used.

In the headers and documentation of the standard library, many parameters and return types are now described using concepts. This way, you know what parameters the template functions and classes expect.

In the case of `integral`, it's simple: for type `T`, the trait `is_integral<T>::value` must be defined as true. According to the standard, this is the case for `bool`, `char`, `char8_t`, `wchar_t`, `short`, `int`, `long`, `long long`, and their unsigned versions (the compiler implementation may offer more).

But not only the error messages get better. Concepts can also distinguish between multiple overloads of a function that would otherwise be indistinguishable. An API could, for example, offer the same function overloaded once for integral and once for floating-point.

```cpp
// https://godbolt.org/z/Kxxz5ETh6
#include <concepts> // integral, floating_point
#include <iostream>
using namespace std;

int64_t trunc_to_10(integral auto val) { return (val/10)*10; }
int64_t trunc_to_10(floating_point auto val) { return int64_t(val/10)*10; }
int main() {
    cout << trunc_to_10(144) << '\n';    // Output: 140
    cout << trunc_to_10(122.2) << '\n';  // Output: 120
}
```

**Listing 23.25** With concepts, you can restrict individual overloads.

The integral implementation covers all data types from char to long long, while the floating-point implementation covers everything from float16 to long double.

Because the implementations for integral and floating-point are slightly different, concepts provide an easy way to separate the two implementations. Without concepts, you would either have to provide many overloads from char to long double or use type traits, which are not as easy to read.

The requires shown so far always introduce a requires clause. I have always referred to an existing concept. However, you can also encounter a requires expression to formulate a condition ad hoc:

```cpp
template<typename T>
  requires requires(T p) { *p; }
auto max_deref_value(T a, T b) { return *a > *b ? *a : *b; }
```

The first requires is the introduction of the requires clause; the second is the introduction of the requires expression for T p when you cannot refer to a named concept.

You can find more useful concepts of the standard library in Table 23.1. There are many more, especially in the `<iterator>` and `<ranges>` headers.

Many concepts of the standard library build on each other, creating a kind of hierarchy. For example, regular includes the equality_comparable and semiregular concepts—with semiregular in turn requiring copyable, which then requires movable.

| Concept | Description |
|---|---|
| `same_as` | T and U are the same type |
| `derived_from` | T is derived from U |
| `convertible_to` | T is implicitly convertible to U |
| `integral` | Integral type |
| `signed_integral` | Signed integral type |
| `unsigned_integral` | Unsigned integral type |
| `floating_point` | Floating-point type |
| `assignable_from` | T is assignable from U |
| `swappable` | `swap()` is applicable on T |
| `destructible` | Can be removed without throwing an exception |
| `constructible_from` | Constructor can be called with Args... |
| `default_initializable` | Has default constructor |
| `move_constructible` | Has move constructor |
| `copy_constructible` | Has copy constructor |
| `copyable` | Copyable |
| `movable` | Can be moved |
| `equality_comparable` | Can be compared with == |
| `totally_ordered` | Can be compared with < |
| `three_way_comparable` | Can be compared with `<=>` (from `<compare>`) |
| `semiregular` | Copy, move, and default constructor |
| `regular` | Semiregular and == |
| `invocable` | F can be called with Args... |
| `predicate` | F can be called with Args... and returns bool |
| `relation` | F can be called with T and returns bool |

**Table 23.1** Some useful concepts from the standard library.

### 23.4.2 How to Use Concepts

In the previous section, you saw some examples of self-written functions that work with existing concepts. When you write functions and classes with concepts yourself, you have a few more tools at your disposal.

The easiest way is to write a concept name instead of typename in the angle brackets `<>` of the template header or before the auto of an abbreviated function template:

```cpp
// https://godbolt.org/z/eaGrE4bqr
auto min2(const std::integral auto &a, const std::integral auto &b) {
    return a<b ? a : b;
};
```

```cpp
auto min3 = []<std::integral T>(const T &a, const T &b, const T &c) {
    return min2(a, min2(b,c));
};
```

For this T, we then specify some requires, which we combine with &&. The first requires is the introduction of the entire requires clause. The subsequent requires each introduce requires expressions within the clause. OR combinations with || are also possible, but much rarer.

The AND combination consists of the individual requirements that must be met. There are three types:

- **Type requirement**  
  In the example, it is copyable<T>. The type T is used in another concept that must be true.
- **Simple requirement**  
  The example states that the mk_string(t) + mk_string(t) expression must be valid for a t of type T. The expression is *not executed*; it is only checked whether the expression compiles based on the types.
- **Composite requirement**  
  Beyond the simple requirement, the arrow -> indicates a type requirement for the expression.

The simple and composite requirements should each end with a semicolon ;.

### 23.4.3 How to Write Concepts

Now, it would be tedious to repeat the entire list of requirements every time you write a function. Therefore, you can define recurring concepts with the concept keyword.

```cpp
// https://godbolt.org/z/Tcxnr6jTM
template<typename T>
concept dbl_quotable = copyable<T> &&
requires(T t) { mk_string(t) + mk_string(t); } &&
requires(T t) {
  {mk_string(t)} -> same_as<string>;
};
string dbl_quote(const dbl_quotable auto& val) {
  auto val2(val); // Create a copy (for demonstration purposes only)
  return "" + mk_string(val) + mk_string(val2) + "";
}
```

**Listing 23.27** Define recurring requirements with concept.

What you previously wrote directly in front of the function with an && chain of requires, you now define with concept and give it a name. You can then use this name in later templates. In the example, I implemented this with the auto of an abbreviated function template.

Finally, I want to mention that you can also use concepts together with using. This way, you can also restrict a type alias with a concept:

```cpp
// https://godbolt.org/z/9qsGW6M8Y
template<std::ranges::range T>        // a range over type T
using ValueTypeOfRange = std::ranges::range_value_t<T>;
// or
template<typename T>
requires std::ranges::range<T>         // a range over type T
using ValueTypeOfRange = std::ranges::range_value_t<T>;
// results in:
ValueTypeOfRange<std::vector<int>> x;  // x is int
ValueTypeOfRange<std::string> y;       // y is char
ValueTypeOfRange<std::list<double>> z; // z is double
ValueTypeOfRange<int> w;               // ✗ int is not a range
```

Even within `if constexpr` you can use concepts. The following listing shows a minimal example of it.

```cpp
if constexpr (std::integral<T>) {
  // T is an integral type
} else if constexpr (std::floating_point<T>) {
  // T is a floating-point type
} else {
  // T is neither
}
```

**Listing 23.28** This is how you use concepts in a constexpr if.

Here, `if constexpr (std::integral<T>)` checks whether T is an integral type, and then `if constexpr (std::floating_point<T>)` checks whether T is a floating-point type. A different example can be found in *Chapter 25*, *Listing 25.6*, where also two `if constexpr` check for concept requirements.

### 23.4.4 Semantic Constraints

So far, I have mainly shown you how to constrain templates using concepts that work based on *syntactic errors*. This means that if something would not compile (or would result in nonsense, as in the case of pointer comparisons), you constrain it with a concept.

However, the standard library also uses concepts to check the semantics of templates. This means that even if it would technically work, you can use traits or other agreements to change the semantics so that concepts notice this and enforce a constraint.
