tions through `constexpr` functions). Once such class types became available, it quickly became desirable to allow them for non-type template parameters. However, problems similar to those of the string literal parameters described above arose. In particular, the "equality" of two class-type values is not a trivial matter, because it is in general determined by `operator==` definitions. This equality determines if two instantiations are equivalent, but in practice, that equivalence must be checkable by the linker by comparing mangled names. One way out may be an option to mark certain literal classes as having a trivial equality criterion that amounts to pairwise comparing of the scalar members of the class. Only class types with such a trivial equality criterion would then be permitted as non-type template parameter types.

# 17.3 PARTIAL SPECIALIZATION OF FUNCTION TEMPLATES

In Chapter 15 we discussed how class templates can be partially specialized, whereas function templates are simply overloaded. The two mechanisms are somewhat different.

Partial specialization doesn't introduce a completely new template: It is an extension of an existing template (the primary template). When a class template is looked up, only primary templates are considered at first. If, after the selection of a primary template, a turn that matches the a partial specialization of that template with a template argument pattern that matches that of the instantiation, its definition (in other words, its body) is instantiated instead of the definition of the primary template. (Full-template specializations work exactly the same way.)

In contrast, overloaded function templates are separate templates that are completely independent of one another. When selecting which template to instantiate, all the overloaded templates are considered together, and overload resolution attempts to choose one as the best fit. At first this might seem like an adequate alternative, but in practice there are a number of limitations:

+   - It is possible to specialize member templates of a class without changing the definition of that class. However, adding an overloaded member does require a change in the definition of a class. In many cases this is not an option because we may not own the rights to do so. Furthermore, the C++ standard does not currently allow us to add new templates to the class's namespace, but it does allow us to specialize templates from that namespace.
+   
+   - To overload function templates, their function parameters must differ in some material way. Consider a function template `convert` whose parameters may vary in some way. For example:
+   
+     ```cpp
+     template<typename T>
+     T convert(T const&);
+   
+     template<typename T>
+     T convert(T const&, T const&);
+     ```
+   
+   - Code that is valid for a nonoverloaded function may no longer be valid when the function is overloaded. Specifically, given two function templates, the expression `f(1)` and `f(1)` (where `T` is a template parameter) may become ambiguous, since there is no way to decide which is meant.
+   
+   - Prior declarations refer to a specific function template or an instantiation of a specific function template. An overloaded version of a function template would not automatically have the privileges granted to the original template.

Together, this led to form a compelling argument in support of a partial specialization construct for function templates.

A natural syntax for partially specializing function templates is the generalization of the class template notation:

Click here to view code image

```
```cpp
template<typename T>
T const& max(T const& x, T const& y) {    // primary template
  return x > y ? x : y;
}
```
```

Click here to view code image

```
```cpp
template<typename T>
T const& max<T>(T const& x, T const& y) {    // partial specialization
  ...
}
```
```

Some language designers worry about the interaction of this partial specialization approach with function template overloading. For example:

Click here to view code image

```
```cpp
template<typename T>
void add(T t, int i);       // a primary template

template<typename T1, typename T2>
void add(T1 t, T2 t2);     // an overloaded primary template

template<typename T>
void add<T>(T t, int i);   // which primary template
                            // does this specialize?
```
```

However, we expect each such example would be deemed errors without major impact on the utility of the feature.

This extension was briefly discussed during the standardization of C++11 but gathered relatively little interest in the end. Still, the topic occasionally arises because it neatly solves some common programming problems. Perhaps it will be taken up again in some future version of the C++ standard.

# 17.4 NAMED TEMPLATE ARGUMENTS