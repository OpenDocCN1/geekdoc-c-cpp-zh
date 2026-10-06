
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

Note The Close method saves and closes the XLSX file.

The type-provider script, presented in Listing 5-22, shows what class members are exposed to the end user. The code opens Book1.xlsx and reads the A1 cell content first. Then the A1 content is changed to 99.

# LISTING 5-22 ExcelTypeProvider script file

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

Note The Close method needs to be invoked, otherwise the script will generate an error after it is executed once. The error message is "Cannot access Book1.xlsx because it is opened by another process."

The type provider code, shown in Listing 5-23, provides several methods. It uses System.Object as a base class to hide the ExcelFile members. It also provides Excel columns and row names as read-only properties.

# LISTING 5-23 ExcelProvider implementation code

```fsharp
// Learn more about F# at http://fsharp.net
// See the 'F# Tutorial' project for more help.

namespace Samples.Fsharp.TypeProviderTemplate

open System.Reflection
open Microsoft.Fsharp.Compiler.Services
open Samples.Fsharp.ProvidedTypes
open ExcelClass

[ContextProvider]
type TypeProvider1(cfg:TypeProviderConfig) as this =
    inherit TypeProviderForNamespaces(types)

// Get the assembly and namespace used to house the provided types
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

PART II F#'s Unique Features

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
typeof<string>,
GetterCode = fun -> <<@ n @>>)
```

```fsharp
file.Close()()
let mi = ProvidedMethod(
  "GetCell",
  [ProvidedParameter("row", typeof<string>),
  ProvidedParameter("col", typeof<string>),
  typeof<CellContent option>],
  InvokeCode = =
    fun me; row; -> <<@
      ((%me:obj)?->ExcelFile).Cell((%row:string),(%col:string))@@>>)
```

```fsharp
let close = ProvidedMethod(
  "Close", [], typeof<unit>,
  InvokeCode = =
    fun me -> <<@(%me:obj)?->ExcelFile).Close()>>)
```

```fsharp
let save = ProvidedMethod(
  "SetCell",
  [ProvidedParameter("row", typeof<string>),
  ProvidedParameter("col", typeof<string>),
  ProvidedParameter("value", typeof<string>),
  typeof<unit>],
  InvokeCode = =
    fun me; row; v -> <<@((%me:obj)?->ExcelFile)
Cell((%row:string),
(%col:string),
(%v:string)) @>>)
```

```fsharp
ty.AddMember(mi)
ty.AddMember(save)
ty.AddMember(close)
ty
do this.Namespace(rootNamespace, [newT])
```

Note The "Incomplete pattern matches on this expression" warnings are expected and can be ignored.

# Using the TypeProvider Base Class

Until now, there has been no way to share information or coordinate actions between methods within a type provider. methods show relationships when invoked. The interesting part about Listing 5-24 is that it stores the file name in the base class and enables methods to share that information between calls.

# Sharing Information Among Members

A simple example is shown in Listing 5-24. The type provider provides a non-object-based property that can be used to store information that can be shared between method calls. The code is very close to HelloWorld type provider except for the base class. One thing that needs to be called out is the constructor. Because the provided type is erased to the base type, the constructor needs to return the base type instance instead of nothing. Listing 5-24 seems to do nothing, but it opens the door to a more interesting scenario, which will be presented in the next section.

LISTING 5-24 Type provider sharing between members

```fsharp
namespace Samples.Fsharp.ShareInfoProvider
open System.Reflection
open Microsoft.Fsharp.Core.CompilerServices
open System.IO
open System.Collections.Generic

// base class the type provider erased to
type Base2() = 
    member val X = "" with get, set

[TypeProvider]
type RegexProvider() as this =
    inherit TypeProviderForNamespaces()

// Get the assembly and namespace used to host the provided types
let thisAssembly = Assembly.GetExecutingAssembly()
let rootNamespace = "Samples.ShareInfo.Test"
let baseType = typeof<Base2>

let regex = ProvidedTypeDefinition(thisAssembly, rootNamespace, "TPTest", Some baseType)

let f1 = ProvidedMethod(
    methodName = "F1",
    parameters = [ProvidedParameter("input", typeof<string>)],
    returnType = typeof(unit),
    IsStaticMethod = false,
    InvokeCode = fun args -> <<%(args.[0]:Base2).X <<%(args.[1])>>)
)

let f2 = ProvidedMethod(
    methodName = "F2",
    parameters = [],
    returnType = typeof<string>,
    IsStaticMethod = false,
    InvokeCode = fun args -> <<%(args.[0]:Base2).X <<>>)
)

// constructor needs to return the Base2 instance
let ctor = ProvidedConstructor(
    parameters = [],
    InvokeCode = fun args -> <<Base2() @>>)

do
    regex.AddMember ctor
    regex.AddMember f1
    regex.AddMember f2

do this.AddNamespace(rootNamespace, [regex])
```

LISTING 5-25 Test script for the TPType provider sharing information between methods

```fsharp
# r "\bin\Debug\ShareInfoSampleProvider.dll"

type T = Samples.ShareInfo.Test.TPTest
let t = T()

t.F1("hello")
let a = t.F2()

printf "%A" a // the print result is hello
```

Because the provided type is based on Base2 and because the constructor returns an instance of Base2, the variable t is of type Base2.

# Using a Wrapper Type Provider

Imagine that you have a sealed class and need to add some logic for each member function, such as logging the function usage. The most common technique for a C# developer is to write a wrapper with the sealed class instance as a variable, as shown in Listing 5-26. It would be a tedious and boring task to refactor the sealed class. Reflection can be an option, but the performance impact of this approach is something that cannot be ignored.

**LISTING 5-26** Wrapper class to expand a sealed class

```csharp
// sealed class A
public sealed class A
{
    public void F1() { ... }
}

// new class to add logging function around the F1 defined in sealed class A
public class MyClass
{
    private A a = new A();
    public void F1()
    {
        LogBefore();
        a.F1();
        LogAfter();
    }
}
```
