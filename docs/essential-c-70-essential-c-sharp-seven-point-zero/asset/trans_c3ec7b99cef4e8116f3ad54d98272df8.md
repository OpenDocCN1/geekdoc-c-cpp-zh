

## 输出 1.4

```
Hey you!
Enter your first name: Inigo
Enter your last name: Montoya
```

在每个提示之后，该程序使用 `System.Console.ReadLine()` 方法获取用户输入的文字，并将其赋值给相应的变量。当第二个 `System.Console.ReadLine()` 赋值完成时，`firstName` 指向值 `Inigo`，而 `lastName` 指向值 `Montoya`。

## 高级主题：System.Console.Read()

除了 `System.Console.ReadLine()` 方法外，还有一个 `System.Console.Read()` 方法。然而，`System.Console.Read()` 方法返回的数据类型是一个整数，对应读取的字符值；如果没有更多可用字符，则返回 -1。为了获取实际字符，必须先将整数转换为字符，如清单 1.15 所示。

### 清单 1.15：使用 System.Console.Read()

```
int readValue;
char character;
readValue = System.Console.Read();
character = (char) readValue;
System.Console.Write(character);
```

`System.Console.Read()` 方法不会在用户按下回车键之前返回输入；即使用户在按下回车键之前输入了多个字符，也不会开始处理这些字符。

在 C# 2.0 及更高版本中，可以使用 `System.Console.ReadKey()`，与 `System.Console.Read()` 相比，它在单次击键后返回输入。它允许开发人员拦截击键并执行操作，例如验证按键或将字符限制为数字。

> 从 2.0 开始
> 结束于 2.0

## 向控制台写入输出

在清单 1.14 中，您使用 `System.Console.Write()` 方法而不是 `System.Console.WriteLine()` 来提示用户输入其名字和姓氏。`System.Console.Write()` 方法不会在显示文本后放置换行符，而是将光标保留在同一行的当前位置。这样，用户输入的任何文本都将与输入提示位于同一行。清单 1.14 的输出展示了 `System.Console.Write()` 的效果。

下一步是将使用 `System.Console.ReadLine()` 获取的值写回控制台。以清单 1.16 为例，程序输出用户的完整姓名。然而，与之前使用 `System.Console.WriteLine()` 不同，这段代码使用了一种略微变化的形式，利用了 C# 6.0 的一个特性，称为**字符串插值**。请注意 `Console.WriteLine` 调用中字符串字面量前的美元符号；它表示将使用字符串插值。输出 1.5 显示了相应的输出结果。

### 清单 1.16：使用字符串插值进行格式化

```csharp
class HeyYou
{
    static void Main()
    {
        string firstName;
        string lastName;

        System.Console.WriteLine("Hey you!");

        System.Console.Write("Enter your first name: ");
        firstName = System.Console.ReadLine();

        System.Console.Write("Enter your last name: ");
        lastName = System.Console.ReadLine();

        System.Console.WriteLine(
            $"Your full name is { firstName } { lastName }.");
    }
}
```

### 输出 1.5

```
Hey you!
Enter your first name: Inigo
Enter your last name: Montoya
Your full name is Inigo Montoya.
```

清单 1.16 没有写出 "Your full name is" 后跟随另一个用于 firstName 的 Write 语句，再第三个用于空格的 Write 语句，最后是用于 lastName 的 WriteLine 语句，而是使用 C# 6.0 的字符串插值写出整个输出。使用字符串插值时，编译器将字符串内花括号内部的内容解释为可以嵌入代码（表达式）的区域，编译器将评估这些表达式并将其转换为字符串。字符串插值允许您一次性完成这些操作，而不是分别执行许多代码片段并在最后将结果组合为一个字符串。这使得代码更容易理解。

在 C# 6.0 之前，C# 使用另一种方法，即**复合格式化**。使用复合格式化时，代码首先提供一个**格式字符串**来定义输出格式——参见清单 1.17。

### 清单 1.17：使用 System.Console.WriteLine() 的复合格式化进行格式化

```csharp
class HeyYou
{
    static void Main()
    {
        string firstName;
        string lastName;

        System.Console.WriteLine("Hey you!");

        System.Console.Write("Enter your first name: ");
        firstName = System.Console.ReadLine();

        System.Console.Write("Enter your last name: ");
        lastName = System.Console.ReadLine();

        System.Console.WriteLine(
            "Your full name is {0} {1}.", firstName, lastName);
    }
}
```

在这个例子中，格式字符串是 `Your full name is {0} {1}`。它标识了字符串中两个用于数据插入的索引占位符。每个占位符对应格式字符串后出现的参数的顺序。

请注意，索引值从零开始。每个插入的参数（称为**格式项**）按照与索引值对应的顺序出现在格式字符串之后。在本例中，由于 `firstName` 是紧跟在格式字符串后的第一个参数，因此它对应索引值 0。类似地，`lastName` 对应索引值 1。

请注意，格式字符串内的占位符不必按顺序出现。例如，清单 1.18 交换了索引占位符的顺序并添加了一个逗号，这改变了姓名的显示方式（参见输出 1.6）。

### 清单 1.18：交换索引占位符及对应变量

```csharp
System.Console.WriteLine("Your full name is {1}, {0}", firstName, lastName);
```

### 输出 1.6

```
Hey you!
Enter your first name: Inigo
Enter your last name: Montoya
Your full name is Montoya, Inigo
```

除了格式字符串中的占位符不必连续出现外，还可以在格式字符串中多次使用同一个占位符。此外，可以省略某个占位符。但是，不能有不对应任何参数的占位符。

### 注意

由于 C# 6.0 风格的字符串插值几乎总是比替代的复合字符串方法更容易理解，因此在本书的其余部分，我们默认使用字符串插值。

## 注释

在本节中，我们通过添加注释来修改清单 1.17 中的程序。这种修改在没有任何改变程序执行方式的情况下；相反，在代码中提供注释可以简单地使代码在原本不直观的地方更加易于理解。清单 1.19 显示了新代码，输出 1.7 显示了相应的输出结果。

### 清单 1.19：为你的代码添加注释

```csharp
class CommentSamples
{
    static void Main()
    {
        string firstName; // 用于存储名字的变量
        string lastName; // 用于存储姓氏的变量

        System.Console.WriteLine("Hey you!");
        System.Console.Write /* 不换行 */ ("Enter your first name: ");
        firstName = System.Console.ReadLine();
        System.Console.Write /* 不换行 */ ("Enter your last name: ");
        lastName = System.Console.ReadLine();

        /* 使用复合格式化向控制台显示问候语。 */
        System.Console.WriteLine("Your full name is {0} {1}", firstName, lastName);

        // 这是
        // 程序清单的结尾
    }
}
```

### 输出 1.7

```
Hey you!
Enter your first name: Inigo
Enter your last name: Montoya
Your full name is Inigo Montoya.
```

尽管插入了注释，编译并执行新程序所产生的输出与之前相同。

程序员使用注释来描述和解释他们正在编写的代码，特别是在语法本身难以理解，或者某个特定算法实现令人意外的地方。由于注释仅对审查代码的程序员相关，编译器会忽略注释，并生成一个不包含任何注释痕迹的程序集，这些注释原本是新源代码的一部分。

表 1.2 展示了四种不同的 C# 注释类型。清单 1.18 中的程序包含了其中两种。

