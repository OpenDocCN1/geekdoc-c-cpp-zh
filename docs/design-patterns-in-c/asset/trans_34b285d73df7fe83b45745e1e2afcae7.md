

值类型。结合 ICloneable 接口，我们可以为 Settings 类提供一个 Clone() 方法，该方法调用 MemberwiseClone()。

```csharp
public class Settings : ICloneable
{
    public Settings()
    {
        // Load ApplicationSettings from Configuration
        // Load ThemeSettings from Database
        // Load UserSettings from Database
        Thread.Sleep(3000); // Simulate a delay for the above operations

        ApplicationSettings = "ApplicationSettings1";
        ThemeSettings = "ThemeSettings1";
        UserSettings = "UserSettings1";
    }

    public string ApplicationSettings
    {
        get;
        set;
    }

    public string ThemeSettings
    {
        get;
        set;
    }

    public string UserSettings
    {
        get;
        set;
    }

    public object Clone()
    {
        return this.MemberwiseClone();
    }

    public override string ToString()
    {
        return this.ApplicationSettings + " " +
               this.ThemeSettings + " " +
               this.UserSettings;
    }
}
```

### 执行应用程序

现在我们可以尝试操作类实例。首先我们创建一个 Settings 实例（这是一个 3 秒的延迟过程）。之后我们对 Settings 实例进行克隆并修改属性。我们可以看到新的实例是使用 Clone() 方法创建的。

```csharp
static void Main(string[] args)
{
    Settings settings = new Settings();
    Settings settingsClone = (Settings)settings.Clone();
    settingsClone.ApplicationSettings = "NewSettings"; // Change property
    Console.WriteLine("INSTANCE 1: " + settings.ToString());
    Console.WriteLine("INSTANCE 2: " + settingsClone.ToString());
    Console.ReadKey(false);
}
```

执行应用程序后我们可以看到以下结果。

![](img/10a39e9a5b1ae55cb003d638eba7aaa0_79_0.png)

我们可以从上面的代码看出：

1. 实例 1 是使用 new 关键字创建的
2. 实例 2 是使用 Clone() 方法创建的
3. 修改实例 2 不会影响实例 1

至此，我们对原型模式的实验就结束了。

### 参考

http://sourcemaking.com/design_patterns/prototype

### 总结

在本章中我们探索了原型模式。原型模式的使用可以总结为：

- 使用所需属性更快地创建实例
- 实例创建时可以避免使用 new 关键字
- 为抽象工厂模式提供一种替代方案
- 在运行时指定实例属性

## 21. 桥接模式

在本章中我们可以探索桥接模式，该模式在应用程序中常用。

### 挑战

你正在处理一个抽象业务类。该类需要通过写入文件、向用户发送电子邮件等方式记录信息。我们需要避免业务类与记录器紧密耦合，因为未来可能会出现记录器的新版本。

### 紧耦合设计

![](img/10a39e9a5b1ae55cb003d638eba7aaa0_81_0.png)

如何实现解耦的解决方案？

### 定义

GoF 定义："将抽象与其实现分离，以便两者可以独立变化"

### 实现

我们可以为表示 Logger 创建一个抽象类。让抽象业务类持有对新的抽象 Logger 的引用。在运行时我们可以指定 Logger 类的实际实现实例。 （文件写入器或电子邮件发送器）以下是使用桥接模式后的类图快照：

![](img/10a39e9a5b1ae55cb003d638eba7aaa0_82_0.png)

这里具体的 Logger 实现派生自 AbstractLogger 类。具体的 TransactionBL 派生自 AbstractBL 类。AbstractBL 类持有对 Logger（抽象 Logger）的引用。

使用如上所示的桥接模式，实现与抽象解耦。它允许在不修改 BL 类的情况下对 Logger 类进行未来扩展。

### 代码

以下是调用上述 Transaction 和 Logger 类的代码。

```
AbstractBL bl = new TransactionBL();
bl.Logger = new TextFileLogger();
bl.ProcessPayment();

bl.Logger = new EmailLogger();
bl.ProcessPayment();

Console.ReadKey(false);
```

运行应用程序后我们可以看到以下输出。

![](img/10a39e9a5b1ae55cb003d638eba7aaa0_83_0.png)

以下是使用桥接模式后的耦合快照。

![](img/10a39e9a5b1ae55cb003d638eba7aaa0_83_1.png)

### 注意

我们可以看出该模式是使用抽象类和接口的简单实现。桥接模式与策略模式有一些相似之处，因为两者都涉及在运行时更改实现。这里的类与策略模式相比是抽象的。

### 总结

在本章中我们探索了桥接设计模式。它通过抽象类或接口的桥梁为分离抽象与实现提供了便捷方式。附带的源代码包含我们讨论的示例。

## 22. 解释器模式

在本章中我想演示解释器模式的使用。这不是一个广泛使用的模式，但揭示了一种良好的编程方式。它说的是创建一种语言以及该语言的解释器。语言可用于表示状态、动作、循环等，具体取决于编程需求。这里我们使用该模式来解决持久化问题。

### 挑战

你正在开发一个绘图应用程序，允许在画布上创建线条和圆圈。Line 和 Circle 类为你完成了这项工作。你需要将绘图与拥有各自应用程序副本的多个用户进行通信。当前使用上述类的序列化进行绘图持久化会产生大尺寸文件，并且不允许通过聊天窗口发送消息。如何提供更小尺寸、更易于通信的持久化解决方案？

### 定义

GoF 定义："给定一种语言，为其语法定义一种表示形式，以及一个使用该表示形式来解释该语言中句子的解释器"

### 实现

我们可以使用解释器模式来解决这个问题。我们需要构建一种包含命令的语言以及执行操作的解释器。

![](img/10a39e9a5b1ae55cb003d638eba7aaa0_84_0.png)

以下是我们绘图应用程序涉及的类：

- 一个 Line 类
- 一个 Circle 类

解释器 Execute() 方法的主体如下所示：

```
public void Execute(string commands, Graphics graphics)
{
    graphics.Clear(Color.FromArgb(237, 253, 200));

    int i = 0;

    foreach (string rawCommand in commands.Split(';'))
    {
        string command = rawCommand.Replace(Environment.NewLine, string.Empty).Trim();

        if (command.StartsWith("line"))
        {
            i = 0;
            int x = 0, y = 0, width = 0, height = 0;

            foreach (string argument in command.Split(','))
            {
                if (i == 1)
                    x = int.Parse(argument);
                else if (i == 2)
                    y = int.Parse(argument);
                else if (i == 3)
                    width = int.Parse(argument);
                else if (i == 4)
                    height = int.Parse(argument);

                i++;
            }

            new Line(graphics).Draw(x, y, width, height);
        }
        else if (command.StartsWith("circle"))
        {
            i = 0;
            int x = 0, y = 0, radius = 0;

            foreach (string argument in command.Split(','))
            {
                if (i == 1)
                    x = int.Parse(argument);
                else if (i == 2)
                    y = int.Parse(argument);
                else if (i == 3)
                    radius = int.Parse(argument);

                i++;
            }

            new Circle(graphics).Draw(x, y, radius);
        }
    }
}
```

