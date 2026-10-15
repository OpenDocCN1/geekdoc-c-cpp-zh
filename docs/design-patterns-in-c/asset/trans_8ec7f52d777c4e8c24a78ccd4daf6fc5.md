

以下是类图：

![](img/10a39e9a5b1ae55cb003d638eba7aaa0_87_0.png)

至此，我们使用解释器模式的应用就结束了。现在这些操作可以被转换为一种语言以便后续解释。

## 命令模式与解释器模式的比较

你可以在命令模式和解释器模式之间找到一些相似之处。命令模式说的是将操作转换为命令以用于记录或撤销目的。这里的命令是对象，但对于解释器模式来说，命令是句子。

命令模式可用于通过序列化命令列表来持久化对象，与解释器模式相比会导致文件较大。解释器模式在运行时提供了一种更简单的方法，但代价是需要开发一个解释器。

### 解释器模式的应用

你正在创建自己的 Photoshop 应用。图层上绘制的对象可以转换为一系列命令。之后，整个绘图可以用命令文件表示，该文件与整个画布序列化相比体积会更小。你将获得将文件发送给其他人的优势，他/她可以：

- 重新生成绘图
- 查看所有绘图操作
- 修改绘图操作项
- 撤销最后的绘图操作

### 参考

http://www.dofactory.com/Patterns/PatternInterpreter.aspx#_self1

### 总结

在本章中，我们通过一个小型应用了解了解释器模式。上述应用仅展示了简单的用法以供学习，但在真实世界的场景中，该语言可能包含循环、条件等。附件包含我们讨论的应用的源代码。

## 23. 组合模式

在本章中我们可以探索组合设计模式。它在与单个对象和对象组进行通信时提供了一种更好的方法。如常，我们可以从挑战-解决方案方法开始。

### 挑战

你正在开发一个包含总部和分支机构的分布式应用。每个办公室在夏令时期间都需要全局更新 2 个时钟控件。

![](img/10a39e9a5b1ae55cb003d638eba7aaa0_89_0.png)

上图显示了当前结构。总部只有一个，下设多个分支。总部和每个分支都将拥有 2 个时钟控件。时间更改过程从总部开始，在当前方法中，总部必须记住所有分支以及每个分支内部的所有时钟。这非常繁琐，并且在分支合并到一个分支组时会失效。

如何提供更好的解决方案？

### 定义

GoF 定义：“将对象组合成树形结构以表示整体-部分层次结构。组合模式让客户端可以统一地处理单个对象和对象组合”

### 实现

我们可以在上述场景中使用组合设计模式。一旦我们的解决方案实现，总部只需要考虑分支。分支将考虑各自的时钟。

我们的解决方案中有 2 个类：Office 和 Clock。Office 类可以表示总部和分支。Clock 类管理用于更改时间的时钟控件。

我们需要引入一个接口，由 Office 和 Clock 类实现。

```csharp
interface IComponent
{
    void Add (IComponent notifier);
    void SetTime(DateTime time);
}
```

Add() 方法确保添加类型为 IComponent 的组件。可用于添加 Office 或 Clock 实例。

SetTime() 方法可用于更改当前时间。

### 类实现

以下是 Office 和 Clock 类的实现：

```csharp
class Office : IComponent
{
    private IList<IComponent> _list = new List<IComponent>();

    public void Add(IComponent notifier)
    {
        _list.Add(notifier);
    }

    public void SetTime(DateTime time)
    {
        foreach (IComponent n in _list)
            n.SetTime(time);
    }
}

class Clock : IComponent
{
    public ClockControl ClockControl;

    public void Add(IComponent notifier)
    {
        throw new ApplicationException("You cannot add IClock!");
    }

    public void SetTime(DateTime time)
    {
        ClockControl.CurrentTime = time;
    }
}
```

请注意，Office 类的 SetTime() 实现负责通知所有添加的 IComponent 实例。因此总部可以通知所有分支。分支将通知所有时钟实例。

### 创建实例

以下是总部和分支实例创建的代码。

```csharp
_headOffice = new Office();
_headOffice.Add(new Clock() { ClockControl = hForm.clock1 });
_headOffice.Add(new Clock() { ClockControl = hForm.clock2 });

Office branch1 = new Office();
branch1.Add(new Clock() { ClockControl = b1Form.clock1 });
branch1.Add(new Clock() { ClockControl = b1Form.clock2 });
_headOffice.Add(branch1);

Office branch2 = new Office();
branch2.Add(new Clock() { ClockControl = b2Form.clock1 });
branch2.Add(new Clock() { ClockControl = b2Form.clock2 });
_headOffice.Add(branch2);
```

请注意，分支实例已添加到总部。

### 运行应用

点击设置时间按钮，你可以看到所有时钟都重置为上午 10:00。

![](img/10a39e9a5b1ae55cb003d638eba7aaa0_91_0.png)

这里总部不需要考虑分支的所有时钟实例。这里单个对象（时钟）和组合对象（分支）被统一处理，满足了模式定义。

### 总结

在本章中，我们探索了组合模式。它在与单个对象和组合对象通信时提供了一种集中化的方法。附件包含我们讨论的示例应用，包括时钟控件。

### 参考

该电子书是在收集书籍、MSDN 和其他在线资源的信息后编译的。花费了近 1 年时间覆盖所有章节，因此部分参考链接可能会失效。

你可以使用以下链接找到有关设计模式的更多信息：

http://www.dofactory.com

http://www.oodesign.com

### 源代码

电子书的源代码可在 http://jeanpaulva.com 上找到。

