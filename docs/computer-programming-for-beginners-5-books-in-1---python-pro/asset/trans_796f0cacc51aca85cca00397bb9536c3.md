
```csharp
//declare an event of type delegate
public event BeforeDisplay beforeDisplayEvent;

public DisplayHelper()
{

}
public void DisplayNumber(int x)
{
    //call the delegate method before moving to display
    if (beforeDisplayEvent != null)
        beforeDisplayEvent();

    Console.WriteLine("Number: {0,-12:N0}", x);
}

public void PrintDecimal(int dec)
{
    if (beforeDisplayEvent != null)
        beforeDisplayEvent();

    Console.WriteLine("Decimal: {0:G}", dec);
}
public void DisplayMoney(int amount)
{
    if (beforeDisplayEvent != null)
        beforeDisplayEvent();

    Console.WriteLine("Money: {0:C}", amount);
}

public void DisplayTemperature(int x)
{
    if (beforeDisplayEvent != null)
        beforeDisplayEvent();

    Console.WriteLine("Temperature: {0,4:N1} F", x);
}
public void DisplayHexadecimal(int dec)
{
    if (beforeDisplayEvent != null)
        beforeDisplayEvent();

    Console.WriteLine("Hexadecimal: {0:X}", dec);
}
}
```

*DisplayHelper* 是一个发布者类，负责发布 *beforeDisplay* 事件。在每个 *display* 方法中，它首先检查以确定 *beforeDisplayEvent* 是否不为 null，然后调用 *beforeDisplayEvent()* 方法。

现在我们需要创建一个订阅者。请考虑下面给出的类：

```csharp
using System;

public class MyProgram
{
    public static void Main()
    {
        NumberClass nc = new NumberClass(200);
        nc.DisplayMoney();
        nc.DisplayNumber();
    }
}

class NumberClass
{
    private DisplayHelper _displayHelper;

    public NumberClass(int x)
    {
        _value = x;

        _displayHelper = new DisplayHelper();
        //subscribe to the beforeDisplayEvent event
        _displayHelper.beforeDisplayEvent += displayHelper_beforeDisplayEvent;
    }

    //beforeDisplayEvent handler
    void displayHelper_beforeDisplayEvent()
    {
        Console.WriteLine("BeforeDisplayEventHandler: DisplayHelper will print a value");
    }

    private int _value;

    public int Value
    {
        get { return _value; }
        set { _value = value; }
    }

    public void DisplayMoney()
    {
        _displayHelper.DisplayMoney(_value);
    }

    public void DisplayNumber()
    {
        _displayHelper.DisplayNumber(_value);
    }

    public class DisplayHelper
    {
        // declare a delegate
        public delegate void BeforeDisplay();

        //declare an event of type delegate
        public event BeforeDisplay beforeDisplayEvent;

        public DisplayHelper()
        {

        }

        public void DisplayNumber(int y)
        {
            //call a delegate method before printing
            if (beforeDisplayEvent != null)
                beforeDisplayEvent();

            Console.WriteLine("Number: {0,-12:N0}", y);
        }

        public void DisplayDecimal(int dec)
        {
            if (beforeDisplayEvent != null)
                beforeDisplayEvent();

            Console.WriteLine("Decimal: {0:G}", dec);
        }

        public void DisplayMoney(int amount)
        {
            if (beforeDisplayEvent != null)
                beforeDisplayEvent();

            Console.WriteLine("Money: {0:C}", amount);
        }

        public void DisplayTemperature(int y)
        {
            if (beforeDisplayEvent != null)
                beforeDisplayEvent();

            Console.WriteLine("Temperature: {0,4:N1} F", y);
        }

        public void DisplayHexadecimal(int dc)
        {
            if (beforeDisplayEvent != null)
                beforeDisplayEvent();

            Console.WriteLine("Hexadecimal: {0:X}", dc);
        }
    }
}
```

该代码返回以下结果：

![](img/239ff1e8a63502805c86c4dfbd71509a_633_0.png)

所有订阅者都必须有一个处理程序函数，该函数将在发布者引发事件后被调用。

## 第22章：提示和重要资源

尽管我相信，如果你按照本书的步骤学习，你将在短时间内非常透彻且牢固地掌握 C#，但毫无疑问，你可能仍然有一些尚未得到解答的问题。

我们如今生活在一个技术娴熟的世界，其美妙之处在于，这本书并不是你学习和掌握 C# 编程与编码的唯一资源。

我相信你现在已经感到准备就绪，并且能够应对许多你希望用 C# 形式编码解决的挑战；你可能会来到一个十字路口，不确定解决问题的下一个潜在步骤是什么。本章应当作为你的指南，帮助你找到那些在本书页面中未得到解答的问题的答案。

首先，我鼓励你检查代码中是否有空格或大小写方面的简单错误。

有时，如果你习惯用另一种语言编码，你可能会不小心在 C# 中本应使用分号的地方输入了句点，甚至在本不该使用括号的地方输入了括号。

这些是我觉得最令人沮丧的错误类型，而且通常也是我犯过的错误。本质上，当你遇到一个似乎不断给你错误消息的沮丧节点时，一定要反复检查你的工作。

另外，如果你尝试了这个策略但仍不奏效，并且你准备放弃——那就休息一下！在你让自己放松、把注意力从项目上移开之后，再回到你的项目。当你回来并以焕然一新的眼光看待它时，你可能会发现自己的错误所在。

我还会利用的另一种资源是专门针对 C# 的在线论坛。尽管一些编程论坛提供了很好的通用建议，但我鼓励你用 Google 搜索“C# help forum”之类的内容，以便找到其他可能对如何解决问题有明智建议的人。

很可能你并不是唯一一个遇到过某个阻碍你完成项目某一部分的减速带的人。利用互联网的力量，这些方式可以成为快速找到答案的绝佳且便捷的途径。

尽管我已经提到了接下来的这些资源，但我想重申代码编辑器和库可能有多么重要。

正如在任何编程语言中一样，你可以在库中找到看似无穷无尽的答案，这些答案将允许你为许多不同情况编码。然而，正如我之前建议的那样，请在你冒险进入使用代码的世界之前，牢固掌握编码和编程的过程。

如果代码中发生了变化，而你找不到错误，你的程序或项目可能会遭受无法修复的损害。代码编辑器可以帮助你在让代码上线之前发现这些错误，因此我强烈建议你持续利用这一资源，直到你成为 C# 大师——也许即使到那时也要使用，以防你成为人为错误的受害者。

如果你发现你需要对本书中的任何内容或超出本书范围的内容有更好的视觉理解——我鼓励你访问我最喜欢的视频网站——YouTube！

只需搜索你在编码和编程过程中试图弄明白的关键短语或单词，我保证你会找到有用的视频。有时，它可能不是你遇到的第一条视频，但它一定会在那里。

你可能已经有一个偏好的 YouTuber，你会去找他用另一种语言编写的示例——也许可以去看看他或她订阅的其他用户，看看他们的内容是否对你有帮助。

永远不要认为仅仅因为你正在挣扎，你的整个项目就结束了。

我可以根据自己的亲身经历告诉你，当这类问题出现时，让自己充分探索并解决问题，会给你一个机会在你的大脑中创建新的通路，这些通路将在你未来遇到困难时大有裨益。

回想一下你在生活中或编程经历中解决其他问题的方式，并让自己思考如何以及为什么可以将其应用到当前情况中。

在了解自己如何思考以及想要实现什么方面，你是自己最好的盟友。尽你所能利用你的资源，尽可能变得博学——知识和学习的力量是一项非常了不起的技能。

编程和编码可以被视为一种解决问题的事情，你用它来创建执行特定目的的程序，从而让你和他人的生活更轻松。始终朝着适合你技能组合的可实现目标努力，同时继续推动自己学习更多并达到下一个能力水平。

你可以从以下参考链接获取有关 C# 语言的更详细信息。

- Visual Studio 应用程序 – 用于创建 C# 应用程序的 IDE。
- C#（编程指南）– C# 编程语言概述
- C# 编程 – 解释使用 .NET 框架的 C# 功能相关信息
- Mono – 使用该软件可以轻松创建跨平台应用程序。

