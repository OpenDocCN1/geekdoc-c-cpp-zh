```
namespace N3
{
    class B : R1::A, R2.I {} // Error, R1 and R2 unknown
}
```

the scopes of the alias directives that introduce R1 and R2 only extend to member declarations in the namespace body in which they are contained, so R1 and R2 are unknown in the second namespace declaration. However, placing the alias directives in the containing compilation unit causes the alias to become available within both namespace declarations:

```
extern alias R1;
```

```
using R2 = N1.N2;
```

```
namespace N3
{
    class B : R1::A, R2.I {}
}
```

```
namespace N3
{
    class C : R1::A, R2.I {}
}
```

end example

Each extern_alias_directive or using_alias_directive in a compilation_unit or namespace_body contributes a name to the alias declaration space (§7.3) of the immediately enclosing compilation_unit or namespace_body. The identifier of the alias directive shall be unique within the corresponding alias declaration space. The alias identifier need not be unique within the global declaration space or the declaration space of the corresponding namespace.

Example:

```
extern alias X;
extern alias Y;
```

```
using X = N1.N2; // Error: alias X already exists
```

```
class Y {} // Ok
```

The using alias named X causes an error since there is already an alias named X in the same compilation unit. The class named Y does not conflict with the extern alias named Y since these names are added to distinct declaration spaces. The former is added to the global declaration space and the latter is added to the alias declaration space for this compilation unit.

When an alias name matches the name of a member of a namespace, usage of either must be appropriately qualified:

```
namespace N1.N2
{
    class B {}
}
```

```
namespace N3
{
    class A {}
}
```