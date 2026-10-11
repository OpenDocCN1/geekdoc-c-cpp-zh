
当你最初尝试编译你刚写的程序时，编译器确定你试图执行的方法不存在，因为 `c1` 被静态类型化为 `SimulatedDynamic` 类型。但是，当你将其静态类型更改为 `dynamic` 时，编译器不再执行类型检查，从而导致运行时异常发生。

## 在运行时确定动态类型

在编译时，`dynamic` 变量被编译为 `object` 类型，编译器确保存储关于每条语句试图做什么的元数据。在运行时，这些信息会被检查，任何无效的语句都会导致运行时异常。

当运行时遇到“动态”类型（实际上只是一个带有额外元数据的 `object` 类型，指示它应该被动态评估）时，它

使用对象的运行时类型来确定实际类型应该是什么。在上一个练习的步骤 6 中，方法参数的运行时类型是 `System.Int32`。这导致运行时尝试解析具有以下签名的方法：

```csharp
void Method1(int)
```

由于类型 `SimulatedDynamic` 中不存在这样的方法，因此会抛出运行时异常。然而，在步骤 8 中，运行时尝试解析具有以下签名的方法：

```csharp
void Method1(string)
```

该方法确实存在。

## 转换

大多数动态操作的结果是另一个动态对象。然而，动态对象与其他类型之间存在转换，这使得您可以轻松地在动态行为和非动态行为之间切换。

所有预定义数据类型与 `dynamic` 之间存在隐式转换，这意味着列表 21.1 中显示的所有以下语句都是有效的。

### 列表 21.1 与动态类型的隐式转换

```csharp
dynamic d1 = 42;
dynamic d2 = "The quick brown fox";
dynamic d3 = DateTime.Now;

int s1 = d1;
string s2 = d2;
DateTime s3 = d3;
```

### 注意！

### 动态转换

存在的隐式转换是动态转换，像所有动态操作一样，它们在运行时解析。您应该小心，不要将动态和非动态转换混合使用。例如，尝试将 `d3` 赋值给 `s1` 会导致运行时异常。

## 动态重载解析

由于 `dynamic` 类型值的实际类型直到运行时才已知，如果一个或多个方法参数被指定为 `dynamic`，那么该方法可能直到运行时才能解析。编译器首先尝试正常的重载解析，如果找到精确匹配，则使用该方法的重载。这意味着，如果多个方法都匹配相同的运行时类型，并且运行时无法确定如何解析该歧义，则方法解析会因模糊匹配异常而失败。

考虑列表 21.2 中显示的代码。

### 列表 21.2 包含动态方法的类

```csharp
class MethodResolution
{
    public void M(int i) { }
    public void M(int i, dynamic d) { }
    public void M(dynamic d, int i) { }
    public void M(dynamic d1, dynamic d2) { }
}
```

以下代码将在运行时失败，如图 21.4 所示。

```csharp
dynamic m = new MethodResolution();
m.M(42, 7);
```

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_463_0.png)

**图 21.4 运行时模糊方法调用异常**

此方法调用是模糊的，因为两个参数的运行时类型都是 `System.Int32`。当运行时尝试解析方法 `M` 时，它将这些方法视为如在列表 21.3 中定义的那样。

### 列表 21.3 用于方法解析的动态方法

```csharp
class MethodResolution
{
    public void M(int i) { }
    public void M(int i, object d) { }
    public void M(object d, int i) { }
    public void M(object d1, object d2) { }
}
```

根据该重载列表，它们都不是最佳匹配，因为每个方法在其中一个参数上比另一个匹配得更好。由于无法解析该方法，因此会抛出运行时错误。

## 理解 DLR

为了让 C# 能够处理动态类型，它利用了 DLR，这是一个位于 CLR 之上的运行时环境，为动态语言提供语言服务和支持。这使得动态语言能够享受静态类型语言所享有的同等程度的语言互操作性，并为这些语言引入了动态对象。图 21.5 显示了 DLR 的基本架构，并展示了它如何与 .NET Framework 的其他部分集成。

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_464_0.png)

与 ADO.NET 数据提供程序类似，DLR 使用绑定器来封装语言语义并指定如何执行操作。这不仅实现了统一的语法，还使静态类型语言能够使用 DLR 提供的服务。

语言绑定器使用 LINQ 表达式树来执行操作。为了支持这一点，DLR 扩展了 LINQ 表达式树，以包含控制流、赋值和其他语言特定的节点。代码中执行动态对象操作的任何位置都被视为**动态调用站点**，DLR 会缓存所涉及的动态类型的元数据以及关于正在执行的操作的信息。如果随后再次执行该操作，信息将从缓存中检索，从而提高性能。

最后，为了支持与其他语言的互操作性，DLR 提供了 `IDynamicMetaObjectProvider` 接口以及 `DynamicObject` 和 `ExpandoObject` 类。

> **理解 `IDynamicMetaObjectProvider`**
>
> `IDynamicMetaObjectProvider` 接口表示一个动态对象。如果您有定义动态对象行为的高级场景，应该创建 `IDynamicMetaObjectProvider` 自己的实现；否则，应该从 `DynamicObject` 派生或使用 `ExpandoObject`。

如果您需要一个对象来在运行时动态添加或删除成员，您可以创建一个 `ExpandoObject` 的实例。`ExpandoObject` 的实例可以在任何支持 DLR 的语言之间共享。例如，您可以在 C# 中创建一个实例，并将其用作 IronPython 函数的参数。列表 21.4 展示了一个使用 `ExpandoObject` 动态添加新属性的简单示例。

### 列表 21.4 使用 ExpandoObject

```csharp
dynamic expando = new ExpandoObject();

expando.ExampleProperty = "This is a dynamic property.";
Console.WriteLine(expando.ExampleProperty);
Console.WriteLine(expando.ExampleProperty.GetType());
```

图 21.6 显示了列表 21.4 中代码的输出。

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_465_0.png)

如果您需要为类定义特定操作，以便在动态使用时生效，您可以将您的类从 `DynamicObject` 派生。正如 `ExpandoObject` 实例一样，任何支持 DLR 的语言都可以共享派生的 `DynamicObject` 类型的实例。

列表 21.5 中的代码显示了一个动态字典，它允许您通过键访问字典值，就好像它们是实际属性一样。它重写了 `TrySetMember` 和 `TryGetMember` 方法以提供这种动态语法。

### 列表 21.5 创建自定义动态对象

```csharp
public class CustomDictionary : DynamicObject
{
    Dictionary<string, object> internalDictionary =
        new Dictionary<string, object>();

    public int Count
    {
        get
        {
            return internalDictionary.Count;
        }
    }

    public override bool TryGetMember(GetMemberBinder binder, out object result)
    {
        return this.internalDictionary.TryGetValue(binder.Name.ToLower(),
            out result);
    }

    public override bool TrySetMember(SetMemberBinder binder, object value)
    {
        this.internalDictionary[binder.Name.ToLower()] = value;
        return true;
    }
}
```

列表 21.6 显示了如何使用这个新字典。

### 列表 21.6 使用自定义动态对象

```csharp
public class Program
{
    static void Main(string[] args)
    {
        dynamic contact = new CustomDictionary();
        contact.FirstName = "Ray";
        contact.LastName = "Manzarek";

        Console.WriteLine(contact.FirstName + " " + contact.LastName);
    }
}
```

列表 21.6 中代码的输出如图 21.7 所示。

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_466_0.png)

## 试一试

### 创建自定义动态类型

要实现自定义动态字典并查看如何在运行时使用它，请遵循以下步骤。

- 1. 在 Visual Studio 中创建一个新的控制台应用程序。
- 2. 添加一个名为 `CustomDictionary` 的新类，其样式如列表 21.5 所示。
- 3. 修改 `Program` 类的 `Main` 方法，使其样式如列表 21.6 所示。
- 4. 通过按 `Ctrl+F5` 运行应用程序。输出应与图 21.7 中显示的内容匹配。
- 5. 更改您在步骤 3 中输入的第一个语句，使 `contact` 被定义为 `dynamic` 类型。
- 6. 为接触类添加额外的“属性”，并在 `Console.WriteLine` 语句中输出它们。
- 7. 再次按 `Ctrl+F5` 运行应用程序，并观察输出结果变为显示新添加的属性。

# 与 COM 互操作

尽管 .NET Framework 一直允许你与 COM 进行互操作，特别是与 Office COM API，但 DLR 极大地简化了你需要编写的代码。由于许多 COM 方法将类型作为 `object` 返回，动态类型使你能够轻松地将它们作为动态对象来处理。

为了与 COM API 互操作，你需要使用主要互操作程序集（PIA），它在非托管的 COM API 和托管的 .NET 应用程序之间形成桥梁。为此，你在 Visual Studio 项目中添加对 PIA 的引用，使你的应用程序可以访问已定义的类型。添加引用后，你可以选择仅嵌入你的应用程序实际使用的那些类型。

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_467_0.png)

**嵌入式主要互操作程序集**

由于每个 PIA 必须包含 COM API 中定义的每种类型、接口、枚举等的托管等价物，因此一些 PIA（例如 Office PIA）可能相当大。

仅嵌入应用程序使用的互操作类型有助于减少部署大小，并且完全不需要部署 PIA。此外，通过将 COM 签名中的对象出现视为动态的，这还允许你避免处理 COM API 时的许多复杂性。

清单 21.7 中的代码展示了如何使用 COM 互操作打开 Microsoft Word 文档的简单示例。

### 清单 21.7 不使用动态类型的 COM 互操作

```csharp
public static void Main(string[] args)
{
    object missing = System.Reflection.Missing.Value;
    object readOnly = false;
    object isVisible = true;
    object fileName = "SampleDocument.docx";

    Microsoft.Office.Interop.Word.ApplicationClass wordApp =
        new Microsoft.Office.Interop.Word.ApplicationClass();
    wordApp.Visible = true;
    Document doc = wordApp.Documents.Open(ref fileName, ref missing,
        ref readOnly, ref missing, ref missing, ref missing, ref missing,
        ref missing, ref missing, ref missing, ref missing, ref isVisible,
        ref missing, ref missing, ref missing, ref missing);

    doc.Activate();
}
```

将其与清单 21.8 中显示的代码进行对比，该代码执行相同的操作，但使用动态类型。此代码还利用了命名参数和隐式类型化，展示了所有这些功能如何结合使用，允许你编写简洁的代码，既易于阅读又易于维护。

### 清单 21.8 使用动态类型的 COM 互操作

```csharp
public static void Main(string[] args)
{
    var wordApp = new Microsoft.Office.Interop.Word.ApplicationClass();
    wordApp.Visible = true;
    string fileName = "SampleDocument.docx";

    Document doc = wordApp.Documents.Open(fileName, ReadOnly: true, Visible: true);
    doc.Activate();
}
```

# 反射互操作性

更进一步，假设你想调用 `Calculator` 对象的 `Multiply` 方法。如果 `Calculator` 对象是用 C# 定义的，你可以轻松做到，如清单 21.9 所示。

### 清单 21.9 在 C# 对象中调用方法

```csharp
var calculator = GetCalculator();
int sum = calculator.Multiply(6, 7);
```

如果你不知道 `Calculator` 对象是用 .NET 编写的，或者需要因为编译器无法确定该对象实现了 `Multiply` 方法而使用反射，你就需要使用如清单 21.10 所示的代码。

### 清单 21.10 以反射方式调用方法

```csharp
object calculator = GetCalculator();
Type type = calculator.GetType();
object result = type.InvokeMember("Multiply", BindingFlags.InvokeMethod, null,
            calculator, new object[] { 6, 7 });
int sum = Convert.ToInt32(result);
```

如你所见，这远没有那么简单。然而，通过利用动态类型，代码变成了清单 21.11 中所示的样子。

### 清单 21.11 以动态方式调用方法

```csharp
dynamic calculator = GetCalculator();
int sum = calculator.Multiply(6, 7);
```

如果 `Calculator` 对象是在 IronPython 等动态语言中定义的，清单 21.11 中显示的相同代码仍然可以使用。唯一的区别在于 `GetCalculator` 方法的实现，它需要创建一个 IronPython 运行时的实例并加载相应的文件，如清单 21.12 所示。

### 清单 21.12 从 IronPython 获取动态对象

```csharp
dynamic GetCalculator()
{
    ScriptRuntime pythonRuntime = Python.CreateRuntime();
    return pythonRuntime.UseFile("calculator.py");
}
```

## 摘要

包含动态语言运行时（DLR）大大扩展了 .NET Framework 可以支持的语言数量。它还使 C# 等静态类型语言能够轻松访问在动态语言中定义的对象。使用动态类型允许你使用基本上与对象是静态定义时相同的代码语法来访问动态对象。

在本小时中，你学习了使用动态类型的基础知识，包括如何使用 `ExpandoObject` 以及如何通过继承 `DynamicObject` 创建自己的自定义动态对象。在探索 DLR 的基本架构后，你学习了如何在处理 COM API（如 Office COM API）以及在其他语言（如 IronPython）中定义的对象时使用动态类型。

## 问答

*   **问。** 什么是动态类型？
*   **答。** 动态类型是一种其操作绕过编译时类型检查，而是在运行时解析的类型。
*   **问。** `ExpandoObject` 的好处是什么？
