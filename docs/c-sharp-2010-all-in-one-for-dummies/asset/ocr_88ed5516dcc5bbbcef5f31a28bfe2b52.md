![](bbox=[0.02, 0.18, 0.12, 0.3])

```
public class Car
{
    public static int numberOfCars; // The number of cars built
    public string licensePlate;     // The license plate ID
}
```

Static members aren't accessed through the object. Instead, you access them by way of the class itself, as this code snippet demonstrates:

```
// Create a new object of class Car.
Car newCar = new Car();
newCar.licensePlate = "ABC123";
// Now increment the count of cars to reflect the new one.
Car.numberOfCars++;
```

The object member newCar.licensePlate is accessed through the object newCar, and the class (static) member Car.numberOfCars is accessed through the class Car. All Cars share the same numberOfCars member, so each car contains exactly the same value as all other cars.

![](bbox=[0.02, 0.55, 0.12, 0.67])

Class members are static members. Nonstatic members are specific to each 'instance' (each individual object) and are instance members. The italicized phrases you see here are the generic way to refer to these types of members.

# Defining const and readonly Data Members

One special type of static member is the const data member, which represents a constant. You must establish the value of a const variable in the declaration, and you cannot change it anywhere within the program, as shown here:

```
class Program
{
    // Number of days in the year (including leap day)
    public const int daysInYear = 366;   // Must have initializer.
    public static void Main(string[] args)
    {
        // This is an array, covered later in this chapter.
        int[] maxTemperatures = new int[daysInYear];
        for(int index = 0; index < daysInYear; index++)
        {
            // . . . accumulate the maximum temperature for each
            // day of the year . . .
        }
    }
}
```

You can use the constant daysInYear in place of the value 366 anywhere within your program. The const variable is useful because it can replace a mysterious number such as 366 with the descriptive name daysInYear to enhance the readability of your program.