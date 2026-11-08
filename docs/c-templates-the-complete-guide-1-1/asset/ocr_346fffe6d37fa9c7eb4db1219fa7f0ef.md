```
```cpp
return contains(buf);
}
```
```

if constexpr (IsInt) produces an int; we want to pass that int to the value (say more bytes to take an address of it). That exposes an important property: the return type of a function with deduced return type can depend on the value of its arguments. For example, `decltype(auto)` (see Section 8.1.4 on page 183) produces an `int` for this function if we call it with `int` (or `short`):

![](bbox=[0.1, 0.12, 0.9, 0.13])

```
```cpp
decltype(auto) g = [](auto& maybeIsInt) // IsInt
{
    int i = 1024;
    return maybeIsInt; // MAYBE int
};
```
```

Note that parentheses in the initializer may be significant (they are significant for the `decltype` semantics as discussed in Section 8.1.4 on page 183).

![](bbox=[0.1, 0.23, 0.9, 0.24])

```
```cpp
int i1;
decltype(auto) a = g(i1); // object of type int
decltype(auto) a = g(42); // reference of type int&&
```
```

This essentially means that parentheses can have an impact on the validity of return statements.

![](bbox=[0.1, 0.33, 0.9, 0.34])

```
```cpp
int i2;
decltype(auto) f() {
    int i = 0;
    return (i); // RUNTIME ERROR: reference to temporary
}
```
```

Since `i2` and `(i2)` differ in type, they can be used for notable template metaprogramming techniques (see Section 8.1.4 on page 183). The following example illustrates that:

![](bbox=[0.1, 0.43, 0.9, 0.44])

```
```cpp
template<typename T> class S {
private:
    T value;
public:
    constexpr S(T const& v) : value{ v } { }
    constexpr T const& get() const {
        return value;
    }
};
S<int> s = 42;
S<decltype(s)>* p = &s; // does not work
S<decltype((s))>* q = &s; // works
```
```

In line 2, the lack of parentheses around `s` causes the deduced type to be of the type `(int&)`, `(int&&)` or `(int)`. Because a non-`const` expression of type `S<int>`, this expression is an lvalue, so `(s)` is an lvalue, so `decltype((s))` is `S<int>&`. This means `p` has the type `S<S<int>>`, which means we cannot use it in the same way we handle the typical use of `decltype`. Thus, with this declaration the class template depends on a reference to `S`, and any change of value might impact the behavior of `(class S)`. (See Section 8.1.4 on page 183 for details.) But `(s)` is an lvalue, so `decltype((s))` is a reference type, `(s)` is an lvalue, and the resulting type is `S<int>&`. In other words, `decltype((s))` and `decltype(s)` are of the same type here. Note that the nature of the two cases is somewhat different; we do therefore we do not have a `decltype((s))` `p` will have a reference type. This means we cannot change `p`, and so `decltype((s))` `q` will be `S<int>&`. This means `q` can be a reference to an `S` object. Note that the nature of the two cases is somewhat different; we do therefore we do not have a `decltype((s))` `p` will have a reference type. This means we cannot change `p`, and so `decltype((s))` `q` will be `S<int>&`. This means `q` can be a reference to an `S` object.

Finally, a comment about using `decltype` with non-type template parameters:

![](bbox=[0.1, 0.76, 0.9, 0.77])

```
```cpp
template<int N> struct S { };
template<int N> void f(int(&)[N]) { }
int a[] = { 1, 2, 3, 4, 5 };
int b[10];
f(a); // OK
```
```

In this example, the type of the parameter `f` of function template `f` is `int(&)[N]`. This deduced from the type of the template parameter `N`. If `a` is passed to `f`, `N` must be `5`, because `a` is a `int[5]` declared with `[]` and `int` elements. Note that the type of the parameter is deduced from the argument type. This is not a reference to an array. However, note that for `b` `N` is `10`.

![](bbox=[0.1, 0.86, 0.9, 0.87])

```
```cpp
template<int N> struct S { };
int a[] = { 1, 2, 3, 4, 5 };
int b[10];
S<decltype(a)> s1; // OK
S<decltype(b)> s2; // ERROR: decltype(a) is a reference type
```
```

In this case, `decltype(a)` is a non-deduced context. There is no unique way to deduce `N` from `a` and `a` is an array of `int` and `a` is of type `int[5]` and `b` is of type `int[10]`. Therefore, the non-type template parameter `N` must be explicitly specified to be able to call this function.

# 5.10.4 Special Situations for Auto Deduction

There are a few special situations for auto deduction: The same deduction rules for `auto` apply, but there is a special case for `auto` in a function template. Note that the `auto` in a function template parameter is not a template parameter but a placeholder for a type. The `auto` in a function template parameter is not a template parameter but a placeholder for a type. The `auto` in a function template parameter is not a template parameter but a placeholder for a type.