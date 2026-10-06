# LISTING 5-16 Sample file

| Distance (metre),Time (second) |
| 50,3.73 |
| 100,4.22 |
| 150,7.3 |

The type information is stored in the first line of the CSV file. Each row, except the first row, also needs a type to hold all of the fields. ProvidedMeasureBuilder is needed when creating unit-of-measure types. Listing 5-17 shows how to create kg, meter, and kg/m².

# LISTING 5-17 Creating unit-of-measure types in provider

```
let measures = ProvidedMeasureBuilder.Default

// make the kilogram and meter
let kg = measures.SI "Kilogram"
let m = measures.SI "Meter"

// make float<kg> type
let float_kg = measures.AnnotateType(typeof<float>,[kg])

// make float<m> type
let kgm2 = measures.Ratio(kg, measures.Square)

// make float<kg/m> type
let dkgm2 = measures.AnnotateType(typeof<float>,[kgm2])

// make Nullable<float<kg/m>> type
let nullableDecimal1_kgm2 = typeof(System.Nullable<>).MakeGenericType([dkgm2]) |
```

Referencing a local file is easy as long as the user gets the correct file path. A relative path is preferred, TypeProviderConfig being used. The instance of a provider can take an instance of a named TypeProviderConfig during construction, which contains the resolution folder for the type provider, the list of referenced assemblies, and other information. Listing 5-18 shows how to use the TypeProviderConfig value.

# LISTING 5-18 Using the TypeProviderConfig value to get a resolution path

```
<TypeProvider>
type public CsvProvider(cfg:TypeProviderConfig) as this =
    inherit TypeProviderForNamespaces()
...

// Resolve the filename relative to the resolution folder.
let resolvedFilename = System.Path.Combine(cfg.ResolutionFolder, filename)
```

234 PART II F#'s Unique Features