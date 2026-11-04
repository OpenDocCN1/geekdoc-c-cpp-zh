# 27

# Using Interfaces

In .NET programming, an *interface* is like a contract. It defines the public properties, methods, and events that a class must provide to satisfy the contract. It doesn't indicate how the class must provide these features, however. That's left up to the class's code. It only defines an interface that the class must show to the rest of the world.

In this lesson, you learn how to implement interfaces that are predefined by the .NET Framework. You also learn how to define your own interfaces to make your code safer and more efficient.

# INTERFACE ADVANTAGES

The following sections discuss two of the most important advantages provided by interfaces: multiple inheritance and code generalization.

# Multiple Inheritance

Suppose you define a `Vehicle` class with properties such as `NumberOfPassengers`, `MilesPerGallon`, and `NumberOfCupHolders`. From this class you can derive other classes such as `Car`, `PickupTruck`, and `Unicycle`.

Suppose you also define a `Domicile` class that has properties such as `SquareFeet`, `NumberOfBedrooms`, and `HasAnnoyingNeighbor`. From this class you can derive `Apartment`, `Condo`, and `VacationHome`.

Next you might like to derive the `MotorHome` class from both `Vehicle` and `Domicile` so it has the properties and methods of both parent classes. Unfortunately you can't do that in C#. In C#, a class can inherit from only a single parent class.

Although a class can have only one parent, it can implement any number of interfaces. For example, if you turn the `Domicile` class into the `IDomicile` interface, the `MotorHome` class can inherit from `Vehicle` and implement `IDomicile`. The interface doesn't provide the code needed to implement such features as the `HasAnnoyingNeighbor` property, but at least it defines that property so code that uses a `MotorHome` object knows the property is available.