Just as with ordinary friend declarations, a friend template can be a definition only if it names an unqualified function name that is not followed by angle brackets.

A friend template can declare only primary templates and members of primary templates. Any partial specializations and explicit specializations associated with a primary template are automatically considered friends too.

# 12.6 AFTER NOTES

The general concept and syntax of C++ templates have remained relatively stable since their inception in the late 1980s. Class templates and function templates were part of the initial template facility. So were type parameters and non-type parameters.

However, there were also some significant additions to the original design, mainly driven by the needs of the C++ standard library. Member templates may well be the most fundamental of those additions. Curiously, only member function templates were formally voted into the C++ standard. Member class templates became part of the standard by an editorial oversight.

Friend templates, default template arguments, and template template parameters came afterward during the standardization of C++98. The ability to declare template parameters is sometimes called higher-order genericity. They were originally introduced to support a certain allocator model in the C++ standard library, but that allocator model was later replaced by one that does not rely on template template parameters. Later, template template parameters came close to being removed from the language because their specification had remained incomplete until very late in the standardization process for the 1998 standard. Eventually a majority of committee members voted to keep them and their specifications were completed.

Alias templates were introduced as part of the 2011 standard. Alias templates serve the same needs as the oft-requested "typedef templates" feature by making it easy to write a template that is merely a different spelling of an existing class template. The specification (C++11) stated that the alias template is not a new type, but rather an alternative spelling for an existing type.

Variadic templates were driven by the needs of the C++11 standard library and the Boost libraries (see [Boost]), where C++ template libraries were using increasingly advanced (and powerful) techniques to provide type-safe abstractions that accept an arbitrary number of template arguments. Doug Gregor, Jaakko Järvi, Gary Powell, Jean-Marc Jézéquel, and Jason Merrill proposed the initial specification for the standard (N1483). Doug Gregor also developed the original implementation of the feature in GNU C++ while the specification was being developed, which much helped the ability to use the feature in the standard library.

Fold expressions were the work of Andrew Sutton and Richard Smith. They were added to C++17 through their paper N4191.

+   1. As exceptions since C++14 are the implicit template type parameters for a generic lambda; see Section 15.6.1, page 509.
+   2. The keyword `class` does not imply that the substituting argument should be a class type. It could be any accessible type.
+   3. Template template parameters do not denote types; however, their distinction from non-type parameters is sometimes subtle.
+   4. At the time of this writing, only “pointer to object” and “pointer to function” types are permitted, which excludes types like `void*`. However, all compilers appear to accept `void*` also.
+   5. See Appendix B for a discussion of value categories such as rvalues and lvalues.
+   6. Template arguments for subsequent template parameters can still be determined by template argument deduction; see Chapter 15.
+   7. However, a constructor template can be a default constructor.
+   8. The term variadic is borrowed from C’s variadic functions, which accept a variable number of function arguments. Variadic templates also borrowed from C the use of the ellipsis to denote zero or more arguments and are intended as a type-safe replacement for C’s variadic functions.
+   9. This syntactic understanding of pack expansion is a useful tool, but it breaks down when the template parameter pack has length zero. Section 16.4 provides more details about the interpretation of pack expansions.
+   10. “Mixins” are discussed in further detail in Section 21.3 on page 508.
+   11. There is a similar restriction on members of class templates and nested classes within class templates. If a member is declared with a type that does not appear to be a function type, but after instantiation the type of that member is a function type, the program is ill-formed because the member is not defined as a member function.