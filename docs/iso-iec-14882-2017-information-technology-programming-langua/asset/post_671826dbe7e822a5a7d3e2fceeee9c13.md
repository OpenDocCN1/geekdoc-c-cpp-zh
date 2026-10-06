
# ISO/14882:2017(E)

```cpp
return [](auto& ... ts) {
    printer(std::forward<decltype(ts)>(ts)...);
}
```

```cpp
return []() {
    printer(is);
};

auto p = vlambda((auto v1, auto v2, auto v3) {
    std::cout << v1 << v2 << v3; 
});
auto q = p(1, 'a', 3.14);

```

The function call or operator template is declared const (12.2.2) and only if the lambda-expression's parameter-declaration-clause is not followed by mutable. It is neither virtual nor volatile. Any noexcept-specifier specified on a lambda-expression-seq pertains to the corresponding function call operator or operator template. A lambda-declarator pertains to the type of the corresponding function call operator or operator template specializing in the corresponding lambda-expression is declared by const, or satisfies the requirements for a constexpr function (10.1.5). [Note: Names referred to in the lambda-declarator are looked up in the context in which the lambda-expression appears.

```cpp
auto ID = [](auto a) { return a; };
static_assert(ID == 3); // OK
```

Example: 

```cpp
struct NonLiteral {
    NonLiteral(int n) : n(n) {}
};
static_assert(NonLiteral(3).n == 3); // ill-formed

auto monoid = [](auto v) { return [=] { return v; }; };
auto add = [](auto m1) constexpr {
    auto ret = m1();
    return [=](auto m2) mutable {
        auto mval = m1();
        auto plus = [=](auto m2) mutable {
            return mval += m2;
        };
        return plus;
    };
    return monoid(ret);
};

constexpr auto zero = monoid();
constexpr auto one = add(one);
static_assert(add(one)(zero()) == one()); // OK
```

// Since two is below is not declared constexpr, an evaluation of this constexpr member function call operator // cannot perform an value-to-reference conversion on one of its subobjects (that represents its capture) // in a constant expression.

```cpp
auto two = monoid(2);
assert(two() == 2); // OK, not a constant expression.
```

§ 8.1.5.1 ©ISO/IEC 2017 - All rights reserved 100

# ISO/IEC 14882:2017(E)

```cpp
static_assert(add(one)one() == two()); // ill-formed: two is not a constant expression
static_assert(add(one)one() == monoid(2)); // OK
// end example
```

- 6 The closure for a non-generic-lambda with lambda-capture has a conversion function to pointer to function with C++ language (10.5) having the same parameter and return types as the closure's type call operator. The conversion is “pointer to noexcept function” if the function call operator has a non-throwing exception specification. The value returned by this conversion function is the address of a function F that, which has the same effect as invoking the closure's type call operator. F is a const function. For a generic lambda with lambda-capture the closure template has a conversion function template to pointer. The conversion function template has the same parameters as the function call operator. The return type of the pointer to function shall behave as it is a decay-specifier type the return type of the corresponding call operator template specialization.

- 7 Note: If the lambda has no-return-type or the trailing-return-type type detection of the corresponding function call operator type specialization is to be done. The corresponding specialization is instantiation of the function call operator template with the same arguments as those declared for the conversion function template. Consider the following:
```cpp
auto lambda = [](auto a) { return a; };
int f(lambda) = lambda();
```
The behavior of the conversion function of lambda is like that of the following conversion function:
```cpp
struct Closure {
template<class T> T operator()(T t) const { ... };
template<class T> T static auto lambda_call_operator_invoker(T a) a {
    // forwards execution to operator()(a) and therefore has
    
}
template<class T> T> operator fptr_t<T> const
ndecltype(lambda_call_operator_invoker(declval<T>())) (*)(T);
template<class T> T> operator fptr_t<T>() {
    return &lambda_call_operator_invoker;
};
```

--Example:
```cpp
void f1(int (*)(int)) { }
void f2(char (*)(int)) { }
```
```cpp
void g(int (*)(int)) { } // #1
void g(char (*)(int)) { } // #2
```
```cpp
void h(int (*)(int)) { } // #3
void h(char (*)(int)) { } // #4
```

```cpp
auto lambda = [](auto a) { return a; };
f1(lambda); // OK
f2(lambda); // error: ID is not convertible
g(lambda); // error: ambiguous
h(lambda); // OK: calls #3 since it is convertible from ID
```

§ 8.1.5.1

ISO/IEC 2017 - All rights reserved 101

# ISO/IEC 14882:2017(E)

```cpp
auto lambda = [](auto a) { return a; };
int f(lambda) = lambda();
```
The behavior of the conversion function of lambda is like that of the following conversion function:
```cpp
struct Closure {
template<class T> T operator()(T t) const { ... };
template<class T> T static auto lambda_call_operator_invoker(T a) a {
    // forwards execution to operator()(a) and therefore has
    
}
template<class T> T> operator fptr_t<T> const
ndecltype(lambda_call_operator_invoker(declval<T>())) (*)(T);
template<class T> T> operator fptr_t<T>() {
    return &lambda_call_operator_invoker;
};
```

--Example:
```cpp
void f1(int (*)(int)) { }
void f2(char (*)(int)) { }
```
```cpp
void g(int (*)(int)) { } // #1
void g(char (*)(int)) { } // #2
```
```cpp
void h(int (*)(int)) { } // #3
void h(char (*)(int)) { } // #4
```

```cpp
auto lambda = [](auto a) { return a; };
f1(lambda); // OK
f2(lambda); // error: ID is not convertible
g(lambda); // error: ambiguous
h(lambda); // OK: calls #3 since it is convertible from ID
```

§ 8.1.5.1

```cpp
auto lambda = [](auto a) { return a; };
int f(lambda) = lambda();
```
The behavior of the conversion function of lambda is like that of the following conversion function:
```cpp
struct Closure {
template<class T> T operator()(T t) const { ... };
template<class T> T static auto lambda_call_operator_invoker(T a) a {
    // forwards execution to operator()(a) and therefore has
    
}
template<class T> T> operator fptr_t<T> const
ndecltype(lambda_call_operator_invoker(declval<T>())) (*)(T);
template<class T> T> operator fptr_t<T>() {
    return &lambda_call_operator_invoker;
};
```

# ISO/IEC 14882:2017(E)

## 8.1.5.2 Captures

[PAGE 114]

# ISO/IEC 14882:2017(E)

### lambda-capture-capture

lambda-capture:
  capture-default
  capture-list
capture-default:
  =
capture-list:
  ... opt
  capture-list , ... opt
capture:
  simple-capture
  init-capture
simple-capture:
  identifier
  & identifier
  this
  * this
init-capture:
  identifier initializer
  & identifier initializer

[expr.prim.lambda.capture]

1. The body of a lambda-expression may refer to variables with automatic storage and the *this object (if any) of enclosing blocks by capturing these entities, as described.
2. If a lambda-capture includes a capture-default that is =, a simple-capture of that-capture shall be preceded by &. A lambda-capture includes a capture-default that is =, each simple-capture of that-capture shall be of the form "&identifier" or "*this". [Note: The form [&,] is redundant but accepted for compatibility with C++ 2014.] Ignoring appearances in initializers of init-capture, an identifier shall not appear more than once in a lambda-capture. Example:

```cpp
struct S2 { void f(int i); };
void f(int i) {
[i]; // OK
[&](); // error: i preceded by & when & is the default
[*this](); // OK
[*this](); // error: when = is the default
[i](); // error: i repeated
[this, i](); // error: this appears twice
}
```

3. The identifier whose smallest enclosing scope is a block scope (6.3.3) is a local lambda expression; any other lambda-expression shall not have a capture-default or simple-capture in its lambda-introducer. The reaching scope of a local lambda expression is the set of enclosing scopes up to the innermost function and its parameters. [Note: This reaching scope includes any intervening lambda-expressions.

The identifier in a simple-capture is looked up the usual rules for unqualified name lookup (6.4.1) where such lookup shall find an entity. An entity designated by a simple-capture is said to be explicitly captured, and shall be *this (when the simple-capture is "this" or "*this") or a variable with automatic storage duration declared in the reaching scope of the local lambda expression.
