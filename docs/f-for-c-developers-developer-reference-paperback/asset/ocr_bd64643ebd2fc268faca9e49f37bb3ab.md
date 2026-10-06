The type-provider API also provides a way to decorate a property with an attribute. Listing 5-52 shows how to add an attribute to a property and how to generate the type that is returned from the DefineStaticParameters function.

# LISTING 5-52 Adding an attribute to a generated property

```
namespace Samples.FSharp.TypeProviderTemplate

open System.Reflection
open Microsoft.FSharp.Core.CompilerServices
open Samples.FSharp.ProvidedTypes

type MyAttribute() =
    inherit System.Attribute()

[<Provider>
type public TypeProvider1() as =
    inherit TypeProviderForNamespaces())

// Get the assembly and namespace used to house the provided types
let thisAssembly = Assembly.GetExecutingAssembly()"C:\TypeCode\tt.dll"
let rootNamespace = "Samples.Info.TPTest"
let baseType = typeof<obj>

let newT = ProvidedTypeDefinition(thisAssembly, rootNamespace, "TPTest", baseType)
let assembly = ProvidedAssembly()
let data = ProvidedStaticParameter("filename", typeof<string>)
doT.DefineStaticParameters(
    data,
    fun typeName [:]? string as data [] ->
        let ty = ProvidedTypeDefinition(
            thisAssembly,
            rootNamespace,
            typeName,
            Some(typeof<obj>))
        ty.AddMember(ProvidedConstructor([], InvokeCode = fun -> <<@obj @>>)
        let p = ProvidedProperty(data, typeof<string>,
            p.AddAttribute(typeofOfMyAttribute))
            Getter = [me] -> <<@data @>>)
        ty.AddMember(p)

tyy.IsErased <- false
tyy.SuppressRelocation <- false
assembly.AddTypes [ty])
```
```

278 PART II F#'s Unique Features