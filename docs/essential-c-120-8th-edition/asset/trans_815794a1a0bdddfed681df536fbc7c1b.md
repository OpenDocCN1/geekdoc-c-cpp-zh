

## 第一章：介绍 C#

## 进阶主题

### System.Console.Read()

除了 `System.Console.ReadLine()` 方法，还有一个 `System.Console.Read()` 方法。然而，`System.Console.Read()` 方法返回的数据类型是对应于字符值的整数，如果没有更多可用字符，则返回 -1。要获取实际字符，需要将整数强制转换为字符，如列表 1.17 所示。

列表 1.17：使用 System.Console.Read()

```
int readValue;
char character;
readValue = Console.Read();
character = (char)readValue;
Console.Write(character);
```

`Console.Read()` 方法在用户按下 Enter 键之前不会返回输入；如果用户在按下 Enter 键之前输入了多个字符，它不会对单个按键进行任何处理。

你可以使用 `Console.ReadKey()`，它与 `Console.Read()` 不同，在单击按键后就会返回输入。它允许开发者拦截按键并执行诸如按键验证或限制字符为数字的操作。

## 向控制台写入输出

列表 1.16 使用 `Console.Write()` 方法而非 `Console.WriteLine()` 提示用户输入姓和名。`Console.Write()` 方法没有在显示文本后放置换行符，而是将当前位置留在同一行。通过这种方式，用户输入的任何文本将与输入提示处于处于同一行。列表 1.16 的输出演示了 `Console.Write()` 的效果。

- 在 C# 2.0 及以上版本。

```
public class HeyYou
{
    public static void Main()
    {
        string firstName;
        string lastName;

        Console.Write("Enter your first name: ");
        firstName = Console.ReadLine();

        Console.Write("Enter your last name: ");
        lastName = Console.ReadLine();

        Console.WriteLine(
            $"Your full name is {firstName
```

12. C# 6.0 的特性。

对于 `lastName` 的语句，列表 1.18 写出了整个字符串插值输出。通过字符串插值，编译器会解释字符串区域大括号内部的内容，在这些区域中你可以嵌入代码（表达式），编译器将评估并将其转换为字符串。与其单独执行许多代码段并在最后将结果组合成字符串，字符串插值允许你一步完成此操作。这使得代码更容易于理解。

在 C# 6.0 之前，C# 使用不同的方法，提供复合格式化。通过复合格式化，代码提供一个格式化字符串来定义输出格式——见列表 1.19。

列表 1.19：使用 Console.WriteLine() 的复合格式化进行格式

```
public class HeyYou
{
    public static void Main()
    {
        string firstName;
        string lastName;

        Console.WriteLine("Hey you!");

        Console.Write("Enter your first name: ");
        firstName = Console.ReadLine();

        Console.Write("Enter your last name: ");
        lastName = Console.ReadLine();

        Console.WriteLine(
            "Your full name is {0} {1}.", firstName, lastName);
    }
}
```

在此示例中，格式化字符串为 `Your full name is {0} {1}`。它识别了字符串中用于插入数据的两个索引占位符。每个占位符与格式化字符串之后出现的参数顺序对应。

注意索引值从零开始。每个插入的参数（称为格式化项目）按照与索引值对应的顺序出现在格式化字符串之后。在此示例中，由于 `firstName` 是紧随格式化字符串的第一个参数，因此它对应于索引值 0。同样，`lastName` 对应索引值 1。

注意格式字符串中的占位符不需要按顺序出现。例如，列表 1.20 交换了索引占位符的顺序并添加了逗号，这改变了名的显示方式（见输出 1.6）。

## 列表 1.20：交换索引占位符和相应的变量

```
Console.WriteLine("Your full name is {1}, {0}.", firstName, lastName);
```

## 输出 1.6

```
Hey you!
Enter your first name: Inigo
ter your last name: Montoya

Your full name is Montoya, Inigo
```

除了占位符在格式字符串中不连续出现外，还可以在格式中多次使用同一个占位符。此外，可以省略占位符。然而，不允许没有对应参数的占位符。

> 注意
字符串插值几乎总是比替代的复合字符串方法更容易理解，在本书的剩余部分中，请默认使用字符串插值。

## 注释

在本节中，我们通过为列表 1.19 添加注释来修改程序。这种修改没有任何方式会改变程序的执行；相反，在代码中提供注释可以使代码在本身不明显的区域更易理解。列表 1.21 显示了新代码，输出 1.7 显示了相应的输出。

## 列表 1.21：为你的代码注释

## 输出 1.7

Hey you!
Enter your first name: Inigo
Enter your last name: Montoya

Your full name is Inigo Montoya.

尽管插入了注释，编译和执行新程序产生的输出与之前相同。

程序员使用注释来描述和解释他们正在编写的代码，特别是在语法本身难以理解，或者可能某个特定的算法实现令人惊讶的地方。由于注释仅对查看代码的程序员相关，编译器忽略注释并生成不包含任何注释的程序集。

## 控制台输入和输出

表 1.2 显示了四种 C# 注释类型。程序 1.21 包含了其中。

## 表 1.2：C# 注释类型

| 注释类型 | 描述 | 示例 |
| --- | --- | --- |
| 定界符注释 | 正斜杠后跟星号 `/*` 标识定界符注释的开始。结束注释时使用星号后跟正斜杠 `*/`。这种形式的注释可以跨行，也可以嵌入代码行中。 | `/*comment*/` |
| 单行注释 | 由两个连续的正斜杠字符 `//` 定义。编译器将从分隔符到行尾的所有文本视为注释。这种形式被认为是单行的。然而，可以将单行注释连续放置，如列表 1.19 中的注释所示。 | `//comment` |
| XML 定界符注释 | 以 `/**` 开始并以 `*/` 结束的注释被称为 XML 定界符注释。它们与普通定界符注释具有相同特征，但编译器可以将它们放置到单独的文件中。 | `/**comment*/` |
| XML 单行注释 | XML 单行注释以 `//` 开始持续到行尾。此外，编译器可以将它们与 XML 定界符注释一起保存到单独的文件。 | `//comment` |

13. XML 定界符注释在 C# 2.0 中显式添加，但语法兼容 C# 1.0。

## 第一章：介绍 C#

在编程历史上有一个时期，大量的注释意味着一个纪律严明且经验丰富的程序员。现在不再如此了。相反，不需要注释即可阅读的代码比需要注释的代码更有价值。如果开发者发现有必要通过注释来澄清一段代码的作用，他们倾向于重写更清晰的代码，而不是对其进行注释。简单重复清晰代码的注释只会干扰代码、降低其可读性，并增加注释因代码变化而未更新的概率。

> 指南
不要使用注释，除非它们描述了编写代码的人看来不明显的内容。
倾向于编写更清晰的代码，而不是通过注释澄清复杂的算法。

## 初学者主题

可扩展标记语言 (XML) 是一种简单且灵活的分层文本格式。XML 是可扩展的，因为 XML 文档中的信息描述了数据，即元数据。这是一个简单的 XML 文件：

```xml
<?xml version="1.0" encoding="utf-8" ?>
<body>
  <book title="Essential C# 11.0">
    <chapters>
      <chapter title="Introducing C#"/>
      <chapter title="Data Types"/>
      ...
    </chapters>
  </book>
</body>
```

