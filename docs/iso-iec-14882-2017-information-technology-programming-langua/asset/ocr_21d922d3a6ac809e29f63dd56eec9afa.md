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

+   9. If a given type, deduction succeeds in both directions (i.e., the types are identical after the transformations) both P and A were references (both being replaced with the type above):
    - if the deduction from the argument type is an invalid reference and the type from the parameter template was not, the parameter type is not considered to be at least as specialized as the argument type;
    - otherwise;
    - if the deduction from the argument type is more cv-qualified than the type from the parameter template (as described above), the parameter type is not considered to be at least as specialized as the argument type.

+   10 Function F is at least as specialized as function G, for each pair of types to deduce ordering, the type of F is at least as specialized as the type from G and G is more specialized than F if F is at least as specialized as G, then F is more specialized than G.

+   11. If considering above, function template F is as specialized as function template G and vice-versa, and if G has a trailing parameter pack for F does not have a corresponding parameter, and if F does not have a trailing parameter pack, then F is more specialized than G.

+   12 In most cases, deduction fails if not template parameters have values, but for partial ordering the template parameter may remain without a value provided it is not used in the types used for partial ordering. —Note: A template parameter used in a non-deduced context is considered used.—Example:

```
template<Class T> T(int);             // #1
template<Class T1, Class U> T(f(0));     // #2
void g() {                              n  f<int>(1);                           // calls #1
}
```

+   13 [Note: Partial ordering of function templates containing template parameter packs is independent of the number of deduced arguments for those template parameter packs.—end note.] [Example:

```
template<Class...>                           
template<Class..., Types...> void g(Tuple<Types...>);   // #1
template<Class T1, Class..., Types...> void g(Tuple<T1, Types...>);   // #2
template<Class T1, Class T2, Types...> void g(Tuple<T1, T2...>);   // #3
```

```
g(Tuple<()>());                           // calls #1
g(Tuple<int, float>());());                // calls #2
g(Tuple<int, float#>());                 // calls #3
```

§ 17.8.2                               ISO/IEC 2017 - All rights reserved               412