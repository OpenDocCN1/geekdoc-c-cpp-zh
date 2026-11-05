
对包含*对象初始值设定项*或*集合初始值设定项*的*对象创建表达式*的处理，包括先处理实例构造函数，然后处理由*对象初始值设定项*（§7.6.10.2）或*集合初始值设定项*（§7.6.10.3）指定的成员初始化或元素初始化。

如果可选*实参列表*中的任何实参具有编译时类型 *dynamic*，则该*对象创建表达式*是动态绑定的（§7.2.2），并且在运行时使用*实参列表*中那些具有编译时类型 *dynamic* 的实参的运行时类型来应用以下规则。但是，对象创建会经历有限的编译时检查，如 §7.5.4 所述。

对形式为 `new T(A)` 的*对象创建表达式*的绑定时间处理，其中 *T* 是*类类型*或*值类型*，*A* 是可选*实参列表*，包括以下步骤：

- 如果 *T* 是*值类型*且 *A* 不存在：

  该*对象创建表达式*是默认构造函数调用。该*对象创建表达式*的结果是类型 *T* 的值——即 §4.1.1 中定义的 *T* 的默认值。

- 否则，如果 *T* 是*类型参数*且 *A* 不存在：

  如果没有为 *T* 指定值类型约束或构造函数约束（§10.1.5），则发生绑定时间错误。

  该*对象创建表达式*的结果是类型参数所绑定到的运行时类型的值——即调用该类型的默认构造函数的结果。运行时类型可以是引用类型或值类型。

- 否则，如果 *T* 是*类类型*或*结构类型*：
  - 如果 *T* 是抽象*类类型*，则发生编译时错误。
  - 要调用的实例构造函数使用 §7.5.3 的重载决策规则确定。候选实例构造函数集由 *T* 中声明的、相对于 *A* 适用的所有可访问实例构造函数组成（§7.5.3.1）。如果候选实例构造函数集为空，或无法标识单个最佳实例构造函数，则发生绑定时间错误。
  - 该*对象创建表达式*的结果是类型 *T* 的值——即通过调用上一步确定的实例构造函数而生成的值。

- 否则，该*对象创建表达式*无效，并发生绑定时间错误。

即使该*对象创建表达式*是动态绑定的，其编译时类型仍然是 *T*。

对形式为 `new T(A)` 的*对象创建表达式*的运行时处理，其中 *T* 是*类类型*或*结构类型*，*A* 是可选*实参列表*，包括以下步骤：

- 如果 *T* 是*类类型*：
  - 分配类 *T* 的新实例。如果没有足够内存可用于分配新实例，则引发 `System.OutOfMemoryException`，并且不执行后续步骤。
  - 新实例的所有字段都初始化为其默认值（§5.2）。
  - 根据函数成员调用规则（§7.5.4）调用实例构造函数。对新分配实例的引用会自动传递给实例构造函数，并且可以在该构造函数内以 `this` 访问该实例。

- 如果 *T* 是*结构类型*：
  - 通过分配临时局部变量创建类型 *T* 的实例。由于*结构类型*的实例构造函数必须为所创建实例的每个字段明确赋值，因此无需初始化临时变量。
  - 根据函数成员调用规则（§7.5.4）调用实例构造函数。对新分配实例的引用会自动传递给实例构造函数，并且可以在该构造函数内以 `this` 访问该实例。

### 7.6.10.2 对象初始值设定项

对象初始值设定项为对象的零个或多个字段或属性指定值。

```
object-initializer:
  { }
  { member-initializer-list }
  { member-initializer-list , }

member-initializer-list:
  member-initializer
  member-initializer-list , member-initializer

member-initializer:
  identifier = initializer-value

initializer-value:
  expression
  object-or-collection-initializer
```

对象初始值设定项由一系列成员初始值设定项组成，这些成员初始值设定项括在 `{` 和 `}` 标记中并用逗号分隔。每个成员初始值设定项必须命名正在初始化的对象的一个可访问字段或属性，后跟一个等号以及一个表达式、对象初始值设定项或集合初始值设定项。对象初始值设定项为同一字段或属性包含多个成员初始值设定项是错误的。对象初始值设定项不可能引用它正在初始化的新创建对象。

在等号后指定表达式的成员初始值设定项，其处理方式与对字段或属性的赋值（§7.17.1）相同。

在等号后指定对象初始值设定项的成员初始值设定项是*嵌套对象初始值设定项*——即嵌入对象的初始化。嵌套对象初始值设定项中的赋值不会向字段或属性赋新值，而是被视为对字段或属性的成员进行赋值。嵌套对象初始值设定项不能应用于具有值类型的属性，也不能应用于具有值类型的只读字段。

在等号后指定集合初始值设定项的成员初始值设定项是嵌入集合的初始化。该初始值设定项不会向字段或属性分配新集合，而是将初始值设定项中给定的元素添加到该字段或属性引用的集合中。该字段或属性必须是满足 §7.6.10.3 中指定要求的集合类型。

以下类表示具有两个坐标的点：

```csharp
public class Point
{
    int x, y;

    public int X { get { return x; } set { x = value; } }
    public int Y { get { return y; } set { y = value; } }
}
```

可以按如下方式创建并初始化 Point 的实例：

```csharp
Point a = new Point { X = 0, Y = 1 };
```

其效果与以下代码相同：

```csharp
Point __a = new Point();
__a.X = 0;
__a.Y = 1;
Point a = __a;
```

其中 `__a` 是一个在其他情况下不可见且不可访问的临时变量。以下类表示由两个点创建的矩形：

```csharp
public class Rectangle
{
    Point p1, p2;

    public Point P1 { get { return p1; } set { p1 = value; } }
    public Point P2 { get { return p2; } set { p2 = value; } }
}
```

可以按如下方式创建并初始化 Rectangle 的实例：

```csharp
Rectangle r = new Rectangle {
    P1 = new Point { X = 0, Y = 1 },
    P2 = new Point { X = 2, Y = 3 }
};
```

其效果与以下代码相同：

```csharp
Rectangle __r = new Rectangle();
Point __p1 = new Point();
__p1.X = 0;
__p1.Y = 1;
__r.P1 = __p1;
Point __p2 = new Point();
__p2.X = 2;
__p2.Y = 3;
__r.P2 = __p2;
Rectangle r = __r;
```

其中 `__r`、`__p1` 和 `__p2` 是在其他情况下不可见且不可访问的临时变量。

> JOSEPH ALBAHARI  使用隐藏的临时变量可以消除在初始化期间引发异常时最终得到部分初始化对象的可能性。相反，新构造的对象会被完全放弃：

```csharp
Point p = null;
int zero = 0;
try { p = new Point { X = 3, Y = 4 / zero }; } // Throws DivideByZeroException
catch { Console.WriteLine(p == null); } // True
```

> ERIC LIPPERT  使用隐藏的临时变量还清楚地说明了明确赋值规则是什么。这里的第二行与第一行并不等效：

```csharp
Point p1 = new Point(); p1.Y = p1.X; // Legal
Point p2 = new Point() { Y = p2.X }; // Not legal; p2 is not assigned yet
```

如果 Rectangle 的构造函数分配两个嵌入的 Point 实例：

```csharp
public class Rectangle
{
    Point p1 = new Point();
    Point p2 = new Point();
    public Point P1 { get { return p1; } }
    public Point P2 { get { return p2; } }
}
```
