```
<member name="M:Graphics.Point.Translate(System.Int32,System.Int32)">
  <summary>
    This method changes the point's location by
    the given x- and y-offsets.
    <example>For example:
    <code>
    Point p = new Point(3,5);
    p.Translate(-1,3);
    </code>
    results in <c>p</c>'s having the value (2,8).
    </example>
    <see cref="M:Graphics.Point.Move(System.Int32,System.Int32)"/>
  </summary>
  <param><c>dx</c> is the relative x-offset.</param>
  <param><c>dy</c> is the relative y-offset.</param>
</member>
<member name="M:Graphics.Point.Equals(System.Object)">
  <summary>
    This method determines whether two Points have the same location.
  </summary>
  <param>
    <c>o</c> is the object to be compared to the current object.
  </param>
  <returns>
    True if the Points have the same location and they have
    the exact same type; otherwise, false.
  </returns>
  <seealso
    cref="M:Graphics.Point.op_Equality(Graphics.Point,Graphics.Point)" />
  <seealso
    cref="M:Graphics.Point.op_Inequality(Graphics.Point,Graphics.Point)"/>
</member>
<member name="M:Graphics.Point.ToString">
  <summary>
    Report a point's location as a string.
  </summary>
  <returns>
    A string representing a point's location, in the form (x,y),
    without any leading, training, or embedded whitespace.
  </returns>
</member>
<member name="M:Graphics.Point.op_Equality(Graphics.Point,Graphics.Point)">
  <summary>
    This operator determines whether two Points have the same location.
  </summary>
  <param><c>p1</c> is the first Point to be compared.</param>
  <param><c>p2</c> is the second Point to be compared.</param>
  <returns>
    True if the Points have the same location and they have
    the exact same type; otherwise, false.
  </returns>
  <seealso cref="M:Graphics.Point.Equals(System.Object)"/>
  <seealso
    cref="M:Graphics.Point.op_Inequality(Graphics.Point,Graphics.Point)"/>
</member>
```