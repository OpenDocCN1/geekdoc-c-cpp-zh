
Pass this for the instance of the containing type as a constructor argument for the nested type. The following example

```csharp
using System;
class C
{
    int i = 123;

    public void F() {
        Nested n = new Nested(this);
        n.G();
    }

    public class Nested
    {
        C this_c;

        public Nested(C c) {
            this_c = c;
        }

        public void G() {
            Console.WriteLine(this_c.i);
        }
    }
}

class Test
{
    static void Main() {
        C c = new C();
        c.F();
    }
}
```

shows this technique. An instance of C creates an instance of Nested and passes its own this to Nested's constructor to provide subsequent access to C's instance members.

> **JON SKEET** This section of the specification may seem strange at first sight: Why bother to specify what you can't do? Why would anyone expect to be able to get at an instance of the containing type from an instance of a nested type? Well, in Java, that's exactly how inner classes do work. To achieve C#-like nested type behavior, you need to declare the nested type as static—which is nothing like a static class in C#!

### 10.3.8.5 Access to Private and Protected Members of the Containing Type

A nested type has access to all of the members that are accessible to its containing type, including members of the containing type that have private and protected declared accessibility. The example

```csharp
using System;

class C
{
    private static void F() {
        Console.WriteLine("C.F");
    }

    public class Nested
    {
        public static void G() {
            F();
        }
    }
}

class Test
{
    static void Main() {
        C.Nested.G();
    }
}
```

shows a class C that contains a nested class Nested. Within Nested, the method G calls the static method F defined in C, and F has private declared accessibility.

> > **JON SKEET**  Again, this behavior is different from that in Java, where an outer type has access to the private members of a nested type, but not vice versa. I find the C# approach to be more sensible. It also allows for some nice patterns, such as creating an abstract class with a private constructor: All the derived classes have to be nested within the abstract class. Oddly enough, I find the main use case for this behavior is emulating Java enums.

A nested type also may access protected members defined in a base type of its containing type. In the example

```csharp
using System;

class Base
{
    protected void F() {
        Console.WriteLine("Base.F");
    }
}

class Derived: Base
{
    public class Nested
    {
        public void G() {
            Derived d = new Derived();
            d.F();          // Okay
        }
    }
}
class Test
{
    static void Main() {
        Derived.Nested n = new Derived.Nested();
        n.G();
    }
}
```

the nested class Derived.Nested accesses the protected method F defined in Derived’s base class, Base, by calling through an instance of Derived.

### 10.3.8.6 Nested Types in Generic Classes

A generic class declaration can contain nested type declarations. The type parameters of the enclosing class can be used within the nested types. A nested type declaration can contain additional type parameters that apply only to the nested type.

Every type declaration contained within a generic class declaration is implicitly a generic type declaration. When writing a reference to a type nested within a generic type, the containing constructed type, including its type arguments, must be named. However, from within the outer class, the nested type can be used without qualification; the instance type of the outer class can be implicitly used when constructing the nested type. The following example shows three different—and correct—ways to refer to a constructed type created from Inner; the first two are equivalent:

```csharp
class Outer<T>
{
    class Inner<U>
    {
        public static void F(T t, U u) {...}
    }

    static void F(T t) {
        Outer<T>.Inner<string>.F(t, "abc");   // These two statements
        Inner<string>.F(t, "abc");            // have the same effect

        Outer<int>.Inner<string>.F(3, "abc"); // This type is different

        Outer.Inner<string>.F(t, "abc");      // Error: Outer needs type arg
    }
}
```

Although it is bad programming style, a type parameter in a nested type can hide a member or type parameter declared in the outer type:

```csharp
class Outer<T>
{
    class Inner<T>    // Valid: hides Outer's T
    {
        public T t;   // Refers to Inner's T
    }
}
```

## 10.3.9 Reserved Member Names

To facilitate the underlying C# runtime implementation, for each source member declaration that is a property, event, or indexer, the implementation must reserve two method signatures based on the kind of the member declaration, its name, and its type. It is a compile-time error for a program to declare a member whose signature matches one of these reserved signatures, even if the underlying runtime implementation does not make use of these reservations.

The reserved names do not introduce declarations; thus they do not participate in member lookup. However, a declaration's associated reserved method signatures do participate in inheritance (§10.3.3) and can be hidden with the new modifier (§10.3.4).

The reservation of these names serves three purposes:

- It allows the underlying implementation to use an ordinary identifier as a method name for get or set access to the C# language feature.
- It allows other languages to interoperate use of an ordinary identifier as a method name for get or set access to the C# language feature.
- It helps ensure that the source accepted by one conforming compiler is accepted by another, by making the specifics of reserved member names consistent across all C# implementations.

The declaration of a destructor (§10.13) also causes a signature to be reserved (§10.3.9.4).

### 10.3.9.1 Member Names Reserved for Properties

For a property P (§10.7) of type T, the following signatures are reserved:

```
T get_P();
void set_P(T value);
```

Both signatures are reserved, even if the property is read-only or write-only.

> > **BILL WAGNER** Even though you could write methods that are named `get_<something>` and `set_<something>`, if `<something>` is not a property name, this technique is not recommended. Avoiding it will minimize the need to update the code in the future.

In the example

```csharp
using System;

class A
{
    public int P {
        get { return 123; }
    }
}

class B: A
{
    new public int get_P() {
        return 456;
    }

    new public void set_P(int value) {
    }
}

class Test
{
    static void Main() {
        B b = new B();
        A a = b;
        Console.WriteLine(a.P);
        Console.WriteLine(b.P);
        Console.WriteLine(b.get_P());
    }
}
```

a class A defines a read-only property P, thus reserving signatures for get_P and set_P methods. The class B derives from A and hides both of these reserved signatures. The example produces the following output:

```
123
123
456
```

### 10.3.9.2 Member Names Reserved for Events

For an event E (§10.8) of delegate type T, the following signatures are reserved:

```
void add_E(T handler);
void remove_E(T handler);
```

### 10.3.9.3 Member Names Reserved for Indexers

For an indexer (§10.9) of type T with parameter-list L, the following signatures are reserved:

```
T get_Item(L);
void set_Item(L, T value);
```

Both signatures are reserved, even if the indexer is read-only or write-only. Furthermore, the member name Item is reserved.

### 10.3.9.4 Member Names Reserved for Destructors

For a class containing a destructor (§10.13), the following signature is reserved:

```
void Finalize();
```

## 10.4 Constants

A constant is a class member that represents a constant value—a value that can be computed at compile time. A constant-declaration introduces one or more constants of a given type.

```
constant-declaration:
    attributes_opt constant-modifiers_opt const type constant-declarators ;
```

```
constant-modifiers:
    constant-modifier
    constant-modifiers constant-modifier
```

- new
- public
- protected
- internal
- private

```
constant-declarators:
    constant-declarator
    constant-declarators , constant-declarator
```
