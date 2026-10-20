
```cpp
typename std::enable_if<std::is_convertible<T, std::string>::value>::type
void processString(T&& args);
```

There is an important lesson to be learned here: it is better to have a ridiculous but clear syntax than to have a cool but confusing mess.

## 10.5 Summary

- You can use universal references to bind to all const and non-const objects without losing the information about the constness of the object.
- You can use universal references to implement special handling for passed arguments with move semantics even without using std::forward<>().
- To have a universal reference of a specific type, you need concepts/requirements (since C++20) or some template tricks (up to C++17).
- Only rvalue references of function template parameters are universal references. Rvalue references of class template parameters, members of template parameters, and full specializations are ordinary rvalue references, you can only bind to rvalues.
- When specifying the types of universal references explicitly, they act no longer as universal references. Use Type& to be able to pass lvalues then.
- The C++ standards committee introduced forwarding reference as a “better” term for universal reference. Unfortunately, the term forwarding reference restricts the purpose of universal references to a common specific use case and creates the unnecessary confusion of having two terms for the same thing. Therefore, use universal/forwarding reference to avoid even more confusion.

This page is intentionally left blank

## Chapter 11: Perfect Passing with auto&&

After discussing the usual case of move semantics in generic code, perfect forwarding a parameter, we now have to talk about dealing with return values perfectly. In this chapter, we discuss how to forward return values perfectly to somewhere else. For this purpose, we introduce `auto&&` as another way to declare a *universal reference* (again also called *forwarding reference*). However, we also discuss applications of `auto&&` that have nothing to do with forwarding values.

The next chapter then discusses how to perfectly return values.

### 11.1 Default Perfect Passing

We often have to pass a return value to another function:

```cpp
// pass return value of compute() to process():
process(compute(t));  // OK, uses perfect forwarding of returned value
```

In non-generic code, you know the types involved. However, in generic code, you want to make sure that the return value of `compute()` is perfectly passed to `process()`.

The good news is: if you pass a return value to another function directly, the value is passed perfectly, keeping its type and value category. You do not have to worry about move semantics; it will automatically be used if supported.

### 11.1.1 Default Perfect Passing in Detail

Here is a complete example:

```cpp
#include <iostream>
#include <string>

void process(const std::string& t) {
    std::cout << "process(const std::string&)\n";
}
void process(std::string&) {
    std::cout << "process(std::string&)\n";
}
void process(std::string&&) {
    std::cout << "process(std::string&&)\n";
}
const std::string& computeConstLRef(const std::string& str) {
    return str;
}
std::string& computeLRef(std::string& str) {
    return str;
}
std::string& computeRRef(std::string&& str) {
    return std::move(str);
}
std::string computeValue(const std::string& str) {
    return str;
}
int main() {
    process(computeConstLRef("tmp")); // calls process(const std::string&)
    std::string str{"lvalue"};
    process(computeLRef(str)); // calls process(std::string&)
    process(computeRRef("tmp")); // calls process(std::string&&)
    process(computeRRef(std::move(str))); // calls process(std::string&&)
    process(computeValue("tmp")); // calls process(std::string&&)
}
```

- If compute() returns a const lvalue reference:

```cpp
const std::string& computeConstLRef(const std::string& str) {
    return str;
}
```

the value category of the return value is an lvalue, which means that the return value is perfectly forwarded with the best match for a const lvalue reference:

```cpp
process(computeConstLRef("tmp")); // calls process(const std::string&)
```

- If compute() returns a non-const lvalue reference:

```cpp
std::string& computeLRef(std::string& str) {
    return str;
}
```

the value category of the return value is an lvalue, which means that the return value is perfectly forwarded with the best match for a non-const lvalue reference:

```cpp
std::string str{"lvalue"};
process(computeLRef(str));                // calls process(std::string&)
```

- If compute() returns an rvalue reference:

```cpp
std::string&& computeRRef(std::string&& str) {
    return std::move(str);
}
```

the value category of the return value is an xvalue, which means that the return value is perfectly forwarded with the best match for an rvalue reference, allowing process() to steal its value:

```cpp
process(computeRRef("tmp"));                // calls process(std::string&&)
process(computeRRef(std::move(str)));          // calls process(std::string&&)
```

- If compute() returns a new temporary object by value:

```cpp
std::string computeValue(const std::string& str) {
    return str;
}
```

the value category of the return value is a prvalue, which means that the return value is perfectly forwarded with the best match for an rvalue reference, allowing process() to also steal its value:

```cpp
process(computeValue("tmp"));                // calls process(std::string&&)
```

Note that by returning a const value:

```cpp
const std::string computeConstValue(const std::string& str) {
    return str;
}
```

or a const rvalue reference:

```cpp
const std::string&& computeConstRRef(std::string&& str) {
    return std::move(str);
}
```

you have again disabled move semantics:

```cpp
process(computeConstValue("tmp"));          // calls process(const std::string&)
process(computeConstRRef("tmp"));             // calls process(const std::string&)
```

If we had a declaration for const&&, that overload would be taken.

Therefore: do not mark values returned by value with const and do not mark returned non-const rvalue references with const.

### 11.2 Universal References with auto&&

However, in generic code, how can you program passing a return value later but still keeping its type and value category?

The answer is that again, you need a universal/forwarding reference, which, however, is not declared as a parameter. For this purpose, `auto&&` was introduced.

Instead of:

```cpp
// pass return value of compute() to process():
process(compute(t));  // OK, uses perfect forwarding of returned value
```

you can also implement the following:

```cpp
// pass return value of compute() to process() with some delay:
auto&& ret = compute(t);                // initialize a universal reference with the return value
...
process(std::forward<decltype(ret)>(ret));  // OK, uses perfect forwarding of returned value
```

Or, when using brace initialization:

```cpp
// pass return value of compute() to process() with some delay:
auto&& ret{compute(t)};                // initialize a universal reference with the return value
...
process(std::forward<decltype(ret)>(ret));  // OK, uses perfect forwarding of returned value
```

See generic/perfectautoref.cpp for a complete example with all cases.

### 11.2.1 Type Deduction of auto&&

If you declare something with `auto&&`, you also declare a universal reference. You define a reference that binds to all value categories and the type of this reference preserves the type and the value category of its initial value.

If you declare

```cpp
auto&& ref{...};        // ref is a universal/forwarding reference
```

the type ref is deduced according to the same type deduction rules as universal references being function template parameters:

```cpp
template<typename T>
void callFoo(T&& ref);  // ref is a universal/forwarding reference
```

By rule, the type of ref (which is the type `auto&&` or `T&&`) is

- An lvalue reference if we refer to an lvalue
- An rvalue reference if we refer to an rvalue

For example:

```cpp
// forward declarations:
std::string retByValue();
std::string& retByRef();
std::string&& retByRefRef();
const std::string& retByConstRef();
const std::string&& retByConstRefRef();

// deduced auto&& types:
std::string s;

auto&& r1{s};        // std::string&
auto&& r2{std::move(s)};    // std::string&&
```

