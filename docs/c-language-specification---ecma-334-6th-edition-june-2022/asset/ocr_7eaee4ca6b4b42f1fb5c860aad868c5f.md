Because names may be ambiguous when more than one imported namespace introduces the same type name, a using_alias_directive is useful to disambiguate the reference.

Example: In the following code

```
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

    class B : A {} // Error, A is ambiguous
}
```
```

both N1 and N2 contain a member A, and because N3 imports both, referencing A in N3 is a compile-time error. In this situation, the conflict can be resolved either through qualification of references to A, or by introducing a using_alias_directive that picks a particular A. For example:

```
```
namespace N3
{
    using N1;
    using N2;
    using A = N1.A;

    class B : A {} // A means N1.A
}
```
```

end example

Furthermore, when more than one namespace or type imported by using_namespace_directives or using_static_directives in the same compilation unit or namespace body contain types or members by the same name, references to that name as a simple_name are considered ambiguous.

Example:

```
```
namespace N1
{
    class A {}
}

class C
{
    public static int A;
}

namespace N2
{
    using N1;
    using static C;
```
```