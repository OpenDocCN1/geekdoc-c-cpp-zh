

```fsharp
// 传递给 typeofFun 的函数
let f = fun (t:System.Type) -> t.Name
```

```fsharp
// 获取类型的代码
let intType = typeof<int> | typeof f
let tupleType = typeof<int,float> | typeof f
let funType = typeof<string> | typeof f
let funType2 = typeof<string->float32> | typeof f
let intOption = typeof<int> | typeof f
let stringList = typeof<string list> | typeof f
```

```fsharp
// 打印结果
[ intype; tupleType; funType; funType2; intOption; stringList; ]
> Seq.iter(printf "%A")
```

执行结果：

Abbreviation([], "System.Int32")
Tuple ([Abbreviation([], "System.Int32"), Abbreviation([], "System.Double")])
Function (Abbreviation([], "System.Int32"),Abbreviation([], "System.String"))
Function
  (Abbreviation([], "System.Int32"),)
  Function (Abbreviation([], "System.String"),Abbreviation([], "System.Single"))
DU ("FSharpOption1",["None"], ["Some"], ["Int32"])
DU ("FSharpList1",["Empty"], ["Cons"], ["String"], ["FSharpList1"])

# 使用代码引用（Code Quotation）

F# 代码引用（code quotation，可以缩写为 quotation）是暴露代码信息的另一种方式——甚至比反射（reflection）提供的信息更多。反射只能提供函数的浅层信息，例如返回类型或参数类型。然而，引用提供的树形结构可以显示函数的实现细节。

你可以选择是否让引用的结果包含类型信息。 列表 6-120 显示了如何声明带类型信息和不带类型信息的引用。`<@>` 用于获取带类型的代码引用，而 `@@@` 用于获取不带类型的代码引用。结果显示 `expr` 是一个 `Expr<int>` 类型，而 `expr2` 是一个 `Expr`（不带类型）。

* 注意

# 列表 6-120 定义一个引用

```fsharp
源代码
open Microsoft.CSharp.Quotations

// 一个带类型的代码引用。
let expr : Expr<float> = <@ 1.2 + 2.4 @>

// 一个未被使用的代码引用。
let expr2 : Expr = <@ 1.2 + 2.4 @@>

执行结果
val expr : Quotations.Expr<int> =
  Call (None, op_Addition, [Value (1), Value (1)])
let expr2 : Quotations.Expr = Call (None, op_Addition, [Value (1), Value (1)])
```

对于复杂的函数，`<@>` 和 `<<>>` 不是获取引用的最方便方法。如果是是的话，你可以像列表 6-121 所示，使用 `ReflectedDefinition` 属性。在 F# 3.0 之前，`ReflectedDefinition` 只能应用于函数上。F# 3.0 现在也支持在模块（module）上使用该属性。如果一个模块装饰了该属性，它的效果就像模块内的所有函数都应用了该属性。

# 列表 6-121 使用 ReflectedDefinition 属性

```fsharp
源代码
[<ReflectedDefinition>]
let ff a b =
  if a then b + 1 else b + 3

let q = <@ ff @>

执行结果
val ff : a:bool -> b:int -> int
val q : Expr<bool -> int -> int> =
  Lambda (a, Lambda (b, Call (None, ff, [a, b])))
```

引用是一个结构，你可以通过递归函数对其进行迭代。列表 6-122 中的函数是一个骨架，可以用于遍历引用树。你可以替换每个用例（case）中的 `()` 来遍历表达式树。如果你想将 F# 代码转换为另一种语言（例如 .NET IL 代码），那么函数函数是一个很好的起点。

```fsharp
let rec iterate exp
match exp with
  | DerivedPatterns.Applications (e, ell) -> ()
  | DerivedPatterns.AndAlsp (e0, el) -> ()
  | DerivedPatterns.Bool e -> ()
  | DerivedPatterns.Byte e -> ()
  | DerivedPatterns.Char e -> ()
  | DerivedPatterns.Double e -> ()
  | DerivedPatterns.Int16 e -> ()
  | DerivedPatterns.Int32 e -> ()
  | DerivedPatterns.Int64 e -> ()
  | DerivedPatterns.OfLife (e0, el) -> ()
  | DerivedPatterns.SByte e -> ()
  | DerivedPatterns.Single e -> ()
  | DerivedPatterns.String e -> ()
  | DerivedPatterns.UInt16 e -> ()
  | DerivedPatterns.UInt32 e -> ()
  | DerivedPatterns.UInt64 e -> ()
  | DerivedPatterns.Unit e -> ()
  | Patterns.AddressOf -> ()
  | Patterns.AddressSet (exp0, exp1) -> ()
  | Patterns.Application (expopt, exp1) -> ()
  | Patterns.Call (exoption, mi) -> ()
  | Patterns.Coerce (t, exp) -> ()
  | Patterns.DefaultValue exp -> ()
  | Patterns.FieldSet (expoption, fi) -> ()
  | Patterns.IntegerFieldLoop (v, e0, el) -> ()
  | Patterns.IfThenElse (cons, exp0) -> ()
  | Patterns.Lambda (var, body) -> ()
  | Patterns.Let (var, exp0) -> ()
  | Patterns.LetRecursive (tuple, exp) -> ()
  | Patterns.NewArray (t, exp) -> ()
  | Patterns.NewObjData (t, var) -> ()
  | Patterns.NewObject (t, exp) -> ()
  | Patterns.NewRecord (t, exp) -> ()
  | Patterns.NewTuple (expl) -> ()
  | Patterns.UnionCase (t, exp) -> ()
  | Patterns.PropertyGroup (expoption, pi) -> ()
```

