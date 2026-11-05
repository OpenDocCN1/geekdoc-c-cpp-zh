```
return (p1.X == p2.X) && (p1.Y == p2.Y);
}
    return false;
}
```

```
/// <summary>
/// This operator determines whether two Points have the same location.
/// </summary>
/// <param><c>p1</c> is the first Point to be compared.</param>
/// <param><c>p2</c> is the second Point to be compared.</param>
/// <returns>
/// True if the Points do not have the same location and the
/// exact same type; otherwise, false.
/// </returns>
/// <seealso cref="Equals"/>
/// <seealso cref="operator=="/>
public static bool operator!=(Point p1, Point p2) => !(p1 == p2);
}
```

# D.5.2 Resulting XML

Here is the output produced by one documentation generator when given the source code for class Point, shown above:

```
<?xml version="1.0"?>
<doc>
  <assembly>
    <name>Point</name>
  </assembly>
  <members>
    <member name="T:Graphics.Point">
      <summary>Class <c>Point</c> models a point in a two-dimensional plane.</summary>
    </member>
    <member name="M:Graphics.Point.#ctor">
      <summary>This constructor initializes the new Point to (0, 0).</summary>
    </member>
    <member name="M:Graphics.Point.#ctor(System.Int32,System.Int32)">
      <summary>
        This constructor initializes the new Point to
        (<paramref name="xPosition"/>,<paramref name="yPosition"/>).
      </summary>
      <param><c>xPosition</c> is the new Point's x-coordinate.</param>
      <param><c>yPosition</c> is the new Point's y-coordinate.</param>
    </member>
    <member name="M:Graphics.Point.Move(System.Int32,System.Int32)">
      <summary>
        This method changes the point's location to
        the given coordinates.
        <see cref="M:Graphics.Point.Translate(System.Int32,System.Int32)"/>
      </summary>
      <param><c>xPosition</c> is the new x-coordinate.</param>
      <param><c>yPosition</c> is the new y-coordinate.</param>
    </member>
```