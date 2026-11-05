```
```csharp
class B: A
{
    public override void F() {
        base.F();               // Error: base.F is abstract
    }
}
```
```

a compile-time error is reported for the base.F() invocation because it references an abstract method.

An abstract method declaration is permitted to override a virtual method. This allows an abstract class to force reimplementation of the method in derived classes, and makes the original implementation of the method unavailable. In the example

```
```csharp
using System;

class A
{
    public virtual void F() {
        Console.WriteLine("A.F");
    }
}

abstract class B: A
{
    public abstract override void F();
}

class C: B
{
    public override void F() {
        Console.WriteLine("C.F");
    }
}
```
```

class A declares a virtual method, class B overrides this method with an abstract method, and class C overrides the abstract method to provide its own implementation.

> > **MAREK SAFAR** There are no visibility restrictions on abstract methods except that they cannot be private. That access choice can cause trouble when someone accidentally declares an internal abstract method within a public abstract class; such a class, even though it is declared public, cannot be used outside the class assembly.

# 10.6.7 External Methods

When a method declaration includes an extern modifier, that method is said to be an *external method*. External methods are implemented externally, typically using a language