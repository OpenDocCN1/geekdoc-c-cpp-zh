
## 10.6.3 Virtual Methods

When an instance method declaration includes a virtual modifier, that method is said to be a virtual method. When no virtual modifier is present, the method is said to be a non-virtual method.

> **BILL WAGNER** You can create virtual generic methods, even in a nongeneric class. When you do so, any overrides must also be generic. You cannot override a particular instantiation.

> **JON SKEET** Private methods cannot be virtual, even though there is one corner case where it would make sense: A nested class derived from its own container class could override it (with another private method). While it's a tiny bit inelegant for this possibility to be forbidden by the specification, it means that methods that are accidentally private and virtual can be treated as errors—and this is a far more common case.

The implementation of a nonvirtual method is invariant: The implementation is the same whether the method is invoked on an instance of the class in which it is declared or an instance of a derived class. In contrast, the implementation of a virtual method can be superseded by derived classes. The process of superseding the implementation of an inherited virtual method is known as overriding that method (§10.6.4).

In a virtual method invocation, the runtime type of the instance for which that invocation takes place determines the actual method implementation to invoke. In a nonvirtual method invocation, the compile-time type of the instance is the determining factor. In precise terms, when a method named N is invoked with an argument list A on an instance with a compile-time type C and a runtime type R (where R is either C or a class derived from C), the invocation is processed as follows:

- First, overload resolution is applied to C, N, and A to select a specific method M from the set of methods declared in and inherited by C. This is described in §7.6.5.1.
- Then, if M is a nonvirtual method, M is invoked.
- Otherwise, M is a virtual method, and the most derived implementation of M with respect to R is invoked.

For every virtual method declared in or inherited by a class, there exists a most derived implementation of the method with respect to that class. The most derived implementation of a virtual method M with respect to a class R is determined as follows:

- If R contains the introducing virtual declaration of M, then it is the most derived implementation of M.
- Otherwise, if R contains an override of M, then it is the most derived implementation of M.
- Otherwise, the most derived implementation of M with respect to R is the same as the most derived implementation of M with respect to the direct base class of R.

The following example illustrates the differences between virtual and nonvirtual methods:

```
using System;
class A
{
    public void F() { Console.WriteLine("A.F"); }
    public virtual void G() { Console.WriteLine("A.G"); }
}
class B : A
{
    new public void F() { Console.WriteLine("B.F"); }
    public override void G() { Console.WriteLine("B.G"); }
}
class Test
{
    static void Main() {
        B b = new B();
        A a = b;
        a.F();
        b.F();
        a.G();
        b.G();
    }
}
```

In the example, A introduces a nonvirtual method F and a virtual method G. The class B introduces a new non-virtual method F, thus hiding the inherited F, and also overrides the inherited method G. The example produces the following output:

A.F
B.F
B.G
B.G

Notice that the statement a.G() invokes B.G, not A.G. This outcome occurs because the runtime type of the instance (which is B), not the compile-time type of the instance (which is A), determines the actual method implementation to invoke.

Because methods are allowed to hide inherited methods, it is possible for a class to contain several virtual methods with the same signature. This does not present an ambiguity problem, since all but the most derived method are hidden. In the example

```
using System;
class A
{
    public virtual void F() { Console.WriteLine("A.F"); }
}
class B : A
{
    public override void F() { Console.WriteLine("B.F"); }
}
class C : B
{
    new public virtual void F() { Console.WriteLine("C.F"); }
}
class D : C
{
    public override void F() { Console.WriteLine("D.F"); }
}
class Test
{
    static void Main() {
        D d = new D();
        A a = d;
        B b = d;
        C c = d;
        a.F();
        b.F();
        c.F();
        d.F();
    }
}
```

the C and D classes contain two virtual methods with the same signature: the one introduced by A and the one introduced by C. The method introduced by C hides the method inherited from A. Thus the override declaration in D overrides the method introduced by C, and it is not possible for D to override the method introduced by A. The example produces the following output:

```
B.F
B.F
D.F
D.F
```

Note that it is possible to invoke the hidden virtual method by accessing an instance of D through a less derived type in which the method is not hidden.

## 10.6.4 Override Methods

When an instance method declaration includes an override modifier, the method is said to be an override method. An override method overrides an inherited virtual method with the same signature. Whereas a virtual method declaration introduces a new method, an override method declaration specializes an existing inherited virtual method by providing a new implementation of that method.

The method overridden by an override declaration is known as the overridden base method. For an override method M declared in a class C, the overridden base method is determined by examining each base class type of C, starting with the direct base class type of C and continuing with each successive direct base class type, until in a given base class type at least one accessible method is located that has the same signature as M after substitution of type arguments. For the purposes of locating the overridden base method, a method is considered accessible if it is public, if it is protected, if it is protected internal, or if it is internal and declared in the same program as C.

A compile-time error occurs unless all of the following are true for an override declaration:

- An overridden base method can be located as described above.
- There is exactly one such overridden base method. This restriction has effect only if the base class type is a constructed type where the substitution of type arguments makes the signature of two methods the same.
- The overridden base method is a virtual, abstract, or override method. In other words, the overridden base method cannot be static or non-virtual.
- The overridden base method is not a sealed method.
- The override method and the overridden base method have the same return type.
- The override declaration and the overridden base method have the same declared accessibility. In other words, an override declaration cannot change the accessibility of the virtual method. However, if the overridden base method is protected internal and it is declared in a different assembly than the assembly containing the override method, then the override method's declared accessibility must be protected.
- The override declaration does not specify type-parameter-constraints-clauses. Instead, the constraints are inherited from the overridden base method. Note that constraints that are type parameters in the overridden method may be replaced by type arguments in the inherited constraint. This can lead to constraints that are not legal when explicitly specified, such as value types or sealed types.

The following example demonstrates how the overriding rules work for generic classes:

```
abstract class C<T>
{
    public virtual T F() {...}
    public virtual C<T> G() {...}
    public virtual void H(C<T> x) {...}
}
class D: C<string>
{
    public override string F() {...}        // Okay
    public override C<string> G() {...}    // Okay
    public override void H(C<T> x) {...}   // Error: should be C<string>
}
class E<T,U>: C<U>
{
    public override U F() {...}            // Okay
    public override C<U> G() {...}         // Okay
    public override void H(C<T> x) {...}   // Error: should be C<U>
}
```

An override declaration can access the overridden base method using a *base-access* (§7.6.8). In the example

```
class A
{
    int x;
    public virtual void PrintFields() {
        Console.WriteLine("x = {0}", x);
    }
}
class B: A
{
    int y;
    public override void PrintFields() {
        base.PrintFields();
        Console.WriteLine("y = {0}", y);
    }
}
```

The base.PrintFields() invocation in B invokes the PrintFields method declared in A. A *base-access* disables the virtual invocation mechanism and simply treats the base method as a non-virtual method. Had the invocation in B been written ((A)this).PrintFields(), it
