TestScript.fx* × TypeProviderL1

```
# @"\Fsharp.Debug\RegularExpressionProvider
type T = Samples.ShareInfo.TPTest.RegularExpr
let t = T()
t.Match("425-123-4567")
t.Match("425-123-4567")

```

TestScript.fx* × TypeProviderL1

```
# @"\Fsharp.Debug\RegularExpressionProvider
type T = Samples.ShareInfo.TPTest.RegularExpr
let t = T()
t.Match("425-123-4567")
t.Match("425-123-4567")

```

![](bbox=[0.318, 0.142, 0.753, 0.258])

FIGURE 5-5 IntelliSense affected by the base type; Match is used as the type in the image on the right

LISTING 5-14 Completing the regular-expression type-provider

```
// Learn about F# at http://fsharp.net
// See the "F# Tutorial" project for more help.
namespace Samples.FSharp.RegularExpressionProvider
open System.Reflection
open Microsoft.FSharp.Core.CompilerServices
open Samples.FSharp.ProvidedTypes

<TypeProvider>
type public TypeProvider1() as this =
inherit TypeProviderForNamespaces()

    // Get the base assembly and namespaces used to house the provided types
let thisAssembly = Assembly.ExecutingAssembly()
let rootNamespace = "Samples.ShareInfo.TPTest"
let baseTy = typeof<'T>

let newT = ProvidedTypeDefinition(thisAssembly, rootNamespace,
"RegularExpressionProvider", Some baseTy)

let staticParams = [ProvidedStaticParameter("pattern", typeof<string>)]
dow.DefineStaticParameters(
    parameters-staticParams,
instantiationFunction=(Fun projectName parameterValues ->
match parameterValues
| [ ? string as pattern] ->
    let ty = ProvidedTypeDefinition(
        thisAssembly,
        rootNamespace,
        typeName,
        Some baseTy,
        HideObjectMethods = true))
let r = System.Text.RegularExpressions.Regex(pattern)

```

CHAPTER 5 Write Your Own Type Provider 231