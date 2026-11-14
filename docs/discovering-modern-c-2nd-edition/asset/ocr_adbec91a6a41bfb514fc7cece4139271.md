```
auto i = 2 * 4, j; // Error: j not initialized
auto v = g(x, y, z); // result of g
```

We can qualify `auto` with `const` and reference qualifiers:

Click here to view code image

```
auto& ri = i; // reference on i
const auto& cri = i; // constant reference on i
auto&& fr = g(x, y, z); // forward reference to result of g
```

The type deduction with `auto` variables works exactly like the deduction of function parameters, as described in Section 3.1.2. This means, for instance, that the variable `v` in the preceding snippet is not a reference even when `g` returns a reference. Likewise, the universal reference `fr` is either an rvalue —when `g` returns a value or an rvalue reference—or an lvalue—when `g` returns an lvalue reference.

# C++11 3.4.2 Type of an Expression

The other new feature for type deduction in C++11 is `decltype`. It looks like a function and returns the type of an expression. If `f` in the first `auto` example returns a value, we could also express it with `decltype`:

Click here to view code image

```
decltype(f(g(x, y, z) + 3 * x)) a = f(g(x, y, z) + 3 * x);
```

Obviously, this is too verbose and thus not very useful in this context.

The feature is very important in places where an explicit type is needed: first all as a type argument for class templates. We can, for instance, declare a vector whose elements can hold the sum of two other vectors’ elements, e.g., the type of `v1[0] + v2[0]`. This allows us to express the appropriate return type for the sum of two vectors of different types:

Click here to view code image

```
template <typename Vector1, typename Vector2>
auto operator+(const Vector1& v1, const Vector2& v2)
-> vector< decltype(v1[0] + v2[0]) >;
```

This code snippet also introduces another new feature: *Trailing Return Type*. In C++11, we are still obliged to declare the `return` type of every