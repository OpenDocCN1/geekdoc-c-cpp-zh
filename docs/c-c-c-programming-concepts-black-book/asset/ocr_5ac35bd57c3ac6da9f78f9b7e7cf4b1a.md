```
```csharp
        {
            Console.WriteLine("Vehicle type is car");
        }
    }
    public class Bike : Vehicle
    {
        public override void PrintVehicleType()
        {
            Console.WriteLine("Vehicle type is Bike");
        }
    }
```
```

In Listing 18.22, we have defined a base class Vehicle, which is generic in type. In addition, we have defined two derived classes that represent two different vehicle types car and bike. After that, we have overridden the PrintVehicleType() method in both the derived classes. Listing 18.22 shows how to call the overridden methods:

# Listing 18.22: Showing the Procedure to Call the Overridden Methods

```
```csharp
    public class Program
    {
        public static void Main(string[] args)
        {
            Car car = new Car();
            Bike bike = new Bike();
            car.PrintVehicleType();
            bike.PrintVehicleType();
        }
    }
```
```

In the Main() method, we have called the overridden methods by creating the objects of derived classes.

In addition, we can call the two overridden methods by first instantiating an object array of the base class and then assigning its derived classes as array elements, as shown in Listing 18.23:

# Listing 18.23: Showing an Alternative Procedure to Call the Overridden Methods

```
```csharp
    public class Program
    {
        public static void Main(string[] args)
        {
            Vehicle[] vehicleList = new Vehicle[2];
            vehicleList[0] = new Car();
            vehicleList[1] = new Bike();
            foreach(Vehicle obj in vehicleList)
            {
                obj.PrintVehicleType();
            }
        }
    }
```
```

The output of the preceding code is given as follows:

```
```
Vehicle type is car
Vehicle type is Bike
```
```

Using the concept of inheritance, chain inheritance can be defined where all the classes inherit the properties, methods, and interfaces of some base classes. For example, if the Vehicle class has one virtual method that has been overridden by its derived class Four Wheeler, then regardless of whether the derived class is declared overridden or sealed, the virtual method will remain virtual indefinitely; and therefore, the child class of the Four Wheeler class can access that virtual method. Listing 18.24 shows the implementation of this example: