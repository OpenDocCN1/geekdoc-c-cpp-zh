```
```
}
}
```
```

the classes and members have the following accessibility domains:

+   - The accessibility domain of `A` and `A.X` is unlimited.
+   - The accessibility domain of `A.Y`, `B`, `B.X`, `B.Y`, `B.C`, `B.C.X`, and `B.C.Y` is the program text of the containing program.
+   - The accessibility domain of `A.Z` is the program text of `A`.
+   - The accessibility domain of `B.Z` and `B.D` is the program text of `B`, including the program text of `B.C` and `B.D`.
+   - The accessibility domain of `B.C.Z` is the program text of `B.C`.
+   - The accessibility domain of `B.D.X` and `B.D.Y` is the program text of `B`, including the program text of `B.C` and `B.D`.
+   - The accessibility domain of `B.D.Z` is the program text of `B.D`. As the example illustrates, the accessibility domain of a member is never larger than that of a containing type. For example, even though all `X` members have public declared accessibility, all but `A.X` have accessibility domains that are constrained by a containing type.

*end example*

As described in §7.4, all members of a base class, except for instance constructors, finalizers, and static constructors, are inherited by derived types. This includes even private members of a base class. However, the accessibility domain of a private member includes only the program text of the type in which the member is declared.

*Example: In the following code*

```
```csharp
class A
{
    int x;

    static void F(B b)
    {
        b.x = 1;        // Ok
    }
}

class B : A
{
    static void F(B b)
    {
        b.x = 1;        // Error, x not accessible
    }
}
```
```

the `B` class inherits the private member `x` from the `A` class. Because the member is private, it is only accessible within the *class_body* of `A`. Thus, the access to `b.x` succeeds in the `A.F` method, but fails in the `B.F` method.

*end example*