

## 预定义引用类型

C# 支持两种预定义引用类型：`object` 和 `string`，如下表所述。

| 名称 | .NET 类型 | 说明 |
|---|---|---|
| `object` | System.Object | 根类型。所有其他类型（包括值类型）都派生自 `object`。 |
| `string` | System.String | Unicode 字符串 |

## object 类型

许多编程语言和类层次结构都提供了一个根类型，层次结构中的所有其他对象都派生自该根类型。C# 和 .NET 也不例外。在 C# 中，`object` 类型是所有其他内建类型和用户定义类型的最终父类型。这意味着你可以将 `object` 类型用于两个目的：

- 你可以使用 `object` 引用来绑定任何特定子类型的对象。例如，在第 8 章“运算符和强制转换”中，你会看到如何使用 `object` 类型将栈上的值对象装箱并移动到堆上；当代码必须操作特定类型未知的对象时，`object` 引用在反射中也非常有用。
- `object` 类型实现了一些基本的通用方法，包括 `Equals`、`GetHashCode`、`GetType` 和 `ToString`。负责任的用户定义类可能需要使用一种称为*重写*的面向对象技术来提供其中某些方法的替代实现，这将在第 4 章“继承”中讨论。例如，当你重写 `ToString` 时，你为你的类配备了一个能够智能地提供其自身字符串表示的方法。如果你没有在类中为这些方法提供自己的实现，编译器会使用 `object` 中的实现，这些实现在你的类的上下文中可能正确，也可能不正确或不合理。

你将在后续章节中更详细地研究 `object` 类型。

## string 类型

C# 识别 string 关键字，它在底层被转换为 .NET 类 System.String。有了它，字符串连接和字符串复制等操作变得轻而易举：

```
string str1 ="Hello";
string str2 ="World";
string str3 = str1 + str2; // string concatenation
```

尽管采用了这种赋值方式，string 仍然是引用类型。在幕后，字符串对象被分配在堆上，而不是栈上；当你将一个字符串变量赋值给另一个字符串时，你会在内存中得到对同一个字符串的两个引用。然而，string 与引用类型的通常行为不同。例如，字符串是不可变的。

对其中一个字符串进行修改会创建一个全新的字符串对象，而另一个字符串保持不变。请考虑以下代码（代码文件 StringSample/Program.cs）：

```
using static System.Console;

class Program
{
    static void Main()
    {
        string s1 ="a string";
        string s2 = s1;
        WriteLine("s1 is " + s1);
        WriteLine("s2 is " + s2);
        s1 ="another string";
        WriteLine("s1 is now " + s1);
        WriteLine("s2 is now " + s2);
    }
}
```

其输出如下：

```
s1 is a string
s2 is a string
s1 is now another string
s2 is now a string
```

改变 s1 的值对 s2 没有影响，这与你对引用类型的预期相反！这里发生的事情是：当 s1 被初始化为值 a string 时，在堆上分配了一个新的字符串对象。当 s2 被初始化时，引用指向同一个对象，因此 s2 也具有值 a string。然而，当你现在更改 s1 的值时，并不是替换原始值，而是在堆上为新值分配一个新对象。s2 变量仍然指向原始对象，因此它的值不变。在底层，这是运算符重载的结果，这个主题将在第 8 章中探讨。总的来说，string 类的实现使得其语义符合你通常对字符串的直觉预期。

字符串字面量用双引号（`"`）括起来；如果你试图用单引号将字符串括起来，编译器会将该值视为 char 并抛出错误。C# 字符串可以包含与 char 相同的 Unicode 和十六进制转义序列。由于这些转义序列以反斜杠开头，你不能在字符串中使用未转义的反斜杠。相反，你需要使用两个反斜杠（`\\`）对其进行转义：

```
string filepath ="C:\\ProCSharp\\First.cs";
```

即使你确信自己总能记得这样做，输入所有这些双反斜杠也可能很烦人。幸运的是，C# 为你提供了另一种选择。你可以用 at 字符 (@) 作为字符串字面量的前缀，其后的所有字符都按字面值对待；它们不会被解释为转义序列：

```
string filepath = @"C:\ProCSharp\First.cs";
```

这甚至允许你在字符串字面量中包含换行符：

```
string jabberwocky = @"'Twas brillig and the slithy toves
Did gyre and gimble in the wabe.";
```

在这种情况下，jabberwocky 的值将是：

```
'Twas brillig and the slithy toves
Did gyre and gimble in the wabe.
```

C# 6 定义了一种新的字符串插值格式，使用 $ 前缀作为标记。你之前在“使用变量”一节中已经见过这个前缀。你可以将前面演示字符串连接的代码片段改为使用字符串插值格式。给字符串加上 $ 前缀，你就可以在字符串中放入包含变量——甚至代码表达式——的花括号。变量或代码表达式的结果会被放到字符串中花括号所在的位置：

```
public static void Main()
{
    string s1 ="a string";
    string s2 = s1;
    WriteLine($"s1 is {s1}");
    WriteLine($"s2 is {s2}");
    s1 ="another string";
    WriteLine($"s1 is now {s1}");
    WriteLine($"s2 is now {s2}");
}
```

> 注意 字符串和字符串插值的特性将在第 10 章“字符串和正则表达式”中详细介绍。

## 控制程序流

本节讨论语言的真正核心内容：那些允许你控制程序*流程*的语句，而不是按代码在程序中出现的顺序执行每一行。

### 条件语句

条件语句允许你根据是否满足特定条件或表达式的值来分支代码。C# 有两种用于代码分支的结构：`if` 语句（测试是否满足特定条件）和 `switch` 语句（将表达式与多个不同的值进行比较）。

### if 语句

对于条件分支，C# 继承了 C 和 C++ 的 `if.else` 结构。对于任何使用过程式语言进行过编程的人来说，该语法应该相当直观：

```
if (condition)
    statement(s)
else
    statement(s)
```

如果任一条件需要执行多条语句，则需要使用花括号 ({ . }) 将这些语句连接成一个块。（这也适用于其他可以将语句连接成块的 C# 结构，例如 `for` 和 `while` 循环）：

```
bool isZero;
if (i == 0)
{
    isZero = true;
    WriteLine("i is Zero");
}
else
{
    isZero = false;
    WriteLine("i is Non-zero");
}
```

如果你愿意，可以使用没有末尾 `else` 语句的 `if` 语句。你还可以组合 `else if` 子句来测试多个条件（代码文件 `IfStatement/Program.cs`）：

```
using static System.Console;

namespace Wrox
{
    class Program
    {
        static void Main()
        {
            WriteLine("Type in a string");
            string input;
            input = ReadLine();
            if (input =="")
```

