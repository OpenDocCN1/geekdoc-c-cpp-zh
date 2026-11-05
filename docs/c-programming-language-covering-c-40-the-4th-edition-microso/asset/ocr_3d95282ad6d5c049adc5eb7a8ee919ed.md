The example

```
    partial class Dictionary<K,V>
        where K: IComparable<K>
        where V: IKeyProvider<K>, IPersistable
    {
        ...
    }

    partial class Dictionary<K,V>
        where V: IPersistable, IKeyProvider<K>
        where K: IComparable<K>
    {
        ...
    }

    partial class Dictionary<K,V>
    {
        ...
    }
```

is correct because those parts that include constraints (the first two) effectively specify the same set of primary, secondary, and constructor constraints for the same set of type parameters, respectively.

> > **BILL WAGNER** When possible, I prefer specifying the type parameters and constraints on all copies. This technique improves readability.

# ### 10.2.4 Base Class

When a partial class declaration includes a base class specification, it must agree with all other parts that include a base class specification. If no part of a partial class includes a base class specification, the base class becomes System.Object (§10.1.4.1).

# ### 10.2.5 Base Interfaces

The set of base interfaces for a type declared in multiple parts is the union of the base interfaces specified on each part. A particular base interface may be named only once on each part, but it is permitted for multiple parts to name the same base interface(s). There must be only one implementation of the members of any given base interface.

In the example

```
    partial class C: IA, IB {...}
    partial class C: IC {...}
    partial class C: IA, IB {...}
```

the set of base interfaces for class C is IA, IB, and IC.