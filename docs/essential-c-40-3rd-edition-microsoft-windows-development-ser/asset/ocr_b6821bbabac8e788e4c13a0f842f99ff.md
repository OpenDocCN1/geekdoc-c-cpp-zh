them are virtual. This section discusses the details concerning overloading the virtual methods.

# Overriding ToString()

By default, calling ToString() on any object will return the fully qualified name of the class. Calling ToString() on a System.IO.FileStream object will return the string System.IO.FileStream for example. For some classes, however, ToString() can be more meaningful. On string, for example, ToString() returns the string value itself. Similarly, returning a Contact's name would make more sense. Listing 9.1 overrides ToString() to return a string representation of Coordinate.

# Listing 9.1: Overriding ToString()

```
public struct Coordinate
{
    public Coordinate(Longitude longitude, Latitude latitude)
    {
        _Longitude = longitude;
        _Latitude = latitude;
    }

    public Longitude Longitude { get { return _Longitude; } }
    private readonly Longitude _longitude;

    public Latitude Latitude { get { return _Latitude; } }
    private readonly Latitude _latitude;

    public override string ToString()
    {
        return string.Format("{0} {1}", Longitude, Latitude);
    }
    // ...
```

Write methods such as Console.WriteLine() call an object's ToString() method, so overloading it often outputs more meaningful information than the default implementation.

# Overriding GetHashCode()

Overriding GetHashCode() is more complex than overriding ToString(). Regardless, you should override GetHashCode() when you are overriding Equals(), and there is a compiler warning to indicate this. Overriding