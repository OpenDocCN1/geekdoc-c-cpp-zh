```
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
|> Seq.map(fun m ->let methodName = m.Name
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
[baseExpression];Expr;
Value(methodName) ])

let invokeExpr = Expr.Call(baseExpression, mi, args.
tail)
let logAfterExpr = Expr.Call(
typeof<LoggingFunctions>
.Method("LogAfterExecution",
[baseExpression];Expr.
)
Value(methodName)])

Expr.Sequential(
logExpr,
Expr.Sequential(invokeExpr, logAfterExpr)
)

let ctor = ProvidedConstructor(
parameters = [],
InvokeCode = fun args -> <<@ BaseType2() <<@)
```

CHAPTER 5 Write Your Own Type Provider 249