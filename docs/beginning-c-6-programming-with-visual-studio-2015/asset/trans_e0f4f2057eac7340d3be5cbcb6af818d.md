
访问索引小于 0 或大于 51 的卡牌时，你会修改为使用自定义异常。

首先，你需要创建一个名为 Ch13CardLib 的新类库项目，将其保存在 BegVCSharp\Chapter13 目录下，并像之前一样从 Ch12CardLib 复制类，同时将命名空间相应改为 Ch13CardLib。接下来，定义异常。你可以通过在新类文件 CardOutOfRangeException.cs 中定义一个新类来完成，你可以通过 Project → Add Class 将此类添加到 Ch13CardLib 项目（你可以在 Ch13CardLib\CardOutOfRangeException.cs 中找到此代码）：

```
public class CardOutOfRangeException : Exception
{
    private Cards deckContents;
    public Cards DeckContents
    {
        get { return deckContents; }
    }
    public CardOutOfRangeException(Cards sourceDeckContents)
        : base("There are only 52 cards in the deck.")
    {
        deckContents = sourceDeckContents;
    }
}
```

此类的构造函数需要一个 Cards 类的实例。它允许通过 DeckContents 属性访问这个 Cards 对象，并向基类 Exception 构造函数提供合适的错误消息，以便通过类的 Message 属性获取该消息。

接下来，向 Deck.cs 添加使用此异常的代码，替换原来的标准异常（你可以在 Ch13CardLib\Deck.cs 中找到此代码）：

```
public Card GetCard(int cardNum)
{
    if (cardNum >= 0 && cardNum <= 51)
        return cards[cardNum];
    else
        throw new CardOutOfRangeException(cards.Clone() as Cards);
}
```

DeckContents 属性使用 Deck 对象当前内容的深拷贝（以 Cards 对象的形式）进行初始化。这意味着你可以在抛出异常时看到内容，因此后续对牌组内容的修改不会“丢失”此信息。

要测试这一点，可以使用以下客户端代码（你可以在 Ch13CardClient\Program.cs 中找到此代码）：

```
Deck deck1 = new Deck();
try
{
    Card myCard = deck1.GetCard(60);
}
```

> **注意** 事件中使用委托这一事实是委托如此有用的原因之一。这也是第六章花费一定篇幅介绍它们的原因。你可能希望回顾一下这些材料，以重温委托及其使用方法。

处理的基本顺序如下：首先，应用程序创建一个可以引发事件的对象。例如，假设一个即时消息应用程序创建了一个表示与远程用户连接的对象。当通过该连接收到来自远程用户的消息时，该连接对象可能会引发一个事件（见图 13-2）。

![](img/cf72ea860016d2d680fc085fc06f265a_373_0.png)

图 13-2

接下来，应用程序订阅该事件。你的即时消息应用程序可以定义一个与事件所指定的委托类型匹配的方法，并将该方法的引用传递给事件来实现订阅。事件处理程序方法可以是另一个对象上的方法，例如一个表示显示设备的对象，用于在即时消息到达时显示它们（见图 13-3）。

![](img/cf72ea860016d2d680fc085fc06f265a_373_1.png)

图 13-3

当事件被引发时，订阅者会收到通知。当即时消息通过连接对象到达时，显示设备对象上的事件处理程序方法会被调用。由于你使用的是标准方法，引发事件的对象可以通过参数传递任何相关信息，这使得事件非常通用。在示例中，一个参数可能是即时消息的文本，事件处理程序可以将其显示在显示设备对象上。如图 13-4 所示。

![](img/cf72ea860016d2d680fc085fc06f265a_374_0.png)

图 13-4

## 处理事件

如前所述，要处理事件，你需要通过提供一个事件处理程序方法来订阅事件，该方法的返回类型和参数必须与事件使用的委托所指定的类型和参数匹配。下面的示例使用一个简单的计时器对象来引发事件，从而调用处理程序方法。

### 试一试：处理事件（Ch13Ex01\Program.cs）

1. 创建一个名为 Ch13Ex01 的新控制台应用程序，并将其保存在目录 C:\BegVCSharp\Chapter13 中。

2. 修改 Program.cs 中的代码如下：

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Timers;
using static System.Console;

namespace Ch13Ex01
{
    class Program
    {
        static int counter = 0;

        static string displayString =
            "This string will appear one letter at a time.";

        static void Main(string[] args)
        {
            Timer myTimer = new Timer(100);
            myTimer.Elapsed += new ElapsedEventHandler(WriteChar);
            myTimer.Start();
            System.Threading.Thread.Sleep(200);
            ReadKey();
        }

        static void WriteChar(object source, ElapsedEventArgs e)
        {
            Write(displayString[counter++ % displayString.Length]);
        }
    }
}
```

3. 运行应用程序（一旦运行，按任意键将终止应用程序）。短暂片刻后，结果如图 13-5 所示。

![](img/cf72ea860016d2d680fc085fc06f265a_375_0.png)

图 13-5

### 工作原理

用于引发事件的对象是 System.Timers.Timer 类的一个实例。该对象使用一个时间段（以毫秒为单位）进行初始化。当使用其 Start() 方法启动 Timer 对象时，会引发一系列事件，这些事件根据指定的时间段在时间上间隔开。Main() 使用 100 毫秒的计时器周期初始化一个 Timer 对象，因此启动后它将每秒引发 10 次事件：

```
static void Main(string[] args)
{
    Timer myTimer = new Timer(100);
}
```

Timer 对象有一个名为 Elapsed 的事件，该事件所需的事件处理程序必须与 System.Timers.ElapsedEventHandler 委托类型的返回类型和参数匹配，该委托类型是 .NET Framework 中定义的标准委托之一。此委托指定了以下返回类型和参数：

```
void <MethodName>(object source, ElapsedEventArgs e);
```

Timer 对象在第一个参数中发送对自身的引用，在第二个参数中发送一个 ElapsedEventArgs 对象的实例。目前可以安全地忽略这些参数；稍后你会再研究它们。

在你的代码中，你有一个合适的方法：

```
static void WriteChar(object source, ElapsedEventArgs e)
{
    Write(displayString[counter++ % displayString.Length]);
}
```

该方法使用 Program 的两个静态字段 counter 和 displayString 来显示单个字符。每次调用该方法时，都会显示一个不同的字符。

下一个任务是将此处理程序连接到事件——即订阅事件。为此，你可以使用 += 运算符，以使用你的事件处理程序方法初始化的新委托实例的形式向事件添加处理程序：

```
static void Main(string[] args)
{
    Timer myTimer = new Timer(100);
    myTimer.Elapsed += new ElapsedEventHandler(WriteChar);
}
```

此命令（使用了一种看起来有点奇怪的、特定于委托的语法）会向列表中添加一个处理程序，该处理程序将在 Elapsed 事件被引发时被调用。只要所有处理程序都满足所需条件，你可以向此列表添加任意数量的处理程序。当事件被引发时，每个处理程序都会依次被调用。

Main() 剩下要做的就是启动计时器运行：

```
myTimer.Start();
```

你不希望应用程序在处理任何事件之前终止，因此你让 Main() 方法暂停。最简单的方法是请求用户输入，因为此命令在用户按下某个键之前不会完成处理：

```
ReadKey();
```

尽管 Main() 中的处理在此处实际上停止了，但 Timer 对象中的处理仍在继续。当它引发事件时，会调用 WriteChar() 方法，该方法与 ReadKey() 语句同时运行。包含 System.Threading.Thread.Sleep(200) 语句是为了让计时器有机会开始向控制台应用程序发送消息。

请注意，添加事件处理程序的语法可以使用上一章介绍的方法组概念稍微简化，如下所示：

```
myTimer.Elapsed += WriteChar;
```

最终结果完全相同，但你不必显式指定委托类型；编译器会根据使用它的上下文推断出该类型。然而，许多程序员不喜欢这种语法，因为它降低了可读性——不再可能一眼看出你正在使用哪个委托类型。如果你愿意，可以随意使用这种语法，但在本章中，为了更清楚，你使用的所有委托都将被显式引用。
