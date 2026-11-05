```
DayOfWeek friday = (DayOfWeek)Enum.Parse(typeof(DayOfWeek), "Friday"); // DayOfWeek.Friday

DayOfWeek caturday = (DayOfWeek)Enum.Parse(typeof(DayOfWeek), "Caturady"); // Thows ArgumentException

// All names of an enum type as strings
string[] weekdays = Enum.GetNames(typeof(DayOfWeek));
```

# Section 22.7: Enums can have unexpected values

Since an enum can be cast to and from its underlying integral type, the value may fall outside the range of values given in the definition of the enum type.

Although the below enum type DaysOfWeek only has 7 defined values, it can still hold any int value.

```
```csharp
public enum DaysOfWeek
{
    Monday = 1,
    Tuesday = 2,
    Wednesday = 3,
    Thursday = 4,
    Friday = 5,
    Saturday = 6,
    Sunday = 7
}
```
```

```
```csharp
DaysOfWeek d = (DaysOfWeek)31;
Console.WriteLine(d); // prints 31

DaysOfWeek s = DaysOfWeek.Sunday;
s++; // No error
```
```

There is currently no way to define an enum which does not have this behavior.

However, undefined enum values can be detected by using the method Enum.IsDefined. For example,

```
```csharp
DaysOfWeek d = (DaysOfWeek)31;
Console.WriteLine(Enum.IsDefined(typeof(DaysOfWeek),d)); // prints False
```
```

# Section 22.8: Default value for enum == ZERO

The default value for an enum is zero. If an enum does not define an item with a value of zero, its default value will be zero.

```
```csharp
public class Program
{
    enum EnumExample
    {
        one = 1,
        two = 2
    }

    public void Main()
    {
        var e = default(EnumExample);

        if (e == EnumExample.one)
            Console.WriteLine("defaults to one");
    }
}
```
```