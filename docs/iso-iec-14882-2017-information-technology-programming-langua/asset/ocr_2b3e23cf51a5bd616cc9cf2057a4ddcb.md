# ISO/IEC 14882:2017(E)

```
namespace C {
    namespace D {
        using namespace A;
        int j;
        int k;
        int a = i;    // B::hides A::i
    }
    using namespace D;
    int k = 9;     // no problem yet
    int l = k;     // ambiguous: C::k or D::k
    int m = i;     // B::hides A::i
    int n = j;     // D::hides B::j
}
```

— end example —

+   5 If a namespace is extended (10.3.1) after a *using-directive* for that name is given, the additional members of the extended namespace and the members of namespaces nominated by *using-directives* in the extending namespace-definition can be used after the extending *namespace-definition*.

+   6 If a name lookup finds a declaration for a name and the declarations do not declare the same entity and do not declare functions, the use of the name is ill-formed. *Note*: In particular, the name of a variable, function or enumerator does not hide the name of a class or enumeration declared in a different namespace. For example:

```
namespace A {
    class X {
        extern "C" int gO();
        extern "C++" int hO();
    }
}

namespace B {
    void X(int);
    extern "C" int gO();
    extern "C++" int h(int);
}

    using namespace A;
    using namespace B;
```

```
void f() {
    X(1);    // error: name X found in two namespaces
    gO();    // OK: name g refers to the same entity
    hO();    // OK: overload resolution selects A::h
}
```

— end note —

+   7 During overload resolution, all functions from the transitive search are searched for argument matching. The set of declarations found by the transitive search is unordered. *Note*: In the order in which namespaces were created and the relationships between the namespaces implied by the *using-directives* do not cause preference to be given to any of the declarations found by the search. —end note—. An ambiguity exists if the best match finds two functions with the same signature, even if one is in a reachable through *using-directives* of the other ⁵⁹ [Example:

```
namespace C {
```

⁵⁹ During name lookup in a class hierarchy, some ambiguities may be resolved by considering whether one member hides the other along paths (13.2). There is no such disambiguation when considering the set of names found as a result of following *using-directives*.

§ 10.3.4 ©ISO/IEC 2017 — All rights reserved 190