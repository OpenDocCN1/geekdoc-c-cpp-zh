# Snippet | Type Providers and Query Write Type Provider |

seProviderAssembly>]

```
type provider define static parameter
type provider provided constructor
type provider provided method
type provider provided property
type provider skeleton
type provider xml comment
```

Figure 5-11 Code snippets for type-provider writing

TABLE 5-1 Code snippets for type-provider writing

| Snippet Name | Description |
| --- | --- |
| Type provider static parameter | Generates skeleton for the DefineStaticParameters function that takes the static parameter. Here is the default code generated: ```nlet staticParams = [ProvidedStaticParameter("pattern", typeof<string>)
do request.DefineStaticParameters(
parameters=staticParams,
instantiationfunctions=fun typename parameterValues ->
let ty = typeDefinition(
this,
rootnamespace,
typename,
baseType = Some baseTy),
ty.AddXmlDoc("xml comment")
``` |
| Type provided constructor | Generates the type-provider constructor. Here is the default code generated: ```
let ctor = [
parameters = [],
InvokeCode = fun args ->
<< ( base class initialization or null*) ()
>>
``` |
| Type provided method | Generates the type-provider method. Here is the default code generated: ```
let m = ProvidedMethod(
methodName = "methodName",
parameters = [].
returnType = typeof<int>,
IsStatic = false,
InvokeCode = fun args ->
<< 0 + 1 <<
)
``` |
| Type provided property | Generates the type-provider property. Here is the default code generated: ```
let prop1 = ProvidedProperty(
propertyName = "Property1",
propertyType = typeof<string>,
IsStatic=false,
GetterCode=(fun args -> << "Hello!" >>),
SetterCode=(fun args -> << printf("setter code") >>)
``` |

280 PART II F#'s Unique Features **