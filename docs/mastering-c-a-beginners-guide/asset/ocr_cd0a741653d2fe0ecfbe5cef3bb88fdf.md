The compiler will complain that we have not implemented the `IComparer<T>` interface’s Compare method. Example above has a Compare method, but its signature is wrong—that first argument should be a T.

```
public class GenericComparer<T> :
IComparer<T>
{
    public int Compare(T x, T y)
    {
        return x.CompareTo(y);
    }
}
```

That will also fail to compile because the compiler can’t find that CompareTo method we are trying to use. The constraint for T in Example enables the compiler to know what that method really is.

Type constraints don’t have to be interfaces. You can use any type. For example, you can constrain a particular argument to always derive from a specific base class. Moreover, you can also define one parameter’s constraint in terms of another type parameter:

```
public class Foo<T1, T2>
    where T1 : T2
...
```

Type constraints are pretty specific—they require either a special inheritance relationship or the implementation of specific interfaces. However, you can define slightly fewer particular constraints.