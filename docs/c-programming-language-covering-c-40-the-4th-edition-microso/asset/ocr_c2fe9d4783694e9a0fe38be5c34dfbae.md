The instance type is always a closed constructed type at runtime, so its System.Type object depends on the runtime type arguments in use, while the unbound generic type has no type arguments.

The example

```
using System;
class X<T>
{
    public static void PrintTypes() {
        Type[] t = {
            typeof(int),
            typeof(System.Int32),
            typeof(string),
            typeof(double[]),
            typeof(void),
            typeof(T),
            typeof(X<>),
            typeof(X<X<T>>),
            typeof(X<T>)
        };
        for (int i = 0; i < t.Length; i++) {
            Console.WriteLine(t[i]);
        }
    }
}
class Test
{
    static void Main() {
        X<int>.PrintTypes();
    }
}
```

produces the following output:

```
System.Int32
System.Int32
System.String
System.Double[]
System.Void
System.Int32
X`1[System.Int32]
X`1[X`1[System.Int32]]
X`1[T]
```

Note that int and System.Int32 are the same type.

Also note that the result of typeof(X<>) does not depend on the type argument, but the result of typeof(X<T>) does.