
## 9.4.1 Using alias directives

A using-alias-directive introduces an identifier that serves as an alias for a namespace or type within the immediately enclosing compilation unit or namespace body.

```
using-alias-directive:
    using identifier = namespace-or-type-name ;
```

Within member declarations in a compilation unit or namespace body that contains a using-alias-directive, the identifier introduced by the using-alias-directive can be used to reference the given namespace or type. For example:

```
namespace N1.N2
{
    class A {}
}
namespace N3
{
    using A = N1.N2.A;
    class B: A {}
}
```

Above, within member declarations in the N3 namespace, A is an alias for N1.N2.A, and thus class N3.B derives from class N1.N2.A. The same effect can be obtained by creating an alias R for N1.N2 and then referencing R.A:

```
namespace N3
{
    using R = N1.N2;
    class B: R.A {}
}
```

The identifier of a using-alias-directive must be unique within the declaration space of the compilation unit or namespace that immediately contains the using-alias-directive. For example:

```
namespace N3
{
    class A {}
}
namespace N3
{
    using A = N1.N2.A;    // Error, A already exists
}
```

Above, N3 already contains a member A, so it is a compile-time error for a using-alias-directive to use that identifier. Likewise, it is a compile-time error for two or more using-alias-directives in the same compilation unit or namespace body to declare aliases by the same name.

A using-alias-directive makes an alias available within a particular compilation unit or namespace body, but it does not contribute any new members to the underlying declaration space. In other words, a using-alias-directive is not transitive but rather affects only the compilation unit or namespace body in which it occurs. In the example

```
namespace N3
{
    using R = N1.N2;
}
namespace N3
{
    class B: R.A {}    // Error, R unknown
}
```

```
namespace N1.N2
{
    class A {}
}
namespace N3
{
    using N1;
    class B: N2.A {}      // Error, N2 unknown
}
```

the using-namespace-directive imports the types contained in N1, but not the namespaces nested in N1. Thus, the reference to N2.A in the declaration of B results in a compile-time error because no members named N2 are in scope.

Unlike a using-alias-directive, a using-namespace-directive may import types whose identifiers are already defined within the enclosing compilation unit or namespace body. In effect, names imported by a using-namespace-directive are hidden by similarly named members in the enclosing compilation unit or namespace body. For example:

```
namespace N1.N2
{
    class A {}
    class B {}
}
namespace N3
{
    using N1.N2;
    class A {}
}
```

Here, within member declarations in the N3 namespace, A refers to N3.A rather than N1.N2.A.

When more than one namespace imported by using-namespace-directives in the same compilation unit or namespace body contain types by the same name, references to that name are considered ambiguous. In the example

```
namespace N1
{
    class A {}
}
namespace N2
{
    class A {}
}
namespace N3
{
    using N1;
    using N2;
    class B: A {}          // Error, A is ambiguous
}
```

both N1 and N2 contain a member A, and because N3 imports both, referencing A in N3 is a compile-time error. In this situation, the conflict can be resolved either through qualification of references to A, or by introducing a using-alias-directive that picks a particular A. For example:

```
namespace N3
{
    using N1;
```
- Types declared in structs can have public, internal, or private access. The default is private access.

## 9.7 Namespace alias qualifiers

The namespace alias qualifier :: makes it possible to guarantee that type name lookups are unaffected by the introduction of new types and members. The namespace alias qualifier always appears between two identifiers referred to as the left-hand and right-hand identifiers. Unlike the regular . qualifier, the left-hand identifier of the :: qualifier is looked up only as an extern or using alias.

A qualified-alias-member is defined as follows:

```
qualified-alias-member:
    identifier :: identifier type-argument-list_opt
```

A qualified-alias-member can be used as a namespace-or-type-name (§3.8) or as the left operand in a member-access (§7.6.4).

A qualified-alias-member has one of two forms:

- N :: I<A1, ..., Ak>, where N and I represent identifiers, and <A1, ..., Ak> is a type argument list. (K is always at least one.)
- N :: I, where N and I represent identifiers. (In this case, K is considered to be zero.)

Using this notation, the meaning of a qualified-alias-member is determined as follows:

- If N is the identifier global, then the global namespace is searched for I:
  - If the global namespace contains a namespace named I and K is zero, then the qualified-alias-member refers to that namespace.
  - Otherwise, if the global namespace contains a non-generic type named I and K is zero, then the qualified-alias-member refers to that type.
  - Otherwise, if the global namespace contains a type named I that has K type parameters, then the qualified-alias-member refers to that type constructed with the given type arguments.
  - Otherwise, the qualified-alias-member is undefined and a compile-time error occurs.
- Otherwise, starting with the namespace declaration (§9.2) immediately containing the qualified-alias-member (if any), continuing with each enclosing namespace declaration (if any), and ending with the compilation unit containing the qualified-alias-member, the following steps are evaluated until an entity is located:
  - If the namespace declaration or compilation unit contains a using-alias-directive that associates N with a type, then the qualified-alias-member is undefined and a compile-time error occurs.
  - Otherwise, if the namespace declaration or compilation unit contains an extern-alias-directive or using-alias-directive that associates N with a namespace, then:
    - If the namespace associated with N contains a namespace named I and K is zero, then the qualified-alias-member refers to that namespace.
    - Otherwise, if the namespace associated with N contains a non-generic type named I and K is zero, then the qualified-alias-member refers to that type.
    - Otherwise, if the namespace associated with N contains a type named I that has K type parameters, then the qualified-alias-member refers to that type constructed with the given type arguments.
    - Otherwise, the qualified-alias-member is undefined and a compile-time error occurs.
- Otherwise, the qualified-alias-member is undefined and a compile-time error occurs.

Note that using the namespace alias qualifier with an alias that references a type causes a compile-time error.
Also note that if the identifier N is global, then lookup is performed in the global namespace, even if there is a using alias associating global with a type or namespace.

### 9.7.1 Uniqueness of aliases

Each compilation unit and namespace body has a separate declaration space for extern aliases and using aliases.
Thus, while the name of an extern alias or using alias must be unique within the set of extern aliases and using aliases declared in the immediately containing compilation unit or namespace body, an alias is permitted to have the same name as a type or namespace as long as it is used only with the :: qualifier.

In the example

```
namespace N
{
    public class A {}
    public class B {}
}
namespace N
{
    using A = System.IO;
    class X
    {
        A.Stream s1;      // Error, A is ambiguous
        A::Stream s2;     // Ok
    }
}
```

the name A has two possible meanings in the second namespace body because both the class A and the using alias A are in scope. For this reason, use of A in the qualified name A.Stream is ambiguous and causes a compile-time error to occur. However, use of A with the :: qualifier is not an error because A is looked up only as a namespace alias.
