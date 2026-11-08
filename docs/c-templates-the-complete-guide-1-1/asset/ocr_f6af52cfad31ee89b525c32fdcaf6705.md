```
```cpp
static constexpr auto mytypeConst = is_constexpr?;

if constexpr (mytypeConst)       // compile time
{
    // discarded statement
}

static_assert(std::is_const<MyType>::value, "MyType should ...");
```
```

Having distinct types for non-Boolean `integral_constant` specializations is also useful in various metaprogramming contexts. See the discussion of the similar type `CTValue` in Section 24.3 on page 966 and its use for element access of tuples in Section 25.6 on page 959.

# D.1.2 Things You Should Know When Using Traits

There are a few things to note when using traits:

+   - Type traits apply directly to types, but `decltype` allows us to also test the properties of expressions, variables, and functions. Recall, however, that `decltype(<expr>)` produces the type of a variable or function only if the expression is the name of an entity (enclosed in parentheses); for any other expression, it yields a type that also reflects the type category of the expression. For example:

```
```cpp
void foo (std::string& s)
{
    // Check the type of s:
    std::is_lvalue_reference<
        decltype(s)>::value          // true
    std::is_lvalue_reference<
        decltype(std::move(s))>::value // false
    std::is_lvalue_reference<
        decltype((s))>::value         // true, s used as lvalue
}
```
```

See Section 15.10.2 on page 598 for details.

+   - Some traits may have nonintuitive behavior for the novice programmer. See Section 9.1.3 on page 159 for example.
+   
+   - Some traits have requirements or preconditions. Violating these preconditions results in undefined behavior. See Section 20.1.1 on page 164 for some examples.
+   
+   - Many traits require complete types (see Section 10.3.1 on page 54). To be able to use them for incomplete types, we can sometimes introduce templates to defer their evaluation (see Section 11.5 on page 174 for details).
+   
+   - Sometimes the logical operators `&&`, `||`, and `!` cannot be used to define new type traits based on other type traits. In addition, dealing with traits that might fail can become a problem or at least require some drawbacks. For this reason, special traits are provided that allow us to logically combine Boolean traits. See Section D.6 on page 734 for details.
+   
+   - Although the standard alias templates (ending with `_t` or `_v`) are often convenient, they also have downsides, making them unsuitable in some metaprogramming contexts. See Section 19.7.3 on page 424 for details.

# D.2 PRIMARY AND COMPOSITE TYPE CATEGORIES

We start with the standard traits that test primary and composite type categories (see Figure D.1). In general, each type belongs to exactly one primary type category (the white elements in Figure D.1). Composite type categories then merge multiple type categories into higher-level concepts.

![](bbox=[0.08, 0.719, 0.92, 0.836])

# D.2.1 Testing for the Primary Type Category

This section describes type utilities that test the primary type category of a given type. For any given type, exactly one of the primary type categories has a value `true` member that evaluates to `true`. The result is independent of whether the type is qualified with `const` and/or `volatile` (cv-qualified).

Note that for types `std::size_t` and `std::ptrdiff_t`, it is implementation-defined which of these primary type categories yields `true`. For type `std::max_align_t`, which one of these primary type categories yields `true` is also an implementation detail (this, in turn, depends on the language-specific ...).