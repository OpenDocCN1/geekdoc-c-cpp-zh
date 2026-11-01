
```csharp
{
    Console.WriteLine("Element {0} = {1}", i, *(pArray + i));
}

Console.ReadLine();
}
}
}
```

QuickArray 示例的输出如 图 13-7 所示。

![](img/d7d2ffa0a76feaab821930e95daace93_393_0.png)

**图 13-7**

## 摘要

请记住，要成为一名真正精通 C# 的程序员，你必须对内存分配和垃圾回收的工作原理有扎实的理解。本章描述了 CLR 如何在堆和栈上管理并分配内存。它还说明了如何编写正确释放非托管资源的类，以及如何在 C# 中使用指针。这些都是高级主题，初学者往往理解不足且经常实现错误。

本章应作为你在第 15 章错误处理以及第 20 章线程处理中学到的内容的补充。本书的下一章将介绍 C# 中的反射。

## 14 反射

### 本章内容？

- 使用自定义特性
- 使用反射在运行时检查元数据
- 从启用反射的类构建访问点

本章重点介绍自定义特性和反射。自定义特性是一种允许你将自定义元数据与程序元素关联起来的机制。此元数据在编译时创建并嵌入到程序集中。反射是一个通用术语，描述了在运行时检查和操作程序元素的能力。例如，反射允许你：

- 枚举类型的成员
- 实例化新对象
- 执行对象的成员
- 查找有关类型的信息
- 查找有关程序集的信息
- 检查应用于类型的自定义特性
- 创建和编译新程序集

此列表代表了大量功能，并涵盖了 .NET Framework 类库提供的最强大和最复杂的能力之一。虽然本章没有足够的篇幅涵盖反射的所有功能，但它专注于你最有可能最频繁使用的元素。

为了演示自定义特性和反射，你开发了一个基于一家公司定期发布软件升级并希望自动记录这些升级详细信息的示例。在示例中，你定义自定义特性以指示程序元素上次修改的日期以及所做的更改。然后你使用反射开发一个应用程序，该应用程序在程序集中查找这些特性，并可以自动显示自给定日期以来对软件所做的所有升级的详细信息。

本章的另一个示例考虑了一个从数据库读取或写入数据库的应用程序，并使用自定义特性作为标记哪些类和属性对应于哪些数据库表和列的方式。通过在运行时从程序集中读取这些特性，程序能够自动检索或将数据写入数据库中的适当位置，而无需为每个表或列提供特定逻辑。

错误。例如，如果特性类指示特性只能应用于类，但你将其应用于结构体定义，将会发生编译错误。

继续示例，假设你已按如下方式定义 FieldName 特性：

```csharp
[AttributeUsage(AttributeTargets.Property,
    AllowMultiple=false,
    Inherited=false)]
public class FieldNameAttribute: Attribute
{
    private string name;
    public FieldNameAttribute(string name)
    {
        this.name = name;
    }
}
```

以下各节讨论此定义的每个元素。

### AttributeUsage 特性

首先需要注意的是，特性类本身被一个特性标记——System.AttributeUsage 特性。这是由 Microsoft 定义的特性，C# 编译器为其提供特殊支持。（你可以争辩说 AttributeUsage 根本不是一个特性；它更像是一个元特性，因为它仅适用于其他特性，而不仅仅是任何类。）AttributeUsage 的主要目的是标识可以应用自定义特性的程序元素类型。此信息由 AttributeUsage 特性的第一个参数给出——此参数是强制性的，其类型为枚举类型 AttributeTargets。在前面的示例中，你已指示 FieldName 特性只能应用于属性，这很好，因为这正是你在之前的代码片段中对其应用的方式。AttributeTargets 枚举的成员是：

- `All`
- `Assembly`
- `Class`
- `Constructor`
- `Delegate`
- `Enum`
- `Event`
- `Field`
- `GenericParameter` (.NET 2.0 and higher only)
- `Interface`
- `Method`
- `Module`
- `Parameter`
- `Property`
- `ReturnValue`
- `Struct`

此列表标识了可以应用特性的所有程序元素。请注意，当将特性应用于程序元素时，你将其放在方括号中，紧挨在元素之前。然而，前述列表中的两个值不对应于任何程序元素：Assembly 和 Module。特性可以应用于整个程序集或模块，而不是应用于你的

可以从 Wrox 网站 www.wrox.com 下载) 作为一个组合的 Visual Studio 解决方案，如第 16 章“Visual Studio 2010”中所述。下载内容包括所需的 Visual Studio 2010 解决方案文件。

### WhatsNewAttributes 库程序集

本节从核心 WhatsNewAttributes 程序集开始。源代码包含在文件 WhatsNewAttributes.cs 中，该文件位于本章示例代码中 WhatsNewAttributes 解决方案的 WhatsNewAttributes 项目中。执行此操作的语法相当简单。在命令行中，你向编译器提供标志 target:library。要编译 WhatsNewAttributes，请输入以下内容：

```
csc /target:library WhatsNewAttributes.cs
```

WhatsNewAttributes.cs 文件定义了两个特性类，LastModifiedAttribute 和 SupportsWhatsNewAttribute。LastModifiedAttribute 特性是你可以用来标记项目上次修改时间的特性。它接受两个强制参数（传递给构造函数的参数）：修改日期和包含更改描述的字符串。还有一个名为 issues 的可选参数（存在公共属性），可用于描述项目的任何未解决问题。

实际上，你可能希望此特性适用于任何内容。为了保持代码简单，这里将其使用限制为类和方法。你将允许它多次应用于同一项（AllowMultiple=true），因为一项可能被修改多次，并且每次修改都必须用单独的特性实例标记。

SupportsWhatsNew 是一个较小的类，表示一个不接受任何参数的特性。此特性的想法是它是一个程序集特性，用于标记你通过 LastModifiedAttribute 维护文档的程序集。这样，后续将检查此程序集的程序就知道它正在读取的程序集是你实际使用自动化文档流程的程序集。以下是此示例部分的完整源代码：

```csharp
using System;

namespace WhatsNewAttributes
{
    [AttributeUsage(
        AttributeTargets.Class | AttributeTargets.Method,
        AllowMultiple=true, Inherited=false)]
    public class LastModifiedAttribute: Attribute
    {
        private readonly DateTime _dateModified;
        private readonly string _changes;

        public LastModifiedAttribute(string dateModified, string changes)
        {
            _dateModified = DateTime.Parse(dateModified);
            _changes = changes;
        }

        public DateTime DateModified
        {
            get { return _dateModified; }
        }

        public string Changes
        {
            get { return _changes; }
        }

        public string Issues { get; set; }
    }
}
```
