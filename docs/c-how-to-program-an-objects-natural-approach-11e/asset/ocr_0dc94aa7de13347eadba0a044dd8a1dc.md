43 converts type `int` to type `int&`—an *lvalue* reference type. Line 45 converts type `int` to type `int&&`—an *rvalue* reference type. We use `std::is_same_v` to confirm both results.

# Removing *lvalue* and *rvalue* References from a Reference Type

Lines 50, 52 and 54 test the `<type_traits>` header’s predefined `std::remove_reference` metafunction, which removes references from a type. We instantiate `std::remove_ref- erence` with the types `int`, `int&` and `int&&`, respectively:

+   - non-reference types (like `int`) are returned as is,
+   - *lvalue* reference types have the `&` removed, and
+   - *rvalue* reference types have the `&&` removed.

To confirm this, we use `std::is_same_v` to compare `int` to the type returned by each expression in lines 50, 52 and 54. They are the same, so the result is true in each case.

# 15.14 Wrap-Up

This chapter demonstrated the power of generic programming and compile-time polymorphism with templates and concepts. We used class templates to create related custom classes, distinguishing between the templates you write and template specializations the compiler generates from your code when you instantiate templates.

We introduced C++20’s abbreviated function templates and templated lambdas. We used C++20 Concepts to constrain template parameters and overload function templates based on their type requirements. Next, we introduced type traits and showed how they relate to C++20 Concepts. We created our own custom concept and showed how to test it at compile-time with `static_assert`.

We demonstrated how to create a custom concept-constrained algorithm, then used it to manipulate objects of several C++ standard library container classes. Next, we rebuilt our class `MyArray` as a custom container class template with custom iterators. We showed that those iterators enabled C++ standard library algorithms to manipulate `MyArray` elements. We also introduced non-type template parameters for passing compile-time constants to templates and discussed default template arguments.

We demonstrated that variadic templates can receive any number of parameters, first using the standard library’s tuple variadic class template, then with variadic function templates. We also showed how to apply binary operators to variadic parameter packs using fold expressions.

Many of the techniques we demonstrated are newer ways to perform various aspects of compile-time metaprogramming. We also introduced several other metaprogramming techniques, including how to compute values at compile-time with value metafunctions, how to perform compile-time conditional compilation with `constexpr if` and how to modify types at compile-time with type metafunctions.

In the next chapter, we introduce modules—one of C++20’s “big four” features (along with ranges, concepts and coroutines), which provide a new way to organize your code, precisely control which declarations you expose to client code and encapsulate implementation details.