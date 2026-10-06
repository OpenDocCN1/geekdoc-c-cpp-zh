
```fsharp
// set the transition function
member this.SetFunction(name:string, state:IState) =
if functions.ContainsKey(name) then
    functions.[name] <- state
else
    functions.Add(name, state);
```

```fsharp
// invoke the Exit function
member private this.InvokeExit(name:string) =
if functions.ContainsKey(name) then
    Functions.[name].ExitFunction()
```

```fsharp
// invoke the Enter function
member private this.InvokeEnter(name:string) =
if functions.ContainsKey(name) then
    Functions.[name].EnterFunction()
```

The type-provider implementation uses the StateMachine type as a base class. It generates the transition function TransitTo<target name> and the assert function Assert<node name>. Because it is easy to make a type when specifying the state name, I choose to generate the state name as a read-only property. SetFunction is not generated from the type provider; it is a function defined on the StateMachine class. The code is shown in Listing 5-44.

## LISTING 5-44 DGML type provider code

```fsharp
namespace Samples.FSharp.TypeProviderTemplate

open System.Reflection
open Microsoft.FSharp.Core.Compiler
open Samples.FSharp.ProvidedTypes
```

```fsharp
open StateMachineTypeProvider

[<DataProvider>
type public TypeProvider1() as this =
inherit TypeProviderForNamespaces()
```

```fsharp
// Get the assembly and namespace used to house the provided types
let assembly = Assembly.GetExecutingAssembly()
let rootNamespace = "Samples.ShareInfo.TPTest"
let baseType = typeof<StateMachine>
```

```fsharp
let newT = ProvidedTypeDefinition(assembly, rootNamespace, "TPTestType", Some baseType);
```

```fsharp
// define two static parameters: one is the DGML file name
// the other is the initial state
let staticParams = [ProvidedStaticParameter("dgml file name", typeof<string>);
ProvidedStaticParameter("init state", typeof<string>)];
```

```fsharp
do newT.DefineStaticParameters(
  parameters=staticParams,
  instantiationFunction=(fun type parameterValues ->
  let ty = ProvidedTypeDefinition(
    thisAssembly,
    rootNamespace,
    typeName,
    baseType = Some baseTy)
```

```fsharp
let ddml, initState = parameterValues.[0] :? string, parameterValues.[1]:?> string
```

```fsharp
// generate a new StateMachine instance to generate the read-only properties
let stateMachine = StateMachine()
stateMachine.Init(dml, initState)
```

```fsharp
let stateProperties =
  stateMachine.Nodes
  |> Seq.map (fun n ->
  let name = n.Name
  let prop1 = ProvidedProperty(propertyName = n.Name,
    propertyType = typeof<string>,
    IsStatic=false,
    GetterCode=... )
```

```fsharp
stateProperties
|> Seq.iter.AddMember
```

```fsharp
// generate the assert functions
alerts =
  stateMachine.Nodes
  |> Seq.map (fun n ->
  let name = n.Name
  let assertFunction =
    TestMethod=sprintf "Assert_%s" name,
    parameters=[],
    returnType=typeof<unit>,
    IsStaticMethod=false,
    InvokeCode=fun args -> @@(%s.Args[0] : StateMachine).assertFunction)
```

```fsharp
Assert(name) @@@
alerts
|> Seq.iter.AddMember
```

```fsharp
// generate the transition functions
let transits =
  stateMachine.Nodes
  |> Seq.map (fun node ->
  let name = node.Name
```

```fsharp
let m = ProvidedMethod(
  methodName = sprintf "TransitTo_%s" name,
  parameters = [],
  returnType = typeof<unit>,
  IsStaticMethod = false,
  InvokeCode = fun args ->
  <%@args.[0] : StateMachine>
)
```

```fsharp
TransitTo(name)
transits
| Seq.iter.AddMember
```

```fsharp
let setFunction =
  ProvidedMethod(
    methodName = "SetFunction",
    parameters = [ProvidedParameter("name", typeof<string>);
    ProvidedParameter("state class", typeof<IState>)],
    returnType = typeof<unit>,
    IsStaticMethod = false,
    InvokeCode = fun args ->
    <%args.[0] : StateMachine> :
    SetFunction(%args.[1] : string, IState))
```

```fsharp
ty.AddMember(setFunction)
```

```fsharp
// define the constructor
let ctor = ProvidedConstructor(
  parameters = [],
  InvokeCode = fun args -> <@StateMachine(dgm), initState()) <@
ty.AddMember(ctor)
ty.AddXmlDoc "xml comment"
ty))
```

```fsharp
this.AddNamespace(rootNamespace, [newT])
```

```fsharp
[<TypeProviderAssembly>]
do ()
```

Note: The type provider does not erase the type to System.Object anymore; therefore, IntelliSense shows a full list of members from the base class. In the sample, SetFunction is visible in the IntelliSense drop-down list.

This sample shows a way to enhance the experience of working with a DGML file using a general-purpose library. The type provider can customize the property according to a specific DGML file, and any change on the file will be reflected at compile time.

## Separating Run Time and Design Time

The XML type provider shows how type providers handle design-time logic and run-time logic. Actually, design-time logic and run-time logic can be separated into different assemblies. The design-time DLL only provides design-time logic, it also inserts extra logic. Listing 45 shows the run-time DLL. Note: The run-time DLL and type-provider DLL should be located in the same folder. The sample shows two projects. One is for run-time assembly, and the other is design-time provider code. The structure of the solution is shown in Figure 5-9.

**FIGURE 5-9** Type-provider solution separating run time and design time into assemblies

**LISTING 45** Run-time logic for the type provider in Library project

```fsharp
namespace Samples.TypeSpace.Runtime

type ObjectBase() =
    member x.Kind = "in an object"

type ObjectRepresentation(contents:string) =
    inherit ObjectBase()
    member x.Contents = contents

type RuntimeMethods() =
    static member Create(s:string) = ObjectRepresentation(s + " hello!")
    static member GetContents(s:ObjectBase) = (s:ObjectRepresentation).contents
```

This declaration points the compiler to the right design-time DLL for the selected runtime DLL. The type provider will generate an assembly named DesignTimeSeparation. The design-time type-provider code is listed in Listing 46. It generates class members to invoke the functions present in Listing 45.

```fsharp
namespace Samples.FSharp.DesignTimeSeparation

open System.Reflection
open Microsoft.FSharp.Core.CompilerServices
open Samples.FSharp.ProvidedTypes
open Microsoft.FSharp.Quotations

[<TypeProvider>]
type public TypeProvider1(config: TypeProviderConfig) as this =
    inherit TypeProviderForNamespaces()
    let asem = config.RuntimeAssembly
    let runtimeAssembly = System.Reflection.Assembly.ReflectionOnlyLoad(asem)

    let objectBase = runtimeAssembly.GetType("TypeSpace.Runtime.ObjectBase")
    let runtimeMethods = runtimeAssembly.GetType("TypeSpace.Runtime.Methods")
    let createMethod = runtimeMethods.GetMethod("Create")
    let getContentsMethod = runtimeMethods.GetMethod("GetContents")

    // Get the assembly and namespace used to house the provided types
    let rootNamespace = "Samples.ShareInfo.TPTest"
    let baseTy = objectBase

    let newT = ProvidedTypeDefinition(runtimeAssembly, rootNamespace, "TPTest", Some baseTy)

    let ctor = ProvidedConstructor([ProvidedParameter("Contents", typeof<string>);
        InvokeCode = (fun args -> Expr.Call(createMethod, [args.[0])))

    // This is a property. At runtime, the property just gets the string value
    let prop2 = ProvidedProperty(
        "Property2",
        typeof<string>,
        GetterCode= fun args -> Expr.Call(getContentsMethod, [args.[0]]))

    do prop2.AddMemberDelayed(fun () -> "xml comment")
    do newT.AddMember(prop2)
    do newT.AddMember(ctor)
    do this.AddNamespace(rootNamespace, [newT])

[<TypeProviderAssembly>]
do ()
```

Invoking the type provider, as shown in Listing 5-47, is similar to the other example. The reference part is the main difference. In the other examples, there is only one assembly, but now there are assemblies. The run-time DLL is what our type code needs to reference in order to use this type provider.

## LISTING 5-47** Invoking the type provider

```fsharp
# r "@.\binDebug\Library1.dll"

type T = Samples.ShareInfo.TPTest.TPTestType
let t = T("AA")
let c = t.Kind
let d = t.Property2
```

## Generated Type Provider

The last example in this chapter is a generated type provider. The generated type provider behaves like a code generator. It does not support lazy type generation like an erased type provider does. However, there are several advantages to using a generated type provider versus an erased type provider. The generated type provider generates an assembly that can be used from other language. Because the generated assembly is present, you can use .NET reflection to retrieve type information. I'll start by showing how to write a generated type provider. The code needed to create a generated type provider, which is shown in Listing 5-48, is similar to the erased version except that a new ProvidedAssembly class is created. Let's start from a simple HelloWorld type-provider project, TypeProviderTemplate, which is created from the TypeProvider template. If you compare Listing 5-48 and Listing 5-7, there are a few differences. In an assembly whose type is ProvidedAssembly, The ProvidedType newT needs to set its IsParsed and SuppressRelocation properties to false before it can be added to ProvidedAssembly.
