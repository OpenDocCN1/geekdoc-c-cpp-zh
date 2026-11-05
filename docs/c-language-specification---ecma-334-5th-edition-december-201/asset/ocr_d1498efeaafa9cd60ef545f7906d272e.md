```
namespace N3
{
    using R1 = N1;
    using R2 = N1.N2;

    class B
    {
        N1.N2.A a;       // refers to N1.N2.A
        R1.N2.A b;       // refers to N1.N2.A
        R2.A c;          // refers to N1.N2.A
    }
}
```

the names N1.N2.A, R1.N2.A, and R2.A are equivalent and all refer to the class declaration whose fully qualified name is N1.N2.A. end example]

Although each part of a partial type (§15.2.7) is declared within the same namespace, the parts are typically written within different namespace declarations. Thus, different extern alias directives and using directives can be present for each part. When interpreting simple names (§12.7.3) within one part, only the extern alias directives and using directives of the namespace bodies and compilation unit enclosing that part are considered. This may result in the same identifier having different meanings in different parts. [Example:

```
namespace N
{
    using List = System.Collections.ArrayList;

    partial class A
    {
        List x;          // x has type System.Collections.ArrayList
    }
}

namespace N
{
    using List = widgets.LinkedList;

    partial class A
    {
        List y;          // y has type widgets.LinkedList
    }
}
```

end example]

Using aliases can name a closed constructed type, but cannot name an unbound generic type declaration without supplying type arguments. [Example:

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
    using W = N1.A;          // Error, cannot name unbound generic type
    using X = N1.A.B;        // Error, cannot name unbound generic type
    using Y = N1.A<int>;     // Ok, can name closed constructed type
    using Z<T> = N1.A<T>;    // Error, using alias cannot have type
    parameters
}
```

end example]