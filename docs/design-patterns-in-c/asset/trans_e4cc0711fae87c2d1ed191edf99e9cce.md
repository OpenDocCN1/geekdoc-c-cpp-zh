

# C# 中的设计模式

JEAN PAUL V.A

![](img/10a39e9a5b1ae55cb003d638eba7aaa0_0_0.png)

# 致谢

本书是我在设计模式方面过去一年学习成果的汇编。这是一段非常有趣的旅程，我在技能方面获得了宝贵的资产。

我谨向所有朋友以及 c-sharpcorner.com 上的朋友们给予我的鼓励表示感谢。

Copyright © 2012 by Jean Paul V.A (www.jeanpaulva.com)

# 目录

+   1. SINGLETON PATTERN ......................................................... 6
+   2. COMMAND PATTERN ........................................................... 9
+   3. ADAPTER PATTERN ........................................................... 15
+   4. DECORATOR PATTERN ......................................................... 18
+   5. STRATEGY PATTERN ........................................................... 22
+   6. TEMPLATE METHOD PATTERN ................................................... 25
+   7. VISITOR PATTERN ............................................................ 30
+   8. OBSERVER PATTERN ........................................................... 34
+   9. BUILDER PATTERN ............................................................ 38
+   10. CHAIN OF RESPONSIBILITY PATTERN ............................................ 41
+   11. ABSTRACT FACTORY PATTERN ................................................... 46
+   12. FACTORY METHOD PATTERN .................................................... 49
+   13. FLYWEIGHT PATTERN .......................................................... 53
+   14. PROXY PATTERN .............................................................. 57
+   15. FACADE PATTERN ............................................................. 61
+   16. STATE PATTERN .............................................................. 63
+   17. ITERATOR PATTERN ........................................................... 66
+   18. MEDIATOR PATTERN ........................................................... 70
+   19. MEMENTO PATTERN ............................................................ 74
+   20. PROTOTYPE PATTERN .......................................................... 78
+   21. BRIDGE PATTERN ............................................................. 82

22. INTERPRETER PATTERN .........................................................85

23. COMPOSITE PATTERN ...........................................................90

REFERENCES........................................................................93

SOURCE CODE .......................................................................93

CONCLUSION .......................................................................94

# 1. 单例模式

这是 23 种设计模式中最流行的模式。该模式讲述了高效的实例管理。

# 挑战

你正在开发一个应用程序，该应用程序需要将日志信息记录到名为 **Application.Log** 的文件中。日志由名为 **LogManager** 的类管理。LogManager 通过其构造函数对文件保持锁定。

LogManager 实例可以在整个应用程序中创建，这将导致异常。除此之外，LogManager 类只需要一个实例。

上述问题可以使用单例模式解决。

# 定义

> GoF 定义："确保一个类只有一个实例，并提供一个全局访问点"

# 实现

要实现上述规范，我们必须执行以下操作：

+   - 使构造函数私有并仅创建 1 个实例
+   - 创建一个静态属性来访问实例

以下是根据单例模式修改后的类定义。

![](img/10a39e9a5b1ae55cb003d638eba7aaa0_5_0.png)

以下是 LogManager 类中包含的代码。

```
```csharp
public class LogManager
{
    private static LogManager _instance;

    public static LogManager Instance
    {
        get
        {
            if (_instance == null)
                _instance = new LogManager();

            return _instance;
        }
    }

    private LogManager()  // Constructor as Private
    {
        _fileStream = File.OpenWrite(GetExecutionFolder() + "\\Application.log");
        _streamWriter = new StreamWriter(_fileStream);
    }

    private FileStream _fileStream;
    private StreamWriter _streamWriter;

    public void WriteLog(string message)
    {
        StringBuilder formattedMessage = new StringBuilder();
        formattedMessage.AppendLine("Date: " + DateTime.Now.ToString());
        formattedMessage.AppendLine("Message: " + message);

        _streamWriter.WriteLine(formattedMessage.ToString());
        _streamWriter.Flush();
    }

    public string GetExecutionFolder()
    {
        return Path.GetDirectoryName(System.Reflection.Assembly.GetExecutingAssembly().Location);
    }
}
```
```

你可以看到这里的构造函数是私有的。由于它是私有的，外部类无法创建 LogManager 实例。

```
```csharp
private LogManager()  // Constructor as Private
{
    --
}
```
```

你可以看到新的 Instance 属性，它是静态的。它也确保只创建一个实例。

```
public static LogManager Instance
{
    get
    {
        if (_instance == null)
            _instance = new LogManager();

        return _instance;
    }
}
```

要调用写入方法，我们可以使用以下代码：

```
LogManager.Instance.WriteLog("Test Writing");
```

以下图像描述了单例和普通情况下的实例数量。

![](img/10a39e9a5b1ae55cb003d638eba7aaa0_7_0.png)

使用单例的优点如下：

+   - 实例重用使内存管理更有效
+   - 避免了文件锁定开销

单例的局限性如下：

+   - 将构造函数设为私有会带来限制
+   - 在多线程中使用时开销更大（但在 .Net 中是线程安全的）

# 总结

在本章中，我们看到了什么是单例模式以及使用 C#.NET 实现它的一个可能方法。Multiton 是另一种经常与单例进行比较的模式。

# 2. 命令模式

在本章中，我试图展示命令设计模式的使用。这是一种流行的模式，它利用了良好的面向对象结构，并简化了在应用程序中实现撤销功能的逻辑。

# 挑战

你正在开发一个绘画应用程序。对于每次画笔划动，你需要提供撤销功能。

目前可用的画笔是方形和矩形。未来会有更多画笔可用。我们的挑战是为用户提供撤销功能。显然，点击撤销按钮后，最后一次划动应从画布上清除。

你的方法是什么？

# 应用程序屏幕截图

![](img/10a39e9a5b1ae55cb003d638eba7aaa0_8_0.png)

# 类图

![](img/10a39e9a5b1ae55cb003d638eba7aaa0_10_0.png)

当应用程序运行时，用户将看到一个空白的白色屏幕，并有一组可供选择的颜色。默认选择的画笔为方形，点击画布后会在画布上绘制一个新的方形。默认选择的颜色为蓝色，存储在变量 _activeColor 中。

在表单级别声明的变量为：

```
private ShapeEnum _activeShape = ShapeEnum.Square;
private Color _activeColor = Color.Blue;
private Bitmap _bitmap;
private Graphics _graphics;
```

对于每次鼠标按下操作，将创建一个新的方形类。这意味着如果进行 10 次点击，将创建 10 个方形类并调用 Do() 操作。枚举变量 _activeShape 用于跟踪用户当前选择的形状。鼠标按下事件将如下所示。

```
private void Canvas_MouseDown(object sender, MouseEventArgs e)
{
    // Each mouse down creates a new command class instance
    ICommand command = null;
    if (_activeShape == ShapeEnum.Square)
        command = new SquareCommand(_bitmap, _activeColor, e.X, e.Y);
    else if (_activeShape == ShapeEnum.Rectangle)
```

