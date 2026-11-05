
同样，object 类型的值或接口类型的值可以转换回类类型，而无需更改引用（当然，在这种情况下需要进行运行时类型检查）。

由于结构体不是引用类型，因此对于结构体类型，这些操作的实现方式有所不同。当结构体类型的值转换为 object 类型或转换为该结构体所实现的接口类型时，会发生装箱操作。同样，当 object 类型的值或接口类型的值转换回结构体类型时，会发生拆箱操作。与对类类型执行相同操作的关键区别在于，装箱和拆箱会将结构体值复制到装箱实例中，或从装箱实例中复制出来。因此，在执行装箱或拆箱操作之后，对未装箱结构体所做的更改不会反映在装箱结构体中。

> **埃里克·利珀特** 这也是值类型应当不可变的又一个原因：如果更改是不可能的，那么对未装箱结构体所做的更改不会反映在装箱结构体中这一事实也就无关紧要了。与其处理这些意外且令人困惑的语义，不如完全避免它们。

当结构体类型重写从 System.Object 继承的虚方法（例如 Equals、GetHashCode 或 ToString()）时，通过该结构体类型的实例调用该虚方法不会导致发生装箱。即使将该结构体用作类型参数，并且通过该类型参数类型的实例进行调用，也是如此。例如：

```csharp
using System;
struct Counter
{
    int value;

    public override string ToString() {
        value++;
        return value.ToString();
    }
}
class Program
{
    static void Test<T>() where T: new() {
        T x = new T();
        Console.WriteLine(x.ToString());
        Console.WriteLine(x.ToString());
        Console.WriteLine(x.ToString());
    }

    static void Main() {
        Test<Counter>();
    }
}
```

该程序的输出为

1
2
3

尽管让 ToString 产生副作用是一种糟糕的风格，但该示例表明，对 x.ToString() 的三次调用都没有发生装箱。

同样，在访问受约束的类型参数上的成员时，绝不会隐式发生装箱。例如，假设接口 ICounter 包含一个可用于修改值的 Increment 方法。如果将 ICounter 用作约束，则调用 Increment 方法的实现时，会传递对调用 Increment 时所针对的变量的引用——绝不会传递装箱副本。

```csharp
using System;
interface ICounter
{
    void Increment();
}
struct Counter: ICounter
{
    int value;
    public override string ToString() {
        return value.ToString();
    }
    void ICounter.Increment() {
        value++;
    }
}
class Program
{
    static void Test<T>() where T: ICounter, new() {
        T x = new T();
        Console.WriteLine(x);
        x.Increment();
        // Modify x
        Console.WriteLine(x);
        ((ICounter)x).Increment();
        // Modify boxed copy of x
        Console.WriteLine(x);
    }
    static void Main() {
        Test<Counter>();
    }
}
```

第一次调用 Increment 会修改变量 x 中的值。这与第二次调用 Increment 不等价，后者修改的是 x 的装箱副本中的值。因此，该程序的输出为

```
0
1
1
```

有关装箱和拆箱的更多详细信息，请参见 §4.3。

### 11.3.6 this 的含义

在类的实例构造函数或实例函数成员中，this 被归类为值。因此，虽然 this 可用于引用调用该函数成员时所针对的实例，但在类的函数成员中不能对 this 赋值。

在结构体的实例构造函数中，this 对应于该结构体类型的 out 参数；在结构体的实例函数成员中，this 对应于该结构体类型的 ref 参数。在这两种情况下，this 都被归类为变量，并且可以通过对 this 赋值或将 this 作为 ref 或 out 参数传递，来修改调用该函数成员时所针对的整个结构体。

> > **弗拉基米尔·列舍特尼科夫** 结构体内部的匿名函数和查询表达式不能访问 this 或 this 的实例成员。

### 11.3.7 字段初始值设定项

如 §11.3.4 所述，结构体的默认值由以下结果构成：将所有值类型字段设置为其默认值，并将所有引用类型字段设置为 null。因此，结构体不允许实例字段声明包含变量初始值设定项。此限制仅适用于实例字段。结构体的静态字段允许包含变量初始值设定项。

以下示例

```csharp
struct Point
{
    public int x = 1;   // Error: initializer not permitted
    public int y = 1;   // Error: initializer not permitted
}
```

是错误的，因为实例字段声明包含变量初始值设定项。

约瑟夫·阿尔巴哈里 以下模式提供了一种变通方法，为 X 提供默认值 1：

```csharp
struct Point
{
    bool initialized;  // Default value false
    int x;
    public int X {
        get {
            if (!initialized) { x = 1; initialized = true; }
            return x;
        }
    }
}
```

埃里克·利珀特 约瑟夫的技术的一种更简洁的版本是将该标志隐藏在一个可空类型中，并使用 null 合并运算符：

```csharp
struct Point
{
    private int? x; // Default value is null
    public int X { get { return x ?? 1; } }
}
```

由于可空 int 实际上是实现为一个包含 int 和 bool 的结构体，因此这本质上相同，只是稍微更简洁一些。

### 11.3.8 构造函数

与类不同，结构体不允许声明无参数的实例构造函数。相反，每个结构体都隐式具有一个无参数的实例构造函数，该构造函数始终返回以下结果：将所有值类型字段设置为其默认值，并将所有引用类型字段设置为 null（§4.1.2）。结构体可以声明带参数的实例构造函数。例如：

```csharp
struct Point
{
    int x, y;
    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }
}
```

给定上述声明，以下语句

```
Point p1 = new Point();
Point p2 = new Point(0, 0);
```

都会创建一个 Point，其 x 和 y 均初始化为零。

结构体实例构造函数不允许包含形式为 base(...) 的构造函数初始值设定项。

如果结构体实例构造函数未指定构造函数初始值设定项，则 this 变量对应于该结构体类型的 out 参数；与 out 参数类似，在构造函数返回的每个位置，this 都必须明确赋值（§5.3）。如果结构体实例构造函数指定了构造函数初始值设定项，则 this 变量对应于该结构体类型的 ref 参数；与 ref 参数类似，this 在进入构造函数体时被视为已明确赋值。考虑下面的实例构造函数实现：

```csharp
struct Point
{
    int x, y;
    public int X {
        set { x = value; }
    }
    public int Y {
        set { y = value; }
    }
    public Point(int x, int y) {
        X = x; // Error: this is not yet definitely assigned
        Y = y; // Error: this is not yet definitely assigned
    }
}
```

在正在构造的结构体的所有字段都明确赋值之前，不能调用任何实例成员函数（包括属性 X 和 Y 的 set 访问器）。但请注意，如果 Point 是类而不是结构体，则该实例构造函数实现是允许的。

> > **埃里克·利珀特** 规范没有提到，使此方法生效的方式是直接强制调用默认构造函数，以确保字段已初始化：
> > ```csharp
> > public Point(int x, int y) : this() { // Struct is guaranteed to be initialized
> > ```
