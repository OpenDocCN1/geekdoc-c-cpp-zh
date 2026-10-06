# LISTING 9-22 Code structure hosts intermediate functions

```
type Code() =
  inherit System.Collections.Generic.List<string> =
  let mutable functionID = 0
  let mutable variableID = 0
  member.functionID
    with get () = functionID
    and set (v) = functionID <- v
  member.variableID
    with get () = variableID
    and set(v) = variableID <- v
  member.IncreaseFunctionID() =
    functionID <- this.FunctionID + 1
  member.IncreaseVariableID() =
    variableID <- this.VariableID + 1

  member.ToString() =
    #include "CUDALibrary.h" + String.Join("\r\n", this) + "\r\n\r\n\r\n")
```

```
let code = Code()
```

![](bbox=[0.105, 0.435, 0.138, 0.468])

> Note The CUDALibrary.h file is a placeholder file. In this sample, the file content is empty. You can implement additional functions in this file to make the translation easier and the code more readable.

Listing 9-23 shows several functions used to handle the function definitions, including return type and function signatures, in F# and convert them to CUDA code.

# LISTING 9-23 Functions for finding the return type and signature

```
open System
open System.Reflection
open Microsoft.Fsharp.Quotations
open Microsoft.Fsharp.Quotations.Patterns
open Microsoft.Fsharp.Quotations.DerivedPatterns
open Microsoft.Fsharp.Quotations.ExprShape

let rec getFunctionBody(exp:Expr) =
  match exp with
  | DerivedPatterns.Lambdas(c, callPattern) ->
    match callPattern
      | Patterns.Call(e, mi, exprList) ->
        match mi with
          | DerivedPatterns.MethodWithReflectedDefinition ->
            callPattern
```