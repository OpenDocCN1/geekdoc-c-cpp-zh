
> **注意** 正如你在所有值类型中看到的，你可以使用 `?` 修饰符创建一个枚举变量的可空版本。然后你可以将 `null` 值以及由枚举定义的值赋值给变量：

`Season? colorful = null;`

注意，你必须查看 `Season.Fall` 而不仅仅是 `Fall`。所有枚举字面量名称都受其枚举类型的范围限制，这使得不同的枚举可以包含名称相同的字面量。

此外，注意当你使用 `Console.WriteLine` 显示枚举变量时；编译器生成的代码会输出与变量值匹配的字面量名称。如果你需要需要，可以使用所有枚举自动包含的内置 `ToString` 方法，将枚举变量显式转换为表示其当前值的字符串，如下例所示：

点击此处查看代码图像

``` 
string name = colorful.ToString();

Console.WriteLine(name); // 输出 'Fall'
```

你用于整数变量的许多运算符也可以用于枚举变量（位与运算符和移位运算符除外，这些运算符在第 16 章“处理二进制数据和使用索引器”中介绍）。例如，你可以使用相等运算符 (`==`) 比较两个相同类型的枚举变量是否相等，你甚至对枚举变量进行算术运算——尽管结果并不总是有意义！

## 选择枚举字面量值

在内部，枚举类型将枚举的每个元素关联到一个整数值。默认情况下，编号从第一个元素的 0 开始，并以 1 为步长增加。可以检索枚举变量的底层整数值。要做到这一点，必须将其强制转换为其底层类型。第 8 章关于拆箱的讨论说明，强制转换类型会在转换有效且有意义时将数据从一种类型转换为另一种类型。以下代码示例输出了值 2 而不是单词 Fall（记住，在 `Season` 枚举中，`Spring` 是 0，`Summer` 是 1，`Fall` 是 2，`Winter` 是 3）：

点击此处查看代码图像

``` 
enum Season { Spring, Fall, Winter }

...

Season colorful = Season.Fall;

Console.WriteLine((int)colorful); // 输出 '2'
```

如果你愿意，可以将特定的整数常量（例如 1）与枚举字面量（例如 Spring）关联，如下例所示：

点击此处查看代码图像

``` 
enum Season { Spring = 1, Summer, Fall, Winter }
```

> **重要** 初始化枚举字面量的整数值必须是一个编译时常量值（例如 1）。

如果你不显式给枚举字面量常量整数值，编译器会给它一个比上一个枚举字面量大的值，第一个枚举字面量除外，编译器给它的默认值 0。在前面的示例中，`Spring`、`Summer`、`Fall` 和 `Winter` 的值现在是 1、 2、 3 和 4。

你允许给多个枚举字面量赋予相同的底层值。例如，在英国，秋被称为 autumn。你可以这样兼顾这两种文化：

点击此处查看代码图像

``` 
enum Season { Spring, Summer, Fall, Autumn = Fall, Winter }
```

### 选择枚举的底层类型

当你声明枚举时，枚举字面量被赋予 `int` 类型的值。你也可以选择基于不同的底层整数类型作为你的枚举的基础。例如，要声明 `Season` 的底层类型为 `short` 而不是 `int`，你可以这样写：

点击此处查看代码图像

``` 
enum Season : short { Spring, Summer, Fall, Winter }
```

使用 `short` 的主要原因是节省内存；`int` 占据的内存比 `short` 多，如果你不需要整个 int 的值范围，使用较小的数据类型是有意义的。

你可以基于八种整数类型之一创建枚举：`byte`、`sbyte`、`short`、`ushort`、`int`、`uint`、`long` 或 `ulong`。枚举字面量的值必须位于所选类型的范围内。例如，如果你将枚举基于 `byte`，你可以拥有 256 个字面量（从 0 开始）。

现在你已经学会了如何声明枚举，下一步是使用它。在下面的练习中，你将使用一个控制台应用程序来声明并使用一个表示年份的枚举。

### 创建并使用枚举

- 1. 如果 Visual Studio 2017 尚未运行，请启动它。
- 2. 打开 `StructEnums` 解决方案，它位于文档文件夹中的 `Microsoft Press\VCSABS\Chapter 9\StructEnums` 文件夹。
- 3. 在代码文本窗口中显示 `Month.cs` 文件。源文件除了声明 `StructEnums` 命名空间类和 `// TODO` 注释外是空的。
- 4. 将 `// TODO` 注释替换为 `StructEnums` 命名空间内名为 `Month` 的枚举，如下代码加粗所示。此枚举模拟了年份。`Month` 的 12 个枚举字面量从 `January` 到 `December`。
- 5. 在代码编辑器窗口中显示 `Program.cs` 文件。与之前的章节练习一样，`Main` 方法调用 `doWork` 方法并捕获发生的任何异常。
- 6. 在代码编辑器窗口中，在 `doWork` 方法中添加语句，声明一个名为 `first` 的 `Month` 类型变量并将其初始化为 `Month.January`。添加另一个语句将 `first` 变量的值写入控制台。
- 7. 在调试菜单上，点击“转调试调试”。Visual Studio 2017 构建并运行程序。确认单词 `January` 已写入控制台。
- 8. 按回车关闭程序并返回 Visual Studio 2017

编程环境。

+   9. 在 `doWork` 方法中添加两个语句，以增加第一个变量并将新值显示在控制台上，如此处**粗体**所示：

点击此处查看代码图片

``` 
static void doWork()

{

    Month first = Month.January;

    Console.WriteLine(first);

    first++;

    Console.WriteLine(first);

}
```

+   10. 在“调试”（Debug）菜单上，点击“转调试启动”（Start Without Debugging）。

 Visual Studio 2017 编译并运行程序。确认控制台中输出了 `January` 和 `February` 单词。

注意，对枚举变量进行数学运算（如递增操作）会更改变量的内部整数值。当变量被写入控制台时，将显示相应的枚举值。

+   11. 按回车键关闭程序并返回 Visual Studio 2017 编程环境。

+   12. 修改 `doWork` 方法中的第一条语句，将变量初始化为 `Month.December`，如此处**粗体**所示：

点击此处查看代码图片

``` 
static void doWork()

{

    Month first = Month.December;

    Console.WriteLine(first);

    first++;

    Console.WriteLine(first);

}
```

+   13. 在“调试”（Debug）菜单上，点击“转调试启动”。

 Visual Studio 2017 编译并运行程序。这次，控制台上输出了单词 `December`，随后是数字 12。

虽然你可以对枚举进行算术运算，但如果运算结果超出了枚举定义的数值范围，运行时所能做的只是将变量的值解释为相应的整数值。

14. 按回车键关闭程序并返回 Visual Studio 2017 编程环境。

### 使用结构体

第 8 章说明了类（`class`）定义了引用类型，引用类型始终在堆（heap）上创建。在某些情况下，类的数据非常少，以至于管理堆的开销变得不成比例。在这种情况下，将类型定义为结构体（structure）更好。结构体是一种值类型。由于结构体存储在栈上（只要结构体足够小），内存管理的开销通常降低。

与类一样，结构体可以有自己的字段、方法以及构造函数（本章稍后会讨论一个重要的例外）。

> 常见结构体类型

你可能没有意识到，但在书中之前的练习中已经使用了结构体。例如，元组（tuples）实际上是 `System.ValueTuple` 结构的示例。趣的是，在 C# 中，基本类型 `int`、`long` 和 `float` 分别是结构 `System.Int32`、`System.Int64` 和 `System.Single` 的别名。这些结构具有字段和方法，你实际上可以对这些类型的变量和字面量调用方法。例如，所有这些结构都提供了一个 `ToString` 方法，可以将数值转换为字符串表示。以下语句在 C# 中都是合法的：

点击此处查看代码图片

``` 
int i = 55;

Console.WriteLine(i.ToString());

Console.WriteLine(55.ToString());

float f = 98.765F;

Console.WriteLine(f.ToString());

Console.WriteLine(98.765F.ToString());

Console.WriteLine((500, 600).ToString()); // (500, 600) 是一个
```

你没有看到这种对 `ToString` 方法的使用，是因为 `Console.WriteLine` 方法在需要时会自动调用它。更常见的用法是使用这些结构体暴露的一些静态方法。例如，在早期的章节中，你使用了静态的 `int.Parse` 方法将字符串转换为对应的整数值。你实际上在做的是调用 `Int32` 结构的 `Parse` 方法：

点击此处查看代码图片

``` 
string s = "42";
int i = int.Parse(s); // 完全等同于 Int32.Parse
```

这些结构还包含一些静态字段。例如，`Int32.MaxValue` 是 `int` 能包含的最大值，而 `Int32.MinValue` 是你可以在 `int` 中存储的最小值。

下表显示了 C# 中的基本类型及其在 Microsoft .NET Framework 中的等效类型。注意 `string` 和 `object` 类型是类（引用类型）而不是结构体。

| 关键字 | 等效类型 | 类或结构体 |
| --- | --- | --- |
| bool | System.Boolean | 结构体 |
| byte | System.Byte | 结构体 |
| decimal | System.Decimal | 结构体 |
| double | System.Double | 结构体 |
| float | System.Single | 结构体 |
| int | System.Int32 | 结构体 |
| long | System.Int64 | 结构体 |
| object | System.Object | 类 |
| sbyte | System.SByte | 结构体 |
| short | System.Int16 | 结构体 |
| string | System.String | 类 |
| uint | System.UInt32 | 结构体 |
| ulong | System.UInt64 | 结构体 |
| ushort | System.UInt16 | 结构体 |

### 声明结构体

要声明你自己的结构体类型，你使用 `struct` 关键字，后跟类型名称，并在大括号之间包围结构体的体。在语法上，该过程与声明类相似。例如，有一个名为 `Time` 的结构体，包含三个名为 `hours`、`minutes` 和 `seconds` 的公共 `int` 字段：

点击此处查看代码图片

``` 
struct Time
{
    public int hours;
    public int minutes;
    public int seconds;
}
```

与类一样，大多数情况下不建议将字段设为公共（public）；更好的主是将字段设为私有（private），并提供构造函数来初始化它们。例如，如下例所示：

点击此处查看代码图片

```c
struct Time
{
    private int hours;
    private int minutes;
    private int seconds;

    public Time(int hh, int mm, int ss)
    {
        this.hours = hh;
        this.minutes = mm;
        this.seconds = ss;
    }

    public int Hours()
    {
        return hours;
    }
}
```

> 提示 对于主要特征是其值而非功能使用结构体。

### 理解结构体与类的区别

结构体和类在语法上相似，但它们有一些重要的区别。让我们来看一些差异：

- 你不能为结构体声明默认构造函数（无参数的构造函数）。编译器总是会生成一个。以下示例如果 `Time` 是类将可以编译，但因为 `Time` 是结构体，它无法编译：

点击此处查看代码图片

```csharp
struct Time
{
    public Time() { } // 编译错误
}
```

- 你可以通过提供非默认构造函数来初始化字段不同的值。但是，当你这样做时，你的非默认构造函数必须显式初始化结构体中的所有字段；不再进行默认初始化。如果你没有这样做，将得到编译错误。例如，虽然以下示例如果 `Time` 是类将编译并静默初始化 `seconds` 为 0，但由于 `Time` 是结构体，它编译失败：

点击此处查看代码图片

```csharp
struct Time
{
    private int hours, minutes, seconds;
    public Time(int hh, int mm)
    {
        this.hours = hh;
        this.minutes = mm;
    } // 编译错误：seconds 未初始化
}
```

- 在类中，你可以在声明处初始化实例字段。在结构体中不能这样做。以下示例如果 `Time` 是类将编译，但因为 `Time` 是结构体，它会导致编译错误：

点击此处查看代码图片

```csharp
struct Time
{
    private int hours = 0; // 编译错误
    private int minutes;
    private int seconds;
    ...
}
```

下表总结了结构体和类之间的主要区别。

类。

| 问题 | 结构体 | 类 |
|---|---|---|
| 它是值类型还是引用类型？ | 结构体是值类型。 | 类是引用类型。 |
| 实例存储在栈上还是堆上？ | 结构体实例称为值，存储在栈上。 | 类实例称为对象，存储在堆上。 |
| 你可以声明默认构造函数吗？ | 否 | 是 |
| 如果你定义了自己的构造函数，编译器仍然会生成默认构造函数吗？ | 是 | 否 |
| 如果你没有在自己的构造函数中初始化字段，编译器会自动为你初始化它吗？ | 否 | 是 |
| 是否允许在声明点处初始化实例字段？ | 否 | 是 |

类和结构体之间在继承方面还有其他差异。这些差异将在第 12 章“使用继承”中介绍。

### 声明结构体变量

在定义了结构体类型后，你可以像使用任何其他类型一样的方式使用它。例如，如果你定义了 `Time` 结构体，你可以创建 `Time` 类型的变量、字段和参数，如下例所示：

[点击此处查看代码图像](https://example.org)

``` 
struct Time
{
  private int hours, minutes, seconds;
  ..
}
class Example
{
```

``` 
private Time currentTime;
public void Method(Time parameter)
{
    Time localVariable;
    ...
}
```

> 注意：与枚举一样，你可以使用 `?` 修饰符创建结构体变量的可空版本。然后你可以将 `null` 值分配给该变量：

`Time? currentTime = null;`

### 理解结构体初始化

在本章早之前，你已经看到了如何使用构造函数初始化结构体中的字段。如果你调用构造函数，之前描述的各种规则将确保结构体中的所有字段都已初始化：

`Time now = new Time();`

下面的插图描述了该结构体中字段的状态：

| Time now = new Time(); | now.hours | 0 |
|---|---|---|
| now.minutes | 0 |
| now.seconds | 0 |

然而，由于结构体是值类型，你也可以在不调用构造函数的情况下创建结构体变量，如下例所示：

`Time now;`

此时，变量被创建了，但其字段仍处于未初始化的状态。下面的插图描述了 `now` 变量中字段的状态。

任何访问这些字段中值的尝试都会导致编译器错误：

| Time now; | now.hours | ? |
| | now.minutes | ? |
| now.seconds | ? |

注意，在这两种情况下，`now` 变量都是创建在栈上的。

如果你编写了自己的结构体构造函数，你也可以使用它来初始化结构体变量。正如在本章之前解释的那样，结构体构造函数必须始终显式初始化其所有字段。例如：

[点击此处查看代码图像](https://example.org)

``` 
struct Time
{
  private int hours, minutes, seconds;

  public Time(int hh, int mm)
{
    hours = hh;
    minutes = mm;
    seconds = 0;
  }
}
```

下面的示例通过调用用户定义的构造函数来初始化 `now`：

`Time now = new Time(12, 30);`

下面的插图显示了该示例的效果：
