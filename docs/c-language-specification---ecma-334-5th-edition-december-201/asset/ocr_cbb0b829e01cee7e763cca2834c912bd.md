using global.A causes a compile-time error since there is no entity named global in scope. If some entity named global were in scope, then global in global.A would have resolved to that entity.

Using global as the left-hand identifier of a qualified-alias-member always causes a lookup in the global namespace, even if there is a using alias named global. In the code:

```
using global = MyGlobalTypes;
class A { }
class C {
    global.A x; // Valid: References MyGlobalTypes.A
    global::A y; // Valid: References A in the global namespace
}
```

global.A resolves to MyGlobalTypes.A and global::A resolves to class A in the global namespace.
end note]

# 14.8.2 Uniqueness of aliases

Each compilation unit and namespace body has a separate declaration space for extern aliases and using aliases. Thus, while the name of an extern alias or using alias shall be unique within the set of extern aliases and using aliases declared in the immediately containing compilation unit or namespace body, an alias is permitted to have the same name as a type or namespace as long as it is used only with the :: qualifier.

[Example: In the following:

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

the name A has two possible meanings in the second namespace body because both the class A and the using alias A are in scope. For this reason, use of A in the qualified name A.Stream is ambiguous and causes a compile-time error to occur. However, use of A with the :: qualifier is not an error because A is looked up only as a namespace alias. end example]