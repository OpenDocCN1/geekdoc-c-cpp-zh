
## 1. Open the file named `Vehicle.cs`.
- Modify the `Vehicle` class so that it is an abstract class and make the `Operate` method an abstract method.
- Correct the resulting compiler errors.
- Run the application using Ctrl+F5 and observe that the output matches what is shown in Figure 4.6.

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_125_0.png)

**FIGURE 4.6** Result of working with abstract classes

## Interfaces

Because C# does not enable you to inherit from multiple base classes, you need to carefully choose that base class. Fortunately, C# provides an alternative that does enable multiple inheritance. An interface defines a set of common characteristics and behaviors, in the form of public properties and methods, that all derived classes are guaranteed to implement. Think of an interface as a partial type definition, or a type description.

Like abstract classes, an interface cannot be directly instantiated and can have methods, properties, and events. Interfaces cannot contain fields, constructors, or a destructor.

### Interfaces Are Not Contracts

It is common to say that an interface defines a contract which any derived classes must implement. This is only true in the sense that the inherited interface defines the method signatures and properties guaranteed to be available on the derived class.

In no way does this provide any guarantee of a specific implementation. It is entirely possible to satisfy the interface while providing no useful implementation whatsoever. The interface simply defines a contract that specifies any classes inheriting it have specific properties and methods.

### Watch Out!

You declare an interface in much the same way as declaring a class, substituting the keyword `interface` for the `class` keyword. An interface can be `internal`, `public`, `protected`, or `private`; however, if you don’t explicitly indicate the accessibility, interfaces default to `internal` accessibility. All interface members are automatically `public` and cannot specify an access modifier. Because interface members are also automatically `abstract`, they cannot provide an implementation.

When a class inherits an interface, called **interface inheritance** or interface implementation, it inherits only the member names and signatures because the interface doesn’t provide an implementation. This means the derived class must provide an implementation for all members defined by that interface. To inherit an interface, you provide the name of the interface just as if you were inheriting a class. You can inherit from multiple interfaces simply by providing a comma-separated list of interface names.

### By the Way

> ### Inheriting Both a Base Class and Interfaces

C# uses a positional notation to indicate the base class and the interfaces in the inheritance list. If a class inherits from both a base class and one or more interfaces, the base class is always listed first.

You can also “mix and match” inheritance, meaning that you can inherit from only a base class, inherit only one or more interfaces, or inherit from both a base class and one or more interfaces. If a base class inherits from an interface, any classes that derive from that base class inherit that implementation.

Although interfaces cannot inherit from a class, they can inherit from other interfaces. If you think of an interface as a weak contract, interface inheritance simply means that to satisfy this contract, you must also satisfy these other contracts. This enables you to create highly specialized interfaces and then aggregate those interfaces together to form a larger interface. This is particularly useful if you have multiple unrelated classes that need to implement similar functionality, such as saving data to a compressed ZIP file. The behavior and characteristics related to this could be defined by interfaces, which could then be included as part of other interfaces that define your business objects.

### Did you Know?

> ### Interfaces and Extension Methods

In the context of interfaces, extension methods become even more powerful as you can also extend interfaces. Doing this allows all types that implement that interface to gain the extension method. In fact, the entire Language Integrated Query (LINQ) functionality for the generic collections is implemented this way.

When an interface inherits from another interface, the derived interface defines only members that are new; it does not redefine the members of the inherited interfaces. When a class implements this aggregated interface, it must provide implementations for members defined in all the interfaces.

Where the real power and flexibility of using interfaces shines is when used in combination with abstract classes. Because interface methods are implicitly abstract, an abstract class does not need to provide an implementation for an interface member. Instead, it can provide its own abstract member for the interface member. In that case, any derived classes must override it and provide an implementation.

Looking at the vehicle hierarchy from Listing 4.1, what would it take to introduce the concept of emergency vehicles, such as fire trucks, police cars, and police motorcycles? You could introduce a new class, called EmergencyVehicle, but it isn’t entirely clear where this new class fits in the existing hierarchy because it would need to be a base class at the same level as FourWheeledVehicle and TwoWheeledVehicle, and any concrete classes would want to inherit from both EmergencyVehicle or Truck, Car, or Motorcycle. You already know this type of multiple inheritance is not possible, but how would this change if you used interfaces instead?

## Try It Yourself

## Working with Interfaces

These steps explore how to use both interfaces and base classes to create a flexible class hierarchy. If you closed Visual Studio, repeat the previous exercise first.

- Create a new interface named `IVehicle` that defines a method named `Operate` and modify the `Vehicle` class to inherit from it. The `IVehicle.Operate` method should have the same signature as the `Vehicle.Operate` method.
- Create a new interface named `IEmergencyVehicle` that inherits from `IVehicle` and provides a void method named `SoundSiren` that takes no parameters.
- Create three new classes named `PoliceCar`, `PoliceMotorcycle`, and `FireTruck` that derive from the appropriate base class and implement the `IEmergencyVehicle` interface. For the implementation of `SoundSiren`, simply print a message to the console.
- In the `Main` method of the `Program.cs` file, enter code that will:
    - Create a new instance of a `Car`, assigned to a variable named `car`, and call the `Operate` method.
    - Assign a new instance of `PoliceCar` to `car` and call the `Operate` method.
    - Create a new instance of `PoliceCar` named `policeCar` and assign `car` to it. You need to cast `car` to be of type `PoliceCar`.
    - Call `SoundSiren` on `policeCar`.
- Run the application using Ctrl+F5, and observe that the output matches what is shown in Figure 4.7.

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_128_0.png)

When you implemented the interfaces from the last exercise, you used implicit interface implementation, in which the class simply declares public members that match those defined by the interface. This is the most common form of interface implementation.

What happens if the class implements multiple interfaces that specify a member with the same signature, as shown in Listing 4.5?

## LISTING 4.5 Multiple Interface Inheritance

```
interface IVehicle
{
   void Operate();
}

interface IEquipment
{
   void Operate();
}

class PoliceCar : IVehicle, IEquipment
{
   public void Operate()
   {
   }
}
```

In this case, the compiler makes the public method match both interface members. If this isn't what you intended, you must use explicit interface implementation, as shown in Listing 4.6, which requires that you fully qualify the name of the member being implemented. In explicit interface implementation, you do not provide an
