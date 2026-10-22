
Encapsulation is achieved by utilizing access specifiers. An access specifier determines the scope and visibility of a class member. Available access specifiers are public, protected, private, and internal.

### How to Achieve Encapsulation

We can achieve encapsulation by using a private access modifier, as shown in the below example method.

```csharp
private string GetEngineMakeFormula()
{
    private string formula = "a*b";
    return formula;
}
```

### Example—Encapsulation

```csharp
public class Car
{
    public int mileage = 65;
    public string color = "Black";
    private string formula = "a*b";

    //Its public - so accessible outside class
    public int GetMileage()
    {
        return mileage;
    }
    //Its public - so accessible outside class
    public string GetColor()
    {
```

## Abstract Classes

In C#, abstraction is achieved with the help of Abstract classes. An abstract class is declared with the help of an abstract keyword.

In C#, you are not permitted to create objects of the abstract class. Or in other words, you cannot use the abstract class directly with the new operator.

Class that includes the abstract keyword with some of its methods (not all abstract methods) is known as an Abstract Base Class. While a class that includes the abstract keyword with all of its methods is known as pure Abstract Base Class.

You are not allowed to declare the abstract methods outside the abstract class. You are not allowed to declare an abstract class as a sealed class.

For example, we continue with “Car” as an example, and we have no access to the piston directly and use the start button to run the piston. Just imagine if a Car manufacturer allows direct access to the piston, it would be very difficult to control actions on the piston. That’s the reason why a Car provider separates its internal implementation from its external interface.

```csharp
public class Car
{
    public int mileage = 24;
    public string color = "Black";
    private string formula = "a*b";
    //Its public - so accessible outside class
```

```csharp
public static void Main(string[] args)
{
    Car objCar = new Car();
    Console.WriteLine("Car mileage is : " + objCar.GetMileage()); // accessible outside "Car"

    Console.WriteLine("Car color is : " + objCar.GetColor()); //accessible outside "Car"
    //we can’t call this method as it is inaccessible outside "Car"
    //objCar.GetEngineMakeFormula(); //commented because we can’t access it
    Console.WriteLine("Car color is : " + objCar.DisplayMakeFormula()); // accessible outside
    Console.Read();
}
```

As you can see from the above code, necessary methods and properties are exposed using public access modifier, and unnecessary methods and properties are hidden using private access modifier. This way, we can implement abstraction, or we can achieve abstraction in our code or web application.

## Inheritance

The inheritance is a way to make new classes using classes that have already been defined. The newly formed classes are called derived classes; the classes that we derive from are called base classes. Important advantages of inheritance are code reuse and reduction of complexity of a program. The derived classes (descendants) override or extend the functionality of the base classes (ancestors). To illustrate with an example:

```csharp
using System;
public class Being
{
    public Being()
    {
        Console.WriteLine("Being is created");
    }
}

public class Human: Being
{
    public Human()
    {
        Console.WriteLine("Human is created");
    }
}

public class Inheritance
{
static void Main()
    {
        new Human();
    }
}
```

In this program, we have two classes: a base Being class and a derived Human class. The derived class inherits from the base class:

- `public class Human: Being`

In C#, we use the colon (:) operator to create inheritance relations:

- `new Human();`

We instantiate the derived Human class.

The output of the above Inheritance code will be:

- Being is created
- Human is created

We can see that both constructors were called. First, the constructor of the base class is called, then the constructor of the derived class.

## Polymorphism

Polymorphism could be described as applying an operator or function in various ways for different data inputs.

In practical terms, polymorphism means that if class B inherits from class A, it does not have to inherit everything about class A; meaning it can do some of the things that class A does differently.

Polymorphism also stands for the ability to redefine methods for derived classes. There are two types of binding. Example of the runtime polymorphism would be:

```csharp
using System;
public abstract class Shape
{
    protected int x;
    protected int y;
    public abstract int Area();
}
public class Rectangle : Shape
{
    public Rectangle(int x, int y)
    {
        this.x = x;
        this.y = y;
    }
    public override int Area()
    {
    }
}
public class Square: Shape
{
    public Square(int x)
    {
        this.x = x;
    }
    public override int Area()
    {
        return this.x * this.x;
    }
}
public class Polymorphism
{
    static void Main()
    {
        Shape[] shapes = { new Square(5),
            new Rectangle(9, 4), new
            Square(12) };
        foreach (Shape shape in shapes)
        {
            Console.WriteLine(shape.Area());
        }
    }
}
```

In the above program, we have an abstract Shape class. This class morphs into two descendant classes: Rectangle and Square. Both offer their own implementation of the Area() method:

```csharp
public override int Area()
{
    return this.x * this.y;
}
...
public override int Area()
{
    return this.x * this.x;
}
```

The Rectangle and the Square classes have their implementations of the Area() method.

```csharp
Shape[] shapes = { new Square(5),
    new Rectangle(9, 4), new Square(12) };
```

We create an array of three Shapes.

```csharp
foreach (Shape shape in shapes)
{
    Console.WriteLine(shape.Area());
}
```

You will be expected to go through each shape and call the Area() method on it. The compiler returns the most suitable method for each shape. This defines the essence of polymorphism.

## IMPLEMENTATION OF OOP

The main idea behind OOP is to have in a single unit both data and the methods that manage the data; such units are called an object. All OOP languages offer mechanisms that help you implement the object-oriented model—encapsulation, inheritance, polymorphism, and reusability.

### Encapsulation

Encapsulation puts together code and the data it regulates, keeps them both safe. Encapsulation is a protective tool that prevents code and data from being hacked by other code located outside the container.

### Inheritance

Inheritance is the process by which one object receives the properties of another object. Inheritance is most useful when you have to upgrade functionality of an existing type. For instance, all .NET classes inherit from the System.Object class, so a class can hold new functionality as well as use the existing object’s class functions and features.

### Polymorphism

Polymorphism is a feature that allows one interface to be used for a general class of action. This concept is at times defined as “one interface, multiple actions.” The specific action is determined by the exact nature of circumstances.

### Reusability

Once a class has been scripted and debugged, it can be shared with other programmers for use in their own programs. This is called reusability. A programmer can use an existing class and, without optimizing it, add additional features if necessary.

This simple one-class console “Hello world” program elaborates many fundamental concepts:

```csharp
using System;
namespace oops
{
    //class definition
    public class SimpleHelloWorld
    {
        //Entry point of the program
        static void Main(string [] args)
        {
            //print Hello world"
```
