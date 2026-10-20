```
// pass return value of compute() to process():
process(compute(t));  // OK, uses perfect forwarding of returned value
```

you can also implement the following:

```
// pass return value of compute() to process() with some delay:
auto&& ret = compute(t);                // initialize a universal reference with the return value
...
process(std::forward<decltype(ret)>(ret));  // OK, uses perfect forwarding of returned value
```

Or, when using brace initialization:

```
// pass return value of compute() to process() with some delay:
auto&& ret{compute(t)};                // initialize a universal reference with the return value
...
process(std::forward<decltype(ret)>(ret));  // OK, uses perfect forwarding of returned value
```

See generic/perfectautoref.cpp for a complete example with all cases.

# 11.2.1 Type Deduction of auto&&

If you declare something with auto&&, you also declare a universal reference. You define a reference that binds to all value categories and the type of this reference preserves the type and the value category of its initial value.

If you declare

```
auto&& ref{...};        // ref is a universal/forwarding reference
```

the type ref is deduced according to the same type deduction rules as universal references being function template parameters:

```
template<typename T>
void callFoo(T&& ref);  // ref is a universal/forwarding reference
```

By rule, the type of ref (which is the type auto&& or T&&) is

+   - An lvalue reference if we refer to an lvalue
+   - An rvalue reference if we refer to an rvalue

For example:

```
// forward declarations:
std::string retByValue();
std::string& retByRef();
std::string&& retByRefRef();
const std::string& retByConstRef();
const std::string&& retByConstRefRef();
```

```
// deduced auto&& types:
std::string s;
```

```
auto&& r1{s};        // std::string&
auto&& r2{std::move(s)};    // std::string&&
```