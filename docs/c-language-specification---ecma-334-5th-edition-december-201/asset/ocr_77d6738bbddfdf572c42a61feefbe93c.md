# 14.5.2 Using alias directives

A using-alias-directive introduces an identifier that serves as an alias for a namespace or type within the immediately enclosing compilation unit or namespace body.

```
using-alias-directive:
    using identifier = namespace-or-type-name ;
```

Within global attributes and member declarations in a compilation unit or namespace body that contains a using-alias-directive, the identifier introduced by the using-alias-directive can be used to reference the given namespace or type. [Example:

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

Within using directives, global attributes and member declarations in a compilation unit or namespace body that contains an extern-alias-directive, the identifier introduced by the extern-alias-directive can be used to reference the associated namespace. [Example: For example:

```
namespace N1
{
    extern alias N2;
    class B: N2::A {}
}
```

Above, within member declarations in the N1 namespace, N2 is an alias for some namespace whose definition is external to the source code of the program. Class N1.B derives from class N2.A. The same effect can be obtained by creating an alias A for N2.A and then referencing A:

```
namespace N1
{
    extern alias N2;
    using A = N2::A;
    class B: A {}
}
```

An extern-alias-directive or using-alias-directive makes an alias available within a particular compilation unit or namespace body, but it does not contribute any new members to the underlying declaration space. In other words, an alias directive is not transitive, but, rather, affects only the compilation unit or namespace body in which it occurs. [Example: In the following code