```
/// <summary>This operator determines whether two Points have the same
/// location.</summary>
/// <param><c>p1</c> is the first Point to be compared.</param>
/// <param><c>p2</c> is the second Point to be compared.</param>
/// <returns>True if the Points have the same location and they have
/// the exact same type; otherwise, false.</returns>
/// <seealso cref="Equals"/>
/// <seealso cref="operator=="/>
public static bool operator==(Point p1, Point p2) {
    if ((object)p1 == null || (object)p2 == null) {
        return false;
    }

    if (p1.GetType() == p2.GetType()) {
        return (p1.X == p2.X) && (p1.Y == p2.Y);
    }

    return false;
}

/// <summary>This operator determines whether two Points have the same
/// location.</summary>
/// <param><c>p1</c> is the first Point to be compared.</param>
/// <param><c>p2</c> is the second Point to be compared.</param>
/// <returns>True if the Points do not have the same location and the
/// exact same type; otherwise, false.</returns>
/// <seealso cref="Equals"/>
/// <seealso cref="operator=="/>
public static bool operator!=(Point p1, Point p2) {
    return !(p1 == p2);
}

/// <summary>This is the entry point of the Point class testing
/// program.</summary>
/// <para>This program tests each method and operator, and
/// is intended to be run after any non-trivial maintenance has
/// been performed on the Point class.</para></summary>
public static void Main() {
    // class test code goes here
}
}
}
```

# A.4.2 Resulting XML

Here is the output produced by one documentation generator when given the source code for class Point, shown above:

```
<?xml version="1.0"?>
<doc>
    <assembly>
        <name>Point</name>
    </assembly>
    <members>
        <member name="T:Graphics.Point">
            <summary>Class <c>Point</c> models a point in a two-dimensional
            plane.</summary>
        </member>
        <member name="F:Graphics.Point.X">
            <summary>Instance variable <c>x</c> represents the point's
            x-coordinate.</summary>
        </member>
```