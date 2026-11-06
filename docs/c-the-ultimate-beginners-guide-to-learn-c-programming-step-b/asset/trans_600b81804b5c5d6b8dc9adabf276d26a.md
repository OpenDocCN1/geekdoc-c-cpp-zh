
```csharp
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
        // subscribe to the beforeDisplayEvent event
        _displayHelper.beforeDisplayEvent += displayHelper_beforeDisplayEvent;
    }

    // beforeDisplayEvent handler
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
}

public class DisplayHelper
{
    // declare a delegate
    public delegate void BeforeDisplay();

    // declare an event of type delegate
    public event BeforeDisplay beforeDisplayEvent;

    public DisplayHelper()
    {

    }

    public void DisplayNumber(int y)
    {
        // call a delegate method before printing
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

        Console.WriteLine("Temperature: {0:4:N1} F", y);
    }

    public void DisplayHexadecimal(int dc)
    {
        if (beforeDisplayEvent != null)
            beforeDisplayEvent();

        Console.WriteLine("Hexadecimal: {0:X}", dc);
    }
}
```

代码返回以下结果：

```text
BeforeDisplayEventHandler: DisplayHelper will print a value
Money: $200.00
BeforeDisplayEventHandler: DisplayHelper will print a value
Number: 200
```

所有订阅者都必须有一个处理函数，该函数将在发布者引发事件后被调用。

## 结论

既然本书已经接近尾声，你现在已经掌握了成为一名优秀 C# 程序员和编码人员所需的全部信息和技能知识。对我来说重要的是，你能够把本书作为你技能的基础。我努力提供我认为既全面又易于理解的指南。如果没有像 C# 这样的语言，我们在个人和商业生活中都不可能拥有如此惊人的技术。

当你思考编程这样的技术技能在你的生活中创造的机会时，我相信它是一项无价的技能。了解计算机系统设置的最基础知识，可以在职业意义上为你打开大门，带来更复杂和高薪的工作。

然而，在你的个人生活中，你可以运用批判性思维和解决问题的技能，帮助提升你在计算机上的游戏体验，或在技术以外的其他领域中使用这些技能。以你学习 C# 的速度，你应该对自己的成就感到非常自信和满足！

并非每个人都能在一个月内学会一门全新的语言，而你通过探索一个新的虚拟世界，刚刚简单轻松地做到了这一点。这是一项你应该感到高兴的成就，并且真正开始创建你渴望的项目。作为一门面向对象的语言，我相信你一定有一些出色的新想法，可以为软件社区做出贡献。或者，也许你只是希望能够操作你拥有的 Windows 计算机！

我在本书中分解的描述和章节，应该让你能够以这样一种方式掌握并连接 C# 的不同片段和部分：当你读到这个最终结论时，你能够感觉自己可以把知识传授给别人。

我希望这门语言向你表明，它鼓励游戏编程，通过这门语言中使用的许多不同途径来定义和分离可能相互接触（例如类和语句）但不可互换的不同方面。

当你逐渐适应这些细微差别时，它可能看起来令人不知所措、令人困惑——你越是测试自己的技能并将代码示例付诸实践，你就越会意识到它们为你提供的全部影响和优势。

感谢你拿起我的书，并给它一个机会教你一些东西

## 参考文献

- AG, A. (n.d.). *C# /.NET 中的委托和事件。* [在线] Akadia.com。可从以下网址获取：https://www.akadia.com/services/dotnet_delegates_and_events.html [访问于 2019年2月15日]。
- Bodnar, J. (2019). *C# 中的方法——使用 CSharp 方法。* [在线] Zetcode.com。可从以下网址获取：http://zetcode.com/lang/csharp/methods/ [访问于 2019年2月15日]。
- Bodnar, J. (2019). *C# 中的运算符——描述 CSharp 运算符和表达式。* [在线] Zetcode.com。可从以下网址获取：http://zetcode.com/lang/csharp/operators/ [访问于 2019年2月15日]。
- Codescracker.com. (n.d.). *C# 程序结构。* [在线] 可从以下网址获取：https://codescracker.com/c-sharp/c-sharp-program-structure.htm [访问于 2019年2月15日]。
- Csharp.net-informations.com. (n.d.). *C# 文件操作教程。* [在线] 可从以下网址获取：http://csharp.net-informations.com/file/csharp-file-tutorial.htm [访问于 2019年2月15日]。
- Csharp.net-tutorials.com. (n.d.). *变量——完整的 C# 教程。* [在线] 可从以下网址获取：https://csharp.net-tutorials.com/basics/variables/ [访问于 2019年2月15日]。
- Docs.microsoft.com. (2015). *数组——C# 编程指南。* [在线] 可从以下网址获取：https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/arrays/ [访问于 2019年2月15日]。
- Docs.microsoft.com. (2015). *强制转换和类型转换——C# 编程指南。* [在线] 可从以下网址获取：https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/types/casting-and-type-conversions [访问于 2019年2月15日]。
- Docs.microsoft.com. (2015). *委托——C# 编程指南。* [在线] 可从以下网址获取：https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/delegates/ [访问于 2019年2月15日]。
- Docs.microsoft.com. (2015). *goto 语句——C# 参考。* [在线] 可从以下网址获取：https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/goto [访问于 2019年2月15日]。
- Docs.microsoft.com. (2015). *传递参数——C# 编程指南。* [在线] 可从以下网址获取：https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/passing-parameters [访问于 2019年2月15日]。
- Docs.microsoft.com. (2018). *类——C# 编程指南。* [在线] 可从以下网址获取：https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/classes [访问于 2019年2月15日]。
- Docs.microsoft.com. (2018). *默认值表——C# 参考。* [在线] 可从以下网址获取：https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/default-values-table [访问于 2019年2月15日]。
- Docs.microsoft.com. (2018). *使用线程和线程处理。* [在线] 可从以下网址获取：https://docs.microsoft.com/en-us/dotnet/standard/threading/using-threads-and-threading [访问于 2019年2月15日]。
- Docs.microsoft.com. (n.d.). *BinaryReader 类 (System.IO)。* [在线] 可从以下网址获取：https://docs.microsoft.com/en-us/dotnet/api/system.io.binaryreader?view=netframework-4.7.2 [访问于 2019年2月15日]。
- Docs.microsoft.com. (n.d.). *BinaryWriter 类 (System.IO)。* [在线] 可从以下网址获取：https://docs.microsoft.com/en-us/dotnet/api/system.io.binarywriter?view=netframework-4.7.2 [访问于 2019年2月15日]。
- Docs.microsoft.com. (n.d.). *File.AppendText(String) 方法 (System.IO)。* [在线] 可从以下网址获取：https://docs.microsoft.com/en-us/dotnet/api/system.io.file.appendtext?view=netframework-4.7.2 [访问于 2019年2月15日]。
- Download.microsoft.com. (n.d.). *Microsoft 下载中心：Windows、Office、Xbox 及更多。* [在线] 可从以下网址获取：http://download.microsoft.com/ [访问于 2019年2月15日]。
- En.wikipedia.org. (2019). *C Sharp（编程语言）。* [在线] 可从以下网址获取：https://en.wikipedia.org/wiki/C_Sharp_(programming_language) [访问于 2019年2月15日]。
- GeeksforGeeks. (n.d.). *C# | 数组 - GeeksforGeeks。* [在线] 可从以下网址获取：https://www.geeksforgeeks.org/c-sharp-arrays/ [访问于 2019年2月15日]。
- GeeksforGeeks. (n.d.). *C# | 方法 - GeeksforGeeks。* [在线] 可从以下网址获取：https://www.geeksforgeeks.org/c-sharp-methods/ [访问于 2019年2月15日]。
- Guru99.com. (n.d.). [在线] 可从以下网址获取：https://www.guru99.com/c-sharp-data-types.html [访问于 2019年2月15日]。
- Heydrick, C. (2014). *C# 结构体大小。* [在线] Chris Heydrick：Serial Hobbyist。
