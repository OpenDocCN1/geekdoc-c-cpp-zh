```
// Try to decompose this header into a name and unit.
let fieldName, fieldType =
let m = Regex.Match(headerText, @"(?<field>.+) \\((?<unit>.+)\)")
if (m.success {
    let fieldName = m.Groups["field"] .Value
    let unitName = m.Groups["unit"] .Value
    let units = ProvidedMeasureBuilder.Default.Si unitName
    let fieldType = ProvidedMeasureBuilder.Default.AnnotateType(typeof<float>,[ts])
    (fieldName, fieldType)
} else {
    // no units, just treat it as a normal float
    headerText, typeof<float>
}
```

```
let fieldProp = ProvidedProperty(fieldName, fieldType,
    GetCode = fun [row][i] -> <<0
```

```
// Add metadata that defines the property's location in the referenced file.
fieldProp.AddDefinitionLocation(1, headers.[i].Index + 1, filename)
rowTy.AddMemberProp
```

```
// Define the property type
let ty = ProvidedTypeDefinition(asm, ns, typeName, Some(typeof<obj>)
```

```
// A parameterless constructor that loads the file that was used to define the
schema.
let ctor0 = ProvidedConstructor([]),
    InvokeCode = fun _ -> <<0>> <<0>>
```

```
// Add a more strongly typed Data property, which uses the existing property at
runtime.
let prop = ProvidedProperty("Data", typeof<seq_>.MakeGenericType(rowTy),
    GetCode = fun _ -> <<0>> CsvFileModule.data
```

```
ty.AddMember prop
ty.AddMember ctor0
```

```
// Add the row type as a nested type.
ty.AddMember rowTy
ty
```

```
// Add the type to the namespace.
do this.AddNamespace(ns, [csTy])
```

```
[<TypeProviderAssembly>]
do ()
```

Note Wrapping the functions in modules helps

# 236 PART II F#'s Unique Features