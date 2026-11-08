that type. For example:

Click here to view code image

```
```cpp
template<typename T> void f(T&& p); // p is a forwarding reference

void g()
{
    int i;
    int& r = i; // An lvalue reference
    f(i);       // argument is an lvalue: T is int&
    f(r);       // argument is an lvalue: T is int&
    f(1);       // argument is an rvalue: T is int
}
```
```

In the call f(i), the template parameter T is deduced to int&, since the expression is an lvalue type int. Substituting T for int& in the parameter type T& implies reference collapsing, and we apply the rule & + & = & to resolve the resulting parameter type int&, which is the parameter type used for the call f(i). In the call f(1), the argument is an rvalue and the template parameter is therefore deduced to be the type that the call f(1) contains.

Click here to view code image

```
```cpp
template<typename T> void f(T&& p) // p is a forwarding reference
{
    T&& x; // For passed lvalues, x is a reference
    ...
}
```
```

This means that the definition of the function f above needs to be carefully written to ensure that all uses of T (including the return type) are written in a way that works properly with lvalue arguments. To deal with this situation, the std::forward() function template ... reference types is frequently used to represent it as a reference.

Click here to view code image

```
```cpp
template<typename T> void f(T&& p) // p is a forwarding reference
{
    static_assert(!std::is_lvalue_reference<T>::value,
                  "T is not a reference");
    ...
}
```
```

# ### 15.6.3 PERFECT FORWARDING

The combination of the special deduction rule for rvalue references and the reference collapsing rules makes it possible to write a function template with a parameter that accepts almost any argument and captures its special properties (its type and whether it is an lvalue or an rvalue). The function template can then "forward" the argument along to another function as follows:

Click here to view code image

```
```cpp
class C {
    ...
};

void g(C& c1)
{
    C c2;
    f(c1); // forwards C&
    f(c2); // forwards C&
    f(C()); // forwards C&&
}

template<typename T>
void f(T&& x)
{
    g(std::forward<T>(x)); // forward x to g()
}
```
```

The technique illustrated above is called perfect forwarding, because the result of calling g() indirectly through f() will be the same as if the code had called g() directly. No additional copies are made, and the same overloads (if any) will be selected.

In the case of g(), a function call with the function f(C()) requires some additional explanation. In such an instantiation of f, the parameter x will have rvalue reference type or lvalue reference type. Regardless, the expression x will be an lvalue of the type that the argu-