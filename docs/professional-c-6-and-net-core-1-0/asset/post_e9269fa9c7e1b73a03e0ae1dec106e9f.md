
```csharp
private int _number;
public MyNumber(int number)
{
    _number = number;
}
```

If you now try instantiating a MyNumber object using a no-parameter constructor, you get a compilation error:

```csharp
var numb = new MyNumber(); // causes compilation error
```

Note that it is possible to define constructors as private or protected, so that they are invisible to code in unrelated classes too:

```csharp
public class MyNumber
{
    private int _number;
    private MyNumber(int number) // another overload
    {
        _number = number;
    }
}
```

This example hasn’t actually defined any public, or even any protected, constructors for MyNumber. This would actually make it impossible for MyNumber to be instantiated by outside code using the new operator (though you might write a public static property or method in MyNumber that can instantiate the class). This is useful in two situations:

- If your class serves only as a container for some static members or properties, and therefore should never be instantiated. With this scenario, you can declare the class with the modifier static. With this modifier the class can contain only static members and cannot be instantiated.
- If you want the class to only ever be instantiated by calling a static member function (this is the so-called factory pattern approach to object instantiation). An implementation of the Singleton pattern is shown in the following code snippet.

```csharp
public class Singleton
{
    private static Singleton s_instance;
    private int _state;
    private Singleton(int state)
    {
        _state = state;
    }
    public static Singleton Instance
    {
        get { return s_instance ?? (s_instance = new Singleton(42)); }
    }
}
```

The Singleton class contains a private constructor, so you can instantiate it only within the class itself. To instantiate it, the static property Instance returns the field s_instance. If this field is not yet initialized (null), a new instance is created by calling the instance constructor. For the null check, the coalescing operator is used. If the left side of this operator is null, the right side of this operator is processed and the instance constructor invoked.

> NOTE The coalescing operator is explained in detail in Chapter 8.

## Calling Constructors from Other Constructors

You might sometimes find yourself in the situation where you have several constructors in a class, perhaps to accommodate some optional parameters for which the constructors have some code in common. For example, consider the following:

```csharp
class Car
{
    private string _description;
    private uint _nWheels;

    public Car(string description, uint nWheels)
    {
        _description = description;
        _nWheels = nWheels;
    }

    public Car(string description)
    {
        _description = description;
        _nWheels = 4;
    }
    // etc.
}
```

Both constructors initialize the same fields. It would clearly be neater to place all the code in one location. C# has a special syntax known as a constructor initializer to enable this:

```csharp
class Car
{
    private string _description;
    private uint _nWheels;

    public Car(string description, uint nWheels)
    {
        _description = description;
        _nWheels = nWheels;
    }

    public Car(string description) : this(description, 4)
    {
    }
    // etc
}
```

In this context, the this keyword simply causes the constructor with the nearest matching parameters to be called. Note that any constructor initializer is executed before the body of the constructor. Suppose that the following code is run:

```csharp
var myCar = new Car("Proton Persona");
```

In this example, the two-parameter constructor executes before any code in the body of the one-parameter constructor (though in this particular case, because there is no code in the body of the one-parameter constructor, it makes no difference).

A C# constructor initializer may contain either one call to another constructor in the same class (using the syntax just presented) or one call to a constructor in the immediate base class (using the same syntax, but using the keyword `base` instead of `this`). It is not possible to put more than one call in the initializer.

## Static Constructors

One feature of C# is that it is also possible to write a static no-parameter constructor for a class. Such a constructor is executed only once, unlike the constructors written so far, which are instance constructors that are executed whenever an object of that class is created:

```csharp
class MyClass
{
    static MyClass()
    {
        // initialization code
    }
    // rest of class definition
}
```

One reason for writing a static constructor is if your class has some static fields or properties that need to be initialized from an external source before the class is first used.

The .NET runtime makes no guarantees about when a static constructor will be executed, so you should not place any code in it that relies on it being executed at a particular time (for example, when an assembly is loaded). Nor is it possible to predict in what order static constructors of different classes will execute. However, what is guaranteed is that the static constructor will run at most once, and that it will be invoked before your code makes any reference to the class. In C#, the static constructor is usually executed immediately before the first call to any member of the class.

Note that the static constructor does not have any access modifiers. It’s never called explicitly by any other C# code, but always by the .NET runtime when the class is loaded, so any access modifier such as `public` or `private` would be meaningless. For this same reason, the static constructor can never take any parameters, and there can be only one static constructor for a class. It should also be obvious that a static constructor can access only static members, not instance members, of the class.

It is possible to have a static constructor and a zero-parameter instance constructor defined in the same class. Although the parameter lists are identical, there is no conflict because the static constructor is executed when the class is loaded, but the instance constructor is executed whenever an instance is created. Therefore, there is no confusion about which constructor is executed or when.

If you have more than one class that has a static constructor, the static constructor that is executed first is undefined. Therefore, you should not put any code in a static constructor that depends on other static constructors having been or not having been executed. However, if any static fields have been given default values, these are allocated before the static constructor is called.

The next example illustrates the use of a static constructor. It is based on the idea of a program that has user preferences (which are presumably stored in some configuration file). To keep things simple, assume just one user preference—a quantity called BackColor that might represent the background color to be used in an application. Because we don’t want to get into the details of writing code to read data from an external source here, assume also that the preference is to have a background color of red on weekdays and green on weekends. All the program does is display the preference in a console window, but that is enough to see a static constructor at work.

The class UserPreferences is declared with the static modifier; thus it cannot be instantiated and can only contain static members. The static constructor initializes the BackColor property depending on the day of the week (code file StaticConstructorSample/UserPreferences.cs):

```csharp
public static class UserPreferences
{
    public static Color BackColor { get; }

    static UserPreferences()
    {
        DateTime now = DateTime.Now;
        if (now.DayOfWeek == DayOfWeek.Saturday
            || now.DayOfWeek == DayOfWeek.Sunday)
        {
            BackColor = Color.Green;
        }
        else
        {
            BackColor = Color.Red;
        }
    }
}
```

This code makes use of the System.DateTime struct that is supplied with the .NET Framework. DateTime implements a static property Now that returns the current time. DayOfWeek is an instance property of DateTime that returns an enum value of type DayOfWeek.

Color is defined as an enum type and contains a few colors. The enum types are explained in detail later in the section Enums (code file StaticConstructorSample/Enum.cs):
