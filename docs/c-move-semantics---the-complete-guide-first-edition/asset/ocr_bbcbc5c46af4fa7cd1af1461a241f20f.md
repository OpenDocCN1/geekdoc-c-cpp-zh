Any time a prvalue is used where a glvalue (lvalue or xvalue) is expected, a temporary object is created and initialized with the prvalue (remember that prvalues are primarily “initializing values”) and the prvalue is replaced by an xvalue that designates the temporary object. Therefore, in the example above, strictly speaking, we have:

```
```cpp
void f(const X& p);  // accepts an expression of any value category but expects a glvalue

f(X{});              // creates a temporary prvalue and passes it materialized as an xvalue
```
```

Because f() in this example has a reference parameter, it expects a glvalue argument. However, the expression X{} is a prvalue. The “temporary materialization” rule therefore kicks in and the expression X{} is “converted” into an xvalue that designates a temporary object initialized with the default constructor.

Note that materialization does not mean that we create a new/different object. The lvalue reference p still binds to both an xvalue and a prvalue, although the latter now always involves a conversion to an xvalue.

# ## 8.2  Special Rules for Value Categories

We have special rules for the value category of functions and members that have an impact on move semantics.

# ### 8.2.1  Value Category of Functions

A special rule in the C++ standard states that all expressions that are references to functions are lvalues.¹ For example:

```
```cpp
void f(int) {
}

void(&fref1)(int) = f;   // fref1 is an lvalue
void(&&fref2)(int) = f;  // fref2 is also an lvalue

auto& ar = std::move(f); // OK: ar is lvalue of type void(&)(int)
```
```

In contrast to types of objects, we can bind a non-const lvalue reference to a function marked with std::move() because a function marked with std::move() is still an lvalue.

# ### 8.2.2  Value Category of Data Members

If you use data members of objects (e.g., when using members first and second of a std::pair<>), special rules apply.

In general, the value categories of data members are as follows:

+   - Data members of lvalues are lvalues.
+   - Reference and static data members of rvalues are lvalues.
+   - Plain data members of rvalues are xvalues.

¹ Thanks to Daniel Krügler for pointing this out.