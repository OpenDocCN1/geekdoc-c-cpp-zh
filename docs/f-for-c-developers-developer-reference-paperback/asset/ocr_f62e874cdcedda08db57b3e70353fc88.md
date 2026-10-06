```
fun args ->
  (%args.[0]:obj)
  ?:System.Text.RegularExpressions.Regex
    .Match(%args.[1])
  =>obj
  @@

  ty.AddMember(matchMethod)

  ty.AddMember(matchTy)

  ty
))

do this.AddNamespace(rootNamespace, [newT])
```

<ProviderAssembly>

()

# Using the CSV Type Provider

The regular-expression type provider uses a static parameter to provide the type information. The static parameter can also point to a file that contains the type information. The current implementation allows a user to generate only .NET 1x-compatible types. One exception is unit-of-measure types. Type providers do support the generation of unit-of-measure types. The CSV type provider demonstrates how to get type information from a local CSV file and how to generate unit-of-measure types.

As with the previous examples, the first step is to design how the API should look for the end user (See Listing 5-15). The sample CSV file is shown in Listing 5-16.

LISTING 5-15 CSV type-provider test script

```
#r @\.bin\CSVTypeProvider.dll"

type T = Samples.ShareInfo.TPTest.CSVTypeProvider<File1.csv>"
let t = T()
for row in t.Data do
    let time = row.Time
    printf "%f" (float time)
```