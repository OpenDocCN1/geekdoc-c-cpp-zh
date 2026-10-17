
`let fieldType = ProvidedMeasureBuilder.Default.AnnotateType(typeof(float),[units])`

```fsharp
// 没有单位，将其视为普通的 float

headerText, typeof=float

else

let fieldProp = ProvidedProperty(fieldName, fieldType,

    GetterCode = fun [row] -> @@

(3%float(row[].i)) @@
```

```fsharp
// 添加元数据，以定义属性在引用文件中的位置。

fieldProp.AddDefinitionLocation(1, [i].Index + 1, filename)

rowTy.AddMember(fieldProp)
```

```fsharp
// 定义提供的类型

let ty = ProvidedDefinition(asm, ns, tyName, Some(typeof(CsvFile)))
```

```fsharp
// 一个无参数构造函数，加载用于定义 schema 的文件。

let ctor0 = ProvidedConstructor([])

InvokeCode = fun [] -> @@

CsvFile(resolvedfilename) @@
```

```fsharp
// 添加更强类型的数据属性，它在运行时使用现有属性。

let prop = ProvidedProperty("Data", typeof(seq<>)).MakeGeneric(rowTy),

    GetterCode = fun [csvFile] -> @@(%%csvFile:CsvFile).

Data @@0)
```

```fsharp
ty.AddMember prop

ty.AddMember ctor0
```

```fsharp
// 将行类型作为嵌套类型。

ty.AddMember rowTy

ty

// 将类型添加到命名空间。

do this.AddNamespace(ns, [csTy])
```

两个有趣的概念在类型提供程序的实现中引入。类型提供程序和 CSV 文件头通过 schema 定义了数据的含义。从 Excel 2007 开始，引入了一种新的格式，可以通过 Open SDK 访问。

# 使用 Excel 类型程序

图 5-6 Excel 内容

列表 5-21 创建了一个使用 Open SDK 访问 文件的类。要运行此代码，必须向项目添加 `DocumentFormat.OpenXml.dll`、`System.Xml.dll` 和 `WindowsBase.dll`。

|  | A | B | C |
|---|---|---|---|
| 1 | 1 | 2 | 3 |
| 2 |  |  |  |
| 3 |  |  |  |

```fsharp
| Seq.map snd

| (sheet.Name.Value, c))

| Seq.collect id

| Seq.toList

member this.Cells = cells

member this.Cell(col,row) =

    cells |= Seq.Tryfind(fun cell->cell.Name=(col,row)

member this.Cell(col,row, v) =

    let cell = this.row,

    match cell with

    | Some c ->

        if c.Cell.CellFormula = null then

        c.Cell.Value.Text <- v

    | None -> ()

member this.Close() = myWorkbook.Close()
```

注意：`Close` 方法会保存并关闭 XLSX 文件。

列表 5-22 所示类型提供程序脚本展示了向终端用户暴露了类成员。代码打开了 `Book1.xlsx` 并首先读取 A1 单元格的内容。然后将 A1 内容更改为 99。

# 列表 5-22 ExcelTypeProvider 脚本文件

```fsharp
let r =@.\bin\Debug\TypeTemplate2.dll"

type T = Samples.Excel.TypeProvider<"Book1.xlsx">

let t = T()

let (Some(cell)) = t.GetCell(t,A, t.'11')

printf "%A" cell.Value

t.SetCell(t,A, t.'11', "99")

t.Close()

let t2 = T()

let (Some(cell2)) = t2.GetCell(t2,A, t2.'11')

printf "%A" cell2.Value

t2.Close()
```

注意：需要调用 `Close` 方法，否则脚本在执行一次后将生成错误。错误信息为“无法访问 Book1.xlsx，因为它已被另一个进程打开。”

列表 5-23 所示的类型提供器代码提供了几个方法。它使用 `System.Object` 作为基类以隐藏了 `ExcelFile` 成员。它还提供了 Excel 列和行名作为只读属性。

# 列表 5-23 ExcelProvider 实现代码

```fsharp
// 访问 http://fsharp.net 了解更多 F#
// 请参考 'F# Tutorial' 项目以获取更多帮助。

namespace Samples.Fsharp.TypeProviderTemplate

open System.Reflection

open Microsoft.Fsharp.Compiler.Services

open Samples.Fsharp.ProvidedTypes

open ExcelClass

[ContextProvider]

type TypeProvider1(cfg:TypeProviderConfig) as this =

    inherit TypeProviderForNamespaces(types)

// 获取用于存放提供的类型的程序和命名空间

let Assembly = Assembly.GetExecutingAssembly()

let rootNamespace = "Samples.Excel"

let baseType = typeof(obj)

let newT = ProvidedTypeDefinition(

    thisAssembly,

    rootNamespace,

    "ExcelProvider",

    Some baseType)

let filename = DefinedStaticParameter("filename", typeof<string>)

do new.T.DefineStaticParameters(

    [filename],

    fun tyName = [: string filename ] ->

        let path = System.IO.Path.Combine(cfg.ResolutionFolder, filename)

        let ty = ProvidedTypeDefinition(

            thisAssembly, rootNamespace, tyName, Some(typeof<obj>))

        ty.AddMember([], InvokeCode = fun _ -> <<@ExcelFile(path,

true)>>))

let file = ExcelFile(path, false)

let rows = file.Cells

    |> Seq.map (fun cell -> cell.Name)

let cols = file.Cells
```

## 第二部分 F# 的独特特性

```fsharp
| Seq.map (fun cell -> cell.Name)

|> Seq.map (fun col,row) -> col

|> Seq.distinct
```

```fsharp
rows

|> Seq.append cols

|> Seq.iter (fun n ->

ty.AddMember(

  n,
```

```fsharp
//调用 F2 并输出日志信息

t.F2(2)
```

执行结果：
log before Samples.FSharp.ShareInfoProvider.BaseType2 "F1"
hello
log after Samples.FSharp.ShareInfoProvider.BaseType2 "F1"

log before Samples.FSharp.ShareInfoProvider.BaseType2 "F2"
2
log after Samples.FSharp.ShareInfoProvider.BaseType2 "F2"
```

## 列表 5-28 用于包装类型的密封类

```fsharp
[< Sealed >
type BaseType2() =
    member this.F1(s) = printfn "%s" s
    member this.F2(i) = printfn "%d" i

// 日志函数
type LoggingFunctions =
    static member LogBeforeExecution(obj:BaseType2, methodName:string) =
        printf "log before %A %A" obj methodName
    static member LogAfterExecution(obj:BaseType2, methodName:string) =
        printf "log after %A %A" obj methodName
```

下一个任务是确定如何使用引用（quotation）调用日志函数和基类方法。需要解决两个问题，提供解决方案的代码如列表 5-29所示。

- **调用方法**：方法通过 `Expr.Call` 执行，如果该方法不是静态方法，它接受三个参数；如果是静态方法，则只接受两个参数。`Expr.Call` 的参数使用 `Expr.Value` 创建。

- **调用语句序列**：语句的调用由 `Expr.Sequential` 处理。这种这种只接收元素的方法似乎是个问题，特别是当需要调用两个以上的语句时。实际上，这完全不是问题。如果第二个参数是 `Expr.Sequential`，它有一个额外的空间来存放随后的语句。

## 列表 5-29 调用基类方法和日志函数的引用代码

```fsharp
let baseTExpression = <<@%args.[0]:BaseType2> @@
let m1 = baseTy.GetMethod(methodName)
```

```fsharp
// 获取 LogBefore 函数的引用
let logExpr = Expr.Call(typeof<LoggingFunctions>.GetMethod("LogBeforeExecution",
    [baseExpression; Expr.Value(methodName) ])
```

```fsharp
// 调用基类的方法
let invokeExpr = Expr.Call(baseExpression, mi, args.Tail)
```

```fsharp
// 获取 LogAfter 函数引用
let logAfterExpr = Expr.Call(typeof<LoggingFunctions>.GetMethod("LogAfterExecution",
    [baseExpression; Expr.Value(methodName) ])
```

```fsharp
// 调用日志器、基方法和 logAfter
Expr.Sequential(logExpr, Expr.Sequential(invokeExpr, logAfterExpr))
```

完整代码在列表 5-30 中。使用反射来从基类获取方法名并生成所提供的方法。由于反射代码仅在编译时（设计时）执行，生成的 IL（如列表 5-31 所示）不包含任何反射代码。该包装类对基类的公共方法和属性具有可见性，且生成和维护它的成本远低于列表 5-26 所示的手动方法。

包装类型可以用于源代码不可用的情况。`Activator.CreateInstance` 方法对于 C# 开发者来说并不陌生。DLL 路径和类型名称可以作为字符串传递，并可以使用 `CreateInstance` 来创建密封类的实例。

## 列表 5-30 完整的类型提供代码

```fsharp
namespace Samples.FSharp.ShareInfoProvider

open System.Reflection
open Microsoft.FSharp.Core.Compilers
open Samples.FSharp.ProvidedTypes
open System.IO
open System.Collections.Generic
open Microsoft.FSharp.Quotations

[<Sealed>]
type BaseType2() = 
    member this.F1(s) = printfn "%s" s
    member this.F2(i) = printfn "%d" i

type LoggingFunctions =
    static member LogBeforeExecution(obj:BaseType2, methodName:string) =
        printf "log before %A" obj methodName
    static member LogAfterExecution(obj:BaseType2, methodName:string) =
        printf "log after %A" obj methodName
```
