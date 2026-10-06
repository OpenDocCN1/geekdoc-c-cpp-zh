

```fsharp
// 尝试将此标头拆分为名称和单位。
let fieldName, fieldType =
let m = Regex.Match(headerText, @"(?<field>.+) \((?<unit>.+)\)")
if m.success {
    let fieldName = m.Groups["field"].Value
    let unitName = m.Groups["unit"].Value
    let units = ProvidedMeasureBuilder.Default.Si unitName
    let fieldType = ProvidedMeasureBuilder.Default.AnnotateType(typeof<float>,[ts])
    (fieldName, fieldType)
} else {
    // 没有单位，将其视为普通的 float
    headerText, typeof<float>
}
```

```fsharp
let fieldProp = ProvidedProperty(fieldName, fieldType,
    GetCode = fun [row][i] -> <<0
```

```fsharp
// 添加元数据，以定义属性在引用文件中的位置。
fieldProp.AddDefinitionLocation(1, headers.[i].Index + 1, filename)
rowTy.AddMember
```

```fsharp
// 定义属性类型
let ty = ProvidedTypeDefinition(asm, ns, typeName, Some(typeof<obj>)
```

```fsharp
// 一个无参数构造函数，加载用于定义 schema 的文件。
let ctor0 = ProvidedConstructor([]),
    InvokeCode = fun _ -> <<0>> <<0>>
```

```fsharp
// 添加一个更强类型的 Data 属性，它在运行时使用现有属性。
let prop = ProvidedProperty("Data", typeof<seq_>.MakeGenericType(rowTy),
    GetCode = fun _ -> <<0>> CsvFileModule.data
```

```fsharp
ty.AddMember prop
ty.AddMember ctor0
```

```fsharp
// 将行类型作为嵌套类型。
ty.AddMember rowTy
ty
```

```fsharp
// 将类型添加到命名空间。
do this.AddNamespace(ns, [csTy])
```

```fsharp
[<TypeProviderAssembly>]
do ()
```

注意 将函数封装在模块中会有帮助

# 236 第 II部分 F# 的独特特性

另一种方法是使用用户定义的 CSV 类来处理文件并返回数据列表。类型提供程序的工作是为设计智能感知（IntelliSense）提供单位类型和额外的类成员。CSV 类和类型提供程序代码如图 5-20 所示。CSV 文件的第一行由正则表达式解析；列名（也包含单位类型）被检索并生成。CSV 类返回 Data 属性，其内容被传递到生成的类型 `rowTy` 中。`rowTy` 类型为每个数据项提供了单位类型和命名属性。

# 列表 5-20 CSV 文件类

```fsharp
// 在 http://fsharp.net 学习 F#
// 更多帮助请参阅 F# Tutorial ' ' project 项目。

namespace Samples.Fsharp.CSVTypeProvider

open System.Reflection
open Microsoft.Fsharp.Core.CompilerServices
open Samples.Fsharp.ProvidedTypes
open System.IO
open System.Text.RegularExpressions

// CSV 文件类
type CSVFile(filename) =
let data =
    [ for line in File.ReadAllLines(filename) | Seq.skip 1 do
        yield line.Split(',') | Array.map float [] ]
    member .Data = data

// 支持单位的 CSV 类型提供程序代码
[<TypeProvider>
type public CSVProvider(cfg:CfgTypeProviderConfig) as =
    inherit TypeProviderForNamespaces())

// 获取用于存放提供的程序集和命名空间。
let asm = System.Reflection.Assembly.GetExecutingAssembly()
let ns = "Samples.ColorF.Test"

// 创建主提供类型。
let csvTy = ProvidedTypeDefinition(asm, ns, "CSVProvider", some(typeof<obj>))

// 通过文件对类型进行参数化作为模板。
let filename = ProvidedStaticParameter("filename", typeof<string>)

csvTy.DefineStaticParameters([filename], fun typeName [ ?: string as filename ] ->

// 解析相对名称到解析文件夹。
let resolvedFileName = Path.Combine(cfg.ResolutionFolder)

// 获取文件的第一行。
let headerLine = File.ReadLines(resolvedFileName) |> Seq.head
```

```fsharp
// 为每行定义一个提供的类型
```

```fsharp
// 从文件中提取标头名称并使用
// 正则获取字段在行中的位置
let headers = Regex.Matches(headerline, "[^,]+")
```

```fsharp
// 每个 CSV 字段一个属性。
for i in 0 .. headers.Count - 1 do
let headerText = headers[i].Value
```

```fsharp
// 尝试将此标头拆分为名称和单位。
let fieldName, fieldType =
let m = Regex.Match(headerline, @"(?<field>.+)\.(?<unit>.+)\)")
if m.Success then
let fieldName = m.Groups("field").Value
let unitName = m.Groups("unit").Value
let units = ProvidedMeasureBuilder.Default.UnitName
let fieldType = ProvidedMeasureBuilder.Default.AnnotateType(typeof(float),[units])
```

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
let prop = ProvidedProperty("Data", typeof(seq<>>).MakeGeneric(rowTy),
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

列表 5-21 创建了一个使用 Open SDK 访问 文件的类。要运行此代码，必须向项目添加 DocumentFormat.OpenXml.dll、System.Xml.dll 和 WindowsBase.dll。

| | A | B | C |
|---|---|---|---|
| 1 | 1 | 2 | 3 |
| 2 | | | |
| 3 | | |

