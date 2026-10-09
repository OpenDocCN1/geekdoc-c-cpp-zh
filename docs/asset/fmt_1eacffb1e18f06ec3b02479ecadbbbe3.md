
当第二次调用 `Plus` 时，传入了 `"A"`（一个字符串），`Plus` 将 `"AA"`（`"A"` 与自身拼接的结果）返回给调用者，并将此结果存储在变量 `result` 中。然后，再次调用 `M` 方法，并将 `result` 传递给它。这一次，负载代码（payload code）确定传递给 `M` 的实际类型是字符串，并调用接受字符串参数的 `M` 重载方法。

当字段、方法参数、返回类型或局部变量的类型指定为 `dynamic` 时，编译器会将此类型转换为 `System.Object` 类型，并在元数据中的该字段或返回类型上应用 `System.Runtime.CompilerServices.DynamicAttribute` 实例。如果局部变量指定为 `dynamic`，则该变量的类型也将是 `Object`，但不会对其应用 `DynamicAttribute`，因为其用法在方法内部是自包含的。`dynamic` 实际上与 `Object` 相同，你无法编写签名仅通过 `dynamic` 和 `Object` 区分的方法。

在为泛型类（引用类型、值类型）、接口、委托或方法指定泛型类型参数时，也可以使用 `dynamic`。当你这样做时，编译器会将 `dynamic` 转换为 `Object` 并在合理的各种元数据部分应用 `DynamicAttribute`。请注意，你正在使用的泛型代码已经编译完成，并将类型视为 `Object`；将不会执行动态分发，因为编译器没有在泛型内部产生任何负载代码。

任何表达式都可以是 `dynamic`，因为派自 `dynamic` 的类型中的所有表达式都是如此。通常，编译器不允许编写隐式将表达式从 `Object` 转换为其他类型的代码；你必须使用显式转换语法。然而，编译器允许你使用隐式语法将表达式从 `dynamic` 转换为其他类型：

```
Object o1 = 123;           // OK：从 Int32 隐式转换为 Object（装箱）
Int32 n1 = o1;               // 错误：从 Object 隐式转换为 Int32
Int32 n2 = (Int32) o1;   // OK：从 Object 显式转换为 Int32（拆箱）
dynamic d1 = 123;        // OK：从 Int32 隐式转换为 dynamic（装箱）
Int32 n3 = d1;             // OK：从 dynamic 隐式转换为 Int32（拆箱）
```

虽然编译器允许你在从 `dynamic` 转换为某些其他类型时省略显式转换，但 CLR会在运行时验证转换以确保安全性。如果对象的类型与转换不兼容，CLR 将抛出 `InvalidCastException`。

注意，评估 `dynamic` 表达式的结果也是一个 `dynamic` 表达式。查看这段代码：

```
dynamic d = 123;
var result = M(d);      // 注意：'var result' 等于 'dynamic result'
```

> 并且，如既往一样，值类型将被装箱。

## 第章 基本类型、引用类型和值类型 151

在这里，编译器允许代码编译，因为它在编译时不知道它将调用哪个 `M` 方法。因此，它不知道 `M` 将返回什么类型的结果。因此，编译器假设结果变量 `result` 的类型为 `dynamic`；你可以通过将鼠标悬停在 Visual Studio 编辑器中的 `var` 上来验证这一点；IntelliSense 窗口将显示“dynamic: 表示其操作将在运行时解析的对象”。如果运行时调用的 `M` 方法返回类型为 `void`，则不会抛出异常；相反，`result` 将赋值为 `null`。

> 重要 不要混淆 `dynamic` 和 `var`。使用 `var` 声明局部变量只是语法上的快捷方式，编译器借此推断表达式的具体数据类型。`var` 关键字只能用于声明方法内部的局部变量，而 `dynamic` 关键字可以用于局部变量、字段和参数。你不能将表达式转换为 `var`，但可以将表达式转换为 `dynamic`。你必须显式初始化使用 `var` 声明的变量，而不需要初始化用 `dynamic` 声明的变量。关于 C# `var` 的更多信息，请参见第 9 章“参数”中的“隐式类型变量”部分。

在这里，当从 `dynamic` 转换为另一个静态类型时，结果的类型显然是静态类型。同样，通过向构造函数传递一个或多个 `dynamic` 参数来构造类型时，结果是你正在构造的对象类型：

```
dynamic d = 123;
var x = (Int32) d; // 转换：'var x' 等于 'Int32 x'
var dt = new DateTime(d); // 构造：'var dt' 等于 'DateTime dt'
```

如果 `dynamic` 表达式指定为 `foreach` 语句中的集合或 `using` 语句中的资源，编译器将生成代码将表达式转换为 `System.IEnumerable` 接口中的非泛型集合或 `System.IDisposable` 接口。如果转换成功，则使用该表达式且代码将正常运行。如果转换失败，将抛出 `Microsoft.CSharp.RuntimeBinder.RuntimeBinderException`。

> 重要 `dynamic` 表达式的类型与 `System.Object` 相同。编译器假设你对 `dynamic` 进行的任何操作都是合法的，因此编译器不会生成任何警告或错误。然而，如果你尝试执行无效操作，将在运行时抛出异常。此外，Visual Studio 无法为 `dynamic` 表达式提供 IntelliSense 支持来帮助你编写代码。你不能定义扩展 `dynamic` 的扩展方法（第 8 章“方法”中讨论），尽管你可以定义扩展 `Object` 的方法。而且，你不能将 lambda 表达式或匿名方法（均在第 17 章“委托”中讨论）作为动态方法调用的参数，因为编译器无法推断所使用的类型。

这是一个使用 Interop 创建 Microsoft Excel 工作簿并将字符串置于 A1 单元格的 C# 代码示例：

## 第二部分 设计类型

```
using Microsoft.Office.Interop.Excel;
public static void Main() {
    Application excel = new Application();
    excel.Visible = true;
    excel.Workbooks.Add(Type.Missing);
    (Range)excel.Cells[1, 1].Value = "Text in cell A1"; // 将此字符串放入 A1 单元格
}
```

使用 `dynamic` 类型，从 `excel.Cells[1,1]` 返回的值类型为 `Object`，在访问其 `Value` 属性之前必须将其转换为 `Range` 类型。然而，当对 COM 对象使用运行时调用器（RCW）时，COM 方法中的 `VARIANT` 实际上会被转换为 `dynamic`；这被称为动态化（dynamification）。因此，由于 `excel.Cells[1,1]` 是 `dynamic` 类型，在访问其 `Value` 属性之前不需要显式将其转换为 `Range` 类型。动态化可以极大地简化与 COM 对象交互的代码。这里是更简单的示例：

```
using Microsoft.Office.Interop.Excel...
public static void Main() {
    Application excel = new Application();
    excel.Visible = true;
    excel.Workbooks.Add(Type.Missing);
    excel.Cells[1,1].Value = "Text in cell A1"; // 将此字符串放入 A1 单元格
}
```

下面的代码显示了如何使用反射在 String target ("Jeffrey Richter") 上调用方法("Contains")，传递一个 String 参数 ("ff")并将 Int32 结果存储在局部变量 (result) 中：

```
Object target = "Jeffrey Richter";
Object arg = "ff";

// 在 target 上找到所需的参数类型的方法
Type[] types = new Type[] { arg.GetType() };
MethodInfo method = target.GetMethod("Contains", types);

// 在 target 上调用方法并传递所需的参数
Object[] arguments = new Object[] { arg };
Boolean result = Convert.ToBoolean(method.Invoke(target, arguments));
```

使用 C# 的 `dynamic` 类型，代码可以重写为极大改进的语法：

```
dynamic target = "Jeffrey Richter";
dynamic arg = "ff";
Boolean result = target.Contains(arg);
```

早期，我提到 C# 编译器会发出调用代码，在运行时根据对象的实际类型确定要执行的操作。此过程使用称为运行时绑定器（runtime binder）的类。不同的编程语言定义自己的运行时绑定器，封装了该语言的规则。C# 运行时绑定器的代码为

# 第 5 章 原型、引用和值类型 153

在 `Microsoft.CSharp.dll` 程序集中，当你构建使用 `dynamic` 关键字的项目时，必须引用此程序集。该程序集在编译器的默认响应文件 `CSC.rsp` 中被引用。该程序集中的代码会在运行时产生当 `+` 运算符应用于 `Int32` 对象时执行加法、当应用于 `String` 对象时执行字符串拼接的代码。

在运行时，`Microsoft.CSharp` 程序集必须加载到 `AppDomain` 中，这会损害应用程序的性能并增加内存消耗。`Microsoft.CSharp.dll` 还会加载 `System.Core.dll`。如果你使用 `dynamic` 来帮助与 COM 组件交互，`System.Dynamic.dll` 将运行时生成动态代码；这将位于一个名为“匿名托管动态方法程序集”（Anonymously Hosted DynamicMethods Assembly）的内存程序集中。这段代码的目的是当特定调用点使用具有相同运行时类型的动态参数进行多次调用时，提高动态分发的性能。

由于 C# 内置动态评估功能相关的开销，你应该有意识地决定，你获得的语法自由度是否足以抵消加载所有程序集带来的额外性能损失以及它们消耗的额外内存。如果你的程序中只有少数地方需要动态行为，那么采用旧方法可能更高效，通过调用反射方法（对于托管对象）或手动强制转换（对于 COM 对象）。

在运行时，C# 运行时绑定器根据对象的运行时类型来解析动态操作。绑定器首先检查该类型是否实现了 `IDynamicMetaObjectProvider` 接口。如果对象实现了此接口，则调用该接口的 `GetMetaObject` 方法，该方法返回一个派生自 `DynamicMetaObject` 的类型。此过程可以调用该对象的任何成员、方法和操作符绑定。`IDynamicMetaObjectProvider` 接口和 `DynamicMetaObject` 基类定义在 `System.Dynamic` 命名空间中，且它们都位于 `System.Core.dll` 程序集中。

动态语言（如 Python 和 Ruby）赋予其类型派生 `DynamicMetaObject` 的类型，以便能够以适当的方式从其他编程语言（如 C#）进行访问。同样，在访问 COM 组件时，C# 运行时绑定器将使用一个知道如何与 COM 组件通信的派生自 `DynamicMetaObject` 的类型。COM `DynamicMetaObject` 派生类型定义在 `System.Dynamic.dll` 程序集中。

如果动态表达式中使用的对象类型没有实现 `IDynamicMetaObjectProvider` 接口，则 C# 编译器将该对象视为普通 C# 定义类型的实例，并使用反射对对象进行操作。

# 第 6 章

# 类型和成员基础

| 本章内容： | 155 |

| :--- | :--- |

| 不同类型的类型成员 ............................................................ | 158 |

| 类型可见性 ................................................................................ | 160 |

| 成员可访问性 ........................................................................... | 162 |

| 类型可访问性 ........................................................................... | 162 |

| 类、结构体和接口 .......................................... | 164 |

| 组件、多态性和版本控制 ......................................... | 165 |

在本章中，我将解释这些各种成员的共同点，并为后续更详细的章节铺平基础。无论你使用哪种编程语言，相应的编译器都会处理你的源代码，并为上述列表中的每种成员生成元数据（metadata）和中间语言（IL）代码。无论使用什么源编程语言，元数据的格式都是相同的，而这一特性使得 CLR 成为一个通用运行时。元数据是所有语言生成并消耗通用信息，使得一种编程语言中的代码能够无缝访问用完全不同的编程语言编写的代码。

# 不同类型的类型成员

类型可以定义以下更多的类型：

- 常量（Constants）：常量是标识不改变数据值的符号。常量始终与类型相关联。

- 字段（Fields）：字段表示读/写数据。字段可以是静态的，也可以是实例的（非静态的）。我强烈建议你将字段设为私有，以便类型的状态不会被外部破坏。

- 实例构造函数（Instance constructors）：实例构造函数是用于初始化新对象的特殊方法。

- 类型构造函数（Type constructors）：类型构造函数是用于初始化类型的特殊方法。

- 方法（Methods）：方法是执行操作以更改或查询类型（静态方法）或对象（实例方法）状态的函数。方法通常会有返回值。

- 操作符重载（Operator overloads）：操作符重载是定义当某些运算符应用于对象时如何处理该对象的方法。由于并非所有的编程语言都支持操作符重载，因此这些方法不属于公共语言规范（CLS）。

- 转换操作符（Conversion operators）：转换操作符是定义如何隐式或显式将对象从一种类型转换为另一种类型的方法。由于并非所有语言都支持转换操作符，它们不属于 CLS。

- 属性（Properties）：属性是一种允许以类似字段语法设置或查询类型（静态属性）或对象（实例属性）部分状态的机制，同时确保状态不会损坏。属性可以是无参数（常见）或带参数（用于集合类）。

- 事件（Events）：事件是一种允许类型向多个静态或实例方法发送通知的机制。实例事件（非静态）是允许向多个静态或实例方法发送通知的机制。事件通常在提供事件的状态发生变化时触发。除了方法外，事件通常使用委托（delegate）字段来维护已注册的方法集。

- 类型（Types）：类型可以在其内部定义其他类型。这种方法通常用于将大型、复杂的类型拆分为较小的构建块，以简化实现。

# 第 6 章 类型与成员基础 157

元数据（metadata）是整个 Microsoft .NET Framework 开发平台的关键所在；它实现了语言、类型和对象的无缝集成。

下面的 C# 代码显示了一个类型定义，其中包含了所有可能的成员的示例。这里显示的代码可以编译（带有警告），但它并不代表你通常创建的类型；大多数方法并没有任何实际价值。现在，我只是想向你展示编译器如何将此类型及其成员翻译为元数据。再次，我将在接下来的几个章节中讨论各个成员。

```
using System;
```
