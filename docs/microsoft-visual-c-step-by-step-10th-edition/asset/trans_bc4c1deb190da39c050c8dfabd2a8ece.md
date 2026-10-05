

```cs
}
public Circle(int initialRadius) // 重载构造函数
{
    this.radius = initialRadius; }
}
```

关于 circ2.cs 的内容，它们所示：
点击此处查看图像

```cs
partial class Circle
{
    private int radius;
    public double Area()
    {
        return Math.PI * this.radius * this.radius;
    }
}
```

当你编译一个被拆分成单独文件的类时，你必须将所有文件提供给编译器。

在接下来的练习中，你将声明一个模拟二维空间中点的类。该类将包含两个私有字段，用于存储点的 x 坐标和 y 坐标，并提供用于初始化这些字段的构造函数。你将使用 `new` 关键字并调用构造函数来创建类的实例。

## 编写构造函数并创建对象

- 1. 启动 Visual Studio 2022，如果它尚未运行。
- 2. 打开 Classes 解决方案，它位于你文档文件夹中的 \Microsoft Press\VCSABS\Chapter 7 文件夹中。
- 3. 在解决方案管理器中，双击文件 Program.cs 以在代码和文本编辑器窗口中显示它。
- 4. 在 Program 类中，找到 Main 方法。

Main 方法调用 doWork 方法，该方法被封装在一个 `try` 块中，随后紧跟一个 `catch` 处理器。通过这个 `try/catch` 块，你可以将通常放在 Main 内部的代码写在 doWork 方法中，并放心地知道它可以捕获并处理任何异常。doWork 方法目前只包含一个 `// TODO:` 注释。

点击此处查看图像

```cs
class Program
{
    static void doWork()
    {
        // TODO: 测试 Point 类:
    }
    static void Main(string[] args)
    {
        try
        {
            doWork();
        }
        catch (Exception ex)
        {
            Console.WriteLine(ex.Message);
        }
    }
}
```

> // TODO: 注释
开发者经常添加 `// TODO` 注释作为重新访问某些代码的提醒。这些注释通常包含对要执行工作的描述，例如 `// TODO: 实现 doWork 方法`。
Visual Studio 识别这种形式的注释，你可以通过“任务列表”窗口在应用程序中快速定位它们。要显示此窗口，在“视图”菜单上，选择“任务列表”。任务列表窗口默认在代码和文本编辑器窗口下方打开。所有的 TODO 注释都将列出来。然后你可以双击这些注释中的任何一个直接跳转到对应的代码，代码将显示在代码和文本编辑器窗口中。

- 5. 在代码和文本编辑器窗口中显示文件 Point.cs。

此文件定义了一个名为 Point 的类，将用它来表示二维空间中点的位置，该位置由一对 x 和 y 坐标定义。除了另一个 `// TODO:` 注释外，Point 类目前是空的。

- 6. 返回 Program.cs 文件。在 Program 类中，编辑 doWork 方法的体部，并将 `// TODO` 注释替换为以下语句：

```cs
Point origin = new Point();
```

此语句创建了 Point 类的新实例，并调用了它的默认构造函数。

- 7. 在“生成”菜单上，选择“生成解决方案”。

![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_303_0.png)

代码无错误生成，因为编译器自动为 Point 类生成了默认构造函数的代码。然而，你无法看到此构造函数的 C# 代码，因为编译器没有生成任何源语言语句。

- 返回文件 Point.cs 中的 Point 类。将 `// TODO` 注释替换为一个接受两个 `int` 参数（命名为 x 和 y）的公共构造函数，并调用 `Console.WriteLine` 方法将这些参数的值显示在控制台上，如下所示代码示例中的**粗体**部分所示：

点击此处查看图像

- 在“生成”菜单上，选择“生成解决方案”。

编译器现在报告了一个错误：

点击此处查看图像

> 没有对应于 'Point.Point(int, int)' 所需的形式参数 'x' 的参数

这个冗长信息的意思是，在 doWork 中对默认构造函数的调用是无效的，因为它不再是默认构造函数了。你为 Point 类编写了自己的构造函数，因此编译器不再生成默认构造函数。你将通过编写自己的默认构造函数来修复此。

- 编辑 Point 类，添加一个公共默认构造函数，该构造函数调用 `Console.WriteLine` 向控制台写入字符串 "Default constructor called"，如下文示例中的**粗体**所示。Point 类应该像这样所示：

点击此处查看图像

```cs
class Point
{
    public Point()
    {
        Console.WriteLine("Default constructor called");

    public Point(int x, int y)
    {
        Console.WriteLine($"x:{x}, y:{y}");
    }
}
```

- 11. 在“生成”菜单上，选择“生成解决方案”。
- 12. 在 Program.cs 文件中，编辑 doWork 方法。声明一个类型为 Point 的变量名为 bottomRight，并使用带有两个参数的构造函数将其初始化为新的 Point 对象，如下文代码中**粗体类型**的类型所示。提供值 2496 和 1664，根据 2496 × 1664 的分辨率，它们代表屏幕右下角的坐标（Surface 15英寸屏幕的分辨率）。doWork 方法现在所示：

```cs
static void doWork()
{
    var origin = new Point();
    var bottomRight = new Point(2496, 1664);
}
```

- 13. 在“调试”菜单上，选择“转调试调试”。

程序生成并运行，在控制台上显示以下内容：

Default constructor called
x:2496, y:1664

- 14. 按回车键编辑程序并返回 Visual Studio 2022。

- 15. 在 Point.cs 文件中编辑 Point 类，添加两个私有字段 x 和 y，类型为 int，如下文代码中**粗体类型**所示。Point 类现在所示：

```cs
class Point
{
    private int x, y;

    public Point()
    {
        Console.WriteLine("Default constructor called");
    }

    public Point(int x, int y)
    {
        Console.WriteLine($"x:{x}, y:{y}");
    }
}
```

- 16. 修改带有两个参数的 Point 构造函数，将 `Console.WriteLine` 语句替换为以下代码：

```cs
public Point(int x, int y)
{
    this.x = x;
    this.y = y;
}
```

- 17. 编辑默认 Point 构造函数，将 x 和 y 字段初始化为 -1，如下**粗体类型**所示。注意，虽然没有参数引起混淆（Visual Studio 会弹出一个你不需要使用的提示），但以这种方式引用字段仍然是一个良好的习惯：

```cs
public Point()
{
    this.x = -1;
    this.y = -1;
}
```

- 18. 在“生成”菜单上，选择“生成解决方案”。确认代码编译无错误或警告。（你可以运行它，但它还没有任何输出。）

属于类并操作类特定实例的数据的方法被称为实例方法。（你将在本章后面的部分学习其他类型的方法。）在接下来的练习中，你将为 Point 类编写一个名为 DistanceTo 的实例方法，计算两个点之间的距离。

## 编写和调用实例方法

- 1. 在 Visual Studio 2022 的 Classes 项目中，在 Point 构造函数之后添加以下公共实例方法 DistanceTo。该方法接受单个名为 other 的 Point 参数并返回一个 double。

DistanceTo 方法所示：

```cs
class Point
{
    ...
    public double DistanceTo(Point other)
    {
    }
}
```

在接下来的步骤中，你将在 DistanceTo 实例方法体中添加代码，计算并返回调用 Point 对象与作为参数传递的 Point 对象之间的距离。为了实现这一点，你必须计算 x 坐标和 y 坐标之间的差值。

