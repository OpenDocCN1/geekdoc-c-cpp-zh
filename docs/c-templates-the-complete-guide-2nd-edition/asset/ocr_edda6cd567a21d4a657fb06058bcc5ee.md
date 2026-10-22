the expression x does indeed name an entity (in other cases, the parentheses have no effect). For example, if the expression x simply names a variable v, the construct without parentheses becomes `decltype(v)`, which produces the type of the variable v rather than a type reflecting the value category of the expression x referring to that variable.

Thus, using type traits for any expression e, we can check its value category as follows: [Click here to view code image](#)

```
if constexpr (std::is_lvalue_reference<decltype((e))>::value) {
  std::cout << "expression is lvalue\n";
}
else if constexpr (std::is_rvalue_reference<decltype((e))>::value) {
  std::cout << "expression is xvalue\n";
}
else {
  std::cout << "expression is prvalue\n";
}
```

See Section 15.10.2 on page 298 for details.

# B.4 Reference Types

Reference types in C++—such as `int&`—interact with value categories in two important ways. The first is that a reference may limit the value category of an expression it can bind to. For example, a non-const lvalue reference of type `int&` can only be initialized with an expression that is an lvalue of type `int`. Similarly, an rvalue reference of type `int&&` can only be initialized with an expression that is an rvalue of type `int`.

+   The second way in which value categories interact with references is with the return types of functions, where the use of a reference type as the return type affects the value category of a call to that function. In particular:
+   
+   - A call to a function whose return type is an lvalue reference yields an lvalue.
+   - A call to a function whose return type is an rvalue reference to an object type yields an xvalue (rvalue references to function types always result in lvalues).
+   - A call to a function that returns a nonreference type yields a prvalue.

We illustrate the interactions between reference types and value categories in the following example. Given: `int& lvalue();` `int&& xvalue();` `int prvalue();` both the value category and type of a given expression can be determined via `decltype`. As described in Section 15.10.2 on page 298, it uses