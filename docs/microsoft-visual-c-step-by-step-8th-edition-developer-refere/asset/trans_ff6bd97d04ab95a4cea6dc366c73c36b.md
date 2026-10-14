

## 使用枚举

在声明枚举之后，你可以像使用任何其他类型一样使用它。如果你的枚举名称为 *Season*，你就可以创建类型为 *Season* 的变量、类型为 *Season* 的字段以及类型为 *Season* 的参数，如以下示例所示：

Click here to view code image

```
enum Season { Spring, Summer, Fall, Winter }

class Example
{
    public void Method(Season parameter) // method parameter example
    {
        Season localVariable; // local variable example
        ...
    }

    private Season currentSeason; // field example
}
```

在读取枚举变量的值之前，必须为其分配一个值。你只能将枚举中定义的值赋给枚举变量，如下例所示：

Click here to view code image

```
Season colorful = Season.Fall;
Console.WriteLine(colorful);  // writes out 'Fall'
```

### Note

与所有值类型一样，你可以使用 ? 修饰符为枚举变量创建一个可空版本。然后你可以将 *null* 值以及枚举中定义的值赋给该变量：

```
Season? colorful = null;
```

请注意，你必须写 *Season.Fall* 而不是仅写 *Fall*。所有枚举字面量的名称都由其枚举类型限定，这使得不同的枚举可以包含同名的字面量。

另外，请注意，当你使用 *Console.WriteLine* 显示枚举变量时，编译器会生成将变量值匹配的字面量的名称写入输出的代码。如果需要，你可以使用所有枚举自动包含的内置 *ToString* 方法显式地将枚举变量转换为表示其当前值的字符串，如以下示例所示：

Click here to view code image

```
string name = colorful.ToString();
Console.WriteLine(name);      // also writes out 'Fall'
```

你可以在整数变量上使用的许多标准运算符也可以在枚举变量上使用（除位运算符和移位运算符外，后者在第 16 章“使用索引器”中介绍）。例如，你可以使用相等运算符 (==) 比较同一类型的两个枚举变量是否相等，甚至可以对枚举变量执行算术运算——尽管结果可能并不总是合理！

## 选择枚举字面量的值

在内部，枚举类型为枚举的每个元素关联一个整数值。默认情况下，编号从第一个元素的 0 开始，以 1 的步长递增。可以检索枚举变量的底层整数值。为此，必须将其强制转换为其底层类型。第 8 章关于装箱的讨论指出，强制转换类型会在转换有效且有意义的情况下将数据从一种类型转换为另一种类型。以下代码示例写入值 2 而不是单词 Fall（请记住，在 Season 枚举中，Spring 为 0，Summer 为 1，Fall 为 2，Winter 为 3）：

Click here to view code image

```
enum Season { Spring, Summer, Fall, Winter }
...
Season colorful = Season.Fall;
Console.WriteLine((int)colorful); // writes out '2'
```

如果愿意，你也可以将特定的整数常量（例如 1）与枚举字面量（例如 Spring）关联，如以下示例所示：

Click here to view code image

```
enum Season { Spring = 1, Summer, Fall, Winter }
```

### Important

你用来初始化枚举字面量的整数值必须是编译时常量值（例如 1）。

如果你没有显式地为枚举字面量赋常量整数值，编译器会为其赋一个比前一个枚举字面量大 1 的值，除了第一个枚举字面量，编译器会为其赋默认值 0。在前面的示例中，Spring、Summer、Fall 和 Winter 的底层值现在分别为 1、2、3 和 4。

允许为多个枚举字面量赋相同的底层值。例如，在英国，fall 被称为 autumn。你可以同时兼顾两种文化，如下所示：

Click here to view code image

```
enum Season { Spring, Summer, Fall, Autumn = Fall, Winter }
```

## 选择枚举的底层类型

当你声明枚举时，枚举字面量会赋予 int 类型的值。你也可以选择基于不同的底层整数类型。例如，要声明 Season 的底层类型为 short 而不是 int，可以这样写：

Click here to view code image

```
enum Season : short { Spring, Summer, Fall, Winter }
```

使用 short 的主要原因是节省内存；int 占用的内存比 short 多，如果你不需要 int 可用的整个值范围，使用较小的数据类型是有意义的。

你可以将枚举基于以下八种整数类型中的任何一种：byte、sbyte、short、ushort、int、uint、long 或 ulong。所有枚举字面量的值必须适合所选基本类型的范围。例如，如果你将枚举基于 byte 数据类型，最多可以有 256 个字面量（从 0 开始）。

现在你已经知道如何声明枚举，下一步就是使用它。在下面的练习中，你将使用控制台应用程序来声明并使用一个表示一年中月份的枚举。

## 创建和使用枚举

- 1. 如果尚未运行，请启动 Microsoft Visual Studio 2015。
- 2. 打开 StructsAndEnums 项目，该项目位于你的 Documents 文件夹中的 \Microsoft Press\VCSBS\Chapter 9\StructsAndEnums 文件夹中。
- 3. 在代码和文本编辑器窗口中，显示 Month.cs 文件。
  源文件除了声明名为 StructsAndEnums 的命名空间和一个 // TODO: 注释外为空。
- 4. 用 StructsAndEnums 命名空间内的枚举 Month 替换 // TODO: 注释，如以下代码中以粗体显示所示。该枚举模拟一年中的月份。Month 的 12 个枚举字面量为 January 到 December。

Click here to view code image

```
namespace StructsAndEnums
{
    enum Month
    {
        January, February, March, April,
```

```
May, June, July, August,
September, October, November, December
}
}
```

- 5. 在代码和文本编辑器窗口中显示 Program.cs 文件。

与前几章的练习一样，Main 方法调用 doWork 方法并捕获发生的任何异常。

- 6. 在代码和文本编辑器窗口中，向 doWork 方法添加一条语句，声明类型为 Month 的变量 first 并将其初始化为 Month.January。再添加一条语句，将 first 变量的值写入控制台。

doWork 方法应如下所示：

Click here to view code image

```
static void doWork()
{
    Month first = Month.January;
    Console.WriteLine(first);
}
```

### Note

当你键入 Month 后的句点时，Microsoft IntelliSense 会自动显示 Month 枚举中的所有值。

- 7. 在 Debug 菜单上，单击 Start Without Debugging。

Visual Studio 2015 构建并运行程序。确认 January 已写入控制台。

- 8. 按 Enter 关闭程序并返回到 Visual Studio 2015 编程环境。

- 9. 向 doWork 方法添加另外两条语句，以递增 first 变量并显示其新值到控制台，如下以粗体所示：

Click here to view code image

```
static void doWork()
{
    Month first = Month.January;
    Console.WriteLine(first);
    first++;
    Console.WriteLine(first);
}
```

- 10. 在 Debug 菜单上，单击 Start Without Debugging。

Visual Studio 2015 构建并运行程序。确认 January 和 February 已写入控制台。

请注意，对枚举变量执行数学运算（例如递增运算）会更改变量的内部整数值。当变量写入控制台时，会显示相应的枚举值。

- 11. 按 Enter 关闭程序并返回到 Visual Studio 2015 编程环境。

- 12. 修改 doWork 方法中的第一条语句，将 first 变量初始化为 Month.December，如下以粗体所示：

Click here to view code image

```
static void doWork()
{
    Month first = Month.December;
    Console.WriteLine(first);
    first++;
    Console.WriteLine(first);
}
```

- 13. 在 Debug 菜单上，单击 Start Without Debugging。

Visual Studio 2015 构建并运行程序。这次，控制台会写入 December，然后是数字 12。

![](img/16f6e3fe08f01ddadb2741a92c392b0e_261_0.png)

虽然可以对枚举执行算术运算，但如果运算结果超出为枚举定义的值范围，运行时所能做的只是将变量的值解释为相应的整数值。

- 14. 按 Enter 关闭程序并返回到 Visual Studio 2015 编程环境。

## 使用结构

第 8 章说明了类定义引用类型，这些类型始终在堆上创建。在某些情况下，类包含的数据可能非常少，以至于管理堆的开销变得不成比例。在这些情况下，最好将类型定义为结构。结构是值类型。由于结构存储在栈上，只要结构足够小，内存管理开销通常就会减少。

与类一样，结构可以拥有自己的字段、方法和（有一个重要的例外，后面本章会讨论）构造函数。

