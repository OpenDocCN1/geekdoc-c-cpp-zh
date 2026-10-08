Inheritance is easily accomplished in C# by providing the name of the class being inherited on the class declaration. Listing 4.1 shows the hierarchy described by Figure 4.1 in code.

# **LISTING 4.1** A Class Hierarchy in Code

```
public class Vehicle { }

public class FourWheeledVehicle : Vehicle { }
public class TwoWheeledVehicle : Vehicle { }

public class Car : FourWheeledVehicle { }
public class Truck : FourWheeledVehicle { }

public class Motorcycle : TwoWheeledVehicle { }
```

This type of inheritance is also called **implementation inheritance** because you are actually inheriting an implementation from the parent class. Now that you have a code representation of the hierarchy, how would you go about using it?

# **Watch Out!**

> **Designing Class Hierarchies**

The one thing that inheritance does not enable is removing data or behaviors. If you find that you need to remove behavior or data from one of your derived classes, it is most likely because your class hierarchy is not designed correctly. Designing class hierarchies is not always an easy task and usually takes several attempts to get it right. The best approach is to spend a little more time thinking about the relationships between objects you know and those that might be needed later. If your class hierarchy is overly shallow (not a lot of inheritance) or overly deep (a lot of inheritance), you might want to rethink the relationships. Remember, not everything in a class hierarchy must be related to one another. It's perfectly acceptable to have a hierarchy that is conceptually made up of several smaller ones.

In C#, an expression assigned to a variable must be known to be compatible with the type of that variable. This means the following code is not allowed:

```
Car c = new Car();
Truck t = c;
```

This should make sense, as a truck is not the same thing as a car. However, logically both a truck and a car are a `FourWheeledVehicle` and, in turn, a `Vehicle` so the following code is allowed: