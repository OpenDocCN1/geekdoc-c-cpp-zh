+   - At binding-time, overload resolution is applied to C, N, and A, to select a specific method M from the set of methods declared in and inherited by C. This is described in §11.7.8.2.
+   - Then at run-time:
+     - If M is a non-virtual method, M is invoked.
+     - Otherwise, M is a virtual method, and the most derived implementation of M with respect to R is invoked.

For every virtual method declared in or inherited by a class, there exists a **most derived implementation** of the method with respect to that class. The **most derived implementation** of a virtual method M with respect to a class R is determined as follows:

+   - If R contains the introducing virtual declaration of M, then this is the most derived implementation of M with respect to R.
+   - Otherwise, if R contains an override of M, then this is the most derived implementation of M with respect to R.
+   - Otherwise, the most derived implementation of M with respect to R is the same as the most derived implementation of M with respect to the direct base class of R.

*Example:* The following example illustrates the differences between virtual and non-virtual methods:

```
```csharp
using System;

class A
{
    public void F() => Console.WriteLine("A.F");
    public virtual void G() => Console.WriteLine("A.G");
}

class B : A
{
    public new void F() => Console.WriteLine("B.F");
    public override void G() => Console.WriteLine("B.G");
}

class Test
{
    static void Main()
    {
        B b = new B();
        A a = b;
        a.F();
        b.F();
        a.G();
        b.G();
    }
}
```
```

In the example, A introduces a non-virtual method F and a virtual method G. The class B introduces a new non-virtual method F, thus hiding the inherited F, and also overrides the inherited method G. The example produces the output: