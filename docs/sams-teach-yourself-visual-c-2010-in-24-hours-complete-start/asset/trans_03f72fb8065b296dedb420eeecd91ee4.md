

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_455_0.png)

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_455_1.png)

## 代码清单 20.9 在运行时访问单个特性

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        WorkItemAttribute attribute =
            Attribute.GetCustomAttribute(typeof(Test), typeof(WorkItemAttribute))
            as WorkItemAttribute;

        if (attribute != null)
        {
            Console.WriteLine("{0}: {1}", attribute.WorkItemId, attribute.Comment);
        }
    }
}
```

Attribute.GetCustomAttribute 返回单个特性。如果代码元素上定义了多个同类型特性，或者你需要处理多个不同类型的特性，你可以使用 Attribute.GetCustomAttributes 方法来返回一个自定义特性数组。然后，你可以枚举该结果数组，从数组元素中检查并提取信息，如代码清单 20.10 所示。

## 代码清单 20.10 在运行时访问多个特性

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        var workItems = from attribute in
                        Attribute.GetCustomAttributes(typeof(Test)).
                        OfType<WorkItemAttribute>()
                        select attribute;

        foreach (var attribute in workItems)
        {
            Console.WriteLine("{0}: {1}", attribute.WorkItemId,
                              attribute.Comment);
        }
    }
}
```

## 总结

特性提供了一种简单而强大的方式来为你的应用程序添加元数据。它们在 .NET 框架中广泛使用，用于调用非托管代码、描述类、方法和接口的 COM 属性、描述哪些类成员应被序列化以用于持久化、指定安全要求以及控制 JIT 编译器优化，这只是其中几项用途。

在这一章中，你学习了特性，包括 .NET 框架提供的一些常见特性。然后，你创建了自己的自定义特性，并学习了如何在运行时检索该特性并访问其值。

## 问答

- **问。** *什么是特性？*
  **答。** 特性是一个用于向代码元素添加元数据的类。

- **问。** *什么是位置特性参数？*
  **答。** 位置特性参数是特性所需的参数，必须按特定顺序提供。它们由特性的构造函数参数定义。

- **问。** *如何定义自定义特性？*
  **答。** 自定义特性通过创建一个继承自 Attribute 的类来定义。

## 练习场

### 测验

1. `Obsolete` 特性能否生成编译器错误？
2. `Conditional` 特性是否影响编译？
3. 有哪些两种方法可以在运行时检索自定义特性？

## 答案

1. 是的，如果将第二个位置参数设置为 `true`，`Obsolete` 特性可以生成编译器错误。
2. 是的，`Conditional` 特性可以影响编译。如果特性参数中指定的条件符号不存在，则不会包含对该方法的调用。
3. 在运行时检索自定义特性的两种方法是 `Attribute.GetCustomAttribute` 和 `Attribute.GetCustomAttributes`。

## 练习题

本章没有练习题。

*此页故意留白*

# 动态类型与语言互操作性

## 本章学习内容：

- 使用动态类型
- 理解 DLR
- 与 COM 互操作
- 反射互操作性

在第 1 小时“**.NET 框架与 C#**”中，你了解到 .NET 框架的第四个主要组件是动态语言运行时，即 DLR。DLR 建立在公共语言运行时（CLR）之上，并为动态语言（如 IronRuby 和 IronPython）提供语言服务。尽管 C# 语言一直允许你编写与动态语言交互的代码——例如，调用在 JavaScript 对象中定义的方法——但实现这些交互所需的语法远非简单。该语法还会根据你所针对的特定动态语言而变化。

借助 DLR，C# 可以提供一个简单且一致的语言语法来与动态语言进行交互。在这一章中，你将学习动态类型，并了解如何使用它们与动态语言进行互操作。

## 使用动态类型

动态类型由 `dynamic` 关键字指示，其操作绕过了 C# 编译器提供的编译时类型检查。相反，这些操作在运行时解析。绕过静态类型检查简化了对 COM API（如 Office API）和动态语言（如 IronPython 和 JavaScript）的访问。

`dynamic` 关键字指示属性、字段、索引器、参数、返回值或局部变量的类型。它也可以是显式转换的目标类型，或作为 `typeof` 运算符的参数。

### 顺便提一下：动态类型

尽管本章中使用了“动态类型”这一术语，但实际上只有一种“动态”类型，就像只有一种“object”类型一样。当在本章中使用“动态类型”时，指的是被当作 `dynamic` 类型处理的不同类型。

虽然看起来可能有些矛盾，`dynamic` 类型的变量在编译时是静态类型化的 `dynamic` 类型，并且在大多数情况下表现得像是 `object`。当编译器遇到 `dynamic` 类型时，它假设该类型可以支持任何操作。如果代码无效，错误将仅在运行时捕获。

### 动手尝试：探索动态类型

要查看动态类型在编译时和运行时的行为，请遵循以下步骤。

1. 在 Visual Studio 中创建一个新的控制台应用程序。
2. 添加一个名为 `SimulatedDynamic` 的新类，如下所示：

```csharp
class SimulatedDynamic
{
    public SimulatedDynamic() { }
    public void Method1(string s)
    {
        Console.WriteLine(s);
    }
}
```

3. 通过添加以下语句来修改 **Program** 类的 **Main** 方法：

```csharp
SimulatedDynamic c1 = new SimulatedDynamic();
c1.Method1(3);
```

4. 尝试编译应用程序。你应该接收到图 21.1 中显示的编译器错误。

5. 更改你在第 3 步中输入的第一个语句，使 `c1` 的类型为 `dynamic`。

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_461_0.png)

**图 21.1**
错误消息

6. 按 Ctrl+F5 运行应用程序。你应该注意到应用程序现在可以编译，但会抛出运行时异常，如图 21.2 所示。

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_461_1.png)

**图 21.2**
RuntimeBinder 异常

7. 更改第二个语句，使传递的参数为字符串 “3” 而不是整数值 3。
8. 再次按 Ctrl+F5 运行应用程序，并观察输出是否与图 21.3 中显示的一致。

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_461_2.png)

**图 21.3**
探索动态类型的输出

当你最初尝试编译你刚写的程序时，编译器确定你试图执行的方法不存在，因为 `c1` 被静态类型化为 `SimulatedDynamic` 类型。但是，当你将其静态类型更改为 `dynamic` 时，编译器不再执行类型检查，从而导致运行时异常发生。

## 在运行时确定动态类型

在编译时，`dynamic` 变量被编译为 `object` 类型，编译器确保存储关于每条语句试图做什么的元数据。在运行时，这些信息会被检查，任何无效的语句都会导致运行时异常。

当运行时遇到“动态”类型（实际上只是一个带有额外元数据的 `object` 类型，指示它应该被动态评估）时，它
