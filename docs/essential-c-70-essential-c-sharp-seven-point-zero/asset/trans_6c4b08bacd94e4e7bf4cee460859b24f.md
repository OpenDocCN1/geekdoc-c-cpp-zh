

（请注意，`return` 语句会将控制权转移出 `switch`，因此在一个以 `return` 语句结束的 `switch` 块中，不需要 `break` 语句来防止非法的贯穿执行。）

在清单 5.5 中，该方法的最后一条语句不是 `return` 语句，而是一条 `switch` 语句。然而，编译器可以推断出该方法中所有可能的代码路径都会导致 `return`，因此该方法的终点是不可达的。因此，即使该方法没有以 `return` 语句结束，它也是合法的。

如果特定的代码路径在 `return` 之后包含不可达的语句，编译器将发出警告，指出这些额外语句永远不会执行。

虽然 C# 允许方法包含多个 `return` 语句，但通常当方法拥有单一出口位置而不是在各种代码路径中散布多个 `return` 语句时，代码的可读性和可维护性会更好。

指定 `void` 作为返回类型表明该方法没有返回值。因此，对该方法的调用不能赋值给变量，也不能在调用处用作参数类型。`void` 方法调用只能用作语句。此外，在方法体内，`return` 语句变为可选，并且当指定它时，`return` 关键字后面不能跟随任何值。例如，清单 5.4 中 `Main()` 的 `return` 是 `void`，且方法内没有 `return` 语句。然而，`DisplayGreeting()` 包含一个（可选的）`return` 语句，后面没有跟随任何返回结果。

虽然从技术上讲，一个方法只能有一个返回类型，但该返回类型可以是一个元组（tuple）。因此，从 C# 7.0 开始，可以使用 C# 元组语法将多个值打包为元组并返回。例如，您可以声明一个 `GetName()` 方法，如清单 5.6 所示。

## 清单 5.6：使用元组返回多个值

```csharp
class Program
{
    static string GetUserInput(string prompt)
    {
        System.Console.Write(prompt);
        return System.Console.ReadLine();
    }
    
    static (string First, string Last) GetName()
    {
        string firstName, lastName;
        firstName = GetUserInput("Enter your first name: ");
        lastName = GetUserInput("Enter your last name: ");
        return (firstName, lastName);
    }

    static public void Main()
    {
        (string first, string last) name = GetName();
        System.Console.WriteLine($"Hello { name.First } { name.Last }!");
    }
}
```

当然，从技术角度看，我们仍然只返回一种数据类型，即 `ValueTuple<string, string>`；但是，实际上，您可以返回任意数量（最好是合理的数量）的值。

### 表达式体方法

为了支持最简单的没有方法体形式的方法声明，C# 6.0 引入了表达式体方法（expression-bodied methods），它们使用表达式而非完整的方法体来声明。清单 5.4 中的 GetFullName() 方法提供了表达式体方法的一个示例：

```csharp
static string GetFullName( string firstName, string lastName) =>
  $"{ firstName } { lastName }";
```

表达式体方法使用“转到”运算符（在第 13 章中完整介绍）代替方法体中典型的花括号，该运算符产生的结果数据类型必须与方法声明的返回类型匹配。换句话说，尽管表达式体方法的实现中没有显式的 `return` 语句，但表达式的返回类型仍然必须与方法声明的返回类型匹配。

表达式体方法是完整方法体声明的语法快捷方式。因此，其使用应限于最简单的方法实现——通常可以在一行内表达。

## 语言对比：C++——头文件

与 C++ 不同，C# 类从不将实现与声明分离。在 C# 中，没有头文件（.h）或实现文件（.cpp）。相反，声明和实现一起出现在同一个文件中。（C# 支持一种称为 *partial methods* 的高级特性，其中方法的定义声明与其实现是分离的，但就本章而言，我们只考虑非 partial 方法。）

C# 中声明和实现的合并消除了维护冗余声明信息的需求，这些信息在具有分离头文件和实现文件的语言（如 C++）中通常存在于两个位置。

## 初学者主题

### 命名空间

如前所述，命名空间是用于分类和分组相关类型的组织机制。开发者可以通过检查与已知类型位于同一命名空间中的其他类型来发现相关类型。此外，通过命名空间，两个或更多类型可以拥有相同的名称，只要它们通过不同的命名空间加以区分。

### using 指令

完全限定的命名空间名称可能变得非常长且难以管理。但是，可以导入一个或多个命名空间中的所有类型到文件中，以便在不完全限定名称的情况下使用它们。为了实现这一点，C# 程序员通常在文件顶部包含一个 using 指令。例如，在清单 5.7 中，Console 前面没有 System 前缀。由于清单顶部存在 using System 指令，因此可以省略命名空间。

## 清单 5.7：using 指令示例

```csharp
// The using directive imports all types from the
// specified namespace into the entire file
using System;

class HelloWorld
{
  static void Main()
  {
    // No need to qualify Console with System
    // because of the using directive above
    Console.WriteLine("Hello, my name is Inigo Montoya");
  }
}
```

清单 5.7 的结果显示在输出 5.2 中。

## 输出 5.2

Hello, my name is Inigo Montoya

像 `using System` 这样的 using 指令并不能允许你省略在 System 的子命名空间中声明的类型中的 System。例如，如果代码访问 System.Text 命名空间中的 StringBuilder 类型，你必须要么包含额外的 `using System.Text;` 指令，要么完全限定类型为 `System.Text.StringBuilder`，而不仅仅是 `Text.StringBuilder`。简而言之，using 指令不会导入任何嵌套命名空间中的类型。嵌套命名空间（由命名空间中的点标识）始终需要显式导入。

## 语言对比：Java——导入指令中的通配符

Java 允许使用通配符导入命名空间，例如：

```java
import javax.swing.*;
```

相比之下，C# 不支持通配符 using 指令，而是要求显式导入每个命名空间。

## 语言对比：Visual Basic .NET——项目范围导入指令

与 C# 不同，Visual Basic .NET 支持指定 using 指令的等效物 Imports，其范围可以是整个项目，而不仅仅是特定文件。换句话说，Visual Basic .NET 提供了 using 指令的命令行方式，其范围可以覆盖整个编译过程。

频繁使用特定命名空间内的类型暗示，为该命名空间添加 using 指令是一个好主意，而不是完全限定该命名空间内的所有类型。相应地，几乎所有 C# 文件都在顶部包含 `using System` 指令。在本书的其余部分，代码清单通常省略 `using System` 指令。然而，其他命名空间指令会被明确包含。

`using System` 指令的一个有趣效果是，string 数据类型可以用不同的大小写来识别：`String` 或 `string`。前者依赖于 `using System` 指令，后者使用 `string` 关键字。两者都是对 `System.String` 数据类型的有效 C# 引用，且所选版本不影响生成的公共中间语言（CIL）代码。²

## 高级主题

### 嵌套 using 指令

不仅可以在文件顶部拥有 using 指令，还可以在命名空间声明的顶部包含它们。例如，如果声明了一个新的命名空间 EssentialCSharp，那么可以添加一个 using 声明在命名空间声明的顶部（参见清单 5.8）。

## 清单 5.8：在命名空间声明中指定 using 指令

```csharp
namespace EssentialCSharp
{
    using System;

    class HelloWorld
    {
        static void Main()
        {
            // No need to qualify Console with System
            // because of the using directive above
            Console.WriteLine("Hello, my name is Inigo Montoya");
        }
    }
}
```

清单 5.8 的结果显示在输出 5.3 中。

## 输出 5.3

```
Hello, my name is Inigo Montoya
```

将 using 指令放在文件顶部与放在命名空间声明顶部的区别在于，该指令仅在命名空间声明内部有效。如果代码包含一个新的

1. 我更喜欢 `string` 关键字，但无论程序员选择哪种表示方式，项目内的代码理想情况下应当保持一致。

