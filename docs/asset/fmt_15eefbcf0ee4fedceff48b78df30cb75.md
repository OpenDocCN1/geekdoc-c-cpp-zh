
```cs
StringBuilder sb = new StringBuilder();

String s = sb.AppendFormat("{0} {1}", "Jeffrey", "Richter").Replace(" ", "").Replace(4, 3).ToString();

Console.WriteLine(s); // Jeff-Richter
```

你会发现 `String` 和 `StringBuilder` 类并没有完全的方法对等；例如，`String` 拥有 `ToLower`、`ToUpper`、`EndWith`、`PadLeft`、`PadRight`、`Trim` 等。另一方面，`StringBuilder` 类提供了 `Replace` 方法，允许你替换部分（而不是整个字符串）的字符或字符串。这两个类之间没有完全对等遗憾的，因为现在你必须在 `String` 和 `StringBuilder` 之间转换以完成某些任务。例如，要构建一个字符串、将所有字符转换为大写，然后插入一个字符串，需要如下：

```cs
// 构建一个 StringBuilder 执行字符串操作。

StringBuilder sb = new StringBuilder();

// 使用 StringBuilder 执行一些字符串操作。

sb.AppendFormat("{0} {1}", "Jeffrey", "Richter").Replace(" ", "-");

// 将 StringBuilder 转换为 String

// 以便所有字符转换为大写。

String s = sb.ToString().ToUpper();
```

```cs
// 清空 StringBuilder（分配新的字符 数组）。

sb.Length = 0;
```

```cs
// 将大写字符串加载到 StringBuilder，

// 并执行更多操作。

sb.Append(s).Insert(8, "Marc-");
```

```cs
// 将 StringBuilder 转换回字符串。

s = s.ToString();
```

```cs
// 向用户显示字符串。

Console.WriteLine(s); // "JEFFREY-Marc-RICHTER"
```

仅仅因为 `StringBuilder` 没有提供 `String` 的所有操作而编写这些代码是既不方便又低效的。未来，我希望微软为 `StringBuilder` 添加更多字符串操作方法，使其成为一个更完整的类。

## 获取对象的字符串表示：ToString

你经常需要获取对象的字符串表示。通常，当你需要向用户显示数值类型（如 `Byte`、`Int32`、`Single`）或 `DateTime` 对象时，这是必要的。
由于 .NET Framework 是一个面向对象的框架，每个类型都负责提供将实例值转换为等效字符串的代码。在设计类型应如何实现这一点时，FCL 的设计者设计了一种贯穿始终的模式。在本节中，我将描述这种模式。

你可以通过调用 `ToString` 方法获取任何对象的字符串表示。一个公共的、虚拟的、无参数的 `ToString` 方法由 `System.Object` 定义，因此任何类型的实例中都是可用的。语义上，`ToString` 返回一个表示对象当前值的字符串，并且该字符串应该根据调用线程的区域（Culture）进行格式化；也就是说，数字的字符串表示应该使用适当的小数分隔符、数字分组符号与其他分配给调用线程的区域相关的元素。

`Object` 的 `ToString` 实现返回对象类型的全名。
这个值并没有特别有用，但对于许多无法提供合理字符串的类型来说，这是一个合理的默认值。例如，`FileStream` 或 `Hashtable` 对象的字符串表示应该什么样？

所有希望提供合理方式来获取当前值字符串表示的类型都应该重写 `ToString` 方法。许多内置于 FCL 的核心类型（`Byte`、`Int32`、`UInt64`、`Double` 等）重写了它们的 `ToString` 方法并返回一个感知区域的字符串。在 Visual Studio 调试器中，当鼠标悬停在特定变量上时，会显示数据提示（datip）。数据提示中显示的文本是通过调用对象的 `ToString` 方法获得的。因此，当你定义一个类时，应该始终重写 `ToString` 方法，以便获得良好的调试支持。

## 无参数格式和区域

无参数的 `ToString` 方法有两个问题。首先，调用者无法控制字符串的格式。例如，应用程序可能希望将数字格式化为货币字符串、小数字符串、百分比字符串或十六进制字符串。其次，调用者无法轻松选择使用特定区域格式化字符串。第二个问题对于服务器端应用程序代码来说比客户端代码更麻烦。在少数情况下，应用程序需要使用与调用线程关联的区域以外的区域格式化字符串。为了对格式有更多控制，你需要一个允许指定格式和区域信息的 `ToString` 方法版本。

为调用者提供格式和区域选择的类型实现了 `System.IFormatable` 接口。

```cs
public interface IFormatable {
    String ToString(String format, IFormatProvider formatProvider);
}
```

在 FCL 中，所有的基础类型（`Byte`、`SByte`、`Int16`/`UInt16`、`Int32`/`UInt32`、`Int64`/`UInt64`、`Single`、`Double`、`Decimal` 和 `DateTime`）都实现了此接口。此外，其他类型（如 `Guid`）也实现了它。每个枚举类型将自动实现 `IFormatable` 接口，以便从枚举类型的实例中获取有意义的字符串符号。

`IFormatable.ToString` 接受两个参数。第一个是告诉方法对象应如何格式化对象的字符串。`ToString` 的第二个参数 `formatProvider` 是实现 `System.IFormatProvider` 的类型的实例。该类型为 `ToString` 方法提供特定的区域信息。我稍后会讨论。

实现 `IFormatable` 方法的类型决定了它将识别哪些格式。如果你传递一个类型不识别的字符串，该类型应该抛出 `System.FormatException`。

微软定义的许多类型定义了几种格式。例如

此外

这里 `IFormattProvider` 接口背后的基本思想是：当一个类型实现该接口时，它表示该类型的实例能够提供特定区域的格式信息，并且应该忽略与调用线程关联的区域。

`System.Globalization.CultureInfo` 类型是 FCL 定义的极少数实现了 `IFormatProvider` 接口的类型之一。如果你想为（例如）越南格式化字符串，你会构造一个 `CultureInfo` 对象并将其作为 `ToString` 的 `Format` 参数传递。以下代码获取了格式化为越南货币的 `Decimal` 数值的字符串表示。

```cs
Decimal price = 123.54M;
String s = price.ToString("C", new CultureInfo("vi-VN"));
MessageBox.Show(s);
```

![](img/0ce3b788d061e3d3095fa554b1a34adf_367_0.png)

图 14-5 格式化为货币的数值。

## 将格式化对象合并为单个字符串

到目前，我已经解释了单个格式化项如何拥有它自己的对象。然而，有时你想要构造一个由多个格式化对象组成的字符串。例如，下面的字符串包含一个日期、一个名字和一个年龄。

```cs
String s = String.Format("On {0}, {1} is {2} years old.",
new DateTime(2012, 4, 22, 14, 35, 5), "Aidan", 9);
Console.WriteLine(s);
```

如果你编译并运行这段代码（假设 "en-US" 是线程的当前文化），你将看到以下输出：

On 4/22/2012 2:35:00 PM, Aidan is 9 years old.

`String` 的静态方法 `Format` 接收一个字符串，该字符串通过大括号中的数字来标识可替换的参数。示例中使用的格式告诉 `Format` 方法将 `{0}` 替换为字符串后的第一个参数（日期/时间），将 `{1}` 替换为字符串后的第二个参数（"Aidan"），并将 `{2}` 替换为字符串后的第三个参数（7）。

在内部，`Format` 方法会调用每个对象的 `ToString` 方法以获取该对象的字符串表示。返回的字符串都会对齐，并返回完整的最终字符串。这本身很好，但意味着所有对象都是使用你的通用格式化并调用线程的文化信息进行格式化的。

如果你通过在大括号内指定格式信息，你可以进行更详细的格式化。例如，下面的代码与之前的示例相同，但我对可替换参数 0 和 2 添加了格式化信息。

```cs
String s = String.Format("On {0:D}, {1} is {2:E} years old.",
new DateTime(2012, 4, 22, 14, 35, 5), "Aidan", 9);
Console.WriteLine(s);
```

如果你编译并运行这段代码（假设 "en-US" 是线程的当前文化），你将看到以下输出：

On Sunday, April 22, 2012, Aidan is 9.00000E+000 years old.

当 `Format` 方法解析字符串时，它发现可替换参数 0 应该调用其 `IFormable` 对象的 `ToString` 方法并传入 "D" 且其参数为 null。同样，`Format` 会调用可替换参数 2 的 `IFormable` `ToString` 方法，传递 "E" 和 null。如果该类型没有实现 `IFormable` 接口，`Format` 将调用其继承自 `Object` 的 `IFormable` `ToString` 方法（可能已被重写），并将默认格式附加到生成的字符串上。

`String` 类提供了静态方法 `Format` 的几个重载。其中一个版本接收一个实现了 `IFormatProvider` 接口的对象，这样你就可以通过调用特定的文化信息来格式化所有参数。显然，`Format` 会调用每个对象的 `IFormable.ToString` 方法，并传递给 `Format` 的任何 `IFormatProvider` 对象。

如果你使用 `StringBuilder` 而不是 `String` 来构造字符串，可以调用 `StringBuilder` 的 `AppendFormat` 方法。该方法的工作与 `String` 的 `Format` 完全相同，只是将格式化后的字符串追加到 `StringBuilder` 的字符数组中。`String` 的 `Format` 和 `AppendFormat` 都接收一个字符串，并且有一个版本接收一个 `IFormatProvider`。

`System.Console` 提供了 `Write` 和 `WriteLine` 方法，它们也可以格式化字符串和参数。然而，`Console` `write` 和 `WriteLine` 方法没有重载允许你传递一个 `IFormatProvider`。如果你想为特定文化格式化字符串，必须先调用 `String` `Format` 方法，首先传递所需的 `IFormatProvider` 对象，然后将生成的字符串传递给 `Console.Write` 或 `WriteLine`。这不算大问题，因为正如我之前提到的，客户端代码很少使用不同于调用线程相关的文化来格式化字符串。

## 提供自定义格式化器

到目前为止，.NET 框架中的格式化能力设计为为你提供灵活性和控制力。然而，我们还没有结束。你可以定义一个方法，当 `StringBuilder` `AppendFormat` 对任何对象进行格式化时调用该方法。换句话说，`AppendFormat` 不再为每个对象调用 `ToString`，而是调用你定义的函数，允许你以任何想要的方式格式化任何或所有对象。我即将描述的内容也适用于 `String` 的 `Format` 方法。

通过示例来解释这种机制。假设你正在格式化用户将看到的 HTML 文本。

```cs
using System;
using System.Text;
using System.Threading;
public class Program
{
    public static void Main()
    {
        StringBuilder sb = new StringBuilder();
        sb.AppendFormat("<b>{0}</b>: {1}", "Date", DateTime.Now);
        Console.WriteLine(sb.ToString());
    }
}
internal sealed class Bold32 : IFormatProvider
{
    public string Format(string format, object arg, IFormatProvider formatProvider)
    {
        string s = null;
        if (formatProvider != null)
        {
            s = formatProvider.Format(format, arg);
        }
        if (s == null)
        {
            IFormable formable = arg as IFormable;
            if (formable != null)
            {
                s = formable.ToString(format, formatProvider);
            }
            else
            {
                if (arg != null)
                    s = arg.ToString();
                else
                    s = string.Empty;
            }
        }
        return "<b>" + s + "</b>";
    }
    public object GetFormat(Type format)
    {
        if (format == typeof(IFormatProvider))
        {
            return this;
        }
        return null;
    }
}
```

## 解析字符串以获取对象：Parse

在前面的一节中，我解释了如何获取一个对象并得到该对象的字符串表示。在本节中，我将讨论相反的内容：如何获取一个字符串并获取它的对象表示。从字符串获取对象并不是非常常见的操作，但它偶尔会派上用场。微软认为有必要格式化一种机制，可以将字符串解析为对象。

任何可以解析字符串的类型都提供一个名为 `Parse` 的公共静态方法。该方法接收一个 `String` 并返回该类型的实例；在某种意义上，`Parse` 充了工厂的角色。在 CLR 中，所有数值类型以及 `DateTime` 和其他少数类型（如 SQL 数据类型）都存在 `Parse` 方法。

让我们来看下如何将字符串解析为数值类型。几乎所有的数值类型（`Byte`、`SByte`、`Int16`/`UInt16`、`Int32`/`UInt32`、`Int64`/`UInt64`、`Double`、`Decimal` 和 `BigInteger`）都提供至少一个 `Parse` 方法。在这里，我将为您展示由 `Int32` 类型定义的 `Parse` 方法（其他数值类型的 `Parse` 方法工作原理与 `Int32` 类似）。

```c
public static Int32 Parse(String s, NumberStyles style, IFormatProvider provider);
```

仅从原型来看，您应该能够准确猜出此方法的工作原理。`String` 参数标识您想要解析为 `Int32` 对象的数字的字符串表示。`System.Globalization.NumberStyles` 参数是一组标志，用于标识 `Parse` 应该在字符串中找到的字符。而 `IFormatProvider` 参数标识一个 `Parse` 方法可以使用它来获取特定区域信息的对象，正如在本章较早部分讨论的那样。

例如，以下代码会导致 `Parse` 抛出 `System.FormatException`，因为正在解析的字符串包含前导空格。

```c
Int32 x = Int32.Parse(" 123", NumberStyles.None, null);
```

为了允许 `Parse` 跳过前导空格，请样式改为 `AllowLeadingWhite`。

```c
Int32 x = Int32.Parse(" 123", NumberStyles.AllowLeadingWhite, null);
```

请参阅 .NET Framework 文档以获取完整描述 `NumberStyles` 枚举定义的位符号和常用组合。

这里是一个显示如何解析十六进制数的代码片段。

```c
Int32 x = Int32.Parse("1A", NumberStyles.HexNumber, null);
Console.WriteLine(x); // 显示 "26"
```

此 `Parse` 方法接受三个参数。为了方便起见，许多类型提供了 `Parse` 的额外重载，因此您不需要传递许多参数。例如，`Int32` 提供了四个 `Parse` 方法重载。

```csharp
// 使用 NumberStyles.Integer 作为样式
```
