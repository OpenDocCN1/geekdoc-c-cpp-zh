

# 列表 7.1：展示动态数据类型的用法

```
class Program
{
    static dynamic dyn = 1;
    public void Method1(string str)
    {
        Console.WriteLine(str);
    }
    static void Main(string[] args)
    {
        Program p = new Program();
        //This method compiles and runs successfully.
        p.Method1("Hello");
        //This compiles successfully but, shows an error at run time.
        //The value type of dynamic dyn variable is int.
        p.Method1(dyn);
    }
}
```

在列表 7.1 中，你可以看到 Method1 方法在编译时无法识别动态数据类型的取值类型。dyn 参数的数据类型为 int，该类型在运行时才被识别。

## 探索动态语言运行时

DLR 添加了一组服务，例如表达式树、调用站点缓存和动态对象互操作性，用于将 Python 和 Ruby 等动态语言集成到 CLR。动态语言的主要优势在于它可以在运行时识别对象的数据类型。然而，对于 C# 或 Visual Basic 等静态类型语言而言，对象的数据类型必须在设计时指定；否则编译器会报错。

在 Visual Studio 2010 中，除了使动态语言能够在 .NET Framework 上运行之外，DLR 还为静态类型语言提供动态功能，以实现其与动态语言的互操作。支持动态互操作性的库也可以使用 DLR 创建。这使用户能够为操作对象和访问对象成员编写简单的代码。例如，以下代码片段可用于在 C# 中递增 XML 中的计数器：
obj.SetProperty("Count", ((int)GetProperty("Count")) + 1);

以下代码片段展示了使用 DLR 执行相同操作的替代方法：
obj.Count += 1;

与 CLR 类似，DLR 也是 .NET Framework 的一部分，其安装包随 Visual Studio 2010 提供。System.Dynamic 和 System.Runtime.CompilerServices 命名空间包含 DLR 的类。

让我们简要讨论 DLR 提供的各种优势。

## DLR 的优势

你已经了解到 DLR 允许你将动态语言与 CLR 集成。DLR 允许你通过为这些语言添加动态功能来开发动态语言。例如，微软开发了 IronRuby 和 IronPython 语言，它们基于动态语言 Ruby 和 Python。DLR 提供的各种优势如下：

- 允许你轻松地将动态语言实现到 .NET Framework。要使用 DLR，语言需要创建表达式树，其中包含以树形结构表示的语言级代码、运行时辅助例程，以及可选的动态对象，该对象实现 IDynamicMetaObjectProvider 接口。DLR 和 .NET Framework 一起自动执行大量的代码分析和代码生成，这有助于你专注于独有的语言特性。

- 为静态类型语言提供动态功能。静态类型的 .NET Framework 语言，例如 C# 和 Visual Basic 可以创建动态对象并将其与静态类型对象一起使用。

例如，C# 和 Visual Basic 可以使用动态对象进行 .NET 反射 HTML 和文档对象模型 DOM。

- 改善 DLR 和 .NET Framework 的未来发展。DLR 实现的语言可以有利于 DLR 和 .NET Framework 的未来改进。例如，如果微软发布了具有各种改进功能的新版 .NET Framework，例如改进的垃圾回收器或更快的程序集加载时间，使用 DLR 的语言可以立即获得这些功能的好处。即使 DLR 改进了编译或任何其他优化，使用 DLR 实现的语言的性能也会得到提升。

- 实现库和对象的共享，这意味着在一个语言中实现的对象和库可以使用 DLR 被其他语言使用。此外，DLR 还实现了静态类型和动态语言之间的互操作性。例如，C# 可以创建一个动态对象，该对象使用用动态语言编写的库。同时，.NET Framework 的库也可以被动态语言使用。

- 通过支持高级缓存实现动态操作的快速执行。DLR 为在运行时实现中使用对象访问操作创建规则，然后缓存这些规则，以限制在对同一类型对象执行相同代码的后续执行期间耗尽资源的绑定计算。

现在，让我们讨论 DLR 的架构。

## DLR 的架构

动态语言编译器在 DLR 之上实现，并生成抽象语法树，该树由 DLR 库使用。DLR 为 CLR 提供一些服务，例如表达式树、调用站点缓存和动态对象互操作性。DLR 使用表达式树表示语言语义，这有助于绑定器封装语言的语义并指定在调用站点执行的运算。调用站点是指在代码中对动态对象执行逻辑和数学运算，例如 a + b 或 a.b() 的区域。

图 7.2 显示了 DLR 的架构：

![](img/e073a4882197be4ab61103cbe0bcb394_288_0.png)

图 7.2：展示 DLR 的架构

DLR 为 CLR 提供的服务用于支持动态语言。这些服务包括以下内容：

- 表达式树—使 DLR 能够扩展语言集成查询 LINQ 表达式树的功用，例如控制流、赋值和其他语言建模节点到动态语言。这些表达式树以抽象语法树 AST 的形式定义语言的语义。AST 使 DLR 能够动态生成代码，CLR 在运行时执行该代码。

- **调用站点缓存**—使 DLR 能够存储操作和变量特征的信息，例如其数据类型。调用站点缓存还检查是否以前执行过此类操作，并检索有关变量的所有信息。

- **动态对象互操作性**—使 DLR 能够提供表示动态对象和操作的类和接口集合。语言开发人员和动态库的作者可以使用这些类和接口创建可在静态和动态类型语言中使用的类。

让我们学习 ExpandoObject 和 DynamicObject 类。

## 理解 ExpandoObject 和 DynamicObject 类

DLR 是使用 System.Dynamic 命名空间的类和接口创建的。该命名空间包含 ExpandoObject 和 DynamicObject 等类。这些类用于在 C# 中实现运行时功能。ExpandoObject 类是一个其成员可以在运行时显式添加和删除的类。此类的对象可以在运行时动态初始化。换句话说，ExpandoObject 类允许对象的动态绑定，这使你可以使用与 dynobj.Method 方法类似的标准语法，而不是使用更复杂的语法，例如 dynobj.getAttribute("Method")。

DynamicObject 类允许你定义可以在动态对象上执行的具体操作以及执行这些操作的<|message|>方法。例如，你可以定义获取或设置对象属性、调用方法或执行标准数学运算，例如加法和乘法的后果。DynamicObject 类提供了一个指定运行时动态行为的父类。此父类不能直接实例化；因此，要实现动态行为，必须从 DynamicObject 类继承并重写必要的方法。

在详细讨论了 C# 的动态增强功能之后，让我们现在学习如何在各种应用程序中使用这些增强功能。
