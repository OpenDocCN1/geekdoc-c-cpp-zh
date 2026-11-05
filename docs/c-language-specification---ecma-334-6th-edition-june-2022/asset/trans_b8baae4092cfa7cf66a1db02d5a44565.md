
- 表示泛型类型的参数在其后附加一个“,”字符，后跟类型参数的数量
- 具有 out 或 ref 修饰符的参数在其类型名称后有一个 @。按值传递或通过 params 传递的参数没有特殊标记。
- 数组参数表示为 [ lowerbound : size , ... , lowerbound : size ]，其中逗号的数量为秩减一，且每个维度的下界和大小（如果已知）以十进制表示。如果未指定下界或大小，则省略它。如果某个维度的下界和大小均被省略，则“:”也将被省略。不规则数组每个层级用一个“[]”表示。
- 具有除 void 之外的指针类型的参数使用在其类型名称后跟一个 * 表示。void 指针使用类型名为 System.Void 表示。
- 引用在类型上定义的类型参数的参数使用“~”字符后跟类型参数的从零开始的索引进行编码。
- 使用在方法中定义的类型参数的参数使用双反引号“``”代替用于类型的“~”。
- 引用已构造泛型类型的参数使用泛型类型，后跟“{”，后跟逗号分隔的类型参数列表，后跟“}”进行编码。

## D.4.3 ID 字符串示例

以下示例分别展示 C# 代码片段，以及从每个可具有文档注释的源元素生成的 ID 字符串：

类型使用其完全限定名称表示，并附加泛型信息：

```csharp
enum Color { Red, Blue, Green }

namespace Acme
{
    interface IProcess { ... }
    struct ValueType { ... }
    class Widget : IProcess
    {
        public class NestedClass { ... }
        public interface IMenuItem { ... }
        public delegate void Del(int i);
        public enum Direction { North, South, East, West }
    }
    class MyList<T>
    {
        class Helper<U,V> { ... }
    }
}
```

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
```

字段由其完全限定名称表示。

```csharp
namespace Acme
{
    struct ValueType
    {
        private int total;
    }

    class Widget : IProcess
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
        private Widget[], array2;
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

### 构造函数

```csharp
namespace Acme
{
    class Widget : IProcess
    {
        static Widget() { ... }
        public Widget() { ... }
        public Widget(string s) { ... }
    }
}
```

```
"M:Acme.Widget.#ctor"
"M:Acme.Widget.#ctor"
"M:Acme.Widget.#ctor(System.String)"
```

### 析构函数

```csharp
namespace Acme
{
    class Widget : IProcess
    {
        ~Widget() { ... }
    }
}
```

```
"M:Acme.Widget.Finalize"
```

### 方法

```csharp
namespace Acme
{
    struct ValueType
    {
        public void M(int i) { ... }
    }

    class Widget : IProcess
    {
        public class NestedClass
        {
            public void M(int i) { ... }
        }

        public static void M0() { ... }
        public void M1(char c, out float f, ref ValueType v) { ... }
        public void M2(short[] x1, int[,] x2, long[][] x3) { ... }
        public void M3(long[][] x3, Widget[, ,] x4) { ... }
        public unsafe void M4(char *pc, Color **pf) { ... }
        public unsafe void M5(void *pv, double *[,] pd) { ... }
        public void M6(int i, params object[] args) { ... }
    }

    class MyList<T>
    {
        public void Test(T t) { ... }
    }

    class UseList
    {
        public void Process(MyList<int> list) { ... }
        public MyList<T> GetValues<T>(T value) { ... }
    }
}
```

```
"M:Acme.ValueType.M(System.Int32)"
"M:Acme.Widget.NestedClass.M(System.Int32)"
"M:Acme.Widget.M0"
"M:Acme.Widget.M1(System.Char,System.Single@,Acme.ValueType@)"
"M:Acme.Widget.M2(System.Int16[],System.Int32[0:,0:],System.Int64[][])"
"M:Acme.Widget.M3(System.Int64[],[],Acme.Widget[0:,0:,0:][[]])"
"M:Acme.Widget.M4(System.Char*,Color**)"
"M:Acme.Widget.M5(System.Void*,System.Double*[0:,0:][[]])"
"M:Acme.Widget.M6(System.Int32,System.Object[])"
"M:Acme.MyList`1.Test( )"
"M:Acme.UseList.Process(Acme.MyList{System.Int32})"
"M:Acme.UseList.GetValues`1( )"
```

### 属性和索引器

```csharp
namespace Acme
{
    class Widget : IProcess
    {
        public int Width { get { ... } set { ... } }
        public int this[int i] { get { ... } set { ... } }
        public int this[string s, int i] { get { ... } set { ... } }
    }
}
```

```
"P:Acme.Widget.Width"
"P:Acme.Widget.Item(System.Int32)"
"P:Acme.Widget.Item(System.String,System.Int32)"
```

### 事件

```csharp
namespace Acme
{
    class Widget : IProcess
    {
        public event Del AnEvent;
    }
}
```

```
"E:Acme.Widget.AnEvent"
```

### 一元运算符

```csharp
namespace Acme
{
    class Widget : IProcess
    {
        public static Widget operator+(Widget x) { ... }
    }
}
```

```
"M:Acme.Widget.op_UnaryPlus(Acme.Widget)"
```

使用的一元运算符函数名称的完整集合如下：op_UnaryPlus, op_UnaryNegation, op_LogicalNot, op_OnesComplement, op_Increment, op_Decrement, op_True, and op_False.

### 二元运算符

```csharp
namespace Acme
{
    class Widget : IProcess
    {
        public static Widget operator+(Widget x1, Widget x2) { ... }
    }
}
```

```
"M:Acme.Widget.op_Addition(Acme.Widget,Acme.Widget)"
```

使用的二元运算符函数名称的完整集合如下：op_Addition, op_Subtraction, op_Multiply, op_Division, op_Modulus, op_BitwiseAnd, op_BitwiseOr, op_ExclusiveOr, op_LeftShift, op_RightShift, op_Equality, op_Inequality, op_LessThan, op_LessThanOrEqual, op_GreaterThan, and op_GreaterThanOrEqual.

转换运算符在其后带有“~”，后跟返回类型。

```csharp
namespace Acme
{
    class Widget : IProcess
    {
        public static explicit operator int(Widget x) { ... }
        public static implicit operator long(Widget x) { ... }
    }
}
```

```
"M:Acme.Widget.op_Explicit(Acme.Widget)~System.Int32"
"M:Acme.Widget.op_Implicit(Acme.Widget)~System.Int64"
```

## D.5 一个示例

### D.5.1 C# 源代码

以下示例展示了 Point 类的源代码：

```csharp
namespace Graphics
{
    /// <summary>
    /// Class <c>Point</c> models a point in a two-dimensional plane.
    /// </summary>
    public class Point
    {
        /// <summary>
        /// Instance variable <c>x</c> represents the point's x-coordinate.
        /// </summary>
        private int x;

        /// <summary>
        /// Instance variable <c>y</c> represents the point's y-coordinate.
        /// </summary>
        private int y;

        /// <value>
        /// Property <c>X</c> represents the point's x-coordinate.
        /// </value>
        public int X
        {
            get { return x; }
            set { x = value; }
        }
    }
}
```

```csharp
/// <value>
/// Property <c>Y</c> represents the point's y-coordinate.
/// </value>
public int Y
{
    get { return y; }
    set { y = value; }
}

/// <summary>
/// This constructor initializes the new Point to (0,0).
/// </summary>
public Point() : this(0, 0) {}

/// <summary>
/// This constructor initializes the new Point to
/// (<paramref name="xPosition"/>,<paramref name="yPosition"/>).
/// </summary>
/// <param><c>xPosition</c> is the new Point's x-coordinate.</param>
/// <param><c>yPosition</c> is the new Point's y-coordinate.</param>
public Point(int xPosition, int yPosition)
{
    X = xPosition;
    Y = yPosition;
}

/// <summary>
/// This method changes the point's location to
/// the given coordinates. <see cref="Translate"/>
/// </summary>
/// <param><c>xPosition</c> is the new x-coordinate.</param>
/// <param><c>yPosition</c> is the new y-coordinate.</param>
public void Move(int xPosition, int yPosition)
{
    X = xPosition;
    Y = yPosition;
}

/// <summary>
/// This method changes the point's location by
/// the given x- and y-offsets.
/// <example>For example:
/// <code>
/// Point p = new Point(3, 5);
/// p.Translate(-1, 3);
/// </code>
/// results in <c>p</c>'s having the value (2, 8).
/// </example>
/// </summary>
/// <param><c>dx</c> is the relative x-offset.</param>
/// <param><c>dy</c> is the relative y-offset.</param>
public void Translate(int dx, int dy)
{
