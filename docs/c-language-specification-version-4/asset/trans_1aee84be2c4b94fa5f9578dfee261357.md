

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

- 字段由其完全限定名表示：

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
        private Widget[] array2;
        private unsafe int *pCount;
        private unsafe float **ppValues;
    }
}
```

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
```

- 构造函数。

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

```
"M:Acme.Widget.#ctor"
"M:Acme.Widget.#ctor"
"M:Acme.Widget.#ctor(System.String)"
```

- 析构函数。

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

- 方法。

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
        public static void M0() {...}
        public void M1(char c, out float f, ref ValueType v) {...}
        public void M2(short[] x1, int[,] x2, long[][,] x3) {...}
        public void M3(long[][] x3, Widget[][,] x4) {...}
        public unsafe void M4(char *pc, Color **pf) {...}
        public unsafe void M5(void *pv, double *[,] pd) {...}
        public void M6(int i, params object[] args) {...}
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
}
```

```
"M:Acme.ValueType.M(System.Int32)"
"M:Acme.Widget.NestedClass.M(System.Int32)"
"M:Acme.Widget.M0()"
"M:Acme.Widget.M1(System.Char,System.Single@,Acme.ValueType@)"
"M:Acme.Widget.M2(System.Int16[],System.Int32[0:,0:],System.Int64[][])"
"M:Acme.Widget.M3(System.Int64[][],Acme.Widget[0:,0:,0:])"
"M:Acme.Widget.M4(System.Char*,Color**)"
"M:Acme.Widget.M5(System.Void*,System.Double*[0:,0:])"
"M:Acme.Widget.M6(System.Int32,System.Object[])"
"M:Acme.MyList`1.Test(`0)"
"M:Acme.UseList.Process(Acme.MyList<System.Int32>)"
"M:Acme.UseList.GetValues`1(`0)"
```

- 属性和索引器。

```
namespace Acme
{
    class Widget: IProcess
    {
        public int width { get {...} set {...} }
        public int this[int i] { get {...} set {...} }
        public int this[string s, int i] { get {...} set {...} }
    }
}
```

```
"P:Acme.Widget.Width"
"P:Acme.Widget.Item(System.Int32)"
"P:Acme.Widget.Item(System.String,System.Int32)"
```

- 事件。

```
namespace Acme
{
    class Widget: IProcess
    {
        public event Del AnEvent;
    }
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

所使用的一元运算符函数名的完整集合如下：op_UnaryPlus、op_UnaryNegation、op_LogicalNot、op_OnesComplement、op_Increment、op_Decrement、op_True 和 op_False。

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

所使用的二元运算符函数名的完整集合如下：op_Addition、op_Subtraction、op_Multiply、op_Division、op_Modulus、op_BitwiseAnd、op_BitwiseOr、op_ExclusiveOr、op_LeftShift、op_RightShift、op_Equality、op_Inequality、op_LessThan、op_LessThanOrEqual、op_GreaterThan 和 op_GreaterThanOrEqual。

- 转换运算符带有一个尾随的 "~"，后跟返回类型。

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
"M:Acme.Widget.op_Explicit(Acme.Widget)~System.Int32"
"M:Acme.Widget.op_Implicit(Acme.Widget)~System.Int64"

## A.4 示例

### A.4.1 C# 源代码

以下示例展示了 Point 类的源代码：

```
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
        
        /// <summary>This constructor initializes the new Point to
        /// (0,0).</summary>
        public Point() : this(0,0) {}
        
        /// <summary>This constructor initializes the new Point to
        /// <paramref name="x"/><paramref name="y"/></summary>
        /// <param><c>x</c> is the new Point's x-coordinate.</param>
        /// <param><c>y</c> is the new Point's y-coordinate.</param>
        public Point(int x, int y) {
            X = x;
            Y = y;
        }
        
        /// <summary>This method changes the point's location to
        /// the given coordinates.</summary>
        /// <param><c>x</c> is the new x-coordinate.</param>
        /// <param><c>y</c> is the new y-coordinate.</param>
        /// <see cref="Translate"/>
        public void Move(int x, int y) {
            X = x;
            Y = y;
        }
        /// <summary>This method changes the point's location by
        /// the given x- and y-offsets.
        /// <example>For example:
        /// <code>
        Point p = new Point(3,5);
        p.Translate(-1,3);
        </code>
        /// results in <c>p</c>'s having the value (2,8).
        /// </example>
        /// </summary>
        /// <param><c>x</c> is the relative x-offset.</param>
        /// <param><c>y</c> is the relative y-offset.</param>
        /// <see cref="Move"/>
        public void Translate(int x, int y) {
            X += x;
            Y += y;
        }
        /// <summary>This method determines whether two Points have the same
        /// location.</summary>
        /// <param><c>o</c> is the object to be compared to the current object.</param>
        /// <returns>True if the Points have the same location and they have
        /// the exact same type; otherwise, false.</returns>
        /// <seealso cref="operator==" />
        /// <seealso cref="operator!="/>
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
        /// <returns>A string representing a point's location, in the form (x,y),
        /// without any leading, trailing, or embedded whitespace.</returns>
        public override string ToString() {
            return "(" + X + "," + Y + ")";
        }
        
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

### A.4.2 生成的 XML

以下是某个文档生成器在获得上面所示的 Point 类的源代码后生成的输出：

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

