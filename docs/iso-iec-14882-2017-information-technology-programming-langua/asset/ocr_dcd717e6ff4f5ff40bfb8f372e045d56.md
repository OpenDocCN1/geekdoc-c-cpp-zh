# ISO/IEC 14882:2017(E)

```
}
```

-- end example ]

#  10.3.1.1 Unnamed namespaces [namespace::unnamed]

An unnamed-namespace-definition behaves as if it were replaced by

```
inline_t namespace_unique { /* empty body */ }
using namespace_unique;
namespace_unique { namespace_body }
```

where inline appears and only if it appears in the unnamed-namespace-definition and all occurrences of
unique in a translation unit are replaced by the same identifier, and this identifier differs from all other
tifiers in the translation unit. The optional attribute-specifier-seq in the unnamed-namespace-definition
appears to unique. Example:

```
namespace A {
  int i; // unique::i
  void fO() { i++; }; // unique::i
}
namespace A {
  namespace {
    int i; // unique::i
    int j; // unique::j
  }
  void gO() { i++; }; // unique::i++
}
```

```
using namespace A;
void hO() {
  i++; // error: unique::i A or unique::i
  A::i++; // unique::i
  j++; // unique::j
}
```

-- end example ]

#  10.3.1.2 Namespace member definitions [namespace::mdemdef]

+   A declaration in a namespace M (excluding declarations in nested scopes) whose declarator-id is an unqualified-
id (11.3), whose class-name (Clause 12) or enum-name (10.2) is an identifier, or whose elaborated-
type-specifier is of the form class-key-specifier-seq_opt identifier (10.1.7.3), or that is an opaque-enum-\declaration, declarations (or redeclares) its unqualified-id or identifier as a member of M. [Note: An explicit
stantiation (17.7.2) or explicit specification (17.7.3) of a template does not introduce a name and thus
may use an unqualified-id if the primary template
is declared in an unnamed namespace. -- end note ] Example:

```
namespace X {
  void fO() { /* ... */ }; // OK introduces X::fO()
```

```
namespace M {
  void gO() {
    using M::; // OK introduces X::M::gO()
    void gO();
  } // error: conflicts with X::M::gO()
```

-- end example ]

+   Members of a named namespace can also be defined outside that namespace by explicit qualification (6.4.3.2)

# § 10.3.1.2

©ISO/IEC 2017 – All rights reserved 180