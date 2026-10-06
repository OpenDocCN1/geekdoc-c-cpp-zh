
# ISO/IEC 14882:2017(E)

type P of the declator-id of the function parameter pack for subsequent positions in the parameter packs expanded by the function parameter pack. Similarly, if A was transformed from a function parameter pack, it is compared with each remaining parameter type of the parameter template. If deduction succeeds for a given type, the type from the template is considered to be at least as specialized as the type from the template. [Example:

```
template<Class, Args...>    void f(Args... args);      // #1
template<Class T1, Args...>  void f(T1, Args... args);  // #2
template<Class T1, T2>        void f(T1, T2 a2);          // #3
```

```
f();                                     // #1
f(1, 2);                             // #2
f(1,);                              // #3: non-variadic template #3 is more specialized
                                      // by the variadic template #1 and #2
```

- 9. If a given type, deduction succeeds in both directions (i.e., the types are identical after the transformations) both P and A were references (both being replaced with the type above):
    - if the deduction from the argument type is an invalid reference and the type from the parameter template was not, the parameter type is not considered to be at least as specialized as the argument type;
    - otherwise;
    - if the deduction from the argument type is more cv-qualified than the type from the parameter template (as described above), the parameter type is not considered to be at least as specialized as the argument type.

- 10 Function F is at least as specialized as function G, for each pair of types to deduce ordering, the type of F is at least as specialized as the type from G and G is more specialized than F if F is at least as specialized as G, then F is more specialized than G.

- 11. If considering above, function template F is as specialized as function template G and vice-versa, and if G has a trailing parameter pack for F does not have a corresponding parameter, and if F does not have a trailing parameter pack, then F is more specialized than G.

- 12 In most cases, deduction fails if not template parameters have values, but for partial ordering the template parameter may remain without a value provided it is not used in the types used for partial ordering. —Note: A template parameter used in a non-deduced context is considered used.—Example:

```
template<Class T> T(int);             // #1
template<Class T1, Class U> T(f(0));     // #2
void g() {                              n f<int>(1);                           // calls #1
}
```

- 13 [Note: Partial ordering of function templates containing template parameter packs is independent of the number of deduced arguments for those template parameter packs.—end note.] [Example:

```
template<Class...>                           
template<Class..., Types...> void g(Tuple<Types...>);   // #1
template<Class T1, Class..., Types...> void g(Tuple<T1, Types...>);   // #2
template<Class T1, T2, Types...> void g(Tuple<T1, T2...>);   // #3
```

```
g(Tuple<()>());                           // calls #1
g(Tuple<int, float>());());                // calls #2
g(Tuple<int, float>>());                 // calls #3
```

```
g(Tuple<int>()); // calls #3
// end example
```

## 17.8.2.5 Deducing template arguments from a type

- 1 Template arguments can be deduced in different contexts, but in each case a type that is specified in terms of template parameters (call it P) is compared with an actual type (call it A), and an attempt is made to find template values (a type for a type parameter, a value for a non-type parameter, or a value for a template) will make P, after substitution of the deduced values (call the deduced A), compatible with A.

- 2 In some cases, deduction is done using a single set of types P and A; in other cases, it is independently for each P/A pair, and the deduced template arguments are valid for any P/A pair, or if pair deduction leads to more than one set of deduced values, or if different pairs yield different deduced values, or if any template argument remains deduced not explicitly specified, template argument deduction fails. The type of a type is only deduced from an array bound if it is not otherwise deduced.

- 3 A given type P can be composed of a number of other types, templates, and non-type values:
    (3.1) A function type includes the type of the function parameters and the return type.
    (3.2) A pointer to member includes the type of the class pointed to and the type of the member pointed to.
    (3.3) A type that is a specialization of a class template (e.g., A<int>) includes types, and non-type values referenced by the template argument list of specialization.
    (3.4) An array includes the element type and the value of the array bound.

- 4 In most cases, the types, templates, and non-type values are used to determine the value of a template argument, and template argument deduction fails if the value so determined is not consistent with the values determined elsewhere. In certain contexts, however, the value does not participate in deduction, but instead uses values of template arguments that were not explicitly specified. If a template parameter is used only in de-deduced contexts and is not explicitly specified, template argument deduction fails. [Note: Unless 17.8.2.1 and 17.8.2.4, if P contains no template-parameters then P and A need not have the same form. — end note ]

- 5 The de-deduced contexts:
    (5.1) The named-specifier of a type that was specified using a qualified-id.
    (5.2) The expression of a deduce-specifier.
    (5.3) A non-type argument or an array bound in a subexpression references a template parameter.
    (5.4) A template parameter is used in the parameter type of a function parameter that has a default argument that is being used in the call for which argument deduction is being done.
    (5.5) A function argument for which argument deduction cannot be done because the associated argument is a function, or a set of overloaded functions (16.4), and one or more of the following:
    - more than one function matches the type
    - no function matches the type
    - the set of functions matches the argument

- (5.6) A function argument for which argument deduction cannot be done is an initializer list. Example:

```
template<Class T> g(T);
g(1, 2, 3);
```

- (5.7) A function parameter pack that does not occur at the end of the parameter-list. When a type is specified in a list that includes a non-deduced context, all of the types are non-deduced. Likewise, if a type is specified as A<T>, the T in A<T> is non-deduced. If a type is specified as void f(typename A<T>); the T in A<T> is non-deduced.
