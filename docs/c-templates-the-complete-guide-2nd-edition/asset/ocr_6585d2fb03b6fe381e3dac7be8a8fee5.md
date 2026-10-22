references “take precedence” in the reference collapsing rule, the overall type remains int const& (or RCI, which is an equivalent alias). Similarly, the const on top of RRI is discarded, and applying an rvalue reference on top of the resulting rvalue reference type, still leaves us with an rvalue reference type in the end (which is able to bind an rvalue like 42).

# 15.6.2 Forwarding References

As introduced in Section 6.1 on page 91, template argument deduction behaves in a special way when a function parameter is a forwarding reference (an rvalue reference to a template parameter of that function template). In this case, template argument deduction considers not just the type of the function call argument but also whether that argument is an lvalue or an rvalue. In the cases where the argument is an lvalue, the type determined by template argument deduction is an lvalue reference to the argument type, and the reference collapsing rules (see above) ensure that the substituted parameter will be an lvalue reference. Otherwise, the type deduced for the template parameter is simply the argument type (not a reference type), and the substituted parameter is an rvalue reference to that type. For example: Click here to view code image

```
template<typename T> void f(T&& p); // p is a forwarding reference

void g()
{
int i;
int const j = 0;
f(i); // argument is an lvalue; deduces T to int& and
// parameter p has type int&
f(j); // argument is an lvalue; deduces T to int const&
// parameter p has type int const&
f(2); // argument is an rvalue; deduces T to int
// parameter p has type int&&
}
```

In the call f(i) the template parameter T is deduced to int&, since the expression i is an lvalue of type int. Substituting int& for T into the parameter type T&& requires reference collapsing, and we apply the rule & + && ! & to conclude that the resulting parameter type is int&, which is perfectly suited to accept an lvalue of type int. In contrast, in the call f(2), the argument 2 is an rvalue and the template parameter is therefore deduced to simply be the type of that rvalue (i.e., int). No reference collapsing is needed