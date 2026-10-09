
# 规则与指南

关于扩展方法，你还需要了解一些额外的规则和指南：

- C# 仅支持扩展方法；它不提供扩展属性、扩展事件、扩展运算符等。
- 扩展方法（在第一个参数之前带有 `this` 关键字）必须声明在非泛型的静态类中。然而，对类的名称没有限制；你可以随心所欲地为其命名。当然，一个扩展方法必须至少有一个参数，且只有第一个参数可以标记为 `this` 关键字。
- C 编译器只查找在定义于文件作用域（file scope）的静态类中定义的扩展方法。换句话说，如果你在一个类内部嵌套定义了静态类，`C` 编译器将输出以下消息：“error CS1109: 扩展方法必须定义在顶层静态类中；`StringBuilderExtensions` 是一个嵌套类。”
- 由于静态类可以有任何你喜欢的名称，C# 编译器在查找扩展方法时必须查看所有文件作用域内的静态类，并扫描它们的静态方法以查找方法。为了提高性能并避免考虑你可能不需要的扩展方法，C 编译器要求你“导入”扩展方法。例如，如果有人定义了 `Wintellect` 命名空间，那么想要访问该类扩展方法的程序员必须在其代码或源文件顶部放置 `using Wintellect` 指令。

![](img/bd0526960dc8576a05e40e1f7f03c458_227_0.png)

# 第 8 章 方法 211

- 多个静态类可能会定义相同的扩展方法。如果编译器检测到存在两个或多个扩展方法，编译器会发出消息：“error CS0121: 调用在以下方法或属性之间存在歧义：'`StringBuilderExtensions.IndexOf(string, char)'` 和 `'AnotherStringBuilderExtensions.IndexOf(string, char)'`。” 要修修复此错误，你必须修改源代码。具体来说，你不能再使用静态方法语法来调用此静态方法；相反，你现在必须使用静态方法语法并显式指定静态类的名称，以明确告诉编译器你想要调用哪个方法。
- 你应该谨慎地使用此功能，因为并不是所有程序员都熟悉它。例如，当你使用扩展方法扩展一个类型时，你实际上也通过此方法扩展了派生类型。因此，你不应该定义第一个参数为 `System.Object` 的扩展方法，因为此方法可以被所有表达式类型调用，这会严重污染 Visual Studio 的 IntelliSense 提示。
- 扩展方法存在潜在的版本问题。如果未来 Microsoft 在其 `StringBuilder` 类中添加了一个与我的代码尝试调用的原型相同的 `IndexOf` 实例方法，那么当我重新编译代码时，编译器将绑定到 Microsoft 的 `IndexOf` 实例方法而不是我的 `IndexOf` 方法。由于由于，我的程序将产生不同的行为。版本问题是该功能应该谨慎使用的另一个原因。

## 使用扩展方法扩展各种类型

在本章中，我演示了如何为 `StringBuilder` 类定义扩展方法。我想指出，由于扩展方法实际上是对静态方法的调用， CLR 不会生成代码来确保用于调用方法的表达式的值不为空：

```csharp
// sb 为 null
StringBuilder sb = null;
```

```csharp
// 调用扩展方法：在调用 IndexOf 时不会抛出 NullReferenceException
// 在 IndexOf 的循环内部会抛出 NullReferenceException
sb.IndexOf('X');
```

```csharp
// 调用实例方法：在调用 Replace 时将抛出 NullReferenceException
sb.Replace('.', '.', '!');
```

我还想指出，你可以像下面的代码为接口类型定义扩展方法：

```csharp
public static void ShowItems<T>(this IEnumerable<T> collection) {
    foreach (var item in collection)
        Console.WriteLine(item);
}
```

*

# 第二部分 类型设计

上述扩展方法现在可以使用任何结果实现了 `IEnumerable<T>` 接口的类型的表达式来调用：

```csharp
public static void Main() {
    // 在控制台中单独行显示 Char
    "Grant".ShowItems();
    // 在控制台中单独行显示 String
    new[] { "Jeff", "Kristin" }.ShowItems();
    // 在控制台中单独行显示 Int32 值
    List<Int32> new List { 1, 2, 3 }.ShowItems();
}
```

> **重要** 扩展方法是 Microsoft 语言集成查询 (LINQ) 技术的基石。关于提供许多扩展方法的类的绝示例，请参见系统 `Linq.Enumerable` 以及 Microsoft .NET Framework SDK 文档中所有的静态扩展方法。该类中的每个扩展方法都扩展了 `IEnumerable` 或 `IEnumerable<T>` 接口。

你也可以为委托定义扩展方法。关于此示例，请参阅第 8 章第 278 页。

# 部分方法

假设你使用一个生成包含类型定义的 C# 源代码文件的工具。该工具知道在它生成的代码中某些你可能想要自定义类型行为的区域。通常，自定义是通过

# 第二部分 设计类型

工具生成的代码会调用方法。工具生成的代码还必须包含这些虚方法的定义，并且这些方法的实现方式将什么都不做并直接返回。现在，如果你想自定义类的行为，可以定义你自己的类，派生自基类，然后重写任何实现的虚方法，以具备你所需的行为。以下是一个示例：

```csharp
// 某些源代码文件中工具生成的代码：
internal class Base {
    private String m_name;
    // 在更改 m_name 字段之前调用
    protected virtual void OnNameChanging(String value) {
    }
    public String Name {
        get { return m_name; }
        set {
            OnNameChanging(value.ToUpper()); // 通知类潜在的更改
            m_name = value; // 修改字段
        }
    }
}
```

```csharp
// 另一个源代码文件中开发者生成的代码：
internal class Derived : Base {
    protected override void OnNameChanging(string value) {
        if (String.IsNullOrEmpty(value))
            throw new ArgumentNullException("value");
    }
}
```

遗憾的是，上面的代码存在两个问题：

- 类型必须是非密封（sealed）类。你不能对密封类或值类型使用这种技术（因为值类型隐式密封的）。此外，你不能对静态方法使用这种技术，因为它们无法被重写。
- 这里存在效率问题。定义一个类型来重写方法会浪费少量系统资源。而且，即使你不想重写 `OnNameChanging` 的行为，基类仍然调用了一个除了返回之外的虚方法。此外，无论 `OnNameChanging` 是否访问传递给它的参数，都会调用 `ToUpper`。

C# 的部分方法（partial methods）允许你在解决上述问题的同时，提供重写行为或类型的选项。以下代码使用部分方法实现了与之前代码相同的语义：

```csharp
// 某些源代码文件中工具生成的代码：
internal sealed partial class Base {
    private String m_name;
    // 这个定义部分方法的声明在更改 m_name 字段之前调用
    partial void OnNameChanging(String value);
    public String Name {
        get { return m_name; }
        set {
            OnNameChanging(value.ToUpper()); // 通知类潜在的更改
            m_name = value;
            // 修改字段
        }
    }
}
```

```csharp
// 其他源代码文件中开发者生成的代码：
internal sealed partial class Base {
    // 这个实现部分方法的声明在 m_name 更改之前调用
    partial void OnNameChanging(String value) {
        if (String.IsNullOrEmpty(value)) {
            throw new ArgumentNullException("value");
        }
    }
}
```

关于这个新版本的代码有几点需要注意：

- 类现在是密封的（sealed）（尽管它不必是密封）。事实上，该类可以是静态类甚至是值类型。
- 工具生成的代码和开发者生成的代码实际上是两个部分定义，最终共同构成一个类型定义。有关部分类型的更多信息，请参阅第 6 章“类型和成员基础”中的“部分类、结构体和接口”节。
- 工具生成的代码定义了一个部分方法声明。该方法标记了 `partial` 且没有方法体。
- 开发者生成的代码实现了部分方法声明。该方法也标记了 `partial` 标记并有方法体。

现在，当你编译这段代码时，你将看到与我展示给你的原始代码相同的效果。再次，这里的大处在于你可以重新运行工具并在新的源代码文件中生成新代码，但你的代码保留在单独的文件中且不受影响。而且，这种技术适用于密封类、静态类和值类型。

> 注意 在 Visual Studio 编辑器中，如果你输入 `partial` 并按下空格键，IntelliSense 窗口会显示包含该类型定义的、尚未匹配的部分方法声明。然后你可以轻松地从 IntelliSense 窗口选择一个部分方法，Visual Studio 将自动为该方法生成原型。这是一个提高生产力的非常好功能。

但是，部分方法还有另一个巨大的改进。假设你在解决上述问题时不需要重写行为或类型。

## 第 9 章 参数

在本章中：
- 可选参数和命名参数 ... 219
- 隐式类型局部变量 ... 223
- 通过引用将参数传递给方法 ... 225
- 向方法传递可变参数 ... 231
- 参数和返回类型指南 ... 233
- 常属性 (Const-ness) ... 235

本章重点关注向方法传递参数的各种方式，包括可选地指定参数、按名称指定以及通过引用传递参数，以及定义接受可变参数的方法。

### 可选参数和命名参数

在设计方法的参数时，你可以为某些或所有参数分配默认值。然后，调用这些方法的代码可以可选地指定某些参数，从而接受默认值。此外，当调用一个方法时，可以使用参数的名称来指定参数。以下是演示可选参数和命名参数的代码：

```csharp
public static class Program {
    private static Int32 s_n = 0;
    private static void M(Int32 x, String s = "A",
        DateTime dt=default(DateTime), Guid guid = new Guid()) {
        Console.WriteLine("x={0}, s={1}, dt={2}, guid={3}", x, s, dt, guid);
    }
    public static void Main() {
        // 1. 等于 M(9, "A", default(DateTime), new Guid());
        M(9);
        // 2. 等于 M(8, "X", default(DateTime), new Guid());
        M(8, "X");
        // 3. 等于 M(5, "A", DateTime.Now, Guid.NewGuid());
        M(5, Guid.NewGuid(), dt: DateTime.Now);
    }
}
```

```csharp
// 4. Same: as M(0, "1", default(DateTime), new Guid());
M(s_n++, s_n++.ToString());
// 5. Same: as string t1 = "2"; Int32 t2 = 3;
M(t2, t1, default(DateTime), new Guid());
M(s: (s_n++).ToString(), x: s_n++);
}
```

当我运行这个程序时，我得到了如下输出：

```
x=9, s=A, dt=1/1/001 12:00:00 AM, guid00000000-0000-0000-0000-000000000000
x=8, s=X, dt=1/1/001 12:00:00 AM, guid00000000-0000-0000-0000-000000000000
x=5, s=A, dt=7/2/2009 10:14:25 PM, guid=d24a59da-6090-404a-aae9-839155811309
x=0, s=I, dt=1/1/001 12:00:00 AM, guid00000000-0000-0000-0000-000000000000
x=3, s=2, dt=1/1/001 12:00:00 AM, guid00000000-0000-0000-0000-000000000000
```

你可以看到，每当调用时省略了参数，C# 编译器就会嵌入参数的默认值。对 `M` 的第三次和第五次调用使用了 C# 的参数功能。在两次调用中，我显式地为 `x` 传递了一个值，并表示我想为参数 `guid` 和 `dt` 传递参数。

当你向方法传递参数时，编译器会从左到右评估参数。在对 `M` 的第四次调用中，`s_n` 的值 (0) 被传递给 `x`，然后 `s_n` 递增，紧接着 `s_n` 的值 (1) 作为字符串传递给 `s`，且 `s_n` 增加到 2。在对 `M` 的第五次调用中，`s_n` 的值 (2) 被转换为字符串并保存在临时变量 (`t1`) 中。接下来，`s_n` 增加到 3，该值保存在编译器创建的另一个临时变量 (`t2`) 中，然后 `s_n` 增加到 4。最终，`M` 被调用，传递了 `t2`、`t1`、一个默认 `DateTime` 和一个新的 `Guid`。

# 规则与指南

在定义一个为某些参数指定默认值的方法时，你应该了解一些额外的的规则和指南：

- 你可以为方法、构造器方法和属性（C# 索引器）的参数指定默认值。你还可以为委托定义中的参数指定默认值。那么，当调用此种委托类型的变量时，你可以省略参数并接受默认值。
- 带有默认值的参数必须排在没有默认值的参数之后。也就是说，一旦你定义了一个参数具有默认值，那么它右侧的所有参数也必须具有默认值。例如，在我的方法定义中，如果我删除了 `s` 的默认值（"A"），我将得到编译器错误。该规则有一个例外：`params` 数组参数（在本节稍后讨论）必须排在所有参数（包括带有默认值的参数）之后，且该数组本身不能有默认值。
- 默认值必须是编译时已知的常量值。这意味着你可以为 C# 视为基本类型的参数设置默认值，如表 5-1 “基本类型、引用类型和值类型”所示。这包括枚举类型，并且任何引用类型都可以设置为 `null`。对于任意值类型的参数，你可以将默认值设置为该类型的实例，其所有字段均为零。你可以使用 `default` 关键字或 `new` 关键字来表示；两种语法产生相同的中间语言 (IL) 代码。`M` 方法分别使用了这两种语法来为 `dt` 参数和 `guid` 参数设置默认值。
- 不要重命名参数变量，因为通过参数名传递参数的调用者将不得不修改代码。例如，在我的 `M` 方法声明中，如果将 `dt` 变量重命名为 `DateTime`，那么你之前代码中对 `M` 的第三次调用会导致编译器产生以下消息：“error CS1739: 'M' 的最佳重载没有名为 'dt' 的参数。”

```csharp
// 不要这样做：
private static String MakePath(String filename = "Untitled") {
    String.Format("C:\{0}.txt", filename);
}
```

```csharp
// 应该这样做：
private static String MakePath(String filename = null) {
    // 我在这里使用了空合并运算符；请参见第 19 章
    String.Format("C:\{0}.txt", filename ?? "Untitled");
}
```
