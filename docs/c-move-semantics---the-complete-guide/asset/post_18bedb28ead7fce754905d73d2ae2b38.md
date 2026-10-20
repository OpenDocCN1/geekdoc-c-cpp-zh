
## 11.4 Perfect Forwarding in Lambdas

If you want to perfectly forward parameters of generic lambdas, you also have to use universal references and std::forward<>(). However, you simply use auto&& to declare the universal reference.

```cpp
auto callFoo = [](auto&& arg) {
    foo(std::forward<decltype(arg)>(arg)); // perfectly forward arg
};
```

```cpp
std::string s{"BLM"};
callFoo(s); // OK, arg is std::string&
callFoo(std::move(s)); // OK, arg is std::string&&
```

Note that since C++20, you can avoid using decltype(arg) by declaring the lambda with template parameters.

```cpp
[] (auto&&... args) {
    ...
    foo(std::forward<decltype(args)>(args)...);
};
```

Remember that lambdas are just an easy way to define function objects (objects with operator() defined to allow their use as functions). The definition above expands to a compiler-defined class (closure type) with universal references defined as template parameters:

```cpp
class NameDefinedByCompiler {
    ...
public:
    template<typename... Args>
    auto operator() (Args&&... args) const {
        ...
        foo(std::forward<decltype(args)>(args)...);
    }
};
```

Again, note that a generic rvalue reference that is qualified with const (or volatile) is not a universal reference. This also applies to lambdas. If a parameter is declared with const auto&&, you can only pass rvalues:

```cpp
auto callFoo = [](const auto&& arg) { // arg is not a universal reference
    ...
};
```

```cpp
const std::string cs{"BLM"};
callFoo(cs); // ERROR: cs is not an rvalue
callFoo(std::move(cs)); // OK, arg is const std::string&
```

Inside this lambda, it would be enough to use std::move() to perfectly forward the passed argument.

## 11.5 Using auto&& in C++20 Function Declarations

Since C++20, you can also declare ordinary functions with auto&&, which is then handled in the same way: it declares a function template with a universal reference.

The following definition:

```cpp
void callFoo(auto&& val) {
    foo(std::forward<decltype(val)>(val));
}
```

is equivalent to the following:

```cpp
template<typename T>
void callFoo(T&& val) {
    foo(std::forward<decltype(val)>(val));
}
```

This means that you can also explicitly specify the type of the parameter here. However, in the same way as for ordinary function templates, you have to qualify the template parameter with a type that fits the value category of your passed argument:

```cpp
std::string s;
...
callFoo<std::string>(s);                // ERROR: cannot bind rvalue reference to lvalue
callFoo<std::string&>(s);               // OK, does not move and forward s
callFoo<std::string>(std::move(s));     // OK, does move and forward s
callFoo<std::string&&>(std::move(s));   // OK, does move and forward s
```

## 11.6 Summary

- Do not return by value with const (otherwise you disable move semantics for return values).
- Do not mark returned non-const rvalue references with const.
- auto&& can be used to declare a universal reference that is not a parameter. Just like any universal reference, it can refer to all objects of any type and value category and its type is
    - An lvalue reference (Type&) if it binds to an lvalue
    - An rvalue reference (Type&&) if it binds to an rvalue
- Use std::forward<decltype(ref)>(ref) to perfectly forward a universal reference ref that is declared with auto&&.
- You can use universal references to refer to both const and non-const objects and use them multiple times without losing the information about their constness.
- You can use universal references to bind to references that are proxy types.
- Consider using auto&& in generic code that iterates over elements of a collection to modify them. That way, the code works for references that are proxy types.
- Using auto&& when declaring parameters of a lambda (or function, since C++20) is a shortcut for declaring parameters that are universal references in a function template.

This page is intentionally left blank

## Chapter 12 Perfect Returning with decltype(auto)

After discussing perfect forwarding a parameter and perfectly passing through a returned value, we now have to talk about returning values perfectly. This chapter introduces the new placeholder type decltype(auto). We will also see surprising consequences such as the strong recommendation not to use unnecessary parentheses in return statements.

## 12.1 Perfect Returning

In generic code, we often compute a value that we then return to the caller. The question is, how do we perfectly return the value but still keep whatever type and value category it has? In other words: how should we declare the return type of the following function:

```cpp
template<typename T>
??? callFoo(T&& arg)
{
    return foo(std::forward<T>(arg));
}
```

In this function, we call a function called foo() with the perfectly forwarded parameter arg. We do not know what foo() returns for this type; it might be a temporary value (prvalue), an lvalue reference, or an rvalue reference. The return type might be const or not const.

So, how do we perfectly return the return value of foo() to the caller of callFoo()? A couple of options do not work:

- Return type auto will remove the referenceness of the return type of foo(). If, for example, we give access to the element of a container (consider foo() as the at() member function or index operator of a vector), callFoo() would no longer give access to the element. In addition, we might create an unnecessary copy (if not optimized away).

Any return type that is a reference (auto&, const auto&, and auto&&) will return a reference to a local object if foo() returns a temporary object by value. Fortunately, compilers can issue a warning when they detect such a bug.

That is, we need a way to say:

- Return by value if we got/have a value
- Return by reference if we got/have a reference

but still keep both the type and the value category of what we return.

C++14 introduced a new placeholder type for this purpose: decltype(auto).

```cpp
template<typename T>
decltype(auto) callFoo(T&& arg)    // since C++14
{
    return foo(std::forward<T>(arg));
}
```

With this declaration, callFoo() returns by value, if foo() returns by value, and callFoo() returns by reference if foo() returns by reference. In all cases, both the type and the value category are retained.

## 12.2 decltype(auto)

Just like the other placeholder type auto, decltype(auto) is a placeholder type that lets the compiler deduce the type at initialization time. However, in this case, the type is deduced according to the rules of decltype:

- If you initialize it with or return a plain name, the return type is the type of the object with that name.
- If you initialize it with or return an expression, the return type is the type and value category of the evaluated expression as follows with the following encoding:
    - For a prvalue, it just yields its value type: type
    - For an lvalue, it yields its type as an lvalue reference: type&
    - For an xvalue, it yields its type as an rvalue reference: type&&

For example:

```cpp
std::string s = "hello";
std::string& r = s;
```

```cpp
// initialized with name:
decltype(auto) da1 = s;    // std::string
decltype(auto) da2(s);     // same
decltype(auto) da3{s};     // same
decltype(auto) da4 = r;    // std::string&

// initialized with expression:
decltype(auto) da5 = std::move(s);  // std::string&&
decltype(auto) da6 = s+s;           // std::string
decltype(auto) da7 = s[0];          // char&
decltype(auto) da8 = (s);           // std::string&
```

For the expressions, by rule, the types are deduced as follows:

- Because std::move(s) is an xvalue, da5 is an rvalue reference.
- Because operator+ for strings returns a new temporary string by value (so it is a prvalue), da6 is a plain value type.
- Because s[0] returns an lvalue reference to the first character, it is an lvalue and forces da7 to also be an lvalue reference.
- Because (s) is an lvalue, da8 is an lvalue reference. Yes, the parentheses make a difference here.

In contrast to auto&&, which is always a reference, decltype(auto) is sometimes just a value (if initialized with the name of an object of a value type or with a prvalue expression).

Note that decltype(auto) cannot have additional qualifiers:

```cpp
decltype(auto) da{s};          // OK
const decltype(auto)& da1{s};    // ERROR
decltype(auto)* da2{&s};         // ERROR
```

### 12.2.1 Return Type decltype(auto)

When using decltype(auto) as a return type, we use the rules of decltype as follows:

- If the expression returns/yields a plain value, then the value category is a prvalue and decltype(auto) deduces a value type.
- If the expression returns/yields an lvalue reference, then the value category is an lvalue and decltype(auto) deduces an lvalue reference.
- If the expression returns/yields an rvalue reference, then the value category is an xvalue and decltype(auto) deduces an rvalue reference.

That is exactly what we need for perfect returning: for a plain value, we deduce a value, and for a reference, we deduce a reference of the same type and value category.

As a more general example, consider a helper function of a framework that (after some initialization or logging) transparently calls a function as if we were to call it directly:

```cpp
generic/call.hpp

#include <utility>  // for forward<>()

template <typename Func, typename... Args>
decltype(auto) call (Func f, Args&&... args)
{
    ...
    return f(std::forward<Args>(args)...);
}
```

The function declares args as a variadic number of universal references (also called forwarding references). With std::forward<>(), it perfectly forwards these given arguments to the function f passed as first argument. Because we use decltype(auto) as the return type, we perfectly return the return value of f()
