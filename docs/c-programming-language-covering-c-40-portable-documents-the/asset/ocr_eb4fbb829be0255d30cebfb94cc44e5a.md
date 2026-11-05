```
namespace N3
{
    using N1;
    using N2;
    class B : A { }        // Error: A is ambiguous
}
```

both N1 and N2 contain a member A, and because N3 imports both, referencing A in N3 is a compile-time error. In this situation, the conflict can be resolved either through qualification of references to A or by introducing a using-alias-directive that picks a particular A. For example:

```
namespace N3
{
    using N1;
    using N2;
    using A = N1::A;
    class B : A { }        // A means N1::A
}
```

Like a using-alias-directive, a using-namespace-directive does not contribute any new members to the underlying declaration space of the compilation unit or namespace, but rather affects only the compilation unit or namespace body in which it appears.

The namespace-name referenced by a using-namespace-directive is resolved in the same way as the namespace-or-type-name referenced by a using-alias-directive. Thus using-namespace-directives in the same compilation unit or namespace body do not affect one another and can be written in any order.

# 9.5 Namespace Members

A namespace-member-declaration is either a namespace-declaration (§9.2) or a type-declaration (§9.6).

```
namespace-member-declarations:
    namespace-member-declaration
    namespace-member-declarations namespace-member-declaration

namespace-member-declaration:
    namespace-declaration
    type-declaration
```