

```
    public event Del AnEvent;
}
```

```
"E:Acme.Widget.AnEvent"
```

- 一元运算符。

```
namespace Acme
{
    class Widget: IProcess
    {
        public static Widget operator+(Widget x) {...}
    }
}
```

```
"M:Acme.Widget.op_UnaryPlus(Acme.Widget)"
```

所使用的完整一元运算符函数名集合如下：op_UnaryPlus、op_UnaryNegation、op_LogicalNot、op_OnesComplement、op_Increment、op_Decrement、op_True 和 op_False。

- 二元运算符。

```
namespace Acme
{
    class Widget: IProcess
    {
        public static Widget operator+(Widget x1, Widget x2) {...}
    }
}
```

```
"M:Acme.Widget.op_Addition(Acme.Widget,Acme.Widget)"
```

所使用的完整二元运算符函数名集合如下：op_Addition、op_Subtraction、op_Multiply、op_Division、op_Modulus、op_BitwiseAnd、op_BitwiseOr、op_ExclusiveOr、op_LeftShift、op_RightShift、op_Equality、op_Inequality、op_LessThan、op_LessThanOrEqual、op_GreaterThan 和 op_GreaterThanOrEqual。

- 转换运算符带有尾随的 "~"，后跟返回类型。

```
namespace Acme
{
    class Widget: IProcess
    {
        public static explicit operator int(Widget x) {...}
        public static implicit operator long(Widget x) {...}
    }
}
```

```
"M:Acme.Widget.op_Explicit(Acme.Widget)->System.Int32"
"M:Acme.Widget.op_Implicit(Acme.Widget)->System.Int64"
```

## A.4 示例

### A.4.1 C# 源代码

以下示例展示了 Point 类的源代码：

```
```csharp
namespace Graphics
{
    /// <summary>Class <<Point>> models a point in a two-dimensional plane.
    /// </summary>
    public class Point
    {
        /// <summary>Instance variable <<x>> represents the point's
        /// x-coordinate.</summary>
        private int x;
        /// <summary>Instance variable <<y>> represents the point's
        /// y-coordinate.</summary>
        private int y;
        /// <value>Property <<X>> represents the point's x-coordinate.</value>
        public int X
        {
            get { return x; }
            set { x = value; }
        }
        /// <value>Property <<Y>> represents the point's y-coordinate.</value>
        public int Y
        {
            get { return y; }
            set { y = value; }
        }
        /// <summary>This constructor initializes the new point to
        /// (0,0).</summary>
        public Point() : this(0, 0) { }
        /// <summary>This constructor initializes the new point to
        /// <paramref name="x0"/><paramref name="y0"/>.</summary>
        /// <param name="x0"><c>x0</c> is the new point's x-coordinate.</param>
        /// <param name="y0"><c>y0</c> is the new point's y-coordinate.</param>
        public Point(int x0, int y0)
        {
            X = x0;
            Y = y0;
        }
        /// <summary>This method changes the point's location to
        /// the given coordinates.</summary>
        /// <param name="x0"><c>x0</c> is the new x-coordinate.</param>
        /// <param name="y0"><c>y0</c> is the new y-coordinate.</param>
        /// <see cref="Translate"/>
        public void Move(int x0, int y0)
        {
            X = x0;
            Y = y0;
        }
    }
}
```
```

```
/// <summary>This method changes the point's location by
/// the given x- and y-offsets.
/// <example>For example:
/// <code>
/// Point p = new Point(3,5);
/// p.Translate(-1,3);
/// </code>
/// results in <c>p</c>'s having the value (2,8).
/// </example>
/// </summary>
/// <param name="x"><c>x</c> is the relative x-offset.</param>
/// <param name="y"><c>y</c> is the relative y-offset.</param>
/// <see cref="Move"/>
public void Translate(int x, int y)
{
    X += x;
    Y += y;
}
/// <summary>This method determines whether two points have the same
/// location.</summary>
/// <param name="o"><c>o</c> is the object to be compared to the current object.</param>
/// <returns>True if the points have the same location and they have
/// the exact same type; otherwise, false.</returns>
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
/// <returns>A string representing a point's location, in the form (x,y),
/// without any leading, trailing, or embedded whitespace.</returns>
public override string ToString()
{
    return "(" + X + "," + Y + ")";
}
/// <summary>This operator determines whether two points have the same
/// location.</summary>
/// <param name="p1"><c>p1</c> is the first point to be compared.</param>
```

## A. 文档注释

```
```csharp
/// <param name="p2"><c>p2</c> is the second point to be compared.</param>
/// <returns>true if the points have the same location and they have
/// the exact same type; otherwise, false.</returns>
/// <seealso cref="Equals"/>
/// <seealso cref="operator==" />
public static bool operator ==(Point p1, Point p2)
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
/// <summary>This operator determines whether two points have the same
/// location.</summary>
/// <param name="p1"><c>p1</c> is the first point to be compared.</param>
/// <param name="p2"><c>p2</c> is the second point to be compared.</param>
/// <returns>true if the points do not have the same location and the
/// exact same type; otherwise, false.</returns>
/// <seealso cref="Equals"/>
/// <seealso cref="operator==" />
public static bool operator !=(Point p1, Point p2)
{
    return !(p1 == p2);
}
/// <summary>This is the entry point of the Point class testing
/// program.</summary>
/// <para>This program tests each method and operator, and
/// is intended to be run after any nontrivial maintenance has
/// been performed on the Point class.</para></summary>
public static void Main()
{
    // Class test code goes here
}
}
```
```

### A.4.2 生成的 XML

以下是某个文档生成器在获得上面显示的 Point 类源代码后生成的输出：

```
```xml
<?xml version="1.0"?>
<doc>
    <assembly>
        <name>Point</name>
    </assembly>
```
```

```
<members>
    <member name="T:Graphics.Point">
        <summary>
        Class <<Point>> models a point in a two-dimensional
        plane.
        </summary>
    </member>
    <member name="F:Graphics.Point.x">
        <summary>
        Instance variable <<x>> represents the point's
        x-coordinate.
        </summary>
    </member>
    <member name="F:Graphics.Point.y">
        <summary>
        Instance variable <<y>> represents the point's
        y-coordinate.
        </summary>
    </member>
    <member name="M:Graphics.Point.#ctor">
        <summary>
        This constructor initializes the new point to
        (0,0).
        </summary>
    </member>
    <member name="M:Graphics.Point.#ctor(System.Int32,System.Int32)">
        <summary>
        This constructor initializes the new point to
        <paramref name="x0"/>,<paramref name="y0"/>.
        </summary>
        <param name="x0">
        <<x0>> is the new point's x-coordinate.
        </param>
        <param name="y0">
        <<y0>> is the new point's y-coordinate.
        </param>
    </member>
    <member name="M:Graphics.Point.Move(System.Int32,System.Int32)">
        <summary>
        This method changes the point's location to
        the given coordinates.
        </summary>
        <param name="x0">
        <<x0>> is the new x-coordinate.
        </param>
        <param name="y0">
        <<y0>> is the new y-coordinate.
        </param>
        <see cref="M:Graphics.Point.Translate(System.Int32,System.Int32)"/>
    </member>
</members>
```

## A. 文档注释

```
<member name="M:Graphics.Point.Translate(System.Int32,System.Int32)">
<summary>
This method changes the point's location by
the given x- and y-offsets.
<example>
For example:
<code>
Point p = new Point(3,5);
p.Translate(-1,3);
</code>
results in <c>p</c>'s having the value (2,8).
</example>
</summary>
<param name="x">
<c>x</c> is the relative x-offset.
</param>
<param name="y">
<c>y</c> is the relative y-offset.
</param>
<see cref="M:Graphics.Point.Move(System.Int32,System.Int32)"/>
</member>
<member name="M:Graphics.Point.Equals(System.Object)">
<summary>
This method determines whether two points have the same
location.
</summary>
<param name="obj">
<c>obj</c> is the object to be compared to the current object.
</param>
<returns>
True if the points have the same location and they have the exact same type; otherwise, false.
</returns>
<seealso cref="M:Graphics.Point.op_Equality(Graphics.Point,Graphics.Point)"/>
<seealso cref="M:Graphics.Point.op_Inequality(Graphics.Point,Graphics.Point)"/>
</member>
<member name="M:Graphics.Point.ToString">
<summary>Report a point's location as a string.</summary>
<returns>
A string representing a point's location, in the form (x,y),
without any leading, trailing, or embedded whitespace.
</returns>
</member>
<member name="M:Graphics.Point.op_Equality(Graphics.Point,Graphics.Point)">
<summary>
This operator determines whether two points have the same location.
</summary>
```

