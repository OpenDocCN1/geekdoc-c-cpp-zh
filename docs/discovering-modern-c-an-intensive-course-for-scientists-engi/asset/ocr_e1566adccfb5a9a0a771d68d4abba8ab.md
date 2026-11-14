Please note that this rule forbids the implementation and not the declaration as default or delete. There might be cases where the standard library does not provide a class that manages the resource we are interested in. Then we do ourselves a favor when we write a small set of classes that manage the resources as discussed in Section 2.4.2.4 and all high-level classes use those resource managers, and the default behavior of the five operations in the high-level classes is well defined.

# A.5.3.3 Explicit versus Implicit Deletion

Please compare the following two variations of an otherwise identical class implementation:

```
class tray
{
public:
    tray(const tray&) = default;
    // tray(tray&&) = delete; // implied
    tray& operator=(const tray&) = default;
    // tray& operator=(tray&&) = delete; // implied
};
// ...
```

versus

```
class tray
{
public:
    tray(const tray&) = default;
    tray(tray&&) = delete;
    tray& operator=(const tray&) = default;
    tray& operator=(tray&&) = delete;
};
// ...
```

In both cases, the copy operations have default behavior while the move operations are deleted. They should therefore behave equally. But they do not in C++11 when an rvalue is passed:

```
tray b(std::move(a));
c= std::move(b);
```

The first variant of tray compiles with the snippet above. However, the values are actually not moved but copied. The second variant of tray yields a compiler error saying that the move operations are explicitly deleted. The reason for this discrepancy is that the explicitly deleted operations are considered in the overload resolution where they are better matches than the copy operations. In a later compile phase, it will be detected that they cannot be used. Implicitly deleted operations do not exist at all during the overload resolution and the copy operations are the best matches.

Fortunately, this inconsistency disappears in C++14 since explicitly deleted move operations are not considered in the overload resolution either. Thus, copy-only classes will not be possible any longer and every class that cannot be moved will be copied implicitly.