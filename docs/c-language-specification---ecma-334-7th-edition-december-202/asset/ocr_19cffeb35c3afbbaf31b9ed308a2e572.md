```
public override bool Equals(object o)
{
    if (o == null)
    {
        return false;
    }
    if (((object)this == o)
    {
        return true;
    }
    if (GetType() == o.GetType())
    {
        Point p = (Point)o;
        return (X == p.X) && (Y == p.Y);
    }
    return false;
}

/// <summary>
/// This method returns a Point's hashcode.
/// </summary>
/// <returns>
/// The int hashcode.
/// </returns>
public override int GetHashCode()
{
    return X + (Y >> 4);    // a crude version
}

/// <summary>Report a point's location as a string.</summary>
/// <returns>
/// A string representing a point's location, in the form (x,y),
/// without any leading, training, or embedded whitespace.
/// </returns>
public override string ToString() => $"({X},{Y})";

/// <summary>
/// This operator determines whether two Points have the same location.
/// </summary>
/// <param><c>p1</c> is the first Point to be compared.</param>
/// <param><c>p2</c> is the second Point to be compared.</param>
/// <returns>
/// True if the Points have the same location and they have
/// the exact same type; otherwise, false.
/// </returns>
/// <seealso cref="Equals"/>
/// <seealso cref="operator!="/>
public static bool operator==(Point p1, Point p2)
{
    if (((object)p1 == null || (object)p2 == null)
    {
        return false;
    }
    if (p1.GetType() == p2.GetType())
    {
```