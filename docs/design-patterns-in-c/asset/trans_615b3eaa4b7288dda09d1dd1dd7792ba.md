

### 小结

在本章中，我们通过一个 C# 示例探索了迭代器模式。该模式已经在 C# 语言架构中得到了很好的实现。我们也可以在自定义类中扩展该模式的使用。我们上面讨论的示例已包含在源代码附件中。

## 18. 中介者模式

在本章中，我想带您了解使用中介者模式的优势。一如既往，设计模式如果使用得当，会给我们带来更大的灵活性和可管理性。中介者模式也不例外。

### 挑战

您正在开发一个管理航班校验的航空公司应用程序。如您所知，飞机起飞前要经过一系列检查，以确保每个部件的健康状态、燃油量等。

我们的 Flight 类包含以下组件类：

- Engine
- Wheels
- Cockpit
- Aviation

每个组件类都有一个名为 Start() 的方法。调用该方法时，它会通过名为 IsReady() 的方法来确保组件的当前状态有效。如果 IsReady() 方法返回 true，该组件类就会检查其他组件的 IsReady() 方法。

例如，Engine 类分别通过 Wheels 和 Aviation 的 IsReady() 方法来确保它们处于有效状态。而 Cockpit 则检查自身、Engine 和 Aviation 的状态。因此，类之间存在耦合和代码重复。当引入新的组件类时，这种情况会变得更糟。

![](img/10a39e9a5b1ae55cb003d638eba7aaa0_69_0.png)

如何让代码变得更好？

### 定义

GoF 定义：“定义一个对象，封装一组对象如何交互。中介者模式通过避免对象之间显式地相互引用，从而促进松散耦合，并允许你独立地改变它们之间的交互。”

### 实现

我们可以通过引入中介者模式来改进上述情况。通过引入中介者，组件类之间不再直接通信。所有组件都与一个新的中介者类通信。其优点有：

- 组件之间松散耦合
- 集中式管理
- 更改代码时更灵活

新方法如下所示：

![](img/10a39e9a5b1ae55cb003d638eba7aaa0_70_0.png)

这里，各个组件部分将与中介者类通信，以提供继续进行的就绪信号。

### 类

以下是使用中介者模式的新实现所涉及的类。

```csharp
public class FlightMediator
{
    private Engine _engine;
    private Aviation _aviation;
    private Wheels _wheels;
    private Cockpit _cockpit;

    public FlightMediator(Engine engine, Aviation aviation, Wheels wheels, Cockpit cockpit)
    {
        _engine = engine;
        _aviation = aviation;
        _wheels = wheels;
        _cockpit = cockpit;
    }

    public bool IsReady()
    {
        return _engine.IsReady() && _aviation.IsReady() && _wheels.IsReady() &&
               _cockpit.IsReady();
    }
}

public class Engine
{
    public void Start()
    {
    }

    public bool IsReady()
    {
        return true;
    }
}

public class Aviation
{
    private int _FuelLevel = 1000;

    public bool IsReady()
    {
        return _FuelLevel > 5000; // Returns false as not enough fuel
    }
}

public class Wheels
{
    public bool IsReady()
    {
        return true;
    }
}

public class Cockpit
{
    public bool IsReady()
    {
        return true;
    }
}
```

请注意，Aviation 类的 IsReady() 方法返回 false。FlightMediator 构造函数将所有的组件类作为输入。IsReady() 方法会检查所有关联组件的 IsReady() 方法，以确保校验正确。

运行 Windows Forms 应用程序后，您会看到以下界面。

![](img/10a39e9a5b1ae55cb003d638eba7aaa0_72_0.png)

单击 FlightMediator 按钮，您会看到颜色变为红色，因为返回的状态为 false。

![](img/10a39e9a5b1ae55cb003d638eba7aaa0_72_1.png)

### 小结

在本章中，我们探索了中介者模式。该示例是在一个简单的问题场景中提供的，但现实世界中的问题要复杂得多。例如，在一个向导页面框架中，每个页面都需要考虑上一页和下一页，使用中介者模式可以使其变得更好。本章附带了相关的源代码。

## 19. 备忘录模式

在本章中，我想尝试一下备忘录模式。备忘录模式提供了一种面向对象的方式来保存对象的状态。这个状态称为备忘录（Memento），以后可以用来恢复该对象。

Memento 在英语中的意思是“对过去事件的提醒”。

### 挑战

您正在开发一个绘图应用程序，该程序允许用户在画布上绘制线条。用户应该能够在特定时间间隔保存状态，以便可以撤消后续的错误。您需要为这个问题提供解决方案。

### 定义

GoF 定义：“在不违反封装的前提下，捕获并外部化一个对象的内部状态，以便以后可以将该对象恢复到这一状态。”

### 实现

上述问题可以使用备忘录模式来解决。正如定义中所说，该模式保存对象的内部状态，以便日后恢复。对象状态的保存不会违反封装。

![](img/10a39e9a5b1ae55cb003d638eba7aaa0_73_0.png)

以下是 Drawing 类的定义：

![](img/10a39e9a5b1ae55cb003d638eba7aaa0_74_0.png)

AddLine() 方法允许在图形上添加线条。这些信息作为状态存储在 _list 对象中。

CreateMemento() 方法允许在不违反封装的情况下获取内部状态的副本。

RestoreMemento() 方法允许将状态恢复到给定的备忘录。

以下是 Memento 类的定义：

![](img/10a39e9a5b1ae55cb003d638eba7aaa0_74_1.png)

它包含一个 State 属性，用于保存 Drawing 类的状态。

### 执行应用程序

您可以尝试运行附带的应用程序。运行后，在画布上绘制一系列线条，然后使用 Save 按钮保存备忘录。

现在尝试添加一些不需要的线条：

使用“恢复状态”来获取旧的、有效的状态。

![](img/10a39e9a5b1ae55cb003d638eba7aaa0_76_0.png)

至此，我们实现备忘录模式的应用程序就结束了。

### 比较命令模式和备忘录模式

命令模式也通过将操作转换为命令来提供撤销/重做功能。区别在于，命令模式存储每个操作，而备忘录模式仅在请求时保存状态。此外，命令模式对每个操作都有撤销和重做，而备忘录模式则不需要。

可以根据具体场景选择使用命令模式或备忘录模式。

### 小结

在本章中，我们探索了备忘录模式。附带的源代码中包含我们讨论的示例。

## 20. 原型模式

在本章中，我想解释一下原型模式以及 C# 对它的支持。原型模式提供了一种通过复制现有对象的原型来实例化新对象的替代方案。

### 挑战

您正在开发一个应用程序，其设置存储在 Settings 类中。类的属性在构造函数中被赋值。这涉及调用配置文件、安全数据库、用户配置文件数据库等。

您需要将上述实例传递给某个库中的组件。该组件可能会随意修改这些属性，因此我们只能发送 Settings 的另一个实例。由于实例创建的开销很大，我们需要创建上述实例的一个副本。

最佳方法是什么？

### 定义

GoF 定义：“使用原型实例指定要创建的对象的种类，并通过复制这个原型来创建新对象。”

### 解决方案

我们可以使用原型模式来应对这种场景。该模式允许我们以具有所需属性的现有实例为原型来创建新实例。

![](img/10a39e9a5b1ae55cb003d638eba7aaa0_77_0.png)

创建新对象并修改它。从修改后的对象创建原型。

System.Object 类包含一个名为 MemberwiseClone() 的新方法，它提供当前对象的浅拷贝。浅拷贝仅涉及复制

