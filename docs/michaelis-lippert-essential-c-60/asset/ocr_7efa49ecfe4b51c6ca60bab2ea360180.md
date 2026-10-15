```
public Latitude LatitudeDifference { get; }
}

struct Coordinate
{
    // ...
    public static Coordinate operator +(Coordinate source, Arc arc)
    {
        Coordinate result = new Coordinate(
            new Longitude(
                source.Longitude + arc.LongitudeDifference),
            new Latitude(
                source.Latitude + arc.LatitudeDifference));
        return result;
    }
}
```

The +, -, *, /, %, &, |, ^, <<, and >> operators are implemented as binary static methods where at least one parameter is of the containing type. The method name is the operator prefixed by the word operator as a keyword. As shown in Listing 9.8, given the definition of the - and + binary operators, you can add and subtract an Arc to and from the coordinate. Note that Longitude and Latitude will also require implementations of the + operator because they are called by source.Longitude + arc.LongitudeDifference and source.Latitude + arc.LatitudeDifference.

# LISTING 9.8: Calling the – and + Binary Operators

```
public class Program
{
    public static void Main()
    {
        Coordinate coordinate1,coordinate2;
        coordinate1 = new Coordinate(
            new Longitude(48, 52), new Latitude(-2, -20));
        Arc arc = new Arc(new Longitude(3), new Latitude(1));

        coordinate2 = coordinate1 + arc;
        Console.WriteLine(coordinate2);

        coordinate2 = coordinate2 - arc;
        Console.WriteLine(coordinate2);

        coordinate2 += arc;
        Console.WriteLine(coordinate2);
    }
}
```