
```
public class ThisIsAPublicType { ... }

// The type below has internal visibility and can be accessed by code
// in this assembly only.
internal class ThisIsAnInternalType { ... }

// The type below is internal because public/internal
// was not explicitly stated
class ThisIsAlsoAnInternalType { ... }
```

### 友元程序集

设想以下场景：一家公司有一个 TeamA 团队，该团队在一个程序集中定义了一组实用工具类型，并期望这些类型能被另一个 TeamB 团队的成员使用。由于时间安排、地理位置，或者成本中心、汇报结构不同等各种原因，这两个团队无法将所有类型都构建到同一个程序集中；相反，每个团队都会生成自己的程序集文件。

为了让 TeamB 的程序集能够使用 TeamA 的类型，TeamA 必须将其所有实用工具类型定义为 public。然而，这意味着他们的类型对任何程序集都是公开可见的；另一家公司的开发者可以编写使用这些公共实用工具类型的代码，而这并不理想。也许这些实用工具类型会做出某些假设，而 TeamB 在编写使用 TeamA 类型的代码时也假定了这些假设。我们真正想要的是这样一种方式：TeamA 可以将自己的类型定义为 internal，同时仍允许 TeamB 访问这些类型。CLR 和 C# 通过友元程序集支持这一点。当你希望让一个程序集包含针对另一个程序集中的内部类型执行单元测试的代码时，友元程序集功能也很有用。

在构建程序集时，可以通过使用 `System.Runtime.CompilerServices` 命名空间中定义的 `InternalsVisibleTo` 特性来指明它认为哪些其他程序集是“友元”。该特性有一个字符串参数，用于标识友元程序集的名称和公钥（传给该特性的字符串不能包含版本、区域性/文化或处理器架构）。请注意，友元程序集可以访问某个程序集的所有内部类型以及这些类型的内部成员。下面是一个示例，说明一个程序集如何将另外两个名为“Wintellect”和“Microsoft”的强命名程序集指定为其友元程序集：

```
using System;
using System.Runtime.CompilerServices; // For InternalsVisibleTo attribute

// This assembly's internal types can be accessed by any code written
// in the following two assemblies (regardless of version or culture):
[assembly:InternalsVisibleTo("Wintellect, PublicKey=12345678...90abcdef")]
[assembly:InternalsVisibleTo("Microsoft, PublicKey=b77a5c56...1934e089")]

internal sealed class SomeInternalType { ... }
internal sealed class AnotherInternalType { ... }
```

从友元程序集访问上述程序集的内部类型非常简单。例如，下面是一个名为“Wintellect”、公钥为“12345678...90abcdef”的友元程序集如何访问

| CLR 术语 | C# 术语 | 描述 |
| --- | --- | --- |
| Private | private | 该成员只能由定义类型或任何嵌套类型中的方法访问。 |
| Family | protected | 该成员只能由定义类型、任何嵌套类型或其派生类型中的方法访问，与程序集无关。 |
| Family and Assembly | （不支持） | 该成员只能由定义类型、任何嵌套类型中的方法，或同一程序集中定义的任何派生类型访问。 |
| Assembly | internal | 该成员只能由定义程序集中的方法访问。 |
| Family or Assembly | protected internal | 该成员可由任何嵌套类型、任何派生类型（无论程序集）或定义程序集中的任何方法访问。 |
| Public | public | 该成员可由任何程序集中的所有方法访问。 |

当然，任何成员要被访问，都必须定义在一个可见的类型中。例如，如果 AssemblyA 定义了一个带有公共方法的内部类型，则 AssemblyB 中的代码无法调用该公共方法，因为该内部类型对 AssemblyB 不可见。

编译代码时，语言编译器负责检查代码是否正确引用了类型和成员。如果代码错误地引用了某个类型或成员，编译器负责发出相应的错误消息。此外，即时 (JIT) 编译器还确保在运行时将 IL 代码编译为本机 CPU 指令时，对字段和方法的引用是合法的。例如，如果 JIT 编译器检测到代码不正当地尝试访问私有字段或方法，JIT 编译器将分别抛出 `FieldAccessException` 或 `MethodAccessException`。

验证 IL 代码可确保被引用成员的可访问性在运行时得到正确遵守，即使语言编译器忽略了检查可访问性。另一种更可能的情况是：语言编译器编译了访问另一个类型（在另一个程序集中）的公共成员的代码，但在运行时加载了该程序集的另一个版本，而在这个新版本中，该公共成员已经更改，现在变成了 protected 或 private。

在 C# 中，如果你没有显式声明成员的可访问性，编译器通常（但不总是）默认选择 private（所有可访问性中最严格的一种）。CLR 要求接口类型的所有成员都是 public。C# 编译器知道这一点，并禁止程序员显式指定接口成员的可访问性；编译器会直接为你将所有成员设为 public。

**更多信息** 请参阅 C# 语言规范中的“声明可访问性”一节以获取完整

如果检测到任何这些用法，编译器将发出错误。

下面是一个静态类的示例，它定义了一些静态成员；这段代码可以编译（并带有一个警告），但这个类并没有做任何有趣的事情：

```
using System;

public static class AStaticClass {
    public static void AStaticMethod() { }

    public static String AStaticProperty {
        get { return s_AStaticField; }
        set { s_AStaticField = value; }
    }

    private static String s_AStaticField;

    public static event EventHandler AStaticEvent;
}
```

如果你将上述代码编译为一个库 (DLL) 程序集，并使用 ILDasm.exe 查看结果，你将看到图 6-2 所示的内容。正如你在图 6-2 中所见，使用 static 关键字定义类会使 C# 编译器将该类同时设为抽象和密封。此外，编译器不会向该类型中发出实例构造函数方法。请注意，图 6-2 中没有显示实例构造函数 (.ctor) 方法。

![](img/3f2c86949cdef7e2f9e27c37c607b28e_162_0.png)

图 6-2 在元数据中将该类显示为抽象密封的 ILDasm.exe。

### 分部类、结构和接口

在本节中，我将讨论分部类、结构和接口。`partial` 关键字告诉 C# 编译器：单个类、结构或接口定义的源代码可以跨一个或多个源代码文件。应注意，编译器在编译时会将某个类型的所有分部组合在一起；CLR 始终处理完整的类型定义。你可能希望将一个类型的源代码拆分到多个文件中，主要有三个原因：

- **源代码管理** 假设某个类型的定义包含大量源代码，并且一名程序员将其从源代码管理中签出以进行更改。在没有稍后进行合并的情况下，其他程序员将无法同时修改该类型。使用 `partial` 关键字，你可以将该类型的代码拆分到多个源代码文件中，每个文件都可以单独签出，从而使多个程序员可以同时编辑该类型。
- **在单个文件中将类、结构或接口拆分为不同的逻辑单元** 我有时会创建一个提供多项功能的单一类型，以便该类型能够提供完整的解决方案。为了简化实现，我有时会在单个源代码文件中重复声明同一个 `partial` 类型。然后，在 `partial` 类型的每个部分中，我会实现一个功能及其所有字段、方法、属性、事件等。这使我能够轻松看到提供单个功能的所有成员分组在一起，从而简化我的编码。此外，我还可以轻松注释掉 `partial` 类型的某一部分，从而从该类型中移除整个功能，并用另一种实现（通过 `partial` 类型的新部分）替换它。
- **代码拆分器** 在 Microsoft Visual Studio 中，创建新项目时，会自动创建一些源代码文件作为项目的一部分。这些源代码文件包含模板，可帮助你先开始构建这类项目。当你使用 Visual Studio 设计器并将控件拖放到设计图面上时，Visual Studio 会自动为你编写源代码，并将此代码拆分到源代码文件中。这确实提高了你的工作效率。过去，生成的代码会被写入你正在处理的同一个源代码文件中。这样做的问题在于，你可能会意外编辑生成的代码，并导致设计器停止正常工作。从 Visual Studio 2005 开始，当你创建新窗体、用户控件等时，Visual Studio 会创建两个源代码文件：一个用于你的代码，另一个用于设计器生成的代码。由于设计器代码位于单独的文件中，你意外编辑它的可能性会大大降低。

`partial` 关键字应用于所有文件中的类型。当这些文件一起编译时，编译器会组合代码，生成一个位于结果 `.exe` 或 `.dll` 程序集文件（或 `.netmodule` 模块文件）中的类型。正如我在本节开头所述，分部类型功能完全由 C# 编译器实现；CLR 对分部类型一无所知。这就是为什么该类型的所有源代码文件必须使用相同的编程语言，并且它们必须作为一个编译单元一起编译。

### 组件、多态和版本控制

面向对象编程 (OOP) 已经存在很多很多年了。当它在 20 世纪 70 年代末/80 年代初首次被使用时，应用程序的规模要小得多，而且使应用程序运行的所有代码都由一家公司编写。当然，那时已经有操作系统，而且
