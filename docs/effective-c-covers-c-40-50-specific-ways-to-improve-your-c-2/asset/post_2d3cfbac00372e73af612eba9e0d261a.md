
This implementation reuse provides another benefit: If you add a method to the base class, all derived classes are automatically and implicitly enhanced. In that sense, base classes provide a way to extend the behavior of several types efficiently over time: By adding and implementing functionality in the base class, all derived classes immediately incorporate that behavior. Adding a member to an interface breaks all the classes that implement that interface. They will not contain the new method and will no longer compile. Each implementer must update that type to include the new member.

Choosing between an abstract base class and an interface is a question of how best to support your abstractions over time. Interfaces are fixed: You release an interface as a contract for a set of functionality that any type can implement. Base classes can be extended over time. Those extensions become part of every derived class.

The two models can be mixed to reuse implementation code while supporting multiple interfaces. One obvious example in the .NET Framework is the IEnumerable<T> interface and the System.Linq.Enumerable class. The System.Linq.Enumerable class contains a large number of extension methods defined on the System.Collections.Generic.IEnumerable<T> interface. That separation enables very important benefits. Any class that implements IEnumerable<T> appears to include all those extension methods. However, those additional methods are not formally defined in the IEnumerable<T> interface. That means class developers do not need to create their own implementation of all those methods.

Examine this class that implements IEnumerable<T> for weather observations.

```csharp
public enum Direction
{
    North,
    NorthEast,
    East,
    SouthEast,
    South,
    SouthWest,
    West,
    NorthWest
}
```

```csharp
public class WeatherData
{
    public double Temperature { get; set; }
    public int WindSpeed { get; set; }
    public Direction WindDirection { get; set; }
    public override string ToString()
    {
        return string.Format(
            "Temperature = {0}, Wind is {1} mph from the {2}",
            Temperature, WindSpeed, WindDirection);
    }
}
```

```csharp
public class WeatherDataStream : IEnumerable<WeatherData>
{
    private Random generator = new Random();

    public WeatherDataStream(string location)
    {
        // elided
    }

    private IEnumerator<WeatherData> GetElements()
    {
        // Real implementation would read from
        // a weather station.
        for (int i = 0; i < 100; i++)
            yield return new WeatherData
            {
                Temperature = generator.NextDouble() * 90,
                WindSpeed = generator.Next(70),
                WindDirection = (Direction)generator.Next(7)
            };
    }

    #region IEnumerable<WeatherData> Members
    public IEnumerator<WeatherData> GetEnumerator()
    {
        return GetElements();
    }
    #endregion

    #region IEnumerable Members
    System.Collections.IEnumerator System.Collections.IEnumerable.GetEnumerator()
    {
        return GetElements();
    }
    #endregion
}
```

The WeatherDataStream class models a sequence of weather observations. To do that it implements IEnumerable<WeatherData>. That means creating two methods: the GetEnumerator<T>() method and the classic GetEnumerator method. The latter interface is explicitly implemented so that client code would naturally be drawn to the generic interface over the version typed as System.Object.

Implementing those two methods means that the WeatherDataStream class supports all the extension methods defined in System.Linq.Enumerable. That means WeatherDataStream can be a source for LINQ queries:

```csharp
var warmDays = from item in
    new WeatherDataStream("Ann Arbor")
    where item.Temperature > 80
    select item;
```

LINQ query syntax compiles to method calls. The query above translates to the following calls:

```csharp
var warmDays2 = new WeatherDataStream("Ann Arbor").
    Where(item => item.Temperature > 80).
    Select(item => item);
```

In the code above, the Where and Select calls look like they belong to IEnumerable<WeatherData>. They do not. Those methods appear to belong to IEnumerable<WeatherData> because they are extension methods. They are actually static methods in System.Linq.Enumerable. The compiler translates those calls into the following static calls:

```csharp
// Don't write this, for explanatory purposes
var warmDays3 = Enumerable.Select(
    Enumerable.Where(
        new WeatherDataStream("Ann Arbor"),
        item => item.Temperature > 80),
        item => item);
```

I wrote that last version to show you that interfaces really can't contain implementation. You can emulate that by using extension methods. LINQ does that by creating several extension methods on IEnumerable<T> in the System.Linq.Enumerable class.

That brings me to the topic of using interfaces as parameters and return values. An interface can be implemented by any number of unrelated types. Coding to interfaces provides greater flexibility to other developers than coding to base class types. That's important because of the single inheritance hierarchy that the .NET environment enforces.

These three methods perform the same task:

```csharp
public static void PrintCollection<T>(
    IEnumerable<T> collection)
{
    foreach (T o in collection)
        Console.WriteLine("Collection contains {0}",
            o.ToString());
}
```

```csharp
public static void PrintCollection(
    System.Collections.IEnumerable collection)
{
    foreach (object o in collection)
        Console.WriteLine("Collection contains {0}",
            o.ToString());
}
```

```csharp
public static void PrintCollection(
    WeatherDataStream collection)
{
    foreach (object o in collection)
        Console.WriteLine("Collection contains {0}",
            o.ToString());
}
```

The first method is most reusable. Any type that supports IEnumerable<T> can use that method. In addition to WeatherDataStream, you can use List<T>, SortedList<T>, any Array, and the results of any LINQ query. The second method will also work with many types, but uses the less preferable nongeneric IEnumerable. The final method is far less reusable. It cannot be used with Arrays, ArrayLists, DataTables, Hashtables, ImageLists, or many other collection classes. Coding the method using interfaces as its parameter types is far more generic and far easier to reuse.

Using interfaces to define the APIs for a class also provides greater flexibility. The WeatherDataStream class could implement a method that returned a collection of WeatherData objects. That would look something like this:

```csharp
public List<WeatherData> DataSequence
{
    get { return sequence; }
}

private List<WeatherData> sequence = new List<WeatherData>();
```

That leaves you vulnerable to future problems. At some point, you might change from using a List<WeatherData> to exposing an array, a SortedList<T>. Any of those changes will break the code. Sure, you can change the parameter type, but that's changing the public interface to your class. Changing the public interface to a class causes you to make many more changes to a large system; you would need to change all the locations where the public property was accessed.

The second problem is more immediate and more troubling: The List<T> class provides numerous methods to change the data it contains. Users of your class could delete, modify, or even replace every object in the sequence. That's almost certainly not your intent. Luckily, you can limit the capabilities of the users of your class. Instead of returning a reference to some internal object, you should return the interface you intend clients to use. That would mean returning an IEnumerable<WeatherData>.

When your type exposes properties as class types, it exposes the entire interface to that class. Using interfaces, you can choose to expose only the methods and properties you want clients to use. The class used to implement the interface is an implementation detail that can change over time (see Item 26).

Furthermore, unrelated types can implement the same interface. Suppose you're building an application that manages employees, customers, and vendors. Those are unrelated, at least in terms of the class hierarchy. But they share some common functionality. They all have names, and you will likely display those names in controls in your applications.
