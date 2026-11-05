```
class W : B {}    // Error: B is ambiguous
class X : A.B {}  // Error: A is ambiguous
class Y : A::B {} // Ok: uses N1.N2.B
class Z : N3.B {} // Ok: uses N3.B
}
```

In the second namespace body for N3, unqualified use of B results in an error, since N3 contains a member named B and the namespace body that also declares an alias with name B; likewise for A. The class N3.B can be referenced as N3.B or global::N3.B. The alias A can be used in a qualified-alias-member (§14.8), such as A::B. The alias B is essentially useless. It cannot be used in a qualified-alias-member since only namespace aliases can be used in a qualified-alias-member and B aliases a type. end example

Just like regular members, names introduced by alias-directives are hidden by similarly named members in nested scopes. [Example: In the following code

```
using R = N1.N2;
namespace N3
{
    class R {}
    class B: R.A {}    // Error, R has no member A
}
```

the reference to R.A in the declaration of B causes a compile-time error because R refers to N3.R, not N1.N2. end example

The order in which extern-alias-directives are written has no significance. Likewise, the order in which using-alias-directives are written has no significance, but all using-alias-directives must come after all extern-alias-directives in the same compilation unit or namespace body. Resolution of the namespace-or-type-name referenced by a using-alias-directive is not affected by the using-alias-directive itself or by other using-directives in the immediately containing compilation unit or namespace body, but may be affected by extern-alias-directives in the immediately containing compilation unit or namespace body. In other words, the namespace-or-type-name of a using-alias-directive is resolved as if the immediately containing compilation unit or namespace body had no using-directives but has the correct set of extern-alias-directives. [Example: In the following code

```
namespace N1.N2 {}
namespace N3
{
    extern alias E;
    using R1 = E::N;    // OK
    using R2 = N1;      // OK
    using R3 = N1.N2;   // OK
    using R4 = R2.N2;   // Error, R2 unknown
}
```

the last using-alias-directive results in a compile-time error because it is not affected by the previous using-alias-directive. The first using-alias-directive does not result in an error since the scope of the extern alias E includes the using-alias-directive. end example

A using-alias-directive can create an alias for any namespace or type, including the namespace within which it appears and any namespace or type nested within that namespace.

Accessing a namespace or type through an alias yields exactly the same result as accessing that namespace or type through its declared name. [Example: Given

```
namespace N1.N2
{
    class A {}
}
```