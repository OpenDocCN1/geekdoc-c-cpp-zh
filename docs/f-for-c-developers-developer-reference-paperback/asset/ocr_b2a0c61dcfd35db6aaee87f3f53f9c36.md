```
do
newT.IsErased <- false
newT.SuppressRelocation <- false
this.Addnamespace(rootNamespace, [newT])
assembly.AddTypes([newT])
```

[<TypeProviderAssembly>]\ ()

Listing 5-53 shows the attribute is correctly added to the property.

LISTING 5-53 A test-provided property that has an attribute

```
type T = Samples.ShareInfo.TPest.TPTestType="PropertyA"
let t = T()
printf("propertyA value is %A", t.PropertyA)
let pi = t.GetType().GetProperty("propertyA")
printf("propertyA has attribute %s")
  | pi.GetCustomAttribute(typeof-Samples.FSharp.TypeProviderTemplate4.MyAttribute, true)
  |> Seq.head
  |> fun attribute -> attribute.ToString()
```

ignore <| System.Console.ReadKey()

Execution result
propertyA value is "PropertyA"
propertyA has attribute Samples.FSharp.TypeProviderTemplate4.MyAttribute

# Using Type-Provider Snippets

The F# snippets are designed to make the authoring of a type provider even easier. The snippet project is published at http://fsharpcodes.codeplex.com/ as an open source project. Each provider snippet does not have shortcut support; however, you can press Ctrl+K,X to bring up a list of all snippets, as shown in Figure 5-11. Table 5-1 lists the commonly used code snippets for type-provider authoring.