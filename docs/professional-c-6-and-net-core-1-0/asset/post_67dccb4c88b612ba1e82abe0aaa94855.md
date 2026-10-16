
override the method of the base class if it is declared virtual and serves the same purpose. However, in case other methods already invoke this method, a simple rename can lead to breaking other code.

> **NOTE** The `new` method modifier shouldn’t be used deliberately to hide members of the base class. The main purpose of this modifier is to deal with version conflicts and react to changes on base classes after the derived class was done.

## Calling Base Versions of Methods

C# has a special syntax for calling base versions of a method from a derived class: `base.<MethodName>`. For example, you have the `Move` method declared in the base class `Shape` and want to invoke it in the derived class `Rectangle` to use the implementation from the base class. To add functionality from the derived class, you can invoke it using `base` (code file `VirtualMethods/Shape.cs`):

```csharp
public class Shape
{
    public virtual void Move(Position newPosition)
    {
        Position.X = newPosition.X;
        Position.Y = newPosition.Y;
        WriteLine($"moves to {Position}");
    }
    //... other members
}
```

The `Move` method is overridden in the `Rectangle` class to add the term `Rectangle` to the console. After this text is written, the method of the base class is invoked using the `base` keyword (code file `VirtualMethods/ConcreteShapes.cs`):

```csharp
public class Rectangle: Shape
{
    public override void Move(Position newPosition)
    {
        Write("Rectangle");
        base.Move(newPosition);
    }
    //... other members
}
```

Now move the rectangle to a new position (code file `VirtualMethods/Program.cs`):

```csharp
r.Move(new Position { X = 120, Y = 40 });
```

Run the application to see output that is a result of the `Move` method in the `Rectangle` and the `Shape` classes:

```
Rectangle moves to X: 120, Y: 40
```

> **NOTE** *Using the* `base` *keyword you can invoke any method of the base class—not just the method that is overridden.*

## Abstract Classes and Methods

C# allows both classes and methods to be declared as abstract. An abstract class cannot be instantiated, whereas an abstract method does not have an implementation and must be overridden in any nonabstract derived class. Obviously, an abstract method is *automatically* virtual (although you don’t need to supply the `virtual` keyword, and doing so results in a syntax error). If any class contains any abstract methods, that class is also abstract and must be declared as such.

Let’s change the `Shape` class to be `abstract`. With this it is necessary to derive from this class. The new method `Resize` is declared abstract, and thus it can’t have any implementation in the `Shape` class (code file `VirtualMethods/Shape.cs`):

```csharp
public abstract class Shape
{
    public abstract void Resize(int width, int height);   // abstract method
}
```

When deriving a type from the abstract base class, it is necessary to implement all abstract members. Otherwise, the compiler complains:

```csharp
public class Ellipse : Shape
{
    public override void Resize(int width, int height)
    {
        Size.Width = width;
        Size.Height = height;
    }
}
```

Of course, the implementation could also look like the following example. Throwing an exception of type `NotImplementedException` is also an implementation, just not the implementation that was meant to be and usually just a temporary implementation during development:

```csharp
public override void Resize(int width, int height)
{
    throw new NotImplementedException();
}
```

> **NOTE** *Exceptions are explained in detail in Chapter 14, “Errors and Exceptions.”*

Using the abstract `Shape` class and the derived `Ellipse` class, you can declare a variable of a `Shape`. You cannot instantiate it, but you can instantiate an `Ellipse` and assign it to the `Shape` variable (code file `VirtualMethods/Program.cs`):

```csharp
Shape s1 = new Ellipse();
DrawShape(s1);
```

## Sealed Classes and Methods

In case it shouldn’t be allowed to create a class that derives from your class, your class should be sealed. Adding the `sealed` modifier to a class doesn’t allow you to create a subclass of it. Sealing a method means it’s not possible to override this method.

```csharp
sealed class FinalClass
{
    // etc
}

class DerivedClass : FinalClass        // wrong. Cannot derive from sealed class.
{
    // etc
}
```

The most likely situation in which you’ll mark a class or method as sealed is if the class or method is internal to the operation of the library, class, or other classes that you are writing, to ensure that any attempt to override some of its functionality might lead to instability in the code. For example, maybe you haven’t tested inheritance and made the investment in design decisions for inheritance. If this is the case, it’s better to mark your class sealed.

There’s another reason to seal classes. With a sealed class, the compiler knows that derived classes are not possible, and thus the virtual table used for virtual methods can be reduced or eliminated, which can increase performance. The `string` class is sealed. As I haven’t seen a single application not using strings, it’s best to have this type as performant as possible. Making the class sealed is a good hint for the compiler.

Declaring a method as sealed serves a purpose similar to that for a class. The method can be an overridden method from a base class, but in the following example the compiler knows another class cannot extend the virtual table for this method; it ends here.

```csharp
class MyClass : MyBaseClass
{
    public sealed override void FinalMethod()
    {
        // implementation
    }
}

class DerivedClass : MyClass
{
    public override void FinalMethod()  // wrong. Will give compilation error
    {
    }
}
```

In order to use the `sealed` keyword on a method or property, it must have first been overridden from a base class. If you do not want a method or property in a base class overridden, then don’t mark it as virtual.

## Constructors of Derived Classes

Chapter 3 discusses how constructors can be applied to individual classes. An interesting question arises as to what happens when you start defining your own constructors for classes that are part of a hierarchy, inherited from other classes that may also have custom constructors.

Assume that you have not defined any explicit constructors for any of your classes. This means that the compiler supplies default zeroing-out constructors for all your classes. There is actually quite a lot going on under the hood when that happens, but the compiler is able to arrange it so that things work out nicely throughout the class hierarchy, and every field in every class is initialized to whatever its default value is. When you add a constructor of your own, however, you are effectively taking control of construction. This has implications right down through the hierarchy of derived classes, so you have to ensure that you don’t inadvertently do anything to prevent construction through the hierarchy from taking place smoothly.

You might be wondering why there is any special problem with derived classes. The reason is that when you create an instance of a derived class, more than one constructor is at work. The constructor of the class you instantiate isn’t by itself sufficient to initialize the class; the constructors of the base classes must also be called. That’s why we’ve been talking about construction through the hierarchy.

With the earlier sample of the `Shape` type, properties have been initialized using the auto property initializer:

```csharp
public class Shape
{
    public Position Position { get; } = new Position();
    public Size Size { get; } = new Size();
}
```

Behind the scenes, the compiler creates a default constructor for the class and moves the property initializer within this constructor:

```csharp
public class Shape
{
    public Shape()
    {
        Position = new Position();
        Size = new Size();
    }
    public Position Position { get; }
    public Size Size { get; }
}
```
