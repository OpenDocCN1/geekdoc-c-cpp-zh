# 25 • Namespaces, Type Cast Operators, and Smart Pointers 813

If we want to add something in the nested namespace, the syntax is to nest the inner namespace within the outer namespace. For example:

```
namespace A
{
    namespace B
    {
        int c;
    }
}
```

If we don't do that and write only:

```
namespace B
{
    int c;
}
```

then, we define a new namespace named B and to access c, we'd write B::c.
++17 provides an alternative more convenient and easier syntax for nested namespaces, especially as the number of inner levels grows. For example, instead of:

```
namespace A
{
    namespace B
    {
        namespace C
        {
            int a;
            void h();
            ...
        }
    }
}
```

we can write:

```
namespace A::B::C
{
    int a;
    void h();
    ...
}
```

# Namespace Aliases

To create a synonym for a namespace we use the = operator. For example, if we want, for convenience, to make a synonym for a long name or for a nested namespace, we write:

```
namespace long_name_for_namespace
{
    ...
}
```

```
namespace new_name = long_name_for_namespace;
using namespace new_name;
```