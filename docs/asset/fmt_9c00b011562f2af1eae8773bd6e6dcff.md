
> 与与其他常量的惯例一样，你可能更倾向于使用全大写字母和下划线命名枚举常量以提高可读性，就像这里的 `DayOfWeek` 枚举。这将枚举名称与变量区分开来。然而，C# 的开发者在他们的在线文档和语言内置方法中经常违反这一点。例如，`FontStyle` 枚举包含混合驼峰命名（mixedCase）的常量，如 `Bold` 和 `Italic`。当你创建枚举时，应该遵循你的导师或主管偏好的惯例。另一个惯例是使用单数名词或短语作为枚举标识符。换句话说，`DayOfWeek` 比 `DaysOfWeek` 更好。

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_107_0.png)

## 如果你想让列表第一个枚举常量具有 0 以外的值，可以像下面赋值：

```csharp
enum DayOfWeek
{
    SUNDAY = 1, MONDAY, TUESDAY, WEDNESDAY,
    THURSDAY, FRIDAY, SATURDAY
}
```

在这种情况下，`SUNDAY` 是 1，`MONDAY` 是 2，`TUESDAY` 是 3，依此类推。

作为另一种选择，你可以为每个枚举赋值，如下所示：

```csharp
enum SpeedLimit
{
    SCHOOL_ZONE_SPEED = 20,
    CITY_STREET_SPEED = 30,
    HIGHWAY_SPEED = 55
}
```

枚举中的名称必须是唯一的，但分配的值并不一定。当你创建枚举时，它清晰地标记了哪些值是允许的。对于整数值，使用枚举可以让你的代码更具自解释性。

> 像与其他常量的惯例一样，你可能更倾向于使用全大写字母和下划线来命名枚举常量以提高可读性，就像这里的 `DayOfWeek` 枚举。`Intellisense` 提供了更多信息。

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_108_0)

创建枚举后，你可以声明该枚举类型的变量并对其赋值。例如，你可以使用以下语句声明 `payrollDay` 为 `DayOfWeek` 类型并赋值：

```csharp
DayOfWeek payrollDay;
payrollDay = DayOfWeek.TUESDAY;
```

（注）

作为另一种选择，你可以使用类型转换将枚举转换为另一种数据类型，或将整数类型转换为枚举值。例如，以下是有效的语句：

```csharp
int shipDay;
DayOfWeek deliverDay;
shipDay = (int)DayOfWeek.TUESDAY;
deliverDay = (DayOfWeek)shipDay;
```

使用前面的示例，你可以通过以下语句显示 5 和 `THURSDAY`：

```csharp
WriteLine(shipDay);
WriteLine(deliverDay);
```

创建枚举类型为你提供了许多优势。例如，`DayOfWeek` 枚举通过以下方式改进了你的程序：

- 如果你不创建枚举类型，你可以创建另一种类型来表示日期，可能会对这些值应用无效的行为。例如，如果你使用整数表示日期，你可以对日期进行乘法或除法，这在逻辑上是不行的。使用枚举使得类型安全。类型安全是指允许适当行为的数据类型。

- 枚举常量提供了一种形式的自文档。阅读你程序的人可能会将 3 误认为日期值，但当你使用标识符 `WEDNESDAY` 时，困惑会减少。

> 这些讨论只是对枚举的简单介绍。在你学习 C# 的阶段，使用枚举的优势是有限的。枚举对于 `switch` 语句特别有用，你将在“制作决策”章节中学习它。

![](img/7516c1fecf7bbbe7afb10cf209b17ae3_109_0.png)

# 接收控制台输入

允许用户输入的程序是交互式程序。你可以使用 `ReadLine()` 方法来创建一个从键盘接受用户输入的交互式程序。该方法会接受用户输入的所有字符，直到用户按下回车键为止。这些字符被赋值给字符串。例如，以下语句接受用户的输入并将其存储在变量 `myString` 中：

```
myString = ReadLine();
```

`Read()` 方法与 `ReadLine()` 方法类似。`Read()` 仅从输入流中读取一个字符，而 `ReadLine()` 则读取输入流中的每个字符，直到用户按下回车键。

- 在 C# 6.0 发布之前，需要使用限定名称 `Console.ReadLine()` 和 `Console.Read()`。然而，就像 `WriteLine()` 和 `Write()` 一样，你现在可以在文件顶部包含 `using static Console;`，允许你使用更短的方法 `ReadLine()` 和 `Read()`。

如果你将输入值用作字符串以外的类型，则必须使用转换方法将输入字符串转换为正确的类型。转换字符串有两种方法可供——`Convert` 类和 `Parse()` 方法。

## 使用 Convert 类

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

图 2-20 `InteractiveSalesTax` 程序

在图 2-20 中，提示结尾的角括号不是必需；它们仅仅是为了美观。你可能喜欢其他标点符号，如冒号、省略号或连字符来表示需要输入。

```
Enter the price of an item >> 28.77
With a tax rate of 0.06, a $28.77 item costs $1.73 more.
```

图 2-21 `InteractiveSalesTax` 程序的典型执行

作为快捷方式，你可以避免在图 2-20 的程序中声明和使用额外的字符串变量 `itemPriceAsString`。相反，你可以通过嵌套 `ReadLine()` 和 `ToDouble()` 方法调用来接受并转换输入字符串，如下：

```csharp
itemPrice = Convert.ToDouble(ReadLine());
```

表 2-6 显示了你可以使用的 `Convert` 类方法，用于将字符串转换为有用的数据类型。这些方法在名称中使用了系统类型（也是运行时类型）。例如，回想表 2-1，`int` 的“正式”名称是 `Int32`，所以你用于将字符串转换为 `int` 的方法是 `Convert.ToInt32()`。

# 第2章 使用数据

| 方法 | 描述 |
| --- | --- |
| `ToBoolean()` | 将字符串转换为其布尔值 |
| `ToByte()` | 将指定值转换为 8 位无符号整数 |
| `ToChar()` | 将指定值转换为 Unicode 字符 |
| `ToDecimal()` | 将指定值转换为小数 |
| `ToDouble()` | 将指定值转换为双精度浮点数 |
| `ToInt16()` | 将指定值转换为 16 位有符号整数 (short) |
| `ToInt32()` | 将指定值转换为 32 位有符号整数 (int) |
| `ToInt64()` | 将指定值转换为 64 位有符号整数 (long) |
| `ToSingle()` | 将指定值转换为单精度浮点数 |
| `ToString()` | 将指定值转换为其等效字符串表示 |

**表 2-6** 选定的 `Convert` 类方法

## 使用 Parse() 方法

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

   `int age = Convert.ToInt32(ReadLine());`

2. 以下是有效的：

   `double payRate = Convert.ToDouble(ReadLine());`

3. 以下是有效的：

   `int dependents = int.Parse(ReadLine());`

整数是 `ToInt32()`，而不是 `Int()`。

错误的语句是 #1。使用 `Convert` 类方法将字符串转换为整数。

## 你来做

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

图 2-22 `InteractiveAddition` 程序的典型执行

## 章节总结

- 常数是在程序编译后无法更改的数据值；而变量中的值可以改变。C# 提供了 15 种内置数据类型。变量声明包括一个数据类型、一个标识符、一个可选的赋值值和一个分号。

- 你可以在 `WriteLine()` 或 `Write()` 方法调用中使用变量名来显示变量。为了方便生成输出，你可以使用格式化字符串将字符串和变量值合并到单个 `Write()` 或 `WriteLine()` 语句中。

- C# 支持九种整型数据类型：`byte`、`sbyte`、`short`、`ushort`、`int`、`uint`、`ulong` 和 `char`。

- C# 支持三种浮点型数据类型：`float`、`double` 和 `decimal`。你可以使用格式和精度说明符将浮点数据显示为指定数量的小数位。

- 你使用使用二元算术运算符 `+`、`-`、`*` 和 `%` 来处理程序中的值。除非使用括号覆盖正常优先级，否则乘法、除法和取余运算始终在加减法之前进行。C# 提供了几种快捷算术运算符，包括二元运算符 `+=`、`-=`、`*=`、`/=` 以及一元前缀增 (`++`) 和 减 (`--`) 运算符。

- `bool` 变量只能包含两个值——`true` 或 `false`。C# 支持六种比较运算符：`>`、`<`、`<=`、 `>=`、`==` 和 `!=`。表达式可以返回布尔值。

- 当对相同类型的变量或常量进行算术运算时，结果保留该类型。当你对不同类型的操作数进行算术运算时，C# 为结果提供一个统一类型，并隐式将非形成的操作数转换为统一类型。你可以通过执行强制转换来显式覆盖 C# 强制实施的统一类型。

- 你使用 `char` 类型来存储任何单个字符。你将常量字符值放在字符串引号内——包括空格或制表符等非打印字符——并在 `char` 变量中使用。为了存储这些字符，你必须使用以反斜杠开头的义序列。

- 在 C# 中，你使用 `string` 类型来存储一系列字符。字符串的值用双引号表示。虽然字符串字面量可以使用 `==` 和 `!=` 比较运算符，但你也可以使用 `String` 类所属的 `Equals()`、`Compare()`、`CompareTo()` 和 `Substring()` 方法以及 `Length` 属性。

# 第2章 使用数据

- 命名常量是值无法更改的程序标识符。按照习惯，标识符全大写，并插入下划线以提高可读性。枚举是命名常量的列表，默认为整数，且列表通常持有连续的值。

- 你可以使用 `Readline()` 方法接收用户输入。通常，你必须使用 `Convert` 类的方法将输入字符串转换为可用的数据类型。

## 关键术语

**常量 (Constant)** 描述值固定的数据项。

**字面量常量 (literal constant)** 是在每次使用时都按字面取的值。

**数据类型 (data type)** 描述数据项的格式和大小，并定义了对该项可以执行的操作类型。

**内置类型 (Intrinsic types)** 是数据的基本类型；C# 提供了 15 种内置类型。

**别名 (alias)** 是某物的另一个名称。

**简单类型 (simple type)** 是 C# 中的以下类型之一：`byte`、`sbyte`、`short`、`ushort`、`int`、`uint`、`ulong`、`float`、`decimal`、`char` 和 `bool`。

**Unicode** 是一种用于字符的 16 位编码方案。

**变量声明 (variable declaration)** 是命名变量的语句；它包括一个数据类型、一个标识符、一个可选的赋值运算符和赋值值，以及一个结束的分号。

**赋值运算符 (assignment operator)** 是等号 (`=`)；赋值右侧的任何值都会被赋值给或由左侧变量获取。

**初始化 (initialization)** 是在声明变量时进行的赋值。

**int** 数据类型存储一个整数。
