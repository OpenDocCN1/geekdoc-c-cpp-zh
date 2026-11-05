
```csharp
class Derived: Base
{
    public class Nested
    {
        public void G() {
            Derived d = new Derived();
            d.F();        // Okay
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

The nested class Derived.Nested accesses the protected method F defined in Derived’s base class, Base, by calling through an instance of Derived.

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
        Outer<T>.Inner<String>.F(t, "abc");  // These two statements
        Inner<String>.F(t, "abc");           // have the same effect
        Outer<int>.Inner<string>.F(3, "abc"); // This type is different
        Outer.Inner<string>.F(t, "abc");      // Error: Outer needs type arg
    }
}
```

Although it is bad programming style, a type parameter in a nested type can hide a member or type parameter declared in the outer type:

```csharp
class Outer<T>
{
    class Inner<T>                    // Valid: hides Outer's T
    {
        public T t;                    // Refers to Inner's T
    }
}
```

## 10.3.9 Reserved Member Names

To facilitate the underlying C# runtime implementation, for each source member declaration that is a property, event, or indexer, the implementation must reserve two method signatures based on the kind of the member declaration, its name, and its type. It is a compile-time error for a program to declare a member whose signature matches one of these reserved signatures, even if the underlying runtime implementation does not make use of these reservations.

The reserved names do not introduce declarations; thus they do not participate in member lookup. However, a declaration's associated reserved method signatures do participate in inheritance (§10.3.3) and can be hidden with the new modifier (§10.3.4).

The reservation of these names serves three purposes:

- It allows the underlying implementation to use an ordinary identifier as a method name for get or set access to the C# language feature.
- It allows other languages to interoperate using an ordinary identifier as a method name for get or set access to the C# language feature.
- It helps ensure that the source accepted by one conforming compiler is accepted by another, by making the specifics of reserved member names consistent across all C# implementations.

The declaration of a destructor (§10.13) also causes a signature to be reserved (§10.3.9.4).

### 10.3.9.1 Member Names Reserved for Properties

For a property P (§10.7) of type T, the following signatures are reserved:

```csharp
T get_P();
void set_P(T value);
```

Both signatures are reserved, even if the property is read-only or write-only.

> **BILL WAGNER** Even though you could write methods that are named `get_<something>` and `set_<something>`, if `<something>` is not a property name, this technique is not recommended. Avoiding it will minimize the need to update the code in the future.

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

A class A defines a read-only property P, thus reserving signatures for get_P and set_P methods. The class B derives from A and hides both of these reserved signatures. The example produces the following output:

```text
123
123
456
```

### 10.3.9.2 Member Names Reserved for Events

For an event E (§10.8) of delegate type T, the following signatures are reserved:

```csharp
void add_E(T handler);
void remove_E(T handler);
```

### 10.3.9.3 Member Names Reserved for Indexers

For an indexer (§10.9) of type T with parameter-list L, the following signatures are reserved:

```csharp
T get_Item(L);
void set_Item(L, T value);
```

Both signatures are reserved, even if the indexer is read-only or write-only. Furthermore, the member name Item is reserved.

### 10.3.9.4 Member Names Reserved for Destructors

For a class containing a destructor (§10.13), the following signature is reserved:

```csharp
void Finalize();
```

## 10.4 Constants

A constant is a class member that represents a constant value—a value that can be computed at compile time. A constant-declaration introduces one or more constants of a given type.

```text
constant-declaration:
attributes_opt constant-modifiers_opt const type constant-declarators ;

constant-modifiers:
constant-modifier
constant-modifiers constant-modifier

constant-modifier:
new
public
protected
internal
private

constant-declarators:
constant-declarator
constant-declarators , constant-declarator
```

```text
constant-declarator:
    identifier  =  constant-expression
```

A *constant-declarator* may include a set of *attributes* (§17), a new modifier (§10.3.4), and a valid combination of the four access modifiers (§10.3.5). The attributes and modifiers apply to all of the members declared by the *constant-declarator*. Even though constants are considered static members, a *constant-declaration* neither requires nor allows a static modifier. It is an error for the same modifier to appear multiple times in a constant declaration.

The *type* of a *constant-declarator* specifies the type of the members introduced by the declaration. The type is followed by a list of *constant-declarators*, each of which introduces a new member. A *constant-declarator* consists of an *identifier* that names the member, followed by an “=” token, followed by a *constant-expression* (§7.19) that gives the value of the member.

The type specified in a constant declaration must be either `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `char`, `float`, `double`, `decimal`, `bool`, `string`, an *enum-type*, or a *reference-type*. Each *constant-expression* must yield a value of the target type or of a type that can be converted to the target type by an implicit conversion (§6.1).

> **JON SKEET** The inclusion of `decimal` here is interesting when targeting the Common Language Infrastructure. All of the other types have literal representations within the CLI, whereas `decimal` doesn’t. The Microsoft C# compiler achieves the appropriate behavior by creating a static read-only field declaration, albeit decorated with `DecimalConstantAttribute`. A similar attribute exists for `DateTime`, but C# doesn't allow `DateTime` constants.

The *type* of a constant must be at least as accessible as the constant itself (§3.5.4).

The value of a constant is obtained in an expression using a *simple-name* (§7.6.2) or a *member-access* (§7.6.4).

A constant can itself participate in a *constant-expression*. Thus a constant may be used in any construct that requires a *constant-expression*. Examples of such constructs include case labels, goto case statements, enum member declarations, attributes, and other constant declarations.

As described in §7.19, a *constant-expression* is an expression that can be fully evaluated at compile time. Since the only way to create a non-null value of a *reference-type* other than `string` is to apply the `new` operator, and since the `new` operator is not permitted in a *constant-expression*, the only possible value for constants of *reference-types* other than `string` is null.
