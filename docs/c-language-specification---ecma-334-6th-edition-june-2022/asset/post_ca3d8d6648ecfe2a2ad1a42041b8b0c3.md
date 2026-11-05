
```
int x;
static int y;
void F()
{
    x = 1;    // Ok, same as this.x = 1
    y = 1;    // Ok, same as Test.y = 1
}

static void G()
{
    x = 1;    // Error, cannot access this.x
    y = 1;    // Ok, same as Test.y = 1
}

static void Main()
{
    Test t = new Test();
    t.x = 1;    // Ok
    t.y = 1;    // Error, cannot access static member through instance
    Test.x = 1; // Error, cannot access instance member through type
    Test.y = 1; // Ok
}
```

The F method shows that in an instance function member, a simple_name (§11.7.4) can be used to access both instance members and static members. The G method shows that in a static function member, it is a compile-time error to access an instance member through a simple_name. The Main method shows that in a member_access (§11.7.6), instance members shall be accessed through instances, and static members shall be accessed through types.

*end example*

## 14.3.9 Nested types

### 14.3.9.1 General

A type declared within a class or struct is called a nested type. A type that is declared within a compilation unit or namespace is called a non-nested type.

*Example:* In the following example:

```
using System;

class A
{
    class B
    {
        static void F()
        {
            Console.WriteLine("A.B.F");
        }
    }
}
```

class B is a nested type because it is declared within class A, and class A is a non-nested type because it is declared within a compilation unit.

*end example*

### 14.3.9.2 Fully qualified name

The fully qualified name (§7.8.3) for a nested type declaration is S.N where S is the fully qualified name of the type declaration in which type N is declared and N is the unqualified name (§7.8.2) of the nested type declaration (including any generic_dimension_specifier (§11.7.16)).

### 14.3.9.3 Declared accessibility

Non-nested types can have public or internal declared accessibility and have internal declared accessibility by default. Nested types can have these forms of declared accessibility too, plus one or more additional forms of declared accessibility, depending on whether the containing type is a class or struct:

- A nested type that is declared in a class can have any of five forms of declared accessibility (public, protected internal, protected, internal, or private) and, like other class members, defaults to private declared accessibility.
- A nested type that is declared in a struct can have any of three forms of declared accessibility (public, internal, or private) and, like other struct members, defaults to private declared accessibility.

*Example: The example*

```
```csharp
public class List
{
    // Private data structure
    private class Node
    {
        public object Data;
        public Node Next;

        public Node(object data, Node next)
        {
            this.Data = data;
            this.Next = next;
        }
    }

    private Node first = null;
    private Node last = null;

    // Public interface
    public void AddToFront(object o) {...}
    public void AddToBack(object o) {...}
    public object RemoveFromFront() {...}
    public object RemoveFromBack() {...}
    public int Count { get {...} }
}
```
```

declares a private nested class Node.

*end example*

### 14.3.9.4 Hiding

A nested type may hide (§7.7.2.2) a base member. The new modifier (§14.3.5) is permitted on nested type declarations so that hiding can be expressed explicitly.

Example: The example

```
using System;
class Base
{
    public static void M()
    {
        Console.WriteLine("Base.M");
    }
}

class Derived: Base
{
    public new class M
    {
        public static void F()
        {
            Console.WriteLine("Derived.M.F");
        }
    }
}

class Test
{
    static void Main()
    {
        Derived.M.F();
    }
}
```

shows a nested class M that hides the method M defined in Base.

end example

### 14.3.9.5 this access

A nested type and its containing type do not have a special relationship with regard to this_access (§11.7.12). Specifically, this within a nested type cannot be used to refer to instance members of the containing type. In cases where a nested type needs access to the instance members of its containing type, access can be provided by providing the this for the instance of the containing type as a constructor argument for the nested type.

Example: The following example

```
using System;

class C
{
    int i = 123;
    public void F()
    {
        Nested n = new Nested(this);
        n.G();
    }

    public class Nested
{
```

```
~~~csharp
        C this_c;

        public Nested(C c)
        {
            this_c = c;
        }

        public void G()
        {
            Console.WriteLine(this_c.i);
        }
    }

    class Test
    {
        static void Main()
        {
            C c = new C();
            c.F();
        }
    }
~~~
```

shows this technique. An instance of C creates an instance of Nested, and passes its own this to Nested's constructor in order to provide subsequent access to C's instance members.

*end example*

### 14.3.9.6 Access to private and protected members of the containing type

A nested type has access to all of the members that are accessible to its containing type, including members of the containing type that have private and protected declared accessibility.

*Example: The example*

```
~~~csharp
using System;

class C
{
    private static void F() => Console.WriteLine("C.F");

    public class Nested
    {
        public static void G() => F();
    }
}

class Test
{
    static void Main() => C.Nested.G();
}
~~~
```

shows a class C that contains a nested class Nested. Within Nested, the method G calls the static method F defined in C, and F has private declared accessibility.

*end example*

A nested type also may access protected members defined in a base type of its containing type.

Example: In the following code

```
using System;
class Base
{
    protected void F() => Console.WriteLine("Base.F");
}

class Derived: Base
{
    public class Nested
    {
        public void G()
        {
            Derived d = new Derived();
            d.F(); // ok
        }
    }
}

class Test
{
    static void Main()
    {
        Derived.Nested n = new Derived.Nested();
        n.G();
    }
}
```

the nested class Derived.Nested accesses the protected method F defined in Derived's base class, Base, by calling through an instance of Derived.

end example

### 14.3.9.7 Nested types in generic classes

A generic class declaration may contain nested type declarations. The type parameters of the enclosing class may be used within the nested types. A nested type declaration may contain additional type parameters that apply only to the nested type.

Every type declaration contained within a generic class declaration is implicitly a generic type declaration. When writing a reference to a type nested within a generic type, the containing constructed type, including its type arguments, shall be named. However, from within the outer class, the nested type may be used without qualification; the instance type of the outer class may be implicitly used when constructing the nested type.

Example: The following shows three different correct ways to refer to a constructed type created from Inner; the first two are equivalent:

```
class Outer<T>
{
    class Inner<U>
    {
        public static void F(T t, U u) {...}
    }

    static void F(T t)
```

```
{
    Outer<T>.Inner<string>.F(t, "abc");    // These two statements have
    Inner<string>.F(t, "abc");            // the same effect
    Outer<int>.Inner<string>.F(3, "abc"); // This type is different
    Outer.Inner<string>.F(t, "abc");      // Error, Outer needs type arg
}
```

*end example*

Although it is bad programming style, a type parameter in a nested type can hide a member or type parameter declared in the outer type.

*Example:*

```
class Outer<T>
{
    class Inner<T>                     // Valid, hides Outer's T
    {
        public T t;                    // Refers to Inner's T
    }
}
```

*end example*

## 14.3.10 Reserved member names

### 14.3.10.1 General

To facilitate the underlying C# run-time implementation, for each source member declaration that is a property, event, or indexer, the implementation shall reserve two method signatures based on the kind of the member declaration, its name, and its type (§14.3.10.2, §14.3.10.3, §14.3.10.4). It is a compile-time error for a program to declare a member whose signature matches a signature reserved by a member declared in the same scope, even if the underlying run-time implementation does not make use of these reservations.

The reserved names do not introduce declarations, thus they do not participate in member lookup. However, a declaration's associated reserved method signatures do participate in inheritance (§14.3.4), and can be hidden with the new modifier (§14.3.5).

*Note:* The reservation of these names serves three purposes:

1. To allow the underlying implementation to use an ordinary identifier as a method name for get or set access to the C# language feature.
2. To allow other languages to interoperate using an ordinary identifier as a method name for get or set access to the C# language feature.
3. To help ensure that the source accepted by one conforming compiler is accepted by another, by making the specifics of reserved member names consistent across all C# implementations.

*end note*

The declaration of a finalizer (§14.13) also causes a signature to be reserved (§14.3.10.5).

### 14.3.10.2 Member names reserved for properties

For a property P (§14.7) of type T, the following signatures are reserved:
