
For interfaces that are strictly single-inheritance (each interface in the inheritance chain has exactly zero or one direct base interface), the effects of the member lookup (§7.4), method invocation (§7.6.1), and indexer access (§7.6.6.2) rules are exactly the same as for classes and structs: More derived members hide less derived members with the same name or signature. However, for multiple-inheritance interfaces, ambiguities can occur when two or more unrelated base interfaces declare members with the same name or signature. This section shows several examples of such situations. In all cases, explicit casts can be used to resolve the ambiguities.

### In the example

```
interface IList
{
    int Count { get; set; }
}
interface ICounter
{
    void Count(int i);
}
interface IListCounter : IList, ICounter { }
class C
{
    void Test(IListCounter x)
    {
        x.Count(1);            // Error
        x.Count = 1;           // Error
        ((IList)x).Count = 1;  // Okay: invokes IList.Count.set
        ((ICounter)x).Count(1); // Okay: invokes ICounter.Count
    }
}
```

the first two statements cause compile-time errors because the member lookup (§7.4) of Count in IListCounter is ambiguous. As illustrated by the example, the ambiguity is resolved by casting x to the appropriate base interface type. Such casts have no runtime costs—they merely consist of viewing the instance as a less derived type at compile time.

### In the example

```
interface IInteger
{
    void Add(int i);
}
interface IDouble
{
    void Add(double d);
}
interface INumber : IInteger, IDouble { }
```

```
class C
{
    void Test(INumber n)
    {
        n.Add(1);        // Invokes IInteger.Add
        n.Add(1.0);      // Only IDouble.Add is applicable
        ((IInteger)n).Add(1);  // Only IInteger.Add is a candidate
        ((IDouble)n).Add(1);   // Only IDouble.Add is a candidate
    }
}
```

the invocation n.Add(1) selects IInteger.Add by applying the overload resolution rules of §7.5.3. Similarly, the invocation n.Add(1.0) selects IDouble.Add. When explicit casts are inserted, there is only one candidate method and, therefore, no ambiguity.

### In the example

```
interface IBase
{
    void F(int i);
}

interface ILeft: IBase
{
    new void F(int i);
}

interface IRight: IBase
{
    void G();
}

interface IDerived: ILeft, IRight {}

class A
{
    void Test(IDerived d) {
        d.F(1);               // Invokes ILeft.F
        ((IBase)d).F(1);      // Invokes IBase.F
        ((ILeft)d).F(1);      // Invokes ILeft.F
        ((IRight)d).F(1);     // Invokes IBase.F
    }
}
```

the IBase.F member is hidden by the ILeft.F member. The invocation d.F(1) thus selects ILeft.F, even though IBase.F appears to not be hidden in the access path that leads through IRight.

The intuitive rule for hiding in multiple-inheritance interfaces is simply this: If a member is hidden in any access path, it is hidden in all access paths. Because the access path from IDerived to ILeft to IBase hides IBase.F, the member is also hidden in the access path from IDerived to IRight to IBase.

## 13.3 Fully Qualified Interface Member Names

An interface member is sometimes referred to by its fully qualified name. The fully qualified name of an interface member consists of the name of the interface in which the member is declared, followed by a dot, followed by the name of the member. The fully qualified name of a member references the interface in which the member is declared. For example, given the declarations

```
```csharp
interface IControl
{
    void Paint();
}
interface ITextBox : IControl
{
    void SetText(string text);
}
```
```

the fully qualified name of Paint is IControl.Paint and the fully qualified name of SetText is ITextBox.SetText.

In the example above, it is not possible to refer to Paint as ITextBox.Paint.

When an interface is part of a namespace, the fully qualified name of an interface member includes the namespace name. For example:

```
```csharp
namespace System
{
    public interface ICloneable
    {
        object Clone();
    }
}
```
```

Here, the fully qualified name of the Clone method is System.ICloneable.Clone.

## 13.4 Interface Implementations

Interfaces may be implemented by classes and structs. To indicate that a class or struct directly implements an interface, the interface identifier is included in the base class list of the class or struct. For example:

```
```csharp
interface ICloneable
{
    object Clone();
}
```
```

## 13. Interfaces

```
```csharp
interface IComparable
{
    int CompareTo(object other);
}

class ListEntry : ICloneable, IComparable
{
    public object Clone() {...}
    public int CompareTo(object other) {...}
}
```
```

> **JON SKEET**  It bugs me that the interface implementation is usually so totally implicit. There's no indication that the `CompareTo` and `Clone` methods have anything to do with the interfaces for which they're providing implementations. When overriding virtual methods inherited from a base class, the `override` modifier makes this behavior obvious: Anyone refactoring a class and wanting to rename a method is informed that it's linked to a method elsewhere. No such indication is given for interfaces.
> 
> Unfortunately, the design of interface implementation wouldn't quite be consistent with adding a modifier to the declaration. The code declaring a method doesn't necessarily even know that it may be used to implement an interface:
> 
> ```csharp
> interface IFoo { void Foo(); }
> class Base
> {
>     public void Foo();
> }
> // IFoo.Foo is implemented by Base.Foo
> class Derived : Base, IFoo { }
> ```
> 
> This is probably the most pragmatic approach to interfaces, but from a purity (or control freak) standpoint, it feels slightly wrong.

A class or struct that directly implements an interface also directly implements all of the interface's base interfaces implicitly. This is true even if the class or struct doesn't explicitly list all base interfaces in the base class list. For example:

```
```csharp
interface IControl
{
    void Paint();
}

interface ITextBox : IControl
{
    void SetText(string text);
}
```
```

## 13. Interfaces

```
class TextBox : ITextBox
{
    public void Paint() {...}
    public void SetText(string text) {...}
}
```

Here, class TextBox implements both IControl and ITextBox.

When a class C directly implements an interface, all classes derived from C also implement the interface implicitly. The base interfaces specified in a class declaration can be constructed interface types (§4.4). A base interface cannot be a type parameter on its own, although it can involve the type parameters that are in scope. The following code illustrates how a class can implement and extend constructed types:

```
class C<U, V> { }
interface II<V> { }
class D : C<string, int>, II<string> { }
class E<T> : C<int, T>, II<T> { }
```

The base interfaces of a generic class declaration must satisfy the uniqueness rule described in §13.4.2.

### 13.4.1 Explicit Interface Member Implementations

For purposes of implementing interfaces, a class or struct may declare explicit interface member implementations. An explicit interface member implementation is a method, property, event, or indexer declaration that references a fully qualified interface member name. For example:

```
interface IList<T>
{
    T[] GetElements();
}
interface IDictionary<K,V>
{
    V this[K key];
    void Add(K key, V value);
}
class List<T> : IList<T>, IDictionary<int,T>
{
    T[] IList<T>.GetElements() {...}
    T IDictionary<int,T>.this[int index] {...}
    void IDictionary<int,T>.Add(int index, T value) {...}
}
```

## 13. Interfaces

Here IDictionary<int,T>.this and IDictionary<int,T>.Add are explicit interface member implementations.

In some cases, the name of an interface member may not be appropriate for the implementing class, in which case the interface member may be implemented using explicit interface member implementation. A class implementing a file abstraction, for example, would likely implement a Close member function that has the effect of releasing the file resource, and implement the Dispose method of the IDisposable interface using explicit interface member implementation:

```
interface IDisposable
{
    void Dispose();
}

class MyFile : IDisposable
{
    void IDisposable.Dispose()
    {
        Close();
    }

    public void Close()
    {
        // Do what's necessary to close the file
        System.GC.SuppressFinalize(this);
    }
}
```

It is not possible to access an explicit interface member implementation through its fully qualified name in a method invocation, property access, or indexer access. An explicit interface member implementation can be accessed only through an interface instance, and is in that case referenced simply by its member name.

It is a compile-time error for an explicit interface member implementation to include access modifiers, and it is a compile-time error to include the modifiers abstract, virtual, override, or static.

Explicit interface member implementations have different accessibility characteristics than other members. Because explicit interface member implementations are never accessible through their fully qualified names in a method invocation or a property access, they are, in a sense, private. However, because they can be accessed through an interface instance, they are, in a sense, also public.

> VLADIMIR RESHETNIKOV  For the purposes of accessibility constraints checking (see §3.4), explicit interface implementations are considered private.
