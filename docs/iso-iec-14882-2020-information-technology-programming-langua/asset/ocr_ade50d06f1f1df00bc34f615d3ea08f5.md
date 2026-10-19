# 9.8.2.2 Unnamed namespaces [namespace.unnamed]

1 An unnamed-namespace-definition behaves as if it were replaced by

```
inline_opt namespace unique { /* empty body */ }
using namespace unique ;
namespace unique { namespace-body }
```

where inline appears if and only if it appears in the unnamed-namespace-definition and all occurrences of unique in a translation unit are replaced by the same identifier, and this identifier differs from all other identifiers in the translation unit. The optional attribute-specifier-seq in the unnamed-namespace-definition appertains to unique.

[Example 1:

```
namespace { int i; }          // unique::i
void f() { i++; }            // unique::i++

namespace A {
  namespace {
    int i;                    // A::unique::i
    int j;                    // A::unique::j
  }
  void g() { i++; }          // A::unique::i++
}

using namespace A;
void h() {
  i++;                       // error: unique::i or A::unique::i
  A::i++;                    // A::unique::i
  j++;                       // A::unique::j
}
— end example]
```

# 9.8.2.3 Namespace member definitions [namespace.memdef]

1 A declaration in a namespace N (excluding declarations in nested scopes) whose declarator-id is an unqualified-id (9.3.4), whose class-head-name (11.1) or enum-head-name (9.7.1) is an identifier, or whose elaborated-type-specifier is of the form class-key attribute-specifier-seq_opt identifier (9.2.9.4), or that is an opaque-enum-declaration, declares (or redeclares) its unqualified-id or identifier as a member of N.

[Note 1: An explicit instantiation (13.9.3) or explicit specialization (13.9.4) of a template does not introduce a name and thus can be declared using an unqualified-id in a member of the enclosing namespace set, if the primary template is declared in an inline namespace. — end note]

[Example 1:

```
namespace X {
  void f() { /* ... */ }       // OK: introduces X::f()

  namespace M {
    void g();                 // OK: introduces X::M::g()
  }
  using M::g;
  void g();                   // error: conflicts with X::M::g()
}
— end example]
```

2 Members of a named namespace can also be defined outside that namespace by explicit qualification (6.5.4.3) of the name being defined, provided that the entity being defined was already declared in the namespace and the definition appears after the point of declaration in a namespace that encloses the declaration’s namespace.