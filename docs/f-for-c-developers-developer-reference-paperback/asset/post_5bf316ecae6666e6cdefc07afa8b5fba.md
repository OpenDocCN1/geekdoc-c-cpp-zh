
```
//invoke F2 and also output logging info
t.F2(2)
```

Execution result
log before Samples.FSharp.ShareInfoProvider.BaseType2 "F1"
hello
log after Samples.FSharp.ShareInfoProvider.BaseType2 "F1"

log before Samples.FSharp.ShareInfoProvider.BaseType2 "F2"
2
log after Samples.FSharp.ShareInfoProvider.BaseType2 "F2"
```

## LISTING 5-28 Sealed class for the wrapper type provider

```
[< Sealed >
type BaseType2() =
    member this.F1(s) = printfn "%s" s
    member this.F2(i) = printfn "%d" i

// logging functions
type LoggingFunctions =
    static member LogBeforeExecution(obj:BaseType2, methodName:string) =
        printf "log before %A %A" obj methodName
    static member LogAfterExecution(obj:BaseType2, methodName:string) =
        printf "log after %A %A" obj methodName
```

The next task is determining how to invoke the logging functions and base class method using a quotation. The two problems need to be solved, and the code that provides the solution is shown in List 5-29.

- **Invoke a method** The method is performed by Expr.Call, which takes three parameters if the method is not a static method and only two parameters if it is a static method. The parameter to Expr.Call is created using Expr.Value.

- **Invoke a sequence of statements** Invoking statements is handled by Expr.Sequential. It might seem like a problem that this only takes elements, especially when more than two statements need to be invoked. Actually, this is not a problem at all. If the second parameter is an Expr.Sequential, it has an extra space to hold the following statement.

## LISTING 5-29 Quotation code to invoke the base class method and logging function

```
let baseTExpression = <<@%args.[0]:BaseType2> @@
let m1 = baseTy.GetMethod(methodName)
```

```f
// get LogBefore function code quotation
let logExpr = Expr.Call(typeof<LoggingFunctions>.GetMethod("LogBeforeExecution",
    [baseExpression; Expr.Value(methodName) ])
```

```fsharp
// invoke the base class's method
let invokeExpr = Expr.Call(baseExpression, mi, args.Tail)
```

```fsharp
// getLogAfter function quotation
let logAfterExpr = Expr.Call(typeof<LoggingFunctions>.GetMethod("LogAfterExecution",
    [baseExpression; Expr.Value(methodName) ])
```

```fsharp
// invoke logger, base method, and logAfter
Expr.Sequential(logExpr, Expr.Sequential(invokeExpr, logAfterExpr))
```

The complete code is presented in Listing 5-30. Reflection is used to get the method names from the base class and to generate the provided methods. Because the reflection code is only executed at compile time (design time), the generated IL (which is shown in Listing 5-31) does not contain any reflection code. This wrapper class has visibility to the base class' public methods and properties, and the cost to generate and maintain it is significantly lower than the manual way shown in Listing 5-26.

The wrapper type can provide for cases in which source code is not available. The Activator.CreateInstance method is not something new for C# developers. The DLL path and type name can be passed as a string, and CreateInstance can be used to create the sealed class instance.

## LISTING 5-30 The complete type-provider code

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

```fsharp
<TypeProvider>
type public CheckedRegexProvider() as this =
    Inherit TypeProviderForNamespaces()

    // Get the assembly and namespace used to house the provided types
    let thisAssembly = Assembly.Share.GetExecutingAssembly()
    let rootNamespace = "Samples.Info.TPTest"
    let baseTy = typeof(BaseType)

    let regexTy = ProvidedTypeDefinition(thisAssembly, rootNamespace, "TPestType", Some
baseTy)

    let methods = baseTy.GetMethods()
    let getParameters(mi:MethodInfo) =
        let parameters = mi.GetParameters()
        parameters
        |> Seq.map(fun p -> ProvidedParameter(p.Name, p.ParameterType))
        |> Seq.ToList()
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
                    let baseExpression = <<@%(args[0]:BaseType2)>> <<@
                    let mi = baseTy.GetMethod(methodName)
                    let logExpr = Expr.Call(
                        typeof<LoggingFunctions>
                        .Method("LogBeforeExecution",
                        [baseExpression];Expr.Value(methodName) ])

                    let invokeExpr = Expr.Call(baseExpression, mi, args.tail)
                    let logAfterExpr = Expr.Call(
                        typeof<LoggingFunctions>
                        .Method("LogAfterExecution",
                        [baseExpression];Expr.Value(methodName)])

                    Expr.Sequential(
                        logExpr,
                        Expr.Sequential(invokeExpr, logAfterExpr)
                    )

                    let ctor = ProvidedConstructor(
                        parameters = [],
                        InvokeCode = fun args -> <<@ BaseType2() <<@)
                    do
        regexTy.AddMember ctor
        providedMethods |> Seq.iter regexTy.AddMember

    do this.Namespace(rootnamespace, [regexTy])

[<TypeProviderAssembly>
do ()
```

## LISTING 5-31 IL code from the compiled binary reference to the type provider

```
IL_0000: nop
IL_0001: newobj instance void
[ShareInfoSampleTypeProvider]Samples.Fsharp.InfoProvider.BaseType2::ctor()
IL_0006: box [ShareInfoSampleTypeProvider]Samples.Fsharp.InfoProvider.BaseType2
IL_0008: unbox. [ShareInfoSampleTypeProvider]Samples.Fsharp.InfoProvider.BaseType2
IL_0009: dup
IL_0011: stfld class
[ShareInfoSampleTypeProvider]Samples.Fsharp.InfoProvider.BaseType2 '<StartupClassCons
leApplication1>$Program'::$08
IL_0016: stloc.0
IL_0017: call class [ShareInfoSampleTypeProvider]Samples.Fsharp.InfoProvider.
BaseType2.
Program::get_t()
IL_001c: ldr "F1"
IL_0021: call void
[ShareInfoSampleTypeProvider]Samples.Fsharp.InfoProvider.InsertFunctions::LogBeforeEx
ecution(class [ShareInfoSampleTypeProvider]Samples.Fsharp.InfoProvider.BaseType2,
string)
IL_0026: call class [ShareInfoSampleTypeProvider]Samples.Fsharp.InfoProvider.BaseType2
Program::get_t()
IL_002b: ldr "hello"
IL_0030: call void
[ShareInfoSampleTypeProvider]Samples.Fsharp.InfoProvider.InsertFunctions::LogBeforeution


ution(class [ShareInfoInfoTypeProvider]Samples.Fsharp.InfoProvider.
BaseType2
Program::get_t()
IL_003a: ldr "F1"
IL_003f: call void
[ShareInfoSampleTypeProvider]Samples.Fsharp.InfoProvider.InsertFunctions::LogAfterEx
ution(class[ShareInfoSampleTypeProvider]Samples.Fsharp.InfoProvider.BaseType2,
string)
IL_0044: call class [ShareInfoSampleTypeProvider]Samples.Fsharp.InfoProvider.
BaseType2
Program::get_t()
IL_0049: ldr "F2"
```
