# Chapter 17

# Future Directions

C++ templates have been evolving almost continuously from their initial design in 1998, through the various standardization milestones in 1998, 2014, 2017, and 2020. It could be argued that template eras have somewhat related to most major language additions after the original 98 standard.

The first edition of this book listed a number of extensions that we might see after the first standard, and several of those became reality:

+   - The angle bracket hack: C++11 removed the need to insert a space between two closing angle brackets.
+   - Default function template arguments: C++11 allows function templates to have default template arguments.
+   - Typedef templates: C++11 introduced alias templates, which are similar.
+   - The type operator: C++11 introduced the `decltype` operator, which fills the same role (but uses a different token to avoid a conflict with an existing extension that doesn't quite meet the needs of the C++ programmers community).
+   - Static properties: The first edition anticipated a selection of type traits being supported directly by compilers. This has come to pass, although the interface is expressed using the standard library (which is then implemented using compiler extensions for many of the traits).
+   - Custom instantiation diagnostics: The new keyword `static_assert` implements the idea described by `std::instantiation_error` in the first edition of this book.
+   - List parameters: This became parameter packs in C++11.
+   - Layout control: C++11's `alignof` and `alignas` cover the needs described in the first edition. Furthermore, the C++17 library added a `std::variant` template to support discriminated unions.
+   - Initializer deduction: C++17 added class template argument deduction, which addresses the same issue.
+   - Function expressions: C++11 added lambda expressions, providing exactly this functionality (with a syntax somewhat different from that discussed in the first edition).

Other directions hypothesized in the first edition have not made it into the standard language, but most are still discussed on occasion and we keep their presentation in this volume. Meanwhile, other ideas are emerging and we present some of them as well.

# 17.1 RELAXED TYPE NAME RULES

In the first edition of this book, this section suggested that the future might bring two kinds of relaxations to the rules for the use of type names (see Section 13.3.2 on page 258): Allow typename where it was not previously allowed, and make typename optional where a compiler can reliably infer that a qualified name with a dependent qualifier must name a type. The former came to pass (typename in C++11 can be used outside a template), the latter has not.

Recently, however, there has been a renewed call to make typename optional in various common contexts where the exception of a type are unambiguous:

+   - The return type and parameter types of function and member function declarations in namespace and class scope. Similarly with function and member function templates and with lambda expressions appearing in any scope.
+   - The types of variable, variable template, and static data member declarations. Again, similarly with variable templates.
+   - The type after the `=` token in an alias or alias template declaration.
+   - The default argument of a type parameter of a template.
+   - The type appearing in the angle brackets following a `static_cast`, `const_cast`, `dynamic_cast`, or `reinterpret_cast`.
+   - The type named in a new expression.