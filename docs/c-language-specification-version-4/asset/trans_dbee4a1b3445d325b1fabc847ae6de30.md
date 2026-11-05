
| 语句 | 示例 |
|---|---|
| `lock` 语句 | <pre><code>class Account<br>{<br>&nbsp;&nbsp;&nbsp;&nbsp;decimal balance;<br>&nbsp;&nbsp;&nbsp;&nbsp;public void withdraw(decimal amount) {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;lock (this) {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;if (amount > balance) {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;throw new Exception("Insufficient funds");<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;balance -= amount;<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}<br>&nbsp;&nbsp;&nbsp;&nbsp;}<br>}</code></pre> |
| `using` 语句 | <pre><code>static void Main() {<br>&nbsp;&nbsp;&nbsp;&nbsp;using (TextWriter w = File.CreateText("test.txt")) {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;w.WriteLine("Line one");<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;w.WriteLine("Line two");<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;w.WriteLine("Line three");<br>&nbsp;&nbsp;&nbsp;&nbsp;}<br>}</code></pre> |

## 1.6 类和对象

类是 C# 中最基本的类型。类是一种数据结构，将状态（字段）和操作（方法和其他函数成员）组合在一个单元中。类为动态创建的类实例（也称为对象）提供定义。类支持继承和多态，这些机制使派生类能够扩展和特化基类。

使用类声明创建新类。类声明以标头开始，该标头指定类的特性和修饰符、类名、基类（如果给定）以及类实现的接口。标头后面是类主体，主体由写在分隔符 `{` 和 `}` 之间的成员声明列表组成。

下面是一个名为 Point 的简单类的声明：

```csharp
public class Point
{
    public int x, y;
    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }
}
```

类的实例使用 `new` 运算符创建，该运算符为新实例分配内存、调用构造函数初始化实例，并返回对实例的引用。以下语句创建两个 `Point` 对象，并将对这些对象的引用存储在两个变量中：

```csharp
Point p1 = new Point(0, 0);
Point p2 = new Point(10, 20);
```

对象占用的内存在对象不再使用时自动回收。在 C# 中，显式释放对象既不必要也不可能。

### 1.6.1 成员

类的成员要么是静态成员，要么是实例成员。静态成员属于类，实例成员属于对象（类的实例）。

下表概述了类可以包含的成员种类。

| 成员 | 说明 |
|---|---|
| 常量 | 与类关联的常量值 |
| 字段 | 类的变量 |
| 方法 | 类可执行的计算和操作 |
| 属性 | 与读写类的命名属性相关的操作 |
| 索引器 | 与像数组一样索引类实例相关的操作 |
| 事件 | 类可以生成的通知 |
| 运算符 | 类支持的转换和表达式运算符 |
| 构造函数 | 初始化类实例或类本身所需的操作 |
| 析构函数 | 在永久丢弃类实例之前执行的操作 |
| 类型 | 类声明的嵌套类型 |

### 1.6.2 可访问性

类的每个成员都有关联的可访问性，它控制能够访问该成员的程序文本区域。可访问性有五种可能的形式。下表对此进行了总结。

| 可访问性 | 含义 |
|---|---|
| public | 访问不受限制 |
| protected | 访问限于此类或从此类派生的类 |
| internal | 访问限于此程序 |
| protected internal | 访问限于此程序或从此类派生的类 |
| private | 访问限于此类 |

### 1.6.3 类型参数

类定义可以通过在类名后面加上包含类型参数名称列表的尖括号来指定一组类型参数。然后可以在类声明的主体中使用类型参数来定义类的成员。在下面的示例中，`Pair` 的类型参数是 `TFirst` 和 `TSecond`：

```csharp
public class Pair<TFirst,TSecond>
{
    public TFirst First;
    public TSecond Second;
}
```

声明为接受类型参数的类类型称为泛型类类型。结构、接口和委托类型也可以是泛型。

使用泛型类时，必须为每个类型参数提供类型实参：

```csharp
Pair<int,string> pair = new Pair<int,string> { First = 1, Second = "two" };
int i = pair.First; // TFirst is int
string s = pair.Second; // TSecond is string
```

提供了类型实参的泛型类型（如上面的 `Pair<int,string>`）称为构造类型。

### 1.6.4 基类

类声明可以通过在类名和类型参数后面加上冒号和基类名称来指定基类。省略基类规范等同于从 `object` 类型派生。在下面的示例中，`Point3D` 的基类是 `Point`，而 `Point` 的基类是 `object`：

```csharp
public class Point
{
    public int x, y;
    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }
}
public class Point3D: Point
{
    public int z;
    public Point3D(int x, int y, int z): base(x, y) {
        this.z = z;
    }
}
```

类继承其基类的成员。继承意味着类隐式包含其基类的所有成员，但基类的实例构造函数、静态构造函数和析构函数除外。派生类可以向其继承的成员添加新成员，但不能移除继承成员的定义。在前面的示例中，`Point3D` 从 `Point` 继承了 `x` 和 `y` 字段，每个 `Point3D` 实例都包含三个字段：`x`、`y` 和 `z`。

存在从类类型到其任何基类类型的隐式转换。因此，类类型的变量可以引用该类的实例或任何派生类的实例。例如，对于前面的类声明，`Point` 类型的变量可以引用 `Point` 或 `Point3D`：

```csharp
Point a = new Point(10, 20);
Point b = new Point3D(10, 20, 30);
```

### 1.6.5 字段

字段是与类或类实例关联的变量。

使用 `static` 修饰符声明的字段定义静态字段。静态字段标识一个存储位置。无论创建多少个类实例，静态字段始终只有一个副本。

未使用 `static` 修饰符声明的字段定义实例字段。类的每个实例都包含该类所有实例字段的单独副本。

在下面的示例中，`Color` 类的每个实例都有 `r`、`g` 和 `b` 实例字段的单独副本，但 `Black`、`White`、`Red`、`Green` 和 `Blue` 静态字段只有一个副本：

```csharp
public class Color
{
    public static readonly Color Black = new Color(0, 0, 0);
    public static readonly Color White = new Color(255, 255, 255);
    public static readonly Color Red = new Color(255, 0, 0);
    public static readonly Color Green = new Color(0, 255, 0);
    public static readonly Color Blue = new Color(0, 0, 255);
    private byte r, g, b;

    public Color(byte r, byte g, byte b) {
        this.r = r;
        this.g = g;
        this.b = b;
    }
}
```

如前面的示例所示，可以使用 `readonly` 修饰符声明只读字段。对 `readonly` 字段的赋值只能作为字段声明的一部分，或在同一类的构造函数中进行。

### 1.6.6 方法

方法是实现对象或类可以执行的计算或操作的成员。静态方法通过类访问。实例方法通过类的实例访问。

方法有一个（可能为空的）参数列表，表示传递给该方法的值或变量引用，以及一个返回类型，指定该方法计算并返回的值的类型。如果方法不返回值，则其返回类型为 `void`。

与类型一样，方法也可以有一组类型参数，调用方法时必须为其指定类型实参。与类型不同，类型实参通常可以从方法调用的实参推断出来，无需显式给出。

方法的签名在声明该方法的类中必须是唯一的。方法的签名由方法名称、类型参数数量以及参数的数量、修饰符和类型组成。方法的签名不包括返回类型。

#### 1.6.6.1 参数

参数用于向方法传递值或变量引用。方法的参数从调用方法时指定的实参中获取实际值。参数有四种：值参数、引用参数、输出参数和参数数组。

值参数用于输入参数传递。值参数对应于一个局部变量，其初始值来自为该参数传递的实参。对值参数的修改不影响为该参数传递的实参。

值参数可以是可选的，通过指定默认值，以便可以省略相应的实参。

引用参数同时用于输入和输出参数传递。为引用参数传递的实参必须是变量，在方法执行期间，引用参数表示与实参变量相同的存储位置。引用参数使用 `ref` 修饰符声明。下面的示例展示了 `ref` 参数的使用。

```csharp
using System;
class Test
{
    static void Swap(ref int x, ref int y) {
        int temp = x;
        x = y;
        y = temp;
    }
    static void Main() {
        int i = 1, j = 2;
        Swap(ref i, ref j);
        Console.WriteLine("{0} {1}", i, j);      // Outputs "2 1"
    }
}
```

