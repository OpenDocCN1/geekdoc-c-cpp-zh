or concepts once they are supported (see Section 6.5 on page 103 and [Appendix E](#): Click here to view code image

```
template<typename T>
requires !std::is_const_v<T>
void outR (T& arg) {
...
}
```

# 7.2.3 Passing by Forwarding Reference

One reason to use call-by-reference is to be able to perfect forward a parameter (see Section 6.1 on page 91). But remember that when a forwarding reference is used, which is defined as an rvalue reference of a template parameter, special rules apply. Consider the following: Click here to view code image

```
template<typename T>
void passR (T&& arg) { // arg declared as forwarding reference
...
}
```

You can pass everything to a forwarding reference and, as usual when passing by reference, no copy gets created: Click here to view code image

```
std::string s = "hi";
passR(s); // OK: T deduced as std::string& (also the type of arg)
passR(std::string("hi")); // OK: T deduced as std::string, arg is std::string&&
passR(returnString()); // OK: T deduced as std::string, arg is std::string&&
passR(std::move(s)); // OK: T deduced as std::string, arg is std::string&&
passR(arr); // OK: T deduced as int (&)[4] (also the type of arg)
```

However, the special rules for type deduction may result in some surprises: Click here to view code image

```
std::string const c = "hi";
passR(c); //OK: T deduced as std::string const&
passR("hi"); //OK: T deduced as char const (&)[3] (also the type of arg)
int arr[4];
passR("hi"); //OK: T deduced as int (&)[4] (also the type of arg)
```

In each of these cases, inside `passR()` the parameter `arg` has a type that “knows” whether we passed an rvalue (to use move semantics) or a constant/nonconstant lvalue. This is the only way to pass an argument, such that