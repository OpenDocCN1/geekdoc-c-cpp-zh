![](bbox=[0.111, 0.103, 0.174, 0.151])

# **Concepts in C++20: An Evolution or a Revolution?**

This small detour expresses my opinion. First, I present the facts, then I draw my conclusion. The facts are based on what has been presented in this chapter. So which arguments speak for evolution or revolution?

# **Evolution**

+   - Concepts promote working with generic code at a **higher level of abstraction**.
+   - Concepts give you **understandable error messages** when compiling a template fails. They provide nothing you could not achieve with the type-traits library⁷, SFINAE⁸, and static_assert⁹.
+   - auto is a kind of unconstrained placeholder. With C++20, we can use concepts as **constrained placeholders**.
+   - With C++14, we could use generic lambdas as a convenient way to define function templates.

# **Revolution**

+   - Concepts allow us to **verify template requirements** for the first time. Of course, you can also achieve the verification of template parameters with a combination of type-traits library¹⁰, SFINAE¹¹, and static_assert¹², but this technique is way too advanced to regard it as a general solution.
+   - Thanks to the abbreviated function-template syntax, defining templates has been radically improved.
+   - Concepts represent **semantic categories**, but not syntactic constraints. Instead of a concept such as `Addable`, which requires that a type supports the + operator, we should think in terms of a concept `Number`, where `Number` is a semantic category such as `Equal` or `Ordering`.

# **My Conclusion**

There are many arguments whether concepts are an evolutionary step or a revolutionary jump. Mainly because of the semantic categories, I'm on the revolution side. Concepts such as `Number`, `Equal`ity, or `Ordering` remind me of Plato's¹³ world of ideas. It is ***revolutionary*** that we can now reason about programming in such categories.

+   7. https://en.cppreference.com/w/cpp/header/type_traits
+   8. https://en.cppreference.com/w/cpp/language/sfinae
+   9. https://en.cppreference.com/w/cpp/language/static_assert
+   10. https://en.cppreference.com/w/cpp/header/type_traits
+   11. https://en.cppreference.com/w/cpp/language/sfinae
+   12. https://en.cppreference.com/w/cpp/language/static_assert
+   13. https://en.wikipedia.org/wiki/Plato