¹ Alexandres has been the main voice in the world of policy classes, and has described a wide set of techniques based on them.

² In C++11, you have to declare the return type as `-> T`.

³ The order in which the qualifiers is removed has no semantic consequence. We could first remove `volatile` and then `const` instead.

⁴ Using the term decoy might be slightly confusing, because in C it only implies the conversion from array/function types to pointer types, whereas here it also includes the removal of top-level `const`-/`volatile` qualifiers.

⁵ Strictly speaking, the comma prior to the second ellipsis (`...`) is optional but is provided here for clarity. Due to the ellipsis being optional, the function type in the first partial specialization is actually syntactically ambiguous: It can be parsed as either `A<T>(args...)` (a C-style varargs parameter) or `B<T>(args... name)` (a parameter pack). The second interpretation is picked because `Args` is an unexpanded parameter pack. We can implicitly add the comma in the (rare) cases where the other interpretation is desired.

⁶ The difference between the return type and `T` is discoverable by direct use of `decltype`. However, given `declval`'s limited use, this is not of practical interest.

⁷ The fallback declaration can sometimes be a plain member function declaration instead of a member function template.

⁸ However, the SFINAE failure were more limited back then: When substitution of a template corresponds in a malformed type (e.g., `T::where` is `int`), SFINAE worked as expected, but if it resulted in an invalid expression (e.g., `sizeof(f())` where `f()` returns `void`), SFINAE did not kick in and an error was issued straight away.

⁹ The first edition of this book was perhaps the first source for this technique.

¹⁰ Defining `void_t` inside namespace `std` is formally invalid: User code is not permitted to add declarations to namespace `std`. In practice, no current compiler enforces that restriction, nor do they behave unexpectedly if, instead of introducing that doing this to “undefined behavior,” this allows anything to happen.

¹¹ At the time of this writing, Microsoft Visual C++ only supports the unfortunate exception.

¹² Thanks to Loris D'Ancona for pointing out the technique described in this section.

¹³ This very simple pair of helper templates is a fundamental technique that lies at the heart of advanced libraries such as Boost.Hana.

¹⁴ This code is not valid C++ because a lambda expression cannot appear directly in a `decltype` operand for compiler-technical reasons, but the meaning is clear.

¹⁵ For simplicity, the return value just uses `decltype(auto)`. In practice, the return type should also be computed using `decltype(auto)` and `noexcept` to avoid that references are returned.

¹⁶ At the time of this writing, the C++ standardization committee is exploring ways to “reflect” various program entities (like class types and their members) in ways that the program can explore. See Section 17.9 on page 363.

¹⁷ Except that `decltype` expressions do not require a comma before the non-void return type to be complete, unlike expressions in other contexts. Using `decltype` is therefore not always the same as using `decltype(auto)`.

¹⁸ The expression `std::invoke` is a general-purpose tool that can be used to invoke callable objects.

¹⁹ The latest count is 48.

²⁰ Most compilers support intrinsic operators like `__is_union` to help standard libraries implement various traits templates.