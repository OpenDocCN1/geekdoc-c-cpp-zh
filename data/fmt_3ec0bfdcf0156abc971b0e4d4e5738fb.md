
| `method` | 方法、属性 `get` 访问器或属性 `set` 访问器 |
| `param` | 方法或属性 `set` 访问器参数 |
| `property` | 属性 |
| `return` | 方法、索引器属性或属性 `get` 访问器的返回值 |
| `type` | 结构、类、接口或枚举 |

虽然属性通常应用于其前面的元素，但你也可以明确指定其应用的目标。例如，你可以指定属性应用于方法、其参数还是其返回值，如清单 20.4 所示。

### 清单 20.4 属性参数

```csharp
[CustomAttribute]
string Method()
{
    return String.Empty;
}

[method: CustomAttribute]
string Method()
{
    return String.Empty;
}

[return: CustomAttribute]
string Method()
{
    return String.Empty;
}
```

## 使用通用属性

.NET 框架定义了许多你可以用于自己应用程序的属性。最常见的是 *Obsolete* 属性、*Conditional* 属性以及一组全局属性。

### Obsolete 属性

*Obsolete* 属性表明某个代码声明不应再被使用，并导致编译器生成警告或错误，具体取决于属性的配置方式。此属性可以不带参数使用，但建议提供解释并指明是否应生成编译器警告或错误。清单 20.5 显示了使用 *Obsolete* 属性的示例。

### 清单 20.5 Obsolete 属性

```csharp
public class Example
{
    [Obsolete("Consider using OtherMethod instead.", false)]
    public string Method()
    {
        return String.Empty;
    }

    public string OtherMethod()
    {
        return "Test";
    }
}
```

### Conditional 属性

**Conditional** 属性表明某个代码声明依赖于预处理器条件编译符号（例如 `DEBUG`），并且可以应用于类或方法。编译器使用此属性来确定调用是否包含在内或省略。如果在编译期间存在条件符号，则包含该调用；否则不包含。如果将 **Conditional** 属性应用于方法，则该方法必须没有返回值。清单 20.6 显示了使用 **Conditional** 属性的示例。

### 清单 20.6 Conditional 属性

```csharp
public class Example
{
    [Conditional("DEBUG")]
    public void DisplayDiagnostics()
    {
        Console.WriteLine("Diagnostic information.");
    }

    public string Method()
    {
        return "Test";
    }
}
```

**Conditional** 属性还可以应用于自定义属性，在这种情况下，只有当定义了编译符号时，该属性才会添加元数据信息。

### #if 和 #endif 预处理器符号

使用 **Conditional** 属性与使用 `#if` 和 `#endif` 预处理器符号类似，但可以提供一种更干净的替代方案，从而减少错误。下面显示了清单 20.6 中所示的类使用 `#if`/`#endif` 代替 **Conditional** 属性的情况。

> **顺便说一下**

```csharp
public class Example
{
    #if DEBUG
        public void DisplayDiagnostics()
        {
            Console.WriteLine("Diagnostic information.");
        }
    #endif

    public string Method()
    {
        return "Test";
    }
}
```

虽然你可以混合使用 `Conditional` 属性和 `#if`/`#endif` 预处理器符号，但如果这样做，你需要非常小心。使用 `#if`/`#endif` 移除代码发生在编译过程的较早阶段，可能会导致编译器无法编译 `Conditional` 方法。

### 全局属性

虽然大多数属性应用于特定的代码声明，但有些属性应用于整个程序集或模块。这些属性出现在源代码中，位于任何 `using` 指令之后，但位于任何代码声明（如类或命名空间声明）之前。

> **顺便说一下**
>
> **程序集清单**
>
> 程序集清单包含描述程序集内部元素关系的数据，包括版本和安全信息。清单通常包含在编译后的文件中。

通常，全局属性放置在 `AssemblyInfo.cs` 文件中，但如果这些文件在单个编译路径中编译，它们也可以出现在多个文件中。常用的全局属性显示在表 20.2 中。

### 表 20.2 全局属性

| 属性 | 目的 |
| :--- | :--- |
| **程序集标识属性** |  |
| `AssemblyName` | 程序集的名称 |
| `AssemblyVersion` | 程序集的版本 |
| `AssemblyCulture` | 程序集支持的语言环境 |
| `AssemblyFlags` | 指示是否允许多个程序集副本共存 |
| **信息属性** |  |
| `AssemblyProduct` | 指定程序集的产品名称 |
| `AssemblyTrademark` | 指定程序集的商标 |
| `AssemblyInformationalVersion` | 指定程序集的信息版本 |
| `AssemblyCompany` | 指定程序集的公司名称 |
| `AssemblyCopyright` | 指定程序集的版权 |
| `AssemblyFileVersion` | 指定 Windows 文件版本资源的版本号 |
| `CLSCompliant` | 指示程序集是否符合 CLS |
| **程序集清单属性** |  |
| `AssemblyTitle` | 指定程序集清单的标题 |
| `AssemblyDescription` | 指定程序集清单的描述 |
| `AssemblyConfiguration` | 指定程序集清单的配置 |
| `AssemblyDefaultAlias` | 指定程序集清单的友好默认别名 |

## 使用自定义属性

如果你需要为自己的应用程序提供自定义元数据，可以通过定义派生自 **Attribute** 的属性类（直接或间接触发）来创建自定义属性。

例如，你可以定义一个包含与代码更改相关联的 Team Foundation Server 工作项号的自定义属性，如清单 20.7 所示。

### 清单 20.7 创建自定义属性

```csharp
[AttributeUsage(AttributeTargets.All, Inherited = false, AllowMultiple = true)]
public sealed class WorkItemAttribute : System.Attribute
{
    private int workItemId;

    public WorkItemAttribute(int workItemId)
    {
        this.workItemId = workItemId;
    }

    public int WorkItemId
    {
        get
        {
            return this.workItemId;
        }
    }

    public string Comment
    {
        get;
        set;
    }
}
```

自定义属性有一个公有构造函数，其参数构成了属性的位置参数。任何公有读写字段或属性——在这种情况下是 `Comment` 属性——都成为命名参数。最后，`AttributeUsage` 属性表明 `WorkItem` 属性在任何声明上都是有效的，它可以应用多次，并且不会自动应用于派生类型。

然后，你可以如清单 20.8 所示使用此属性。

### 清单 20.8 应用自定义属性

```csharp
[WorkItem(1234,
        Comment = "Created a test class to show how attributes can be used.")]
public class Test
{
    [WorkItem(5678, Comment = "Changed property to use auto-property syntax.")]
    public int P
    {
        get;
        set;
    }
}
```

## 在运行时访问属性

如果你无法在运行时访问该信息，那么通过属性向应用程序添加元数据并没有太大作用。.NET 框架通过称为反射的过程提供对运行时类型信息的访问，包括属性提供的元数据。由于属性提供元数据，与属性关联的代码实际上直到查询属性时才执行。

使用 `Attribute.GetCustomAttribute` 方法检索自定义属性很容易。清单 20.9 显示了在运行时访问清单 20.7 中定义的自定义属性和清单 20.8 中定义的简单类的示例。图 20.1 显示了清单 20.9 的输出。

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

`Attribute.GetCustomAttribute` 返回单个特性。如果代码元素上定义了多个同类型特性，或者你需要处理多个不同类型的特性，你可以使用 `Attribute.GetCustomAttributes` 方法来返回一个自定义特性数组。然后，你可以枚举该结果数组，从数组元素中检查并提取信息，如代码清单 20.10 所示。

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
  **答。** 自定义特性通过创建一个继承自 `Attribute` 的类来定义。

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

在第 1 小时“**.NET 框架与 C#**”中，你了解到 .NET 框架的第四个主要组件是动态语言运行时，即 `DLR`。`DLR` 建立在公共语言运行时（`CLR`）之上，并为动态语言（如 `IronRuby` 和 `IronPython`）提供语言服务。尽管 C# 语言一直允许你编写与动态语言交互的代码——例如，调用在 JavaScript 对象中定义的方法——但实现这些交互所需的语法远非简单。该语法还会根据你所针对的特定动态语言而变化。

借助 `DLR`，C# 可以提供一个简单且一致的语言语法来与动态语言进行交互。在这一章中，你将学习动态类型，并了解如何使用它们与动态语言进行互操作。

## 使用动态类型

动态类型由 `dynamic` 关键字指示，其操作绕过了 C# 编译器提供的编译时类型检查。相反，这些操作在运行时解析。绕过静态类型检查简化了对 COM API（如 Office API）和动态语言（如 `IronPython` 和 `JavaScript`）的访问。

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

6. 按 `Ctrl+F5` 运行应用程序。你应该注意到应用程序现在可以编译，但会抛出运行时异常，如图 21.2 所示。

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_461_1.png)

**图 21.2**

RuntimeBinder 异常

7. 更改第二个语句，使传递的参数为字符串 “3” 而不是整数值 3。
8. 再次按 `Ctrl+F5` 运行应用程序，并观察输出是否与图 21.3 中显示的一致。

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_461_2.png)

**图 21.3**

探索动态类型的输出
