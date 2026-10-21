```
};

// base types are deduced from passed arguments:
template<typename... Ts>
overload(Ts...) -> overload<Ts...>; 
```

you can overload two lambdas as follows:

```
auto twice = overload {
    [](std::string& s) { s += s; },
    [](auto& v) { v *= 2; }
};
```

Here, we create an object of type overload, where we use a deduction guide to deduce the types of the lambdas as base classes of the template type overload and use aggregate initialization to initialize the subobjects for the bases classes with the copy constructor of the closure type of each lambda.

The using declaration then makes both function call operators available for type overload. Without the using declaration, the base classes would have two different overloads of the same member function operator(), which would be ambiguous.

As a result, you can pass a string, which calls the first overload, or pass another type, which (provided operator *= is valid) uses the second overload:

```
int i = 42;
twice(i);
std::cout << "i: " << i << '\n';  // prints: 84
std::string s = "hi";
twice(s);
std::cout << "s: " << s << '\n';  // prints: hihi
```

One application of this technique are std::variant visitors.

# 14.2 Variadic Using Declarations for Inheriting Constructors

Together with some clarifications on inheriting constructors, the following is also possible now: you can declare a variadic class template Multi that derives from a base class for each of its passed types:

tmpl/using2.hpp

```
template<typename T>
class Base {
    T value{};
public:
    Base() {
    ...
```