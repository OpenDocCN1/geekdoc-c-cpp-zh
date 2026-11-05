```
```cpp
namespace N3
{
    extern alias R1;
    using R2 = N1.N2;
}
namespace N3
{
    class B: R1::A, R2.I {}       // Error, R1 and R2 unknown
}
```
```

The scopes of the alias directives that introduce R1 and R2 only extend to member declarations in the namespace body in which they are contained, so R1 and R2 are unknown in the second namespace declaration. However, placing the alias directives in the containing compilation unit causes the alias to become available within both namespace declarations:

```
```cpp
extern alias R1;
using R2 = N1.N2;
namespace N3
{
    class B: R1::A, R2.I {}
}
namespace N3
{
    class C: R1::A, R2.I {}
}
```
```

*end example]*

Each *extern-alias-directive* or *using-alias-directive* in a *compilation-unit* or *namespace-body* contributes a name to the *alias declaration space* (§8.3) of the immediately enclosing *compilation-unit* or *namespace-body*. The *identifier* of the alias directive shall be unique within the corresponding alias declaration space. The alias identifier need not be unique within the global declaration space or the declaration space of the corresponding namespace. [Example:

```
```cpp
extern alias A;
extern alias B;
using A = N1.N2;       // Error: alias A already exists
class B {}             // Ok
```
```

The using alias named A causes an error since there is already an alias named A in the same compilation unit. The class named B does not conflict with the extern alias named B since these names are added to distinct declaration spaces. The former is added to the global declaration space and the latter is added to the alias declaration space for this compilation unit.

When an alias name matches the name of a member of a namespace, usage of either must be appropriately qualified:

```
```cpp
namespace N1.N2
{
    class B {}
}
namespace N3
{
    class A {}
    class B : A {}
}
namespace N3
{
    using A = N1.N2;
    using B = N1.N2.B;
}
```
```