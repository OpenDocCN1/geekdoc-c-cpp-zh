Compare this with the former implementation of this function not using additional parentheses. Here, `decltype` of `(str)` yields `std::string&` because `str` is an lvalue of type `std::string`.

The fact that for `decltype`, it makes a difference when we put additional parentheses around a passed name, will also have significant consequences when we later discuss `decltype(auto)`.

# ### Check for a Value Category Inside Code

In general, you can now check for a specific value category inside code as follows:

+   - `!std::is_reference_v<decltype((expr))>`
+     checks whether `expr` is a **prvalue**.
+   - `std::is_lvalue_reference_v<decltype((expr))>`
+     checks whether `expr` is an **lvalue**.
+   - `std::is_rvalue_reference_v<decltype((expr))>`
+     checks whether `expr` is an **rvalue**.
+   - `!std::is_lvalue_reference_v<decltype((expr))>`
+     checks whether `expr` is an **rvalue**.

Note again the additional parentheses used here to ensure that we use the value-category checking form of `decltype` even if we only pass a name as `expr`.

Before C++20, you have to skip the suffix `_v` and append `::value` instead.

# ## 8.7 Summary

+   - Any expression in a C++ program belongs to exactly one of these primary value categories:
+     - **lvalue** (roughly, for a named object or a string literal)
+     - **prvalue** (roughly, for an unnamed temporary object)
+     - **xvalue** (roughly, for an object marked with `std::move()`)
+   - Whether a call or operation in C++ is valid depends on both the type and the value category.
+   - Rvalue references of types can only bind to rvalues (prvalues or xvalues).
+   - Implicit operations might change the value category of a passed argument.
+   - Passing an rvalue to an rvalue reference binds it to an **lvalue**.
+   - Move semantics is not passed through.
+   - Functions and references to functions are always **lvalues**.
+   - For **rvalues** (temporary objects or objects marked with `std::move()`), plain value members have move semantics but reference or static members have not.
+   - `decltype` can either check for the declared type of a passed name or for the type and the value category of a passed expression.