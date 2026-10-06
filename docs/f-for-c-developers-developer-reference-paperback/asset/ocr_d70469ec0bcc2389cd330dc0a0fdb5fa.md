let regexY = ProvidedTypeDefinition(thisAssembly, rootNamespace, "TPestType", Some baseTy),

```
let f1 = ProvidedMethod(
    methodName = "F1",
    parameters = [ProvidedParameter("input", typeof<string>)],\n    returnType = typeof(unit),
    IsStaticMethod = false,
    InvokeCode = fun args -> <<%(args.[0]:BaseType2).X <<%(args.[1])>> @)>>
)
```

```
let f2 = ProvidedMethod(
    methodName = "F2",
    parameters = [],
    returnType = typeof<string>,
    IsStaticMethod = false,
    InvokeCode = fun args -> <<%(args.[0]:BaseType2).X <<)>>
)
```

```
// constructor needs to return the BaseType2 instance
let ctor = ProvidedConstructor(
    parameters = [],
    InvokeCode = fun args -> <<BaseType2() @>>)
```

```
do
    regex.AddMember ctor
    regex.AddMember f1
    regex.AddMember f2

do this.AddNamespace(rootNamespace, [regex])
```

[<TypeProviderAssembly>] ()

LISTING 5-25 Test script for the TPType provider sharing information between methods

```
# r "\bin\Debug\ShareInfoSampleProvider.dll"

type T = Samples.ShareInfo.TPest.TPTestType
let t = T()
t.F1("hello")
let a = t.F2())

printf "%A" a // the print result is hello
```

Because the provided type is based on BaseType2 and because the constructor returns an instance of BaseType2, the variable t is of type BaseType2.