

```csharp
Write("Enter your last name: ");
lastName = ReadLine();

WriteLine(
    $"Your full name is {firstName} {lastName}.");
}
}
```

`using static` 指令必须出现在文件的顶部。¹ 每次使用 `System.Console` 类时，都不再需要同时使用 `System.Console` 前缀。相反，我们只需直接编写方法名即可。关于 `using static` 指令，有一点重要注意事项：它仅适用于静态方法和属性，不适用于实例成员。

另一个类似的指令是 `using` 指令，它允许消除命名空间前缀——例如 `System.`。与 `using static` 指令不同，`using` 指令在其所在的文件（或命名空间）内普遍适用（不仅限于静态成员）。使用 `using` 指令，你可以（选择性地）消除对命名空间的所有引用，无论是在实例化过程中、静态方法调用中，还是在 C# 6.0 中的 `nameof` 运算符中。

### 字符串格式化

无论你使用 `string.Format()` 还是 C# 6.0 的字符串插值功能来构建复杂的格式化字符串，都有一套丰富且复杂的格式化模式可用于显示数字、日期、时间、时间跨度等。例如，如果 `price` 是一个类型为 `decimal` 的变量，那么 `string.Format("{0,20:C2}", price)` 或等效的插值表达式 `$"{price,20:C2}"` 都会使用默认的货币格式化规则将 `decimal` 值转换为字符串，结果保留小数点后两位，并在 20 个字符宽的字符串中右对齐。篇幅有限，无法详细讨论所有可能的格式化字符串；请参阅 `string.Format()` 的 MSDN 文档以获取格式化字符串的完整列表。

如果你想在插值字符串或格式化字符串中实际包含左花括号或右花括号，可以加倍花括号（双花括号）来表示它不引入模式。例如，插值字符串 `$"{{ {price:C2} }}"` 可能会生成字符串 `"{ $1,234.56 }"`。

- 或者在命名空间声明的顶部。

### 换行符

在输出换行符时，具体的换行字符取决于你正在其上执行代码的操作系统。在 Microsoft Windows 操作系统中，换行符是回车符（`\r`）和换行符（`\n`）的组合，而在 UNIX 系统中仅使用单个换行符。克服不同操作系统之间差异的一种方法是简单地使用 `System.Console.WriteLine()` 来输出一个空行。另一种几乎必不可少的做法（当需要针对同一代码库在多个操作系统上处理换行符时），是使用 `System.Environment.NewLine`。换句话说，`System.Console.WriteLine("Hello World")` 和 `System.Console.Write($"Hello World{System.Environment.NewLine}")` 是等效的。然而，在 Windows 上，`System.Console.WriteLine()` 和 `System.Console.Write(System.Environment.NewLine)` 等效于 `System.Console.Write("\r\n")`——而不是 `System.Console.Write("\n")`。总之，请依赖 `System.Console.WriteLine()` 和 `System.Environment.NewLine`，而不是 `\n`，以便使用相同的代码适配 Windows 特有的操作系统特性，同时该代码也能在 Linux 和 iOS 上运行。

> **准则**
> 请依赖 `System.Console.WriteLine()` 和 `System.Environment.NewLine`，而不是 `\n`，以便使用相同的代码适配 Windows 特有的操作系统特性，同时该代码也能在 Linux 和 iOS 上运行。

### C# 属性

以下部分中提到的 `Length` 成员实际上并不是一个方法，这一点从其调用后没有跟随括号的事实中可以看出。`Length` 是 `string` 的一个属性，C# 语法允许像访问成员变量（在 C# 中称为**字段**）一样访问属性。换句话说，属性具有称为 setter 和 getter 的特殊方法的行为，但访问这些行为的语法却是像访问字段一样。

检查属性的底层 `CIL` 实现可以发现，它被编译为两个方法：`set_<PropertyName>` 和 `get_<PropertyName>`。然而，从 C# 代码中无法直接访问这两个方法，只能通过 C# 属性构造来访问。有关属性的更多细节，请参阅第 6 章。

### 字符串长度

要确定字符串的长度，需要使用称为 Length 的字符串成员。这个特定的成员被称为**只读属性**。因此，它不能被设置，调用它也不需要任何参数。清单 2.16 演示了如何使用 Length 属性，输出 2.11 展示了结果。

**清单 2.16：使用字符串的 Length 成员**

```csharp
class PalindromeLength
{
    static void Main()
    {
        string palindrome;

        System.Console.Write("Enter a palindrome: ");
        palindrome = System.Console.ReadLine();

        System.Console.WriteLine(
            $"The palindrome \"{palindrome}\" is"
            + $" {palindrome.Length} characters.");
    }
}
```

**输出 2.11**

```text
Enter a palindrome: Never odd or even
The palindrome "Never odd or even" is 17 characters.
```

字符串的长度不能直接设置；它是由字符串中的字符数计算得出的。此外，字符串的长度不能改变，因为字符串是**不可变的**。

### 字符串是不可变的

字符串类型的一个关键特征是不可变性。可以为字符串变量分配一个全新的值，但没有机制来修改字符串的内容。因此，不可能将字符串转换为全大写字母。创建一个由旧字符串的大写版本组成的新字符串是很简单的，但在此过程中旧字符串并没有被修改。请考虑清单 2.17 作为一个例子。

**清单 2.17：错误；字符串是不可变的**

```csharp
class Uppercase
{
    static void Main()
    {
        string text;

        System.Console.Write("Enter text: ");
        text = System.Console.ReadLine();

        // UNEXPECTED: Does not convert text to uppercase
        text.ToUpper();

        System.Console.WriteLine(text);
    }
}
```

输出 2.12 展示了清单 2.17 的结果。

**输出 2.12**

```text
Enter text: This is a test of the emergency broadcast system.
This is a test of the emergency broadcast system.
```

乍一看，似乎 `text.ToUpper()` 应该将 `text` 中的字符转换为大写。然而，字符串是不可变的，因此 `text.ToUpper()` 不会进行这样的修改。相反，`text.ToUpper()` 返回一个新的字符串，该字符串需要被保存到变量中或直接传递给 `System.Console.WriteLine()`。修正后的代码显示在清单 2.18 中，其输出显示在输出 2.13 中。

**清单 2.18：处理字符串**

```csharp
class Uppercase
{
    static void Main()
    {
        string text, uppercase;

        System.Console.Write("Enter text: ");
        text = System.Console.ReadLine();

        // Return a new string in uppercase
        uppercase = text.ToUpper();

        System.Console.WriteLine(uppercase);
    }
}
```

**输出 2.13**

```text
Enter text: This is a test of the emergency broadcast system.
THIS IS A TEST OF THE EMERGENCY BROADCAST SYSTEM.
```

如果忽略字符串的不可变性，清单 2.17 中显示的那类错误也可能发生在其他字符串方法中。

要实际更改 `text` 的值，请将 `ToUpper()` 的值重新赋给 `text`，如下面的代码所示：

```csharp
text = text.ToUpper();
```

### System.Text.StringBuilder

如果需要大量的字符串修改，例如在多个步骤中构建一个长字符串时，应使用数据类型 `System.Text.StringBuilder` 而不是 `string`。`StringBuilder` 类型包含诸如 `Append()`、`AppendFormat()`、`Insert()`、`Remove()` 和 `Replace()` 等方法，其中一些方法在 `string` 中也可用。然而，关键区别在于，使用 `StringBuilder` 时，这些方法会修改 `StringBuilder` 本身中的数据，而不仅仅是返回一个新的字符串。

### null 和 void

与类型相关的两个额外关键字是 `null` 和 `void`。由 `null` 关键字标识的 `null` 值表示该变量不指向任何有效对象。`void` 用于指示没有类型或根本没有值。

### null

`null` 也可以作为字符串“字面量”的类型使用。`null` 表示变量被设置为空。引用类型、指针类型和可空值类型可以被赋值为 `null`。到目前为止，本书中涵盖的唯一引用类型是 `string`；第 6 章详细讨论了创建类（即引用类型）的主题。简而言之，引用类型的变量包含一个指向内存位置的引用，该位置不同于变量的值。将变量设置为 `null` 的代码显式地将引用分配为指向无有效值。实际上，甚至可以检查一个引用是否指向空值。清单 2.19 演示了将 `null` 赋给字符串变量的操作。

[1] 或者在命名空间声明的顶部。

