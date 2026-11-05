```
/// <summary>This constructor initializes the new Point to
/// (<paramref name="xor"/>, <paramref name="yor"/>).</summary>
/// <param name="xor">is the new Point's x-coordinate.</param>
/// <param name="yor">is the new Point's y-coordinate.</param>
public Point(int xor, int yor) {
    X = xor;
    Y = yor;
}

/// <summary>This method changes the point's location to
/// the given coordinates. <see cref="Translate"/></summary>
/// <param name="xor">is the new x-coordinate.</param>
/// <param name="yor">is the new y-coordinate.</param>
public void Move(int xor, int yor) {
    X = xor;
    Y = yor;
}

/// <summary>This method changes the point's location by
/// the given x- and y-offsets.
/// <example>For example:
/// <code>
/// Point p = new Point(3,5);
/// p.Translate(-1,3);
/// </code>
/// results in <c>p</c>'s having the value (2,8).
/// <see cref="Move"/></example>
/// </summary>
/// <param name="xor">is the relative x-offset.</param>
/// <param name="yor">is the relative y-offset.</param>
public void Translate(int xor, int yor) {
    X += xor;
    Y += yor;
}

/// <summary>This method determines whether two Points have the same
/// location.</summary>
/// <param name="o">is the object to be compared to the current object.</param>
/// <returns>True if the Points have the same location and they have the exact same type; otherwise, false.</returns>
/// <seealso cref="operator==" />
/// <seealso cref="operator!=" />
public override bool Equals(object o) {
    if (o == null) {
        return false;
    }
    if (this == o) {
        return true;
    }
    if (GetType() == o.GetType()) {
        Point p = (Point)o;
        return (X == p.X) && (Y == p.Y);
    }
    return false;
}

/// <summary>Report a point's location as a string.</summary>
/// <returns>A string representing a point's location, in the form (x,y), without any leading, training, or embedded whitespace.</returns>
public override string ToString() {
    return "(" + X + "," + Y + ")";
}
```