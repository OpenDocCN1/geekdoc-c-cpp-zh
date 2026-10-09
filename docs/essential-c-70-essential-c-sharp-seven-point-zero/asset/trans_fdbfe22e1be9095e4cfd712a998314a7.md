
在 C# 中，你可以在字符串前使用 `@` 符号，表示反斜杠不应被解释为转义序列的开头。由此产生的**逐字字符串字面量**（verbatim string literal）不会重新解释反斜杠字符。当使用 `@` 字符串语法时，空白符也会按原样保留。例如，列表 2.14 中的三角形在控制台中会按照输入的形式原样显示，包括反斜杠、换行符和缩进。输出 2.10 展示了运行结果。

### 列表 2.14：使用逐字字符串字面量显示三角形

```csharp
class Triangle
{
    static void Main()
    {
        System.Console.Write(@"begin
          ^
         / \\
        /___\\"
                  end");
    }
}
```

### 输出 2.10

![](img/ef6a8a417630b222bfb3f3b949facff0_94_0.png)

如果没有 `@` 字符，这段代码甚至无法编译。事实上，即使将形状改为正方形并去掉了反斜杠，代码仍然无法编译，因为未在字符串前添加 `@` 符号的字符串不能直接包含换行符。

逐字字符串支持的唯一转义序列是 `""`，它表示双引号，且不会终止字符串。

## 语言对比：C++——编译时的字符串连接

与 C++ 不同，C# 不会自动连接字符串字面量。例如，你不能像下面这样指定字符串字面量：

```
"Major Strasser has been shot."
"Round up the usual suspects."
```

相反，字符串连接需要使用加号运算符。（不过，如果编译器能在编译时计算出结果，生成的 CIL 代码将是一个单一的字符串。）

如果同一个字符串字面量在程序集中出现多次，编译器只会在程序集内定义一次该字符串，所有变量都将引用同一个字符串。这样，如果同一个包含数千个字符的字符串字面量在代码中多次出现，生成的程序集的大小将仅反映其中一个的大小。

## 字符串插值

如第 1 章所述，从 C# 6.0 开始，使用字符串插值格式时，字符串可以支持嵌入表达式。字符串插值语法在逐字字符串字面量前加一个美元符号，然后在花括号内嵌入表达式。以下是一个示例：

```csharp
System.Console.WriteLine($"Your full name is {firstName} {lastName}.");
```

其中 `firstName` 和 `lastName` 是引用变量的简单表达式。请注意，可以通过在 `@` 符号前指定 `$` 来将逐字字符串字面量与字符串插值结合使用，如下例所示：

```csharp
System.Console.WriteLine(@"Your full name is:
{ firstName } { lastName }");
```

由于这是一个逐字字符串字面量，文本会在两行输出。但是，你可以通过在花括号内放置换行符，在代码中制造类似的换行而不影响输出中的换行，如下所示：

```csharp
System.Console.WriteLine($@"Your full name is: {
firstName } { lastName }");
```

请注意，即使只是在花括号内放置换行符，仍然需要 `@` 符号。

## 高级主题

### 理解字符串插值的内部机制

字符串插值是调用 `string.Format()` 方法的简写方式。例如，像这样的语句：

```csharp
System.Console.WriteLine($"Your full name is { firstName } { lastName }.");
```

将被转换为 C# 中等价的：

```csharp
object[] args = new object[] { firstName, lastName }; 
Console.WriteLine(string.Format("Your full name is {0} {1}.", args));
```

这与复合字符串的工作方式相同，保留了本地化支持，并且不会通过字符串引入编译后的代码注入。

### 字符串方法

与 `System.Console` 类型类似，`string` 类型包含若干方法。例如，有用于格式化、连接和比较字符串的方法。

表 2.5 中的 `Format()` 方法的行为类似于 `Console.Write()` 和 `Console.WriteLine()` 方法，不同之处在于 `string.Format()` 将结果返回给调用者，而不是在控制台窗口中显示结果。当然，随着字符串插值的使用，对 `string.Format()` 的需求大幅减少（除了本地化支持外）。但在底层，字符串插值最终编译为利用 `string.Format()` 的 CIL 代码。

表 2.5 中的所有方法都是**静态**的。这意味着，要调用这些方法，需要在方法名前加上包含该方法所属类型的名称（例如 `string`）。然而，正如本章后面所示，`string` 类中的一些方法是**实例**方法。实例方法使用变量名（或其他对实例的引用）而不是类型名称作为前缀。表 2.6 展示了其中的一些方法及其示例。

### 表 2.5：*string* 静态方法

| 语句 | 示例 |
| :--- | :--- |
| `static string string.Format(string format, ...)` | `string text, firstName, lastName;`<br>`//...`<br>`text = string.Format("Your full name is {0} {1}.", firstName, lastName);`<br>`// 显示 "Your full name is <firstName> <lastName>."`<br>`System.Console.WriteLine(text);` |
| `static string string.Concat(string str0, string str1)` | `string text, firstName, lastName;`<br>`//...`<br>`text = string.Concat(firstName, lastName);`<br>`// 显示 "<firstName><lastName>"，注意名字之间没有空格`<br>`System.Console.WriteLine(text);` |
| `static int string.Compare(string str0, string str1)` | `string option;`<br>`//...`<br>`// 区分大小写的字符串比较`<br>`int result = string.Compare(option, "/help");`<br>`// 显示：`<br>`// 如果相等则为 0`<br>`// 如果 option < /help 则为负数`<br>`// 如果 option > /help 则为正数`<br>`System.Console.WriteLine(result);` |
| | `string option;`<br>`//...`<br>`// 不区分大小写的字符串比较`<br>`int result = string.Compare(option, "/Help", true);`<br>`// 显示：`<br>`// 如果相等则为 0`<br>`// 如果 option < /help 则 < 0`<br>`// 如果 option > /help 则 > 0`<br>`System.Console.WriteLine(result);` |

### 表 2.6：*string* 方法

| 语句 | 示例 |
| :--- | :--- |
| `bool StartsWith(string value)`<br>`bool EndsWith(string value)` | `string lastName;`<br>`//...`<br>`bool isPhD = lastName.EndsWith("Ph.D.");`<br>`bool isDr = lastName.StartsWith("Dr.");` |
| `string ToLower()` | `string severity = "warning";` |
| `string ToUpper()` | `// 以大写字母显示严重程度`<br>`System.Console.WriteLine(severity.ToUpper());` |
| `string Trim()`<br>`string Trim(...)`<br>`string TrimEnd()`<br>`string TrimStart()` | `// 移除开头或结尾的空白符`<br>`username = username.Trim();` |
| `string Replace(string oldValue, string newValue)` | `string filename;`<br>`//...`<br>`// 从字符串中移除 '?'`<br>`filename = filename.Replace("?", "");` |

## 高级主题

### using 指令和 using static 指令

目前我们调用静态方法的方式总是需要在方法名前加上命名空间，再加上类型名称。例如，在调用 `System.Console.WriteLine` 时，尽管调用的方法是 `WriteLine()` 且上下文中没有其他同名方法，但仍然需要在方法名前加上命名空间（System）和类型名称（Console）。有时，你可能希望使用一种简捷方式来避免这种显式写法；为此，可以利用 C# 6.0 的 using static 指令，如列表 2.15 所示。

### 列表 2.15：using static 指令

```csharp
// using 指令允许你省略命名空间
using static System.Console;

class HeyYou
{
    static void Main()
    {
        string firstName;
        string lastName;

        WriteLine("Hey you!");

        Write("Enter your first name: ");
        firstName = ReadLine();
```

