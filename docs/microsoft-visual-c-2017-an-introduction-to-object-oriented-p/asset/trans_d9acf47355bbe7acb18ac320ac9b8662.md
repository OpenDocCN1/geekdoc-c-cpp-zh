

# 接收控制台输入

允许用户输入的程序是交互式程序。你可以使用 `ReadLine()` 方法来创建一个从键盘接受用户输入的交互式程序。该方法会接受用户输入的所有字符，直到用户按下回车键为止。这些字符被赋值给字符串。例如，以下语句接受用户的输入并将其存储在变量 `myString` 中：

```
myString = ReadLine();
```

`Read()` 方法与 `ReadLine()` 方法类似。`Read()` 仅从输入流中读取一个字符，而 `ReadLine()` 则读取输入流中的每个字符，直到用户按下回车键。

- 在 C# 6.0 发布之前，需要使用限定名称 `Console.ReadLine()` 和 `Console.Read()`。然而，就像 `WriteLine()` 和 `Write()` 一样，你现在可以在文件顶部包含 `using static Console;`，允许你使用更短的方法 `ReadLine()` 和 `Read()`。

如果你将输入值用作字符串以外的类型，则必须使用转换方法将输入字符串转换为正确的类型。转换字符串有两种方法可供——`Convert` 类和 `Parse()` 方法。

# 使用 Convert 类

图 2-20 显示了一个交互式程序，它提示用户输入价格并计算 6% 的销售税。程序在屏幕上显示“输入物品价格：”。查看给用户的指令是如何作为提示的。注意程序开头出现了两个语句：

- 使用 `using System;` 以包含 `Convert` 类
- 使用 `static System.Console;` 以包含 `ReadLine()` 和 `WriteLine()` 方法

注意图 2-20 中的程序使用 `Write()` 语句作为提示，而不是 `WriteLine()` 语句，这样输出就会与提示在同一行显示。此外，注意提示包含在结束引号之前，这样提示就不会在屏幕上让用户的输入显得拥挤。

在提示之后，`ReadLine()` 语句接受一个字符字符串并将其赋值给变量 `itemPriceAsString`。在计算税费之前，必须将此值转换为数字。这种转换是通过使用阴影语句中的 `Convert` 类 `ToDouble()` 方法完成的。图 2-21 显示了程序的典型执行过程，用户输入了 28.77 作为输入值。

```csharp
using static System.Console;
class InteractiveSalesTax
{
    static void Main()
    {
        const double TAX_RATE = 0.06;
        string itemPriceAsString;
        double itemPrice;
        double total;
        Write("Enter the price of an item >> ");
        itemPriceAsString = ReadLine();
        itemPrice = Convert.ToDouble(itemPriceAsString);
        total = itemPrice * TAX_RATE;
        WriteLine("With a tax rate of {0}, a {1} item " + 
"costs {2} more.", TAX_RATE, itemPrice.ToString("C"), total.ToString("C"));
    }
}
```

图 2-20 InteractiveSalesTax 程序

在图 2-20 中，提示结尾的角括号不是必需；它们仅仅是为了美观。你可能喜欢其他标点符号，如冒号、省略号或连字符来表示需要输入。

```
Enter the price of an item >> 28.77
With a tax rate of 0.06, a $28.77 item costs $1.73 more.
```

图 2-21 InteractiveSalesTax 程序的典型执行

作为快捷方式，你可以避免在图 2-20 的程序中声明和使用额外的字符串变量 `itemPriceAsString`。相反，你可以通过嵌套 `ReadLine()` 和 `ToDouble()` 方法调用来接受并转换输入字符串，如下：

```csharp
itemPrice = Convert.ToDouble(ReadLine());
```

表 2-6 显示了你可以使用的 `Convert` 类方法，用于将字符串转换为有用的数据类型。这些方法在名称中使用了系统类型（也是运行时类型）。例如，回想表 2-1，`int` 的“正式”名称是 `Int32`，所以你用于将字符串转换为 `int` 的方法是 `Convert.ToInt32()`。

# 第2章 使用数据

| 方法 | 描述 |
| --- | --- |
| ToBoolean() | 将字符串转换为其布尔值 |
| ToByte() | 将指定值转换为 8 位无符号整数 |
| ToChar() | 将指定值转换为 Unicode 字符 |
| ToDecimal() | 将指定值转换为小数 |
| ToDouble() | 将指定值转换为双精度浮点数 |
| ToInt16() | 将指定值转换为 16 位有符号整数 (short) |
| ToInt32() | 将指定值转换为 32 位有符号整数 (int) |
| ToInt64() | 将指定值转换为 64 位有符号整数 (long) |
| ToSingle() | 将指定值转换为单精度浮点数 |
| ToString() | 将指定值转换为其等效字符串表示 |

**表 2-6** 选定的 Convert 类方法

# 使用 Parse() 方法

作为 `Convert` 类方法的替代方案，你可以使用 `Parse()` 方法将字符串转换为数字。例如，在图 2-20 的 `InteractiveSalesTax` 程序中，将字符串转换为 `double`，可以将 `Convert.ToDouble()` 语句替换为以下任一 `Parse()` 方法语句：

```csharp
itemPrice = double.Parse(itemPriceAsString);
```

之前的两个语句都使用了 `Double` 类中定义的 `Parse()` 方法。你可以使用系统名 `Double` 或其相同的类型名 `double`。任一版本都会括号内的字符串参数转换为正确的数据类型。

其他数据类型也存在类似的方法，例如 `int.Parse()` 和 `boolean.Parse()`。例如，以下语句中的任一语句都会读取一个整数，并使用临时字符串持有输入值将其存储在名为 `score` 的变量中：

```csharp
score = int.Parse(ReadLine());
score = Int32.Parse(ReadLine());
```

`Convert` 和 `Parse()` 技术之间存在一些性能差异，这些差异是微小且相对技术性的。当你学习更多 C# 时，应该使用你的教师或组织首选的方法。

“parse”（解析）一词意味着将其分解成组成部分。语法学家谈论“解析句子”，即对其进行解构以描述其语法组件。解析字符串则是将其转换为数值等效值。

# 两个真理和一个谎言

# 接收控制台输入

- 1. 以下是有效的：
   int age = Convert.ToInt32(ReadLine());
2. 以下是有效的：
   double payRate = Convert.ToDouble(ReadLine());
3. 以下是有效的：
   int dependents = int.Parse(ReadLine());

整数是 `ToInt32()`，而不是 `Int()`。
错误的语句是 #1。使用 `Convert` 类方法将字符串转换为整数。

# 你来做

编写一个接受用户输入的程序
在接下来的步骤中，你将编写一个允许用户输入两个整数的交互式程序。程序计算并显示它们的和。

- 1. 打开一个名为 `InteractiveAddition` 的新文件，输入 `Main()` 方法的前几行：

```csharp
using System;
using static System.Console;
class InteractiveAddition
{
    static void Main()
    {
        (继续)
```

# 第2章 使用数据

(继续)

- 2. 添加用于接受用户输入的两个字符串声明。此外，声明三个用于字符串等效值的整数。

```csharp
string name, firstString, secondString;
int first, second, sum;
```

- 3. 提示用户输入姓名，将其接收到字符串 `name` 中，然后向用户显示个性化的问候，以及对第一个整数的提示。

```csharp
Write("Enter your name... ");
name = ReadLine();
Write("Hello! Enter the first integer... ", name);
```

- 4. 以字符串询问用户输入，然后将输入字符串转换为整数。

```csharp
firstString = ReadLine();
first = Convert.ToInt32(firstString);
```

- 5. 添加提示并接收第二个字符串的语句，将其转换为整数。

```csharp
Write("Enter the second integer... ");
secondString = ReadLine();
second = Convert.ToInt32(secondString);
```

- 6. 将两个整数的和赋值给变量 `sum` 并显示所有值。添加 `Main()` 方法的右大括号和类的右大括号。

```csharp
sum = first + second;
WriteLine("{0}, the sum of {1} and {2} is {3}",
name, first, second, sum);
}
}
```

- 7. 保存、编译并运行程序。在提示时，提供你的姓名和任何整数整数，并确认结果显示正确。图 2-22 显示了程序的典型运行。

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_114_0.png)

图 2-22 InteractiveAddition 程序的典型执行

