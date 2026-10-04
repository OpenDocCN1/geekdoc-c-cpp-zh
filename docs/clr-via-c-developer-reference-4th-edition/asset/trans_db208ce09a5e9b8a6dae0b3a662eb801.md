

![](img/0ce3b788d061e3d3095fa554b1a34adf_52_0.png)

**图 1-6** 语言提供了 CLR/CTS 的子集以及 CLS 的超集（但不一定是同一个超集）。

如果你在其中一种语言中设计了一个类型，并预计该类型会被另一种语言使用，那么你不应该在它的公共和受保护成员中利用任何 CLS 之外的特性。这样做意味着你的类型成员可能无法被在其他编程语言中编写代码的程序员访问。

在下面的代码中，正在使用 C# 定义一个符合 CLS 标准的类型。然而，该类型有几个不符合 CLS 标准的结构，导致 C# 编译器对代码报错。

```csharp
using System;
// 告诉编译器检查 CLS 兼容性
[assembly: CLSCompliant(true)]

namespace SomeLibrary {
    // 因为类是公共的，会出现警告
    public class SomeLibraryType {
        // 警告：'SomeLibrary.SomeLibraryType.Abc()' 的返回类型
        // 不符合 CLS 标准
        public UInt32 Abc() { return 0; }

        // 警告：标识符 'SomeLibrary.SomeLibraryType.abc()' 
        // 仅大小写不同，不符合 CLS 标准
        public void abc() {
            // 无警告：此方法是私有的
            private UInt32 ABC() { return 0; }
        }
    }
}
```

在此段代码中，`[assembly:CLRCompliant(true)]` 属性被应用于程序集。该属性告诉编译器确保任何公开的类型都没有任何可能阻止其他编程语言访问该类型的结构。当编译此代码时，C# 编译器会发出两个警告。第一个警告是因为该方法返回无符号整数；某些其他语言无法处理无符号整数值。第二个警告是因为它暴露了两个仅大小写和返回类型不同的公共方法：Ab 和 abc。Visual Basic 以及其他某些语言无法调用这两个方法。

有趣的是，如果你删除 `sealed class SomeLibraryType` 前的 `public` 并重新编译，两个警告都会消失。这是因为 `SomeLibraryType` 类型将默认为内部的（internal），并且不再暴露在程序集外部。有关 CLR 规则的完整列表，请参考 .NET Framework SDK 文档中的“跨语言交互性”部分（http://msdn.microsoft.com/en-us/library/730f1wy3.aspx）。

让我们来看一些简单的内容。在 CLR 中，类型的每个成员要么是字段（数据），什么是方法（行为）。这意味着每种编程语言都必须访问字段和方法。某些字段和某些方法以特殊且常见的方式使用。为了方便编程，语言通常提供额外的抽象，以便对这些常见的编程模式进行编码。例如，语言暴露了如枚举、数组、属性、索引器、委托、构造函数、终结器、运算符重载、转换算符等概念。当编译器在你的源码中遇到这些任何一种结构时，它必须将这些结构翻译成字段和方法，以便 CLR 和任何其他编程语言访问该结构。

考虑以下类型定义，它包含一个构造函数、一个终结器、一些重载运算符、一个属性、一个索引器和一个事件。注意，所示代码是为了展示实现类型的正确方法。

```csharp
using System;
internal sealed class Test {
// 构造函数
public Test() {}
// 终结器
~Test() {}
// 运算符重载
public static Boolean operator == (Test t1, Test t2) {
  return true;
}
public static Boolean operator != (Test t1, Test t2) {
  return false;
}
// 另一个运算符重载
public static Test operator + (Test t1, Test t2) { return null; }

// 属性
public String AProperty {
    get { return null; }
    set { }
}

// 索引器
public String this[Int32 x] {
    get { return null; }
    set { }
}

// 事件
public event EventHandler AnEvent;
}
```

当编译器编译这段代码时，结果是一个内部定义了许多字段和方法的类型。你可以使用使用 .NET Framework SDK 提供的 IL 反汇编器工具 (ILDasm.exe) 轻松地检查生成的托管模块，如图 1-7 所示。

![](img/0ce3b788d061e3d3095fa554b1a34adf_54_0.png)

图 1-7 ILDasm 显示类型的字段和方法（获取自元数据）。

表 1-4 显示了语言结构如何映射到等效的 CLR 字段和方法。

# 1-4 Test 类型的字段和方法（获取自元数据）

| 类型成员 | 成员类型 | 等效编程语言结构 |
| :--- | :--- | :--- |
| AnEvent | 字段 | 事件；该字段名为 AnEvent，其类型为 System.EventHandler。 |
| .ctor | 方法 | 构造函数。 |
| Finalize | 方法 | 终结器。 |
| add_AnEvent | 方法 | 事件 add 访问方法。 |

| 类型成员 | 成员类型 | 等效编程语言结构 |
| :--- | :--- | :--- |
| get_AProperty | 方法 | 属性 get 方法。 |
| get_Item | 方法 | 索引器 get 方法。 |
| op_Addition | 方法 | 加法运算符。 |
| op_Equality | 方法 | 相等运算符。 |
| op_Inequality | 方法 | 不等运算符。 |
| add_AnEvent | 方法 | 事件 add 访问方法。 |
| set_AProperty | 方法 | 属性 set 方法。 |
| set_Item | 方法 | 索引器 set 方法。 |

让我们来看一些简单的内容。在 CLR 中，类型的每个成员要么是字段（数据），什么是方法（行为）。这意味着每种编程语言都必须访问字段和方法。某些字段和某些方法以特殊且常见的方式使用。为了方便编程，语言通常提供额外的抽象，以便对这些常见的编程模式进行编码。例如，语言暴露了如枚举、数组、属性、索引器、委托、构造函数、终结器、运算符重载、转换算符等概念。当编译器在你的源码中遇到这些任何一种结构时，它必须将这些结构翻译成字段和方法，以便 CLR 和任何其他编程语言访问该结构。

考虑以下类型定义，它包含一个构造函数、一个终结器、一些重载运算符、一个属性、一个索引器和一个事件。注意，所示代码是为了展示实现类型的正确方法。

当编译器编译这段代码时，结果是一个内部定义了许多字段和方法的类型。你可以使用使用 .NET Framework SDK 提供的 IL 反汇编器工具 (ILDasm.exe) 轻松地检查生成的托管模块，如图 1-7 所示。

表 1-4 显示了语言结构如何映射到等效的 CLR 字段和方法。

# 与非托管代码的交互

.NET Framework 比其他平台提供了许多优势。然而，很少有公司能负担得起重新实现所有代码。微软意识到了并构建了 CLR，使其由托管和非托管部分组成。CLR 支持三种交互场景：

- **托管代码可以调用 DLL 中的非托管函数**：托管代码可以通过 P/Invoke（平台调用）轻松地调用 DLL 中的函数。毕竟，许多类型是在 Kernel32、User32 等中定义的。许多编程语言都暴露了易于调用非托管函数的机制。例如，C# 应用程序可以调用 Kernel32 导出的 Semaphore 函数。

- **托管代码可以使用现有的 COM 组件（服务器）**：许多公司已经实现了许多非托管 COM 组件。使用这些组件的类型库可以创建一个描述该组件的托管程序集。托管代码可以像访问其他类型一样访问托管程序集中的类型。

- **非托管代码可以使用托管类型（服务器）**：某些非托管代码列表要求你提供一个 COM 组件才能使代码正常工作。使用托管代码实现这些组件要容易得多，这样你就可以避免所有与引用计数和接口相关的代码。例如，你可以用 C# 创建 ActiveX 或外壳扩展。

> 注意：微软现在提供了类型库导入器工具的源代码以及 P/Invoke Interop Assistant，以帮助需要与原生代码交互的开发者。这些工具及其源代码可以从 http://CLRInterop.CodePlex.com/ 下载。

