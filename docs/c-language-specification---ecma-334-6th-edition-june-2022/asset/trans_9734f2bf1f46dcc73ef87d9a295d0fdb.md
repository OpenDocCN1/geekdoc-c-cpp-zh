
~~~csharp
        X += dx;
        Y += dy;
    }

    /// <summary>
    /// This method determines whether two Points have the same location.
    /// </summary>
    /// <param>
    /// <c>o</c> is the object to be compared to the current object.
    /// </param>
    /// <returns>
    /// True if the Points have the same location and they have
    /// the exact same type; otherwise, false.
    /// </returns>
    /// <seealso cref="operator=="/>
    /// <seealso cref="operator!="/>
    public override bool Equals(object o)
    {
        if (o == null)
        {
            return false;
        }
        if (this == o)
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

    /// <summary>Report a point's location as a string.</summary>
    /// <returns>
    /// A string representing a point's location, in the form (x,y),
    /// without any leading, trailing, or embedded whitespace.
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
        if ((object)p1 == null || (object)p2 == null)
{
    return false;
}
if (p1.GetType() == p2.GetType())
{
    return (p1.X == p2.X) && (p1.Y == p2.Y);
}
return false;
}

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
~~~
## D.5.2 结果 XML

以下是当给定上述 Point 类的源代码时，由某个文档生成器产生的输出：

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
        <member name="F:Graphics.Point.x">
            <summary>
                Instance variable <c>x</c> represents the point's x-coordinate.
            </summary>
        </member>
        <member name="F:Graphics.Point.y">
            <summary>
                Instance variable <c>y</c> represents the point's y-coordinate.
            </summary>
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
        <c>obj</c> is the object to be compared to the current object.
    </param>
    <returns>
        True if the Points have the same location and they have
        the exact same type; otherwise, false.
    </returns>
    <seealso
        cref="M:Graphics.Point.op_Equality(Graphics.Point,Graphics.Point)"/>
    <seealso
        cref="M:Graphics.Point.op_Inequality(Graphics.Point,Graphics.Point)"/>
</member>
<member name="M:Graphics.Point.ToString">
    <summary>
        Report a point's location as a string.
    </summary>
    <returns>
A string representing a point's location, in the form (x,y),
without any leading, trailing, or embedded whitespace.
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
<member
name="M:Graphics.Point.op_Inequality(Graphics.Point,Graphics.Point)">
<summary>
    This operator determines whether two Points have the same location.
</summary>
<param><c>p1</c> is the first Point to be compared.</param>
<param><c>p2</c> is the second Point to be compared.</param>
<returns>
    True if the Points do not have the same location and the
exact same type; otherwise, false.
</returns>
<seealso cref="M:Graphics.Point.Equals(System.Object)"/>
<seealso
cref="M:Graphics.Point.op_Equality(Graphics.Point,Graphics.Point)"/>
</member>
<member name="M:Graphics.Point.Main">
<summary>
    This is the entry point of the Point class testing program.
<para>
    This program tests each method and operator, and
    is intended to be run after any non-trivial maintenance has
    been performed on the Point class.
</para>
</summary>
</member>
<member name="P:Graphics.Point.X">
<value>
    Property <c>X</c> represents the point's x-coordinate.
</value>
</member>
<member name="P:Graphics.Point.Y">
<value>
    Property <c>Y</c> represents the point's y-coordinate.
</value>
</member>
</members>
</doc>
```

## 参考性文本结束。

## E. 参考文献

**本附录为参考性内容。**

ANSI X3.274-1996, *编程语言 REXX.* (本文档有助于理解浮点十进制算术规则。)

ISO/IEC 9075-1, *信息技术 — 数据库语言 — SQL — 第1部分：框架* (*SQL/Framework*)

ISO/IEC 9899, *编程语言 — C.*

ISO/IEC 14882 *编程语言 — C++.*

ISO 80000-1, *量和单位 — 第1部分：总则.* (本文档定义了“银行家舍入”。)

**参考性文本结束。**
