
```fsharp
|> Seq.map(fun p -> ProvidedParameter(p.Name, p.ParameterType))

|> Seq.ToList()
```

```fsharp
let staticStaticParams = [ProvidedStaticParameter("dll", typeof<string>);
    ProvidedStaticParameter("type", typeof<string>);
    ProvidedStaticParameter("type2", typeof<string>)]
do regexTy.DefineStaticParameters(
    instantiationfunction(fun type parameterValues ->
        let name = parameterValues.[1] ?: string;
        let name2 = parameterValues.[2] ?: string;
        let dll = System.IO.Path.GetDirectoryName(tpc.RuntimeAssembly),
        parameterValues.[0] ?: string;
        let r = MyBase(dll, [ name; name2 ])
        let ty = ProvidedTypeDefinition(
            thisAssembly,
            rootNamespace,
            typeName,
            Some typeof(obj),
            HiddenObjectMethods = true)
        [[ name; name2 ]
        |> Seq.iter(fun n ->
            let methods = r.GetMethods(n)
            let providedMethods =
                methods
                |> Seq.map(fun m -> 
                    let methodName = m.Name
                    ProvidedMethod(
                        methodName = methodName,
                        parameters = (getParameters m),
                        returnType = m.ReturnType,
                        IsStaticMethod = false,
                        InvokeCode = fun args ->
                            let baseValue = r
                            let baseTExpression = <<\0(Args.[0]:obj) ?: MyBase).
                            let mi = baseValue.GetObj(n)
                            .GetType())
                            GetObj(n) @@>>
                            .GetMethod(methodName)
                            Coerce(baseTExpression, t),
```

```fsharp
        let t = System.Type.GetType(n)
        let invokeExpr =
            Expr.Call(Expr).mi,
            invokeExpr,
            args.Tail))
```

```fsharp
        providedMethods |> Seq.iter ty.AddMember
```

```fsharp
let ctor =
    ProvidedConstructor(
        parameters = [],
        InvokeCode = fun args -> @@ MyBase(dll, [| name; name2 |]) : obj)
    ty.AddMember(ctor)
    ty
)
```

```fsharp
let ctor = ProvidedConstructor(parameters = [],
InvokeCode = fun args -> @@ System.Object() @@
```

do
    regexTy.AddMember ctor
    do this.AddNamespace(rootnamespace, [regexTy])

interface System.IDisposable with
    member this.Dispose() = System.AppDomain.CurrentDomain.remove_AssemblyResolve handler

[<TypeProviderAssembly>]

Test脚本
# "@\bin:Debug\ShareInfoSampleTypeProvider.dll"
# "@\bin:Debug\ClassLibrary1.dll"

type T = Samples.ShareInfo.PTTest.MultiInheritanceTypeProvider<
"ClassLibrary1.dll"
"ClassLibrary1.Class1, ClassLibrary1, Version=1.0.0.0, Culture=neutral,
PublicKeyToken=null"
"ClassLibrary1.Class2, ClassLibrary1, Version=1.0.0.0, Culture=neutral,
PublicKeyToken=null">

```fsharp
let t = T
t.F1()
t.F2()
t.F1()
t.F2()
```

> 注意：由于字典返回的是 `System.Object` 类型，并且由于需要转换为正确的类型，因此需要转换代码 `Expr.Coerce(baseTExpression, t)`。

该包装器和多继承类型提供程序示例展示了如何使用类型提供程序进行元编程。传递到类型提供程序的数据除了静态参数、本地文件或两者外，还可以源于类型提供程序代码内部基类或模块。

# 使用 XML 类型提供程序

本节介绍了如何使用 XML 类型提供程序的设计时功能。类型提供程序的定义显示它是一个设计时适配组件。在本节中提供的示例探索了定义中的设计时部分。许多应用程序使用 XML 文件作为输入数据源。这种方法的问题是 XML 可能会变得复杂，且文本文件中的错误只能在运行时进行检查。XML 类型提供程序将通常在运行时进行的验证移动到了设计。

`Provided` 中的 `InvokeMethod` 返回一个代码引申（code quotation），它也可以包含其他代码。该引申将在运行时执行，而其他代码将在设计时执行。这正是插入并执行验证代码的地方。

生产代码和示例 XML 文件分别如列表 5-37 和列表 5-38 所示。这两个列表要求 XML 文件符合某些标准：起始值必须等于或小于结束值。如果验证只能在运行时发生，那可能是一场灾难。另一种方法是使用验证工具，例如检查门禁验证器（check-in gate validator）。如果验证可以及时完成，这些方法都无法提供同比例的编码体验。当用户调用方法时，他会立即看到错误。

## 列表 5-37 类型提供程序调用的生产代码

```fsharp
type MyProductionCode()
    member this.Work() =
        let xml = XDocument.Load("XmlFile.xml")
        let start = xml.Descendants(XName.Get("Start")) |> Seq.head
        let end = xml.Descendants(XName.Get("End")) |> Seq.head
        // if start > end, something bad will happen
        if Convert.ToInt2(start.Value) > Convert.ToInt2(end.Value) then
            failwith("report runtime")
```

## 列表 5-38 XML 文件

```xml
<?xml version="1.0" encoding="utf-8"?>
<Config>
  <Start>6</Start>
  <End>5</End>
</Config>
```

如常，测试脚本首先定义。如果 XML 文件无效，开发者将会在 Visual Studio 中立即看到错误。见图 5-7。列表 39 类型提供程序。

```fsharp
#r "\bin:Debug\ShareInfoSampleTypeProvider.dll"
type T = Samples.ShareInfo.PTTest.MultiInheritanceTypeProvider<"xml file name">
```

```fsharp
#r "\bin:Debug\ClassLibrary1.dll"
type T = Samples.ShareInfo.PTTest.MultiInheritanceTypeProvider<"ClassLibrary1.dll">
```

## 列表 40 类型提供程序代码

这种类型提供程序的优之处在于，验证只有在设计时通过类型提供程序调用时才会执行。与在运行时调用的用例不同，它允许在验证通过时才调用函数。

```python
let ctor = ProvidedConstructor(
    parameters = [],
    InvokeCode = fun args -> @@MyProductionCode(@@@>)
ty.AddMember(ctor)
ty.AddMember(m)
nty.AddXmlDoc("xml comment" ty))
do
    newT.AddMember(ctor)
do this.AddNamespace(rootNamespace, [newT])
```

> 注意：此代码需要引用 `System.Xml` 和 `System.Xml.Linq`。

类型提供程序（Type provider）为用户提供了一个设计设计时逻辑的地方。你可以使用类型提供程序更好地利用 Visual Studio 的编辑功能，而无需深入 Visual Studio SDK 的细节。

## 使用 DGML 文件类型提供程序

Visual Studio 支持定向图图标记语言（DGML）。DGML 用于绘制表示包含节点和边的图结构的图表。你可以使用 DGML 来表示状态机，其中节点表示状态，边表示状态之间可能的转换。图 5-8 展示了 DGML 在 Visual Studio 中的显示方式。它表示一个具有四个状态（从 State0 到 State3）的状态机。DGML 文件实际上是一个 XML 文件。列表 5-41 显示了图 5-8 中所示 DGML 文件的内容。Nodes 部分定义了图中的所有节点，Links 部分定义了所有的边。

图 5-8 DGML 文件表示一个带有存储的状态机

## 列表 5-41 DGML 文件内容

```xml
<xml version="1.0" encoding="utf-8"?>
<DirectedGraph GraphDirection="LeftTo" Layout="Sugiyama"
xmlns="http://schemas.microsoft.com/vs/2009/dgml">
<Nodes>
  <Node Id="State0" Bounds="0,19.02,53.36,25.96" />
  <Node Id="State1" Bounds="170.095,93.02000000001,53.36,25.96" />
  <Node Id="State2" Bounds="85.0474999999999,93.02,53.36.26" />
  <Node Id="State3" Bounds="255.1425,93.02,53.06,21.26" />
</Nodes>
<Links>
  <Link Source="State0" Target="State1"
  Bounds="53.36006103516,32.13,141.7319086914,53.216644281094" />
  <Link Source="State0" Target="State2"
  Bounds="41.5977897644043,44.979994523,48.22275432129,42.13230240527" />
  <Link Source="State0" Target="State3"
  Bounds="53.9286056379109,78.50818-14,22.33571353742,48.6670761108398" />
  <Link Source="State1" Target="State2"
  Bounds="132.53122550594,118.0000356934,50.109100319769,26.99966430664" />
  <Link Source="State1" Target="State3"
  Bounds="138.407051022072,82.204556247418,10.35516374219,16.30454394513" />
  <Link Source="State2" Target="State3"
  Bounds="217.56062318943,18.0000356934,50.109115006859,26.99966430664" />
</Links>
<Properties>
  <Property Id="Bounds" DataType="System.Windows.Rect" />
  <Property Id="GraphDirection"
  DataType="Microsoft.VisualStudio.Diagrams.Layout.LayoutOrientation" />
  <Property Id="Layout" DataType="String" />
</Properties>
</DirectedGraph>
```

正如我在其他类型提供程序示例中所做，我首先定义如何使用 DGML 文件类型提供程序。图 5-8 显示了状态机。列表 5-42 有以下三个部分并展示了如何使用类型提供程序：

- 部分 I 创建类型提供程序，它接受两个参数。一个参数指定 DGML 文件，另一个参数指定状态机的初始状态。此时，状态机从 DGML 文件创建。
- 部分 II 定义了一组转换函数。这些函数封装在一个实现了 `IState` 接口的表达式中，如后续代码所示。`EnterFunction` 和 `ExitFunction`将在进入或退出状态时调用。

```fsharp
type IState =
// 进入状态时调用
abstract member EnterFunction : unit -> unit
// 退出状态时调用
abstract member ExitFunction : unit -> unit
```

- 部分 III 执行一系列转换操作。从 DGML 定义可以看出，前三个转换是有效的。最后一个从 State3 到 State2 的转换是无效的，因此该转换函数不会执行。列表 5-42 用于 DGML 文件的脚本：

```fsharp
// 部分 I
type T =
// 部分 II
// 定义函数
let syncRoot = ref 0
let print str = lock(syncRoot) (fun _ -> printf "%s" str)
// 转换表达式
let printObj = { TypeProvider.IState with
    member EnterFunction() = print ("Enter " + CurrentState)
    member ExitFunction() = print ("Exit " + CurrentState)
}
// 设置转换函数
t.SetFunction(t.State0, printObj)
t.SetFunction(t.State1, printObj)
t.SetFunction(t.State2, printObj)
t.SetFunction(t.State3, printObj)
// 部分 III
// 有效转换
t.TransitTo()
```

状态机读取 DGML 文件并生成图结构。实际实现定义了如列表 5-43 所示的两个类。一个表示带有文件中定义的节点列表和边的 DGML 文件。另一个继承自 `DGMLClass` 并添加了 `MailboxProcessor` 来异步处理转换，以及几个设置转换函数的方法。这些类可以被视为处理任何 DGML 文件的库。

## 列表 5-43 DGML 类型提供程序状态机实现

```fsharp
```
