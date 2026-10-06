
type-provider 类代码如列表 5-2 所示。如你在列表 5-1 中看到的，该类应该有一个无参数的构造函数和一个属性。type-provider 类应该继承自 `TypeFromNamespaces` 类，并用 `TypeProvider` 属性装饰。type-provider 是通过 `ProvidedTypeDefinition` 类创建的。它有四个参数，其中只有两个参数对我们感兴趣。命名空间在创建 `ProvidedTypeDefinition` 实例时指定。像 .NET 中的所有类型一样，它需要一个基类。在示例代码中，基类是 `type<obj>`。提供的类型定义命名为 `newT`，通过调用 `AddNamespace` 并传入命名空间变量添加到代码末尾。

一旦创建了类型，方法和属性就很容易理解。`ProvidedMethod` 接收一个方法名称、一个返回类型、一个指示属性是否为静态的布尔值，以及一个包含代码引用的函数，该函数在方法调用时将被执行。在示例代码中，`InvokeCode` 为 1，因此它将返回 2。属性通过创建 `ProvidedProperty` 来添加，其接收属性名称、属性类型、是否为静态的指示以及 getter/setter。

函数逻辑必须是一个代码引用。代码引用是一个表示 F# 的树形结构。这在 C# LINQ 中没有直接的等价物。生成 F# 代码引用有两种方法：一种是使用 `@@` 和 `@@` 运算符，另一种是使用 `Expr` 函数。这两种方法生成相同的代码引用，你可以任选择一种。本文中的示例代码演示了如何生成代码引用。

F# 类如果没有构造函数无法实例化；因此，对于 type-provider 类型来说，构造函数是强制的，尽管在大多数情况下它什么都不做。`ProvidedConstructor` 不接受任何参数，且构造函数代码什么都不做。最后，提供的属性和构造函数通过调用 `AddMember` 函数添加到 `ProvidedTypeDefinition` 变量 `newT` 中。

# 列表 5-2 生成的 type-provider 代码

```
namespace Samples.FSharp.HelloWorldTypeProvider

open System.Reflection
open Microsoft.FSharp.Core.Compiler
open Samples.FSharp.ProvidedTypes

[TypeProvider]
type public TypeProvider1() as is =
    inherit TypeProviderForNamespaces()

// 获取用于存放提供属性的程序集和命名空间
let thisAssembly = Assembly.GetExecutingAssembly()
let rootNamespace = "Samples.ShareInfo.TPTest"
let baseType = typeof<obj>

let newT = ProvidedTypeDefinition(thisAssembly, rootNamespace, "TPTestType", baseType);
```

```
// 添加其他属性和方法定义
let m = ProvidedMethod(
    methodName = "methodName",
    parameters = [],
    returnType = typeof<int),
    IsStaticMethod = false,
    InvokeCode = fun args ->
    <@0 1 + 1 @@>
)

let ctor = ProvidedConstructor(parameters = [], InvokeCode = fun args -> (* base class initialization or null*) (@))

let prop2 = ProvidedProperty(propertyName = "Property1",
    propertyType = typeof<string>,
    IsStatic=false,
    GetCode = (fun args -> <<@ "Hello! @@),
    SetterCode = (fun args -> <<@ printf "setter code" @@))
```

do prop2.AddMemberDelayed(fun () -> "xml comment")
newT.AddMember(m)
newT.AddMember(prop2)
newT.AddMember(ctor)

do this.AddNamespace(rootnamespace, [newT])

[<ProviderAssembly]
do ()

> 注意：其他函数和属性将在后续章节中介绍。

测试脚本是轻量级的，适合测试和调试小型 type provider，但它不是实现该目的唯一方法。对于复杂的 type providers，使用两个 Visual Studio 实例是明智的选择。使用一个 Visual Studio 实例来开发 type provider，并将其称为 *Developing Visual Studio*（开发 Visual Studio）。使用另一个 Visual Studio 实例托管测试项目，并将其称为 *Testing Visual Studio*（测试 Visual Studio）。*Developing Visual Studio* 需要附加到 *Testing Visual Studio*。

> 提示：由于 type-provider DLL 被 Visual Studio 锁定，重启 Visual Studio 是不可避免的。如果使用测试脚本，请确保在关闭项目时脚本文件不是当前文件；否则，它在下次打开项目时将自动打开并从而锁定 DLL。

# 探索 HelloWorld Type Provider

如果你理解了本节中的 F# type-provider 模板，跟上对你来说很容易。然而，如果上一节中的任何代码 type-provider 示例不清楚，HelloWorld type provider 示例将提供一些说明。这个 type-provider 示例有五个方法和五个属性。列表 5-3 定义了用户如何调用 HelloWorld type provider，可以用于设计和测试 type provider。

**列表 5-3** HelloWorld type-provider 脚本

```
# r @"\bin\Debug\HelloWorldTypeProvider.dll"

let assertFunction x =
    if not x then failwith "expression is false"

type T = Samples.ShareInfo.TPest.HelloWorldTypeProvider
let t = T()
asertFunction(t.Method1()) = 1
asertFunction(t.Method2()) = 2
asertFunction(t.Method3()) = 3
asertFunction(t.Method4()) = 4
asertFunction(t.Method5()) = 5
asertFunction(t.Property6) = "Property 6"
asertFunction(t.Property7) = "Property 7"
asertFunction(t.Property8) = "Property 8"
asertFunction(t.Property9) = "Property 9"
asertFunction(t.Property10) = "Property 10"
```

> 注意：其他函数和属性将在后续章节中介绍。
