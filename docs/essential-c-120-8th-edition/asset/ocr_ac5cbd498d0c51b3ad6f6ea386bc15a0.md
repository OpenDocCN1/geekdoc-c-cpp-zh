# LISTING 10.4: Overloading the – and + Unary Operators

```
// ...
    public static Latitude operator -(Latitude latitude)
{
        return new Latitude(-latitude.Degrees);
    }

    public static Latitude operator +(Latitude latitude)
{
        return latitude;
    }

    // ...
```

public struct Longitude
{

```
// ...
    public static Longitude operator -(Longitude longitude)
{
        return new Longitude(-longitude.Degrees);
    }

    public static Longitude operator +(Longitude longitude)
{
        return longitude;
    }

    // ...
```

public readonly struct Arc
{

```
// ...
    public static Arc operator -(Arc arc)
{
        // Uses unary – operator defined on
        // Longitude and Latitude
        return new Arc(-arc.LongitudeDifference, -arc.LatitudeDifference);
    }
```

```
public static Arc operator +(Arc arc)
{
    return arc;
```