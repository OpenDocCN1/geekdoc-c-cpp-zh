An xvalue is then considered a special location, representing an object whose resources can be reused (usually because the object is near the end of its lifetime).

C++17 then introduces a new term, called materialization (of a temporary), for the moment a prvalue becomes a temporary object. Thus, a temporary materialization conversion is a prvalue-to-xvalue conversion.

Any time a prvalue validly appears where a glvalue (lvalue or xvalue) is expected, a temporary object is created and initialized with the prvalue (remember that prvalues are primarily “initializing values”), and the prvalue is replaced by an xvalue designating the temporary. So in the example above, strictly speaking, we have:

```
void f(const X& p);  // accepts an expression of any value category,
                     // but expects a glvalue

f(X());              // passes a prvalue materialized as xvalue
```

Because f() in this example has a reference parameter, it expects a glvalue argument. However, the expression X() is a prvalue. The “temporary materialization” rule therefore kicks in, and the expression X() is “converted” into an xvalue designating a temporary object initialized with the default constructor.

Note that materialization does not mean that we create a new/different object. The lvalue reference p still binds to both an xvalue and a prvalue, although the latter now always involves a conversion to an xvalue.

With this modification (that prvalues are no longer objects but are instead expressions that can be used to initialize objects), the required copy elision makes perfect sense because the prvalues no longer need to be movable in order to initialize a variable using assignment syntax. We simply pass an initial value around that, sooner or later, is materialized to initialize an object.

# 5.4 Unmaterialized Return Value Passing

Unmaterialized return value passing applies to all forms of returning a temporary object (prvalue) by value:

+   - When we return a literal that is not a string literal:
+   ```
+   int f1() {  // return int by value
+       return 42;
+   }
+   ```
+   - When we return a temporary object by its type or auto:
+   ```
+   auto f2() {  // return deduced type by value
+       ...
+       return MyType{...};
+   }
+   ```
+   - When we return a temporary object by decltype(auto):
+   ```
+   decltype(auto) f3() {  // return temporary from return statement by value
+       ...
+       return MyType{...};
+   }
+   ```