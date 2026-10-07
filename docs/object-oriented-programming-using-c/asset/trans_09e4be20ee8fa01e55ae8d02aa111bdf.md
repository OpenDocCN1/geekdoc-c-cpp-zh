

# 使用 C# 进行面向对象编程

# 案例研究

修改接口设计以适应这一变化是简单的——我们可以：

-   创建一个新面板来适应“紧急消息”的创建
-   由于紧急消息所需的数据与普通消息相同，我们只需要在中间面板添加一个额外的按钮“添加紧急消息”即可。

这些额外需求将如何影响系统底层的类？

如果面向对象（OO）原则有效，那么实现这一额外需求应该相对简单。首先，“消息”（Message）与“紧急消息”（Urgent Message）之间存在明显的关联。

如果这两个类具有某些独特特性，但在功能上有大量重叠，我们可以引入继承层次结构来处理这个问题：

```
<<abstract>>
Message
OrdinaryMessage
UrgentMessage
```

![](img/e143b38d00f95425fa4f3efca0527189_221_0.png)

# 使用 C# 进行面向对象编程

# 案例研究

然而，在这种情况下，普通消息并没有什么独特之处——消息有相关的成本，可以获取成本和文本，并且可以创建新消息。紧急消息也是如此。紧急消息与普通消息，只是文本和成本略有不同。UrgentMessage 是 Message 的一种类型，可以继承 Message 的所有特性，并重写成本和文本方法。

因此，Message 和 UrgentMessage 类之间的关系如下所示，UrgentMessage 继承了与 Message 关联的所有值和方法，但重写了 GetCost() 和 GetText() 方法以反映与紧急消息相关的成本和文本。

![](img/e143b38d00f95425fa4f3efca0527189_222_0.png)

下面是修订后的类图。但这种变化将如何影响系统的其他部分？

![](img/e143b38d00f95425fa4f3efca0527189_222_1.png)

# 使用 C# 进行面向对象编程

# 案例研究

得益于多态性的操作，这一变化对系统的任何其他部分都不会产生影响！

查看类图可以发现 MessageSet 保留并管理一组消息（DummyBoard 保留一组消息 - 一旦它们被上传显示）。但是关于 UrgentMessage 呢？

紧急消息只是特定类型的消息。当在 MessageSet 中调用 AddMessage() 方法时，需要一个 Message 类型的对象，即一个要添加的消息 - 但子类型 UrgentMessage 仍然是“Message”，因此 AddMessage() 方法会接受一个 UrgentMessage 对象。

因此，在不对所有 MessageSet 任何任何更改的情况下，MessageSet 可以维护一个所有要显示的消息集合（包括紧急消息和普通消息）！

此外，当调用 DailyPurge() 方法时，它会调用 Message 对象的 GetCost() 方法，以便向该客户收取费用。在运行时，公共语言运行时（CLR）引擎将确定对象是 Message 类型还是 UrgentMessage 类型，并将会调用 GetCost() 方法的正确版本 - 记住这个方法在 UrgentMessage 中被重写了。这就是多态性的应用！

MessageSet 需要消息，但得益于多态性和方法重写的应用，MessageSet 将乐意地处理任何子类型，就像它们是 Message 对象一样。如果我们以后创建新的消息类型，例如圣诞消息或情人节消息，MessageSet 也能处理这些消息，而无需更改任何行代码！

因此，在该应用程序中，我们能够通过仅添加一个类并对接口进行一个小更改，来扩展系统添加紧急消息的功能。

如果没有应用多态性，我们只需要对系统的其他部分进行额外的更改 - 即 MessageSet 和 DummyBoard。

面向对象使系统能够以最小的努力进行扩展！

# 11.7 类的打包

大型程序应该分段包（packages），因为这提供了适当的封装和访问控制级别（如第 2 章所述）。

此处用于演示教科书中理论的系统很难算得上是大规模——尽管如此，我们决定将相关的类打包在一起，如下所示。

# 使用 C# 进行面向对象编程

# 案例研究

![](img/e143b38d00f95425fa4f3efca0527189_224_0.png)

该图显示了使用的四个包以及每个包中的类。还显示了包之间的关联。不意外的是，存放系统接口的主包与所有其他包都关联——这是因为接口调用了整个系统的功能。

完成设计并适应了变化的需求后，我们可以开始实现系统。这将分两个阶段完成：

![](img/e143b38d00f95425fa4f3efca0527189_224_1.png)

# 使用 C# 进行面向对象编程

在第一阶段，将实现一个基础系统，允许创建消息和客户端，将其写入文件并显示消息。

在第二阶段，将扩展系统功能以允许删除客户端并增加其积分。这种实现方式将允许演示测试驱动开发（如第 10 章所述）。

# 11.8 编写消息类

Message、UrgentMessage 和 MessageSet 的编写相对直接。

Message 具有各种实例变量（String: messageText 和 int: COST, clientID 和 daysRemaining）。它具有相应的属性来访问这些属性（仅 daysRemaining 需要一个 setter）以及一个初始化实例变量的构造函数。它还有以下方法：

```
void DecrementDays() // 减少天数
boolean HasExpired() // 指定是否从集合中移除
String ToString() // 返回显示的文本
```

后期我们需要将 Client 和 MessageSet 对象存储到文件中。为了这样做，所有类（包括 Message 类）都需要标记为 Serializable。最后，要求说明不允许重复的消息（即相同客户的相同文本）。因此，Message 必须重写 Equals() 和 GetHashCode() 方法以确保在存储在 Set 时不允许重复。此类的完整代码如下，但为了简洁排除了注释。带有注释系统的源代码可以通过本章末尾的指令查看。

```
namespace MessageManagerSystem.Messages
{
    [Serializable]
    public class Message
    {
        const int COST = 1;
        public virtual int Cost
        {
            get { return COST; }
        }
        private int clientID;
        public int ClientID
        {
            get { return clientID; }
        }
        private String messageText;
        public String MessageText
        {
            get { return messageText; }
        }
        private int daysRemaining;
        public int DaysRemaining
        {
            get { return daysRemaining; }
            set { daysRemaining = value; }
        }

        public Message(int clientID, String text, int daysRemaining)
        {
            this.clientID = clientID;
            this.messageText = text;
            this.daysRemaining = daysRemaining;
        }

        public void DecrementDays()
        {
            daysRemaining--;
        }

        public bool HasExpired()
        {
            return (daysRemaining <= 0);
        }

        public override String ToString()
        {
            return (messageText);
        }

        public override bool Equals(object obj)
        {
            Message m = (Message)obj;
            return (clientID.Equals(m.clientID) &&
                messageText.Equals(m.MessageText));
        }

        public override int GetHashCode()
        {
            return (messageText + clientID).GetHashCode();
        }
    }
}
```

