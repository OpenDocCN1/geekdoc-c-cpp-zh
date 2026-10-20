# 8.4 When Lvalues become Rvalues

As we have learned, when a function is declared with an rvalue reference parameter of a concrete type, you can only bind these parameters to rvalues. For example:

```
void rvFunc(std::string&&);    // forward declaration

std::string s{...};
rvFunc(s);                     // ERROR: passing an lvalue to an rvalue reference
rvFunc(std::move(s));          // OK, passing an xvalue
```

However, note that sometimes, passing an lvalue seems to work. For example:

```
void rvFunc(std::string&&);    // forward declaration

rvFunc("hello");              // OK, although "hello" is an lvalue
```

Remember that string literals are lvalues when used as an expression. Therefore, passing them to an rvalue reference does not compile. However, there is a hidden operation involved, because the type of the argument (array of six constant characters) does not match the type of the parameter. We have an implicit type conversion, performed by the string constructor, which creates a temporary object that does not have a name.

Therefore, what we really call is the following:

```
void rvFunc(std::string&&);    // forward declaration

rvFunc(std::string{"hello"});  // OK, "hello" converted to a string is a prvalue
```

# 8.5 When Rvalues become Lvalues

Let us now look at the implementation of a function that declares the parameter as an rvalue reference:

```
void rvFunc(std::string&& str) {
    ...
}
```

As we have learned, we can only pass rvalues:

```
std::string s{...};
rvFunc(s);                     // ERROR: passing an lvalue to an rvalue reference
rvFunc(std::move(s));          // OK, passing an xvalue
rvFunc(std::string{"hello"}); // OK, passing a prvalue
```

However, when we use the parameter str inside the function, we are dealing with an object that has a name. This means that we use str as an lvalue. We can do only what we are allowed to do with an lvalue.

This means that we cannot directly call our own function recursively:

```
void rvFunc(std::string&& str) {
    rvFunc(str);                // ERROR: passing an lvalue to an rvalue reference
}
```