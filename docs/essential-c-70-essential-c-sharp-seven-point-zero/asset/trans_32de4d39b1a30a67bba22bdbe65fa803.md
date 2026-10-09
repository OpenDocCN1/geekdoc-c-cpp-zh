

与常量字段不同，带有 `readonly` 修饰符的字段可以在不同的实例之间有所不同。事实上，只读字段的值可以在构造函数内部发生变化。此外，只读字段可以作为实例字段或静态字段存在。另一个关键区别是，你可以在执行时而不是仅在编译时分配只读字段的值。鉴于只读字段必须在构造函数或初始化器中设置，这类字段是唯一一种编译器要求从对应属性之外的代码中访问该字段的情况。除了这一例外情况，你应避免在包裹属性以外的任何地方访问后备字段。

相较于 `const` 字段，带有 `readonly` 修饰符的字段的一个重要特性是，只读字段并不局限于具有字面值的类型。例如，可以声明一个 `readonly` 的 `System.Guid` 实例字段：

```csharp
public static readonly Guid ComIUnknownGuid =
    new Guid("00000000-0000-0000-C000-000000000046");
```

然而，使用常量是无法做到这一点的，因为 C# 中没有 GUID 的字面量表示。

鉴于指南指出字段不应从包裹属性外部访问，在 C# 6.0（或更高版本）环境下编程的人会发现，几乎从未需要过使用 `readonly` 修饰符。相反，更推荐使用只读自动实现属性，正如本章前文所讨论的那样。

请参见清单 6.45 以获取更多只读示例。

## 清单 6.45：声明只读自动实现属性

```csharp
class TicTacToeBoard
{
    // 将两位玩家的移动设置为全为 false（空白）
    //  |   |
    //  |---|
    //  |   |
    //  |---|
    //  |   |
    public bool[,,] Cells { get; } = new bool[2, 3, 3];
    // 错误：属性 Cells 是只读的，
    // 因此无法赋值
    //public void SetCells(bool[,,] value) =>
    //    Cells = new bool[2, 3, 3];
    // ...
}
```

无论是使用 C# 6.0 的只读自动实现属性，还是使用字段上的 `readonly` 修饰符，确保数组引用的不可变性是一种有用的防御性编程技术。它确保数组实例保持不变，同时允许数组内的元素发生变化。如果没有只读约束，人们太容易错误地分配一个新数组给该成员，从而丢弃现有数组而不是更新单个数组元素。换句话说，对数组使用只读方法并不会冻结数组的内容。相反，它冻结了数组实例（因此也冻结了数组中元素的数量），因为不可能将值重新分配给新实例。数组的元素仍然是可写的。

## 指南

-   **应该（DO）** 在 C# 6.0（或更高版本）中优先使用只读自动实现属性，而不是只读字段。
-   **应该（DO）** 在 C# 6.0 之前，使用带有 `public static readonly` 修饰的字段来表示预定义的对象实例。
-   **避免（AVOID）** 如果需要版本 API 兼容性，不要将 C# 6.0 之前 `public readonly` 修饰的字段更改为 C# 6.0（或更高版本）中的只读自动实现属性。

## 嵌套类

除了定义方法、类内部还可以定义类。这样的类称为**嵌套类**。当某个类在其包含类之外没有太大意义时，你就需要使用嵌套类。

考虑一个处理程序命令行选项的类。这样的类通常对每个程序都是独一无二的，因此没有理由让 `CommandLine` 类在包含 `Main()` 方法的类之外可访问。清单 6.46 展示了这样一个嵌套类。

## 清单 6.46：定义嵌套类

```csharp
// CommandLine 嵌套在 Program 中
class Program
{
    // 定义一个用于处理命令行的嵌套类
    private class CommandLine
    {
        public CommandLine(string[] arguments)
        {
            for (int argumentCounter = 0;
                argumentCounter < arguments.Length;
                argumentCounter++)
            {
                switch (argumentCounter)
                {
                    case 0:
                        Action = arguments[0].ToLower();
                        break;
                    case 1:
                        Id = arguments[1];
                        break;
                    case 2:
                        FirstName = arguments[2];
                        break;
                    case 3:
                        LastName = arguments[3];
                        break;
                }
            }
        }

        public string Action;
        public string Id;
        public string FirstName;
        public string LastName;
    }

    static void Main(string[] args)
    {
        CommandLine commandLine = new CommandLine(args);

        switch (commandLine.Action)
        {
            case "new":
                // 创建新员工
                // ...
                break;
            case "update":
                // 更新现有员工的数据
                // ...
                break;
            case "delete":
                // 删除现有员工的文件
                // ...
                break;
            default:
                Console.WriteLine(
                    "Employee.exe " +
                    "new|update|delete <id> [firstname] [lastname]");
                break;
        }
    }
}
```

在这个示例中，嵌套类是 `Program.CommandLine`。与所有类成员一样，在包含类内部引用嵌套类时无需包含类标识符，因此你只需将其称为 `CommandLine` 即可。

嵌套类的一个独特特性是能够指定 `private` 作为类本身的访问修饰符。由于此类目的是解析命令行并将每个参数放入单独的字段中，因此在本应用程序中，`Program.CommandLine` 仅与 `Program` 类相关。使用 `private` 访问修饰符定义了该类的预期可访问性，并防止从类外部访问。只有当类是嵌套时，你才可以这样做。

嵌套类内部的 `this` 成员指的是嵌套类的实例，而不是包含类的实例。嵌套类访问包含类实例的一种方式是通过显式传递包含类实例，例如通过构造函数或方法参数。

嵌套类的另一个有趣特性是它们可以访问包含类的任何成员，包括私有成员。然而，反之则不然：包含类无法访问嵌套类的私有成员。

嵌套类并不常见。如果它们很可能在包含类型外部被引用，则不应定义它们。此外，请谨慎对待公共嵌套类；它们可能表明代码质量较差，容易令人困惑且难以发现。

## 指南

> **避免（AVOID）** 公开暴露的嵌套类型。唯一的例外是，此类类型的声明不太可能发生，或者涉及高级自定义场景。

## 语言对比：Java—内部类

Java 不仅包含嵌套类的概念，还包含内部类（inner class）的概念。内部类对应于与包含类实例相关联的对象，而不仅仅是具有语法关系。在 C# 中，你可以通过在外层类中包含嵌套类型的实例字段来实现相同的结构。工厂方法或构造函数可以确保在内部类实例中也设置了对外层类相应实例的引用。

## 分部类

C# 2.0 中增加的另一个语言特性是**分部类（partial classes）**。分部类是类的一部分，编译器可以将这些部分组合起来形成完整的类。虽然你可以在同一个文件中定义两个或多个分部类，但分部类的一般目的是允许将类定义拆分到多个文件中。这主要对于生成或修改代码的工具非常有用。使用分部类后，工具可以在一个单独的文件上工作，而开发人员则在手动编码另一个文件。

## 定义分部类

C# 2.0（及更高版本）允许通过在 `class` 关键字之前立即添加上下文关键字 *partial* 来声明分部类，如清单 6.47 所示。

## 清单 6.47：定义分部类

```csharp
// 文件: Program1.cs
partial class Program
{
}

// 文件: Program2.cs
partial class Program
{
}
```

在这种情况下，*Program* 的每个部分都被放置到单独的文件中，正如注释所标识的那样。

除了与代码生成器配合使用外，分部类的另一个常见用途是将任何嵌套类放入它们自己的文件中。这符合

