
```
class Widget: IProcess
{
    public class NestedClass {...}
    public interface IMenuItem {...}
    public delegate void Del(int i);
    public enum Direction { North, South, East, West }
}
class MyList<T>
{
    class Helper<U,V> {...}
}
```

"T:Color"
"T:Acme.IProcess"
"T:Acme.ValueType"
"T:Acme.Widget"
"T:Acme.Widget.NestedClass"
"T:Acme.Widget.IMenuItem"
"T:Acme.Widget.Del"
"T:Acme.Widget.Direction"
"T:Acme.MyList`1"
"T:Acme.MyList`1.Helper`2"

- Fields are represented by their fully qualified name:

```
namespace Acme
{
    struct ValueType
    {
        private int total;
    }
    class Widget: IProcess
    {
        public class NestedClass
        {
            private int value;
        }
        private string message;
        private static Color defaultColor;
        private const double PI = 3.14159;
        protected readonly double monthlyAverage;
        private long[] array1;
        private Widget[,] array2;
        private unsafe int *pCount;
        private unsafe float **ppValues;
    }
}
```

"F:Acme.ValueType.total"
"F:Acme.Widget.NestedClass.value"
"F:Acme.Widget.message"
"F:Acme.Widget.defaultColor"
"F:Acme.Widget.PI"
"F:Acme.Widget.monthlyAverage"
"F:Acme.Widget.array1"
"F:Acme.Widget.array2"
"F:Acme.Widget.pCount"
"F:Acme.Widget.ppValues"

## Constructors.

```
namespace Acme
{
    class Widget: IProcess
    {
        static Widget() {...}
        public Widget() {...}
        public Widget(string s) {...}
    }
}
```

"M:Acme.Widget.#ctor"
"M:Acme.Widget.#ctor"
"M:Acme.Widget.#ctor(System.String)"

## Destructors.

```
namespace Acme
{
    class Widget: IProcess
    {
        ~Widget() {...}
    }
}
```

"M:Acme.Widget.Finalize"

## Methods.

```
namespace Acme
{
    struct ValueType
    {
        public void M(int i) {...}
    }
    class Widget: IProcess
    {
        public class NestedClass
        {
            public void M(int i) {...}
        }
    }
```

## A. Documentation Comments

```
```
public static void M0() { ... }
public void M1(char c, out float f, ref ValueType v) { ... }
public void M2(short[] x1, int[,] x2, long[][] x3) { ... }
public void M3(long[][] x3, Widget[][,] x4) { ... }
public unsafe void M4(char *pc, Color **pf) { ... }
public unsafe void M5(void *pv, double *[][,] pd) { ... }
public void M6(int i, params object[] args) { ... }
}
class MyList<T>
{
    public void Test(T t) { }
}
class UseList
{
    public void Process(MyList<int> list) { }
    public MyList<T> GetValues<T>(T inputValue) { return null; }
}
"M:Acme.ValueType.M(System.Int32)"
"M:Acme.Widget.NestedClass.M(System.Int32)"
"M:Acme.Widget.M0"
"M:Acme.Widget.M1(System.Char,System.Single@,Acme.ValueType@)"
"M:Acme.Widget.M2(System.Int16[],System.Int32[0:,0:],System.Int64[][])"
"M:Acme.Widget.M3(System.Int64[][],Acme.Widget[0:,0:,0:][])"
"M:Acme.Widget.M4(System.Char*,Color**)"
"M:Acme.Widget.M5(System.Void*,System.Double*[0:,0:][])"
"M:Acme.Widget.M6(System.Int32,System.Object[])"
"M:Acme.MyList`1.Test(`0)"
"M:Acme.UseList.Process(Acme.MyList{System.Int32})"
"M:Acme.UseList.GetValues``1(`0)"
```

- Properties and indexers.

```
```
namespace Acme
{
    class Widget: IProcess
    {
        public int Width { get {...} set {...} }
        public int this[int i] { get {...} set {...} }
        public int this[string s, int i] { get {...} set {...} }
    }
}
```

"P:Acme.Widget.Width"
"P:Acme.Widget.Item(System.Int32)"
"P:Acme.Widget.Item(System.String,System.Int32)"

- Events.

```
```
namespace Acme
{
    class Widget: IProcess
    {
```
```
public event Del AnEvent;
}
}
"E:Acme.Widget.AnEvent"
```

- Unary operators.

```
namespace Acme
{
    class Widget: IProcess
    {
        public static Widget operator+(Widget x) {...}
    }
}
```

"M:Acme.Widget.op_UnaryPlus(Acme.Widget)"

The complete set of unary operator function names used is as follows: op_UnaryPlus, op_UnaryNegation, op_LogicalNot, op_OnesComplement, op_Increment, op_Decrement, op_True, and op_False.

- Binary operators.

```
namespace Acme
{
    class Widget: IProcess
    {
        public static Widget operator+(Widget x1, Widget x2) {...}
    }
}
```

"M:Acme.Widget.op_Addition(Acme.Widget,Acme.Widget)"

The complete set of binary operator function names used is as follows: op_Addition, op_Subtraction, op_Multiply, op_Division, op_Modulus, op_BitwiseAnd, op_BitwiseOr, op_ExclusiveOr, op_LeftShift, op_RightShift, op_Equality, op_Inequality, op_LessThan, op_LessThanOrEqual, op_GreaterThan, and op_GreaterThanOrEqual.

- Conversion operators have a trailing "~" followed by the return type.

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

"M:Acme.Widget.op_Explicit(Acme.Widget)->System.Int32"
"M:Acme.Widget.op_Implicit(Acme.Widget)->System.Int64"

## A.4 An Example

### A.4.1 C# Source Code

The following example shows the source code of a Point class:

```
```csharp
namespace Graphics
{
    /// <summary>Class <c>Point</c> models a point in a two-dimensional plane.
    /// </summary>
    public class Point
    {
        /// <summary>Instance variable <c>x</c> represents the point's
        /// x-coordinate.</summary>
        private int x;

        /// <summary>Instance variable <c>y</c> represents the point's
        /// y-coordinate.</summary>
        private int y;

        /// <value>Property <c>X</c> represents the point's x-coordinate.</value>
        public int X
        {
            get { return x; }
            set { x = value; }
        }

        /// <value>Property <c>Y</c> represents the point's y-coordinate.</value>
        public int Y
        {
            get { return y; }
            set { y = value; }
        }

        /// <summary>This constructor initializes the new point to
        /// (0,0).</summary>
        public Point() : this(0, 0) { }

        /// <summary>This constructor initializes the new point to
        /// (<paramref name="xor"/>,<paramref name="yor"/>).</summary>
        /// <param><c>xor</c> is the new point's x-coordinate.</param>
        /// <param><c>yor</c> is the new point's y-coordinate.</param>
        public Point(int xor, int yor)
        {
            X = xor;
            Y = yor;
        }

        /// <summary>This method changes the point's location to
        /// the given coordinates.</summary>
        /// <param><c>xor</c> is the new x-coordinate.</param>
        /// <param><c>yor</c> is the new y-coordinate.</param>
        /// <see cref="Translate"/>
        public void Move(int xor, int yor)
        {
            X = xor;
            Y = yor;
        }
    }
}
```
```

```
/// <summary>This method changes the point's location by
/// the given x- and y-offsets.
/// <example>For example:
///
/// <code>
/// Point p = new Point(3,5);
/// p.Translate(-1,3);
/// </code>
/// results in <c>p</c>'s having the value (2,8).
/// </example>
/// </summary>
/// <param><c>xor</c> is the relative x-offset.</param>
/// <param><c>yor</c> is the relative y-offset.</param>
/// <see cref="Move"/>
public void Translate(int xor, int yor)
{
    X += xor;
    Y += yor;
}
/// <summary>This method determines whether two points have the same
/// location.</summary>
/// <param><c>o</c> is the object to be compared to the current object.</param>
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
/// <summary>This method determines whether two points have the same
/// location.</summary>
/// <param><c>p1</c> is the first point to be compared.</param>
```
