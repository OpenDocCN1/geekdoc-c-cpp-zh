# 11.5 Using auto&& in C++20 Function Declarations

Since C++20, you can also declare ordinary functions with auto&&, which is then handled in the same way: it declares a function template with a universal reference.

The following definition:

```
void callFoo(auto&& val) {
    foo(std::forward<decltype(arg)>(arg));
}
```

is equivalent to the following:

```
template<typename T>
void callFoo(T&& val) {
    foo(std::forward<decltype(arg)>(arg));
}
```

This means that you can also explicitly specify the type of the parameter here. However, in the same way as for ordinary function templates, you have to qualify the template parameter with a type that fits the value category of your passed argument:

```
std::string s;
...
callFoo<std::string>(s);                // ERROR: cannot bind rvalue reference to lvalue
callFoo<std::string&>(s);               // OK, does not move and forward s
callFoo<std::string>(std::move(s));     // OK, does move and forward s
callFoo<std::string&&>(std::move(s));   // OK, does move and forward s
```

# 11.6 Summary

+   - Do not return by value with const (otherwise you disable move semantics for return values).
+   - Do not mark returned non-const rvalue references with const.
+   - auto&& can be used to declare a universal reference that is not a parameter. Just like any universal reference, it can refer to all objects of any type and value category and its type is
+     - An lvalue reference (Type&) if it binds to an lvalue
+     - An rvalue reference (Type&&) if it binds to an rvalue
+   - Use std::forward<decltype(ref)>(ref) to perfectly forward a universal reference ref that is declared with auto&&.
+   - You can use universal references to refer to both const and non-const objects and use them multiple times without losing the information about their constness.
+   - You can use universal references to bind to references that are proxy types.
+   - Consider using auto&& in generic code that iterates over elements of a collection to modify them. That way, the code works for references that are proxy types.
+   - Using auto&& when declaring parameters of a lambda (or function, since C++20) is a shortcut for declaring parameters that are universal references in a function template.