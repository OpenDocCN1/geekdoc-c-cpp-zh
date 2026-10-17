
进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```

| 类型提供者骨架 | 生成类型提供者的骨架。以下是生成的默认代码： |
| 类型提供者 XML 注释 | 生成 XML 注释。以下是生成的默认代码： |
| 提供的度构建器（Provided measure builder） | 为类型提供者类型生成度。以下是生成的默认代码： |
| 类型提供者参数 | 生成类型提供者的函数参数。以下是生成的默认代码： |

```fsharp
namespace Samples.FSharp.ShareInfoProvider

open System.Reflection

open Microsoft.FSharp.Core.CompilerServices

open Samples.FSharp.ProvidedTypes

[<TypeProvider>]

type public CheckedRegexProvider() as this = inherit TypeProviderForNamespaces()

// 获取用于存放提供的程序集和命名空间

let thisAssembly = Assembly.GetExecutingAssembly()

let rootNamespace = "Samples.ShareInfo.TPTest"

let baseTy = typeof<>()

let regexTy = ProvidedTypeDefinition(thisAssembly, rootNamespace, "TPTest", Some baseTy)

// 添加其他属性和方法定义

do this.AddNamespace(rootNamespace, [regexTy])
```

```fsharp
ctor.AddDocDelayed(fun () -> "xml comment")
```

```fsharp
let units = ProvidedMeasureBuilder.Default.Is "metre"

let unitType = ProvidedMeasureBuilder.Default.AnnotateType(typeof<float>, [units])
```

```fsharp
ProvidedParameter("var", typeof<string>)
```

## 类型提供者的局限性

F# 3.0 自带的类型提供者机制有一些局限性。读者可能已经注意到的第一个局限性是静态参数只能接收基本类型，例如整数和字符串。另一个局限性是类型提供者只能生成 .NET 1.x 类型。大多数 F# 特有的类型（如 `record`）都不支持。唯一的例外是度类型（units of measure），它们在此版本中是被支持的。这些局限性将在未来的版本中消除，但目前是如此。

## 类型提供者的局限性

... 大多数 F# 特有的类型（如 `record`）都不支持。

## 其它特性

... 这里的引用单元（Reference Cells）

... 最后一个原则（SOLID）设计原则要求程序依赖抽象而非具体实现。

# 引用单元（Reference Cells）

在之前的章节中，我们展示了引用单元。引用单元是用于定义可变数据的。

# 引用单元（Reference Cells）

... 引用单元是用于定义可变数据的单元方式。

# 引用单元（Reference Cells）

... 引用单元是用于定义可变数据的。定义 6-1 引用单元

```fsharp
// 定义接口

type IA =

    abstract member F : int with get, set

// 对象表达式

let objectExpression =

    let dataStorage = ref 9 // 实际数据存储

    {

        new IA with

            member.F

            with get() = !dataStorage

            and set(v) = dataStorage := v

    }
```

> 注意：对象表达式中不支持自动实现的属性。对象表达式中的属性只能通过旧语法进行声明。

如果该字段需要是可变的，另一种方法是使用引用单元（reference cell）。代码列表 6-6 显示了如何在对象表达式内部和外部定义引用单元。代码列表 6-7 显示了如何扩展基类。

# 列表 6-6 带有属性的对象表达式

```fsharp
// 第一个接口

type IMInterface =

    abstract F : unit -> unit

    abstract Prop0 : string with get, set

    abstract Prop1 : string with get, set

// 在 objExpression 外部定义一个引用单元

let myData = ref ""

// 使用对象表达式实现接口

let objExpression =

    // 在 objExpression 内部定义一个引用单元

    let x = ref ""

    new IMInterface with

        member.F() = printf "hello object expression"

        member.Prop0 with get() = !x and set(v) = x := v

        member.Prop1 with get() = !myData and set(v) = myData := v

// 设置 Prop0 并打印结果

objExpression.Prop0 <- "set Prop0"

printf "%s" objExpression.Prop0

// 设置 Prop1 并打印结果

objExpression.Prop1 <- "set Prop1"

printf "%s" objExpression.Prop1
```

### 列表 6-7 基于类的对象表达式

```fsharp
// 定义接口

type IMInterface2 =

    abstract F2 : unit -> unit

// 抽象类定义

[AbstractClass]

type MyAbstractClass() =

    abstract F : unit -> unit

    member.this.F2() = printf "my abstract class"
```

```fsharp
// 带有抽象类和接口的对象表达式

let objExpressionInterfaceAbstract =

    {

        new MyAbstractClass() with

            override this.F() = printf "implement the abstract class"

            interface IInterface2 with

                member this.F2() = printf "from interface2"

    }

// 使用对象表达式重写 ToString 方法

let objExpressionExtendObject =

    {

        new System.Object() with

            override this.ToString() = "hello from object expression"

    }
```

与 C# 类似，基类（包含一些具体的类成员实现）在派生类定义中必须位于所有接口之前。在 F# 对象表达式中，抽象类必须出现在任何内容之前。换句话说，如果在 `objExpressionInterfaceAbstract` 中将 `MyAbstractClass` 放在 `IInterface2` 之后，代码将无法编译。

列表 6-8 是一个实现 WPF 命令的真实示例。WPF 命令通常不涉及类的构造。这是使用对象表达式的绝佳场所。从示例代码可以看出，对象表达式可以拥有在外部无法直接访问的字段。变量 `event1` 可以被视为对象表达式中实现的私有字段。此示例还显示了带参数的对象表达式（如 `createCommand`）可以作为类工厂根据内容创建对象。

# 列表 6-8 使用对象表达式的 WPF 命令

```fsharp
// 生成 WPF 命令的类工厂

let createCommand actionExecute =

    let event1 = Event<ICommand>()

        new ICommand with

            member this.CanExecute(obj) = actionExecute(obj)

            member this.Execute(obj) = actionExecute(obj)

            member this.CanExecuteChanged(handler) =

                event1.Add(handler)

            member this.RemoveExecuteChanged(handler) =

                event1.Remove(handler)

// 创建一个无所事且始终可以执行的虚拟命令

let dummyCommand = createCommand(

  (fun -> ()) // 执行无操作

  (fun -> true) // 命令始终可以执行

)
```

在你的模块中有函数和变量，并且需要一种方法为 C# 方法提供功能的情况。在模块内部组织代码最快的方法是使用对象表达式。列表 6-9 显示了一个包含三个项目的示例。以下显示了如何使用 F# 对象表达式来组织代码：

- 首先，创建一个 C# 项目，在其中定义了接口 `IMInterface`。该项目将被其他 C# 项目和 F# 项目引用。
- 其次，创建一个 C# 项目并定义了一个类 `MyFunction`，它接受 `IMInterface` 作为参数。
- 最后，一个 F# 项目创建了对象表达式并将其传递给该类。

# 列表 6-9 使用对象表达式组织代码

```csharp
// 第一个 C# 项目中的 IMInterface 定义

public interface IMInterface {

  void MyFunction();

  int MyProperty { get; set; }

}

// 第二个 C# 项目中的 MyFunction 定义

public class MyClass {

  public void MyFunction(IMInterface obj) {

    // 我的操作

  }

}
```

# 使用对象表达式组织并调用 C# 函数

```fsharp
// 函数库

module MyFunctionLibrary =

    let myFunction () = // 其他操作

// 使用对象表达式从模块中组织代码

let myData =

    let data = ref 0

    { new IMInterface with

        member.MyFunction() = MyFunctionLibrary.myFunction()

        member.MyProperty with get() = !data and set(v) = data := v

    }

// 使用对象表达式调用 C# 方法

let instance = new MyClass()

instance.MyFunction(myData)
```

对象表达式有一些限制。对象的类型信息是由编译器生成的；因此，类型名称对用户并不友好。对象的类型是密封的，所以当你真的需要复杂的继承体系时，这种类型并没有帮助。

# 处理 Option（选项）

列表 6-10 定义了一个返回 `int` option 的函数。根据 MSDN 文档，Option 具有以下特性：

> F# 中的 option 用于实际值可能不存在的情况。Option 有一个底层类型并可以持有该类型的值。

对于 C# 开发者来说，列表 6-10 类似于 6-11，后者使用了 `Nullable<T>`。C# 函数返回 `NULL`，F# 函数返回 `None`。表 6-1 显示了 option 的成员。

| 属性或方法 | 类型 | 描述 |
| :--- | :--- | :--- |
| None | 'T option | None 值。这是一个静态属性。 |
| IsNone | Boolean | 如果 option 是 None，则返回 TRUE。 |
| IsSome | Boolean | 如果 option 有值，则返回 TRUE。 |
| Some | 'T option |  None，但它返回 Some。 |
| Value | 'T | 获取底层值。如果没有值（None），将抛出 NullReferenceException。 |

`NULL` 和 `None` 之间存在细微区别。首先，F# 类和其他引用对象不接受 `NULL` 作为有效值。例如，列表 2-16 中的 `GetDistance` 函数无法传递 `NULL`。

# 列表 6-10 返回 int option 的函数

```fsharp
// 只返回偶数 option 的函数

let filterOutOddNumber a =

    if a % 2 = 0 then Some(a)

    else None
```

# 列表 6-11 C# 函数过滤奇数

```csharp
static Nullable<int> FilterOutOddNumber(int a) {

    if (a % 2 == 0) {

        return a;

    }

    else {

        return null;

    }

}
```

F# 函数 `GetDistance` 无法接受 `NULL` 参数并不是错误。实际上，这是一个经过仔细设计的 F# 特性。列表 6-12 显示了如何在 C# 和 F# 中检查用户输入。C# 代码看起来完美，直到你发现 `str` 可能为空！所以你必须先检查 `str != null` 然后执行工作。而这种错误只能在运行时捕获。

# 使用 option 的 F# 代码

```sharp
// return a string option to indicate the return value can be an uninitialized value

let str = read_string()

match str with

  Some data -> printf("good, we got value and we can process...")

  None -> printf("what happened, call IT right now!")
```

> > 注意 `read_string()` 的简单实现是 `Console.ReadLine()`。当控制台 Ctrl+Z 时，`Console.ReadLine()` 方法返回 NULL。

对于 F# 程序员来说，情况有所不同。用户可能会提供无效输入，因此代码必须表示这种无效输入。option 类型被用于显式地指示无效状态。当 F# 程序员调用 `read_string` 函数时，返回的 option 类型会提醒（甚至强制）F# 程序员处理这种无效情况。F# 的设计帮助开发者避免了许多 bug。一个典型的例子是 F# 如何引入 option 而不是使用 NULL 值来表示多种类型。如果你数一下你上个月收到的许多 NULL 异常，那么理解为什么 F# 程序员会在代码中报告 bug 就不难了。

让我们来看 C# 中的一个自定义类示例。如果你有一个 `Person` 类型对象，赋值值 NULL 的意义是什么？它要么意味着对象处于未赋值状态，要么意味着对象处于特殊状态（即它有一个无效值）。这种歧义性破坏了单一责任原则，即 SOLID 的第一原则。如果同一团队的两个开发者对 NULL 对对象的含义有不同看法，那么应用程序中可能会出现很多空引用缺陷。如果将其与 F# 的 option 方法相比较，`None` 用于表示没有值，而 `Some(...)` 用于表示任何有效值。这明确了定义。

当我们设计这种语言时，我们知道并不是所有人都会同意上述论点。这完全没，因为你可以使用 `AllowNullable` 特性来使类可为空。列表 6-13 显示了如何使用 `AllowNullLiteral` 特性的示例。

+ 列表 6-13 在类型上使用 AllowNullLiteral

```fsharp
<AllowNullable()]

type NullableType()

  member this.TestNullable(condition) =

    if condition then Nullable()

    else null
```

> 注意 如果类型被装饰了 AllowNullLiteral 特性，则该代码将无法编译。

在读完列表 6-13 后，你可能会疑惑为什么 F# 仍然允许空值。这是因为 F# 处于一个接受 NULL 作为输入值的对象和方法的世界中。如果 F# 不支持 NULL，那么许多 .NET 调用将是不可能的。此外，当变量需要绑定到函数时，需要 NULL。参见列表 6-14。

# 列表 6-14 检查函数初始化

```fsharp
type A() =

    [DefaultValue>]

    val mutable MyFunction : unit -> int

    member this.IsMyFunctionInitialized

    with get() = box this.Function = null
```
