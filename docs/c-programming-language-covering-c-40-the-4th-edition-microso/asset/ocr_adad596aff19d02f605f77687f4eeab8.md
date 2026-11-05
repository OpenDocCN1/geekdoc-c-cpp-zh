Using aliases can name a closed constructed type, but cannot name an unbound generic type declaration without supplying type arguments. For example:

```
namespace N1
{
    class A<T>
    {
        class B {}
    }
}
namespace N2
{
    using W = N1.A;      // Error: cannot name unbound generic type
    using X = N1.A.B;    // Error: cannot name unbound generic type
    using Y = N1.A<int>; // Okay: can name closed constructed type
    using Z<T> = N1.A<T>; // Error: using alias cannot have type parameters
}
```

# 9.4.2 Using Namespace Directives

A using-namespace-directive imports the types contained in a namespace into the immediately enclosing compilation unit or namespace body, enabling the identifier of each type to be used without qualification.

```
using-namespace-directive:
    using namespace-name ;
```

Within member declarations in a compilation unit or namespace body that contains a using-namespace-directive, the types contained in the given namespace can be referenced directly. For example:

```
namespace N1.N2
{
    class A { }
}
namespace N3
{
    using N1.N2;
    class B : A { }
}
```

In this example, within the member declarations in the N3 namespace, the type members of N1.N2 are directly available, and thus class N3.B derives from class N1.N2.A.