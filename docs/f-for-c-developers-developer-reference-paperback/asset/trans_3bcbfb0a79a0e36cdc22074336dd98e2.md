

# 代码片段 | 类型提供者（Type Providers）与查询写入类型提供者 |

```sharp
type provider define static parameter
type provider provided constructor
type provider provided method
type provider provided property
type provider skeleton
type provider xml comment
```

图 5-11 编写类型提供者的代码片段

表 5-1 编写类型提供者的代码片段

| 代码片段名称 | 描述 |
| --- | --- |
| 类型提供者静态参数 | 为 `DefineStaticParameters` 函数生成骨架，该函数接收静态参数。以下是生成的默认代码：``````fsharp
let staticParams = [ProvidedStaticParameter("pattern", typeof<string>)
do request.DefineStaticParameters(
    parameters=staticParams,
    instantiationfunctions=fun typename parameterValues ->
    let ty = typeDefinition(
        this,
        rootnamespace,
        typename,
        baseType = Some baseTy),
    ty.AddXmlDoc("xml comment")
``` |
| 类型提供的的构造函数 | 生成类型提供者的构造函数。以下是生成的默认代码：```fsharp
let ctor = [
    parameters = [],
    InvokeCode = fun args ->
    << ( base class initialization or null*) ()
    >>
``` |
| 类型提供的方法 | 生成类型提供者的方法。以下是生成的默认代码：```fsharp
let m = ProvidedMethod(
    methodName = "methodName",
    parameters = [].
    returnType = typeof<int>,
    IsStatic = false,
    InvokeCode = fun args ->
    << 0 + 1 <<
)
``` |
| 类型提供的的属性 | 生成类型提供者的属性。以下是生成的默认代码：```fsharp
let prop1 = ProvidedProperty(
    propertyName = "Property1",
    propertyType = typeof<string>,
    IsStatic=false,
    GetterCode=(fun args -> << "Hello!" >>),
    SetterCode=(fun args -> << printf("setter code") >>)
``` |
| 类型提供者骨架 | 生成类型提供者的骨架。以下是生成的默认代码：```fsharp
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
``` |
| 类型提供者 XML 注释 | 生成 XML 注释。以下是生成的默认代码：```fsharp
ctor.AddDocDelayed(fun () -> "xml comment")
``` |
| 提供的度构建器（Provided measure builder） | 为类型提供者类型生成度。以下是生成的默认代码：```fsharp
let units = ProvidedMeasureBuilder.Default.Is "metre"
let unitType = ProvidedMeasureBuilder.Default.AnnotateType(typeof<float>, [units])
``` |
| 类型提供者参数 | 生成类型提供者的函数参数。以下是生成的默认代码：```fsharp
ProvidedParameter("var", typeof<string>)
``` |

## 类型提供者的局限性

F# 3.0 自带的类型提供者机制有一些局限性。读者可能已经注意到的第一个局限性是静态参数只能接收基本类型，例如整数和字符串。另一个局限性是类型提供者只能生成 .NET 1.x 类型。大多数 F# 特有的类型（如 record）都不支持。唯一的例外是度类型（units of measure），它们在此版本中是被支持的。这些局限性将在未来的版本中消除，但目前是如此。

## 类型提供者的局限性

... 大多数 F# 特有的类型（如 record）都不支持。

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

