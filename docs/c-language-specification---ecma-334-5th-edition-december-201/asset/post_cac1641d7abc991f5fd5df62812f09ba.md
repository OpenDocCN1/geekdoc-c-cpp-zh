
<member name="M:Graphics.Point.#ctor(System.Int32,System.Int32)">
<summary>This constructor initializes the new Point to
(<paramref name="x"/>, <paramref name="y"/>).</summary>
<param><c>x</c> is the new Point's x-coordinate.</param>
<param><c>y</c> is the new Point's y-coordinate.</param>
</member>

<member name="M:Graphics.Point.Move(System.Int32,System.Int32)">
<summary>This method changes the point's location to
the given coordinates. <see cref="M:Graphics.Point.Translate(System.Int32,System.Int32)"/></summary>
<param><c>x</c> is the new x-coordinate.</param>
<param><c>y</c> is the new y-coordinate.</param>
</member>

<member name="M:Graphics.Point.Translate(System.Int32,System.Int32)">
<summary>This method changes the point's location by
the given x- and y-offsets.
<example>For example:
<code>
Point p = new Point(3,5);
p.Translate(-1,3);
</code>
results in <c>p</c>'s having the value (2,8).
</example>
<see cref="M:Graphics.Point.Move(System.Int32,System.Int32)"/></summary>
<param><c>x</c> is the relative x-offset.</param>
<param><c>y</c> is the relative y-offset.</param>
</member>

<member name="M:Graphics.Point.Equals(System.Object)">
<summary>This method determines whether two Points have the
same
location.</summary>
<param><c>obj</c> is the object to be compared to the current
object.</param>
<returns>True if the Points have the same location and they
have
the exact same type; otherwise, false.</returns>
<seealso cref="M:Graphics.Point.op_Equality(Graphics.Point,Graphics.Point)"/>
<seealso cref="M:Graphics.Point.op_Inequality(Graphics.Point,Graphics.Point)"/>
</member>

<member name="M:Graphics.Point.ToString">
<summary>Report a point's location as a string.</summary>
<returns>A string representing a point's location, in the
form
(x,y),
without any leading, trailing, or embedded
whitespace.</returns>
</member>

<member name="M:Graphics.Point.op_Equality(Graphics.Point,Graphics.Point)"><summary>This operator determines whether two Points have the same location.</summary><param><c>p1</c> is the first Point to be compared.</param><param><c>p2</c> is the second Point to be compared.</param><returns>True if the Points have the same location and they have the exact same type; otherwise, false.</returns><seealso cref="M:Graphics.Point.Equals(System.Object)"/><seealso cref="M:Graphics.Point.op_Inequality(Graphics.Point,Graphics.Point)"/></member>
<member name="M:Graphics.Point.op_Inequality(Graphics.Point,Graphics.Point)"><summary>This operator determines whether two Points have the same location.</summary><param><c>p1</c> is the first Point to be compared.</param><param><c>p2</c> is the second Point to be compared.</param><returns>True if the Points do not have the same location and the exact same type; otherwise, false.</returns><seealso cref="M:Graphics.Point.Equals(System.Object)"/><seealso cref="M:Graphics.Point.op_Equality(Graphics.Point,Graphics.Point)"/></member>
<member name="M:Graphics.Point.Main"><summary>This is the entry point of the Point class testing program.<para>This program tests each method and operator, and is intended to be run after any non-trivial maintenance has been performed on the Point class.</para></summary></member>
<member name="P:Graphics.Point.X"><value>Property <c>X</c> represents the point's x-coordinate.</value></member>
<member name="P:Graphics.Point.Y"><value>Property <c>Y</c> represents the point's y-coordinate.</value></member></members></doc>

End of informative text.
