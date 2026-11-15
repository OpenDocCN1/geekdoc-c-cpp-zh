

## 参数声明

请考虑 `DisplayGreeting()` 和 `GetFullName()` 方法的声明。方法声明括号之间出现的文本是 **参数列表**。参数列表中的每个参数包括参数类型和参数名称。逗号分隔列表中的每个参数。

从行为上看，参数几乎与局部变量相同，参数的命名约定也随之而来。因此，参数名称采用驼峰命名法。此外，不可能声明一个与包含方法的参数同名的局部变量（在方法内部声明的变量），因为这会创建两个同名的“局部变量”。

## 方法返回值声明

除了 `GetUserInput()` 和 `GetFullName()` 需要指定参数之外，这两个方法还都包含 **方法返回值**。你可以通过方法声明中方法名称前紧跟一个数据类型来判断是否有方法返回值。对于 `GetUserInput()` 和 `GetFullName()`，数据类型均为 `string`。与参数不同，只允许有一个方法返回值。

一旦方法包含返回数据类型，且假设未发生错误，则有必要在方法声明中的每个 **代码路径**（或可能连续执行的一组语句）内指定 return 语句。return 语句以 return 关键字开头，后跟方法返回的值。例如，`GetFullName()` 方法的 return 语句是 `return firstName + " " + lastName`。C# 编译器强制要求返回类型必须与 return 关键字后指定的数据类型匹配。

return 语句可以出现在方法实现末尾以外的位置，只要方法有返回类型，所有代码路径都包含 return 即可。例如，方法实现开头的 `if` 或 `switch` 语句可以在条件或 case 语句中包含 return 语句；示例请参见清单 4.5。

## 清单 4.5：方法结束前的 return 语句

```
class Program
{
    static void Main()
    {
        string command;
        // ...
        switch(Command)
        {
            case "quit":
                return; // ...
        } // ...
    }
}
```

return 语句表示跳转到方法末尾，因此 switch 语句中不需要 break。一旦执行遇到 return，方法调用将结束。

如果特定代码路径在 return 之后包含语句，编译器将发出警告，指示这些额外语句永远不会执行。尽管 C# 允许提前返回，但如果方法中只有一个退出位置，而不是在各种代码路径中散布多个 return，代码通常更易读、更易维护。

将 void 指定为返回类型表示方法没有返回值。因此，该方法不支持在调用点赋值给变量或用作参数类型。此外，return 语句变为可选，当指定时，return 关键字后不跟任何值。例如，清单 4.4 中 Main() 的返回为 void，且方法内没有 return 语句。但是，DisplayGreeting() 包含一个不跟任何返回结果的 return 语句。

## 语言对比：C++ — 头文件

与 C++ 不同，C# 类从不将实现与声明分离。在 C# 中，没有头文件（.h）或实现文件（.cpp）。相反，声明和实现出现在同一文件中。从 C# 2.0 开始，可以将类分布在多个文件中，称为 partial 类型。但是即便如此，方法的声明和实现也必须保持在一起。C# 内联声明类型和方法，使语言更加简洁且易于维护。

## 初学者主题

## 命名空间

命名空间是所有类型的组织机制。它们提供嵌套分组机制，以便对类型进行分类。开发人员可以通过检查与初始类型位于同一命名空间中的其他类型来发现相关类型。此外，通过命名空间，两个或多个类型可以具有相同的名称，只要它们由不同的命名空间区分开来即可。

## using 指令

可以将一个命名空间中的类型导入到父命名空间代码块中，或者如果没有父代码块，则导入到整个文件中。结果是，程序员无需完全限定类型。为了实现这一点，C# 程序员包含一个 using 指令，通常位于文件顶部。例如，在清单 4.6 中，Console 没有 System 前缀。相反，它在清单顶部包含 using 指令，using System。

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

清单 4.6 的结果显示在输出 4.2 中。

## 输出 4.2：

```
Hello, my name is Inigo Montoya
```

命名空间是嵌套的。这意味着诸如 using System 这样的 using 指令并不能允许在更具体的命名空间中的方法中省略 System。例如，如果代码访问 System.Text 命名空间中的类型，则必须要么为 System.Text 包含额外的 using 指令，要么完全限定该类型。using 指令不会导入任何嵌套命名空间。由命名空间中的句点标识的嵌套命名空间需要显式导入。

## 语言对比：Java — import 指令中的通配符

Java 允许使用通配符导入命名空间，例如：

```
import javax.swing.*;
```

相比之下，C# 不支持通配符 using 指令，而是要求每个命名空间都显式导入。

## 语言对比：Visual Basic .NET — 项目范围导入指令

与 C# 不同，Visual Basic .NET 支持指定 using 指令等效项（Imports）的功能，适用于整个项目，而不仅仅是特定文件。换句话说，Visual Basic .NET 提供了一种跨越整个编译的 using 指令命令行方式。

通常，在特定命名空间中广泛使用类型会导致为该命名空间添加 using 指令，而不是完全限定命名空间中的所有类型。遵循这一趋势，几乎所有文件都在顶部包含 using System 指令。然而，在本书的其余部分，代码清单通常会省略 using System 指令。其他命名空间指令将显式包含。

using System 指令的一个有趣效果是，string 数据类型可以用不同的大小写来标识：String 或 string。前者依赖于 using System 指令，后者使用 string 关键字。两者都是对 System.String 数据类型的有效 C# 引用，生成的 CIL 代码不受所选版本的影响。²

## 高级主题

## 嵌套 using 声明

你不仅可以在文件顶部使用 using 声明，还可以在命名空间声明顶部包含它们。例如，如果声明了一个新命名空间 Awl.Michaelis.EssentialCSharp，则可以在命名空间声明顶部添加一个 using 声明（请参见清单 4.7）。

## 清单 4.7：在命名空间声明内指定 using 指令

```
namespace Awl.Michaelis.EssentialCSharp
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

清单 4.7 的结果显示在输出 4.3 中。

## 输出 4.3：

```
Hello, my name is Inigo Montoya
```

将 using 声明放在文件顶部而不是命名空间声明顶部的区别在于，该声明是

2. 我更喜欢 string 关键字，但无论程序员选择哪种表示法，理想情况下，项目中的代码应保持一致。

