

满足条件的方法是使方法的最后一条语句成为 return 语句。然而，return 语句可以出现在方法实现末尾之外的位置。例如，方法实现中的 if 或 switch 语句可能在其内部包含 return 语句；请参阅清单 4.5 中的示例。

## 清单 4.5：方法结束前的 return 语句

```
class Program
{
    static bool MyMethod()
    {
        string command = ObtainCommand();
        switch(command)
        {
            case "quit":
                return false;
            // ... omitted, other cases
            default:
                return true;
        }
    }
}
```

（请注意，return 语句会将控制权从 switch 中转移出去，因此在以 return 语句结束的 switch 部分中不需要 break 语句来防止非法的贯穿。）

在清单 4.5 中，方法中的最后一条语句不是 return 语句，而是一个 switch 语句。然而，编译器可以推断出通过该方法的所有可能代码路径都会导致返回，因此该方法的终点是不可达的。因此该方法合法，即使它没有以 return 语句结束。

如果特定代码路径在 return 之后包含不可达的语句，编译器会发出警告，指出这些附加语句永远不会执行。

尽管 C# 允许方法具有多个 return 语句，但如果只有一个退出位置而不是在方法的各种代码路径中散布多个 return，代码通常更易读且更易于维护。

指定 void 作为返回类型表示方法没有返回值。因此，对该方法的调用不能分配给变量或在调用站点用作参数类型。void 方法调用只能用作语句。此外，在方法体内部，return 语句变为可选，并且当指定时，return 关键字后面不得有值。例如，清单 4.4 中 Main() 的返回类型为 void，并且方法内部没有 return 语句。然而，DisplayGreeting() 包含一个（可选的）return 语句，其后没有返回结果。

## 表达式体方法

为了支持最简单的无方法体形式的方法声明，C# 6.0 引入了表达式体方法，它们使用表达式而不是完整的方法体来声明。清单 4.4 的 GetFullName() 方法提供了表达式体方法的示例：

```
static string GetFullName( string firstName, string lastName) =>
    $"{ firstName } { lastName }";
```

代替方法体常见的花括号，表达式体方法使用“goes to”运算符（在第 12 章中完全介绍），其结果数据类型必须与方法的返回类型匹配。换句话说，即使在表达式体方法实现中没有显式的 return 语句，仍然需要表达式的返回类型与方法声明的返回类型匹配。

表达式体方法是完整方法体声明的语法快捷方式。因此，其使用应限于最简单的方法实现——通常可在单行中表达。

## 语言对比：C++—头文件

与 C++ 不同，C# 类从不将实现与声明分离。在 C# 中，没有头文件（.h）或实现文件（.cpp）。相反，声明和实现出现在同一个文件中。（C# 确实支持一种名为“partial methods”的高级功能，其中方法的定义声明与其实现是分开的，但就本章而言，我们只考虑非 partial 方法。）C# 中没有单独的声明和实现，去除了在具有单独头文件和实现文件的语言（如 C++）中需要在两个地方维护冗余声明信息的要求。

## 初学者主题

## 命名空间

如前所述，命名空间是用于对相关类型进行分类和分组的组织机制。开发人员可以通过检查与熟悉类型在同一命名空间中的其他类型来发现相关类型。此外，通过命名空间，两个或多个类型可以具有相同的名称，只要它们通过不同的命名空间来区分。

## using 指令

完全限定的命名空间名称可能变得相当长且难以处理。然而，可以将一个或多个命名空间中的所有类型“导入”到文件中，以便在不使用完全限定的情况下使用。为此，C# 程序员在文件顶部包含 using 指令。例如，在清单 4.6 中，Console 未以 System 为前缀。命名空间可以省略，因为在列表顶部出现了 using System 指令。

## 清单 4.6：using 指令示例

```
// The using directive imports all types from the
// specified namespace into the entire file.
using System;

class HelloWorld
{
    static void Main()
    {
        // No need to qualify Console with System
        // because of the using directive above.
        Console.WriteLine("Hello, my name is Inigo Montoya");
    }
}
```

清单 4.6 的结果出现在输出 4.2 中。

## 输出 4.2

```
Hello, my name is Inigo Montoya
```

像 using System 这样的 using 指令并不能让你从 System 的子命名空间中声明的类型中省略 System。

例如，如果你的代码访问了 `System.Text` 命名空间中的 `StringBuilder` 类型，你必须包含额外的 `using System.Text;` 指令或将类型完全限定为 `System.Text.StringBuilder`，而不是仅 `Text.StringBuilder`。简而言之，using 指令不会“导入”任何 **嵌套命名空间** 中的类型。嵌套命名空间由命名空间中的句点标识，始终需要显式导入。

## 语言对比：Java—import 指令中的通配符

Java 允许使用通配符导入命名空间，如下所示：

```
import javax.swing.*;
```

相比之下，C# 不支持通配符 using 指令，而是要求每个命名空间都必须显式导入。

## 语言对比：Visual Basic .NET—项目范围 Imports 指令

与 C# 不同，Visual Basic .NET 支持为整个项目指定 `using` 指令等效项 `Imports` 的能力，而不仅仅是特定文件。换句话说，Visual Basic .NET 提供了跨越整个编译的 `using` 指令的命令行方式。

频繁使用特定命名空间中的类型意味着添加该命名空间的 using 指令是个好主意，而不是完全限定该命名空间中的所有类型。因此，几乎所有 C# 文件都在顶部包含 using System 指令。在本书的其余部分，代码列表通常会省略 using System 指令。然而，其他命名空间指令会显式包含。

using System 指令的一个有趣效果是字符串数据类型可以用不同的大小写标识：String 或 string。前者依赖于 using System 指令，后者使用 string 关键字。两者都是对 System.String 数据类型的有效 C# 引用，并且产生的 CIL 代码不受所选版本的影响。

## 高级主题

## 嵌套 using 指令

你不仅可以在文件顶部有 using 指令，还可以在命名空间声明顶部包含它们。例如，如果声明了一个新命名空间 EssentialCSharp，则可以在命名空间声明顶部添加 using 声明（见清单 4.7）。

```
```csharp
namespace EssentialCSharp
{
    using System;

    class HelloWorld
    {
        static void Main()
        {
            // No need to qualify Console with System
            // because of the using directive above.
            Console.WriteLine("Hello, my name is Inigo Montoya");
        }
    }
}
```
```

清单 4.7 的结果出现在输出 4.3 中。

```
```text
Hello, my name is Inigo Montoya
```
```

将 using 指令放在文件顶部与将其放在命名空间声明顶部之间的区别在于，该指令仅在命名空间声明内有效。如果代码包含新

