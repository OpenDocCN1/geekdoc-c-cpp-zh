
> **ERIC LIPPERT** If you need a pair, triple, and so on, the generic “tuple” types defined in the CLR 4 version of the framework are handy types.

When the generic class is used, type arguments must be provided for each of the type parameters:

```csharp
Pair<int,string> pair = new Pair<int,string> { First = 1, Second = "two" };
int i = pair.First;    // TFirst is int
string s = pair.Second; // TSecond is string
```

A generic type with type arguments provided, like `Pair<int,string>` above, is called a constructed type.

### 1.6.4 Base Classes

A class declaration may specify a base class by following the class name and type parameters with a colon and the name of the base class. Omitting a base class specification is the same as deriving from type object. In the following example, the base class of Point3D is Point, and the base class of Point is object:

```csharp
public class Point
{
    public int x, y;

    public Point(int x, int y)
    {
        this.x = x;
        this.y = y;
    }
}

public class Point3D : Point
{
    public int z;

    public Point3D(int x, int y, int z) : base(x, y)
    {
        this.z = z;
    }
}
```

A class inherits the members of its base class. Inheritance means that a class implicitly contains all members of its base class, except for the instance and static constructors, and the destructors of the base class. A derived class can add new members to those it inherits, but it cannot remove the definition of an inherited member. In the previous example, Point3D inherits the x and y fields from Point, and every Point3D instance contains three fields, x, y, and z.

> **JESSE LIBERTY** There is nothing more important to understand about C# than inheritance and polymorphism. These concepts are the heart of the language and the soul of object-oriented programming. Read this section until it makes sense, or ask for help or supplement it with additional reading, but do not skip over it—these issues are the sine qua non of C#.

An implicit conversion exists from a class type to any of its base class types. Therefore, a variable of a class type can reference an instance of that class or an instance of any derived class. For example, given the previous class declarations, a variable of type Point can reference either a Point or a Point3D:

```csharp
Point a = new Point(10, 20);
Point b = new Point3D(10, 20, 30);
```

### 1.6.5 Fields

A field is a variable that is associated with a class or with an instance of a class.

A field declared with the static modifier defines a static field. A static field identifies exactly one storage location. No matter how many instances of a class are created, there is only ever one copy of a static field.

> **ERIC LIPPERT** Static fields are per constructed type for a generic type. That is, if you have a
>
> ```csharp
> class Stack<T> {
>     public readonly static Stack<T> empty = whatever; ...
> }
> ```
>
> then `Stack<int>.empty` is a different field than `Stack<string>.empty`.

A field declared without the static modifier defines an instance field. Every instance of a class contains a separate copy of all the instance fields of that class.

In the following example, each instance of the Color class has a separate copy of the r, g, and b instance fields, but there is only one copy of the Black, White, Red, Green, and Blue static fields:

```csharp
public class Color
{
    public static readonly Color Black = new Color(0, 0, 0);
    public static readonly Color White = new Color(255, 255, 255);
    public static readonly Color Red = new Color(255, 0, 0);
    public static readonly Color Green = new Color(0, 255, 0);
    public static readonly Color Blue = new Color(0, 0, 255);

    private byte r, g, b;

    public Color(byte r, byte g, byte b)
    {
        this.r = r;
        this.g = g;
        this.b = b;
    }
}
```

As shown in the previous example, read-only fields may be declared with a readonly modifier. Assignment to a readonly field can occur only as part of the field's declaration or in a constructor in the same class.

> **BRAD ABRAMS** readonly protects the location of the field from being changed outside the type's constructor, but does not protect the value at that location. For example, consider the following type:
>
> ```csharp
> public class Names
> {
>     public static readonly StringBuilder FirstBorn = new StringBuilder("Joe");
>     public static readonly StringBuilder SecondBorn = new StringBuilder("Sue");
> }
> ```
>
> Outside of the constructor, directly changing the FirstBorn instance results in a compiler error:
>
> ```csharp
> Names.FirstBorn = new StringBuilder("Biff");
> // Compile error
> ```
>
> However, I am able to accomplish exactly the same results by modifying the StringBuilder instance:
>
> ```csharp
> Names.FirstBorn.Remove(0, 6).Append("Biff");
> Console.WriteLine(Names.FirstBorn);    // Outputs "Biff"
> ```
>
> It is for this reason that we strongly recommend that read-only fields be limited to immutable types. Immutable types do not have any publicly exposed setters, such as int, double, or String.

> **BILL WAGNER** Several well-known design patterns make use of the read-only fields of mutable types. The Adapter, Decorator, Façade, and Proxy patterns are the most obvious examples. When you are creating a larger structure by composing smaller structures, you will often express instances of those smaller structures using read-only fields. A read-only field of a mutable type should indicate that one of these structural patterns is being used.

### 1.6.6 Methods

A method is a member that implements a computation or action that can be performed by an object or class. Static methods are accessed through the class. Instance methods are accessed through instances of the class.

Methods have a (possibly empty) list of parameters, which represent values or variable references passed to the method, and a return type, which specifies the type of the value computed and returned by the method. A method's return type is void if it does not return a value.

Like types, methods may also have a set of type parameters, for which type arguments must be specified when the method is called. Unlike types, the type arguments can often be inferred from the arguments of a method call and need not be explicitly given.

The signature of a method must be unique in the class in which the method is declared. The signature of a method consists of the name of the method, the number of type parameters, and the number, modifiers, and types of its parameters. The signature of a method does not include the return type.

> **ERIC LIPPERT** An unfortunate consequence of generic types is that a constructed type may potentially have two methods with identical signatures. For example, class `C<T> { void M(T t){} void M(int t){} ... }` is perfectly legal, but `C<int>` has two methods M with identical signatures. As we'll see later on, this possibility leads to some interesting scenarios involving overload resolution and explicit interface implementations. A good guideline: Don't create a generic type that can create ambiguities under construction in this way; such types are extremely confusing and can produce unexpected behaviors.

#### 1.6.6.1 *Parameters*

Parameters are used to pass values or variable references to methods. The parameters of a method get their actual values from the *arguments* that are specified when the method is invoked. There are four kinds of parameters: value parameters, reference parameters, out parameters, and parameter arrays.

A *value parameter* is used for input parameter passing. A *value parameter* corresponds to a local variable that gets its initial value from the argument that was passed for the parameter. Modifications to a value parameter do not affect the argument that was passed for the parameter.

> **BILL WAGNER** The statement that modifications to value parameters do not affect the argument might be misleading because mutator methods may change the contents of a parameter of reference type. The value parameter does not change, but the contents of the referred-to object do.

Value parameters can be optional, by specifying a default value so that corresponding arguments can be omitted.

A *reference parameter* is used for both input and output parameter passing. The argument passed for a reference parameter must be a variable, and during execution of the method, the reference parameter represents the same storage location as the argument variable. A reference parameter is declared with the `ref` modifier. The following example shows the use of `ref` parameters.

```csharp
using System;

class Test
{
    static void Swap(ref int x, ref int y) {
        int temp = x;
        x = y;
        y = temp;
    }
    static void Main() {
        int i = 1, j = 2;
        Swap(ref i, ref j);
        Console.WriteLine("{0} {1}", i, j); // Outputs "2 1"
    }
}
```
