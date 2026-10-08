

# 辨别联合 (Discriminated Unions)

辨别联合（或称为标记联合）是代数数据类型的一种，可以取自预定义的一组形状。在代码中使用辨别联合的一个直接优势是，编译器可以检查你在操作这些形状时是否处理了所有可能的形状，正如你稍后在模式匹配中将看到的那样。**然而**，从根本上说，更重要的优势是它们为其所承载的值提供了类型安全的访问，这与你之前遇到的 C 风格联合体不同。辨别联合在函数式编程中是重要的抽象，因为它们将值空间划分为一组形状，使得处理这些值变得更容易且在概念上更清晰。

考虑以下示例：

```
type Expr =
  Num of float
  Var of string
  UnOp of (float -> float) * Expr
  BinOp of (float -> float -> float) * Expr * Expr
  static Member Add (el, e2) = BinOp (+), e2)
  static Member Sub (el, e2) = BinOp (-), e2)
  static Member Mul (el, e2) = BinOp (*), e2)
  static Member Div (el, e2) = BinOp ( /), e2)
  static Member Sin (el) = UnOp (Math.Sin, el)
  static Member Cos (el) = UnOp (Math.Cos, el)
```

在这里，你创建了一个辨别联合来表示具有四种基本形状的数学表达式：数字、变量和二运算。为了方便构造这种类型的（表达式），你还添加了一些成员来表示基本的算术运算、正弦和余弦。你也可以添加任意数量的成员以表示相同的方式。

现在你可以轻松地构造数学表达式了。考虑以下代表 cos(x+y) 的内容：

```
let num = Expr.Cos (Expr.Add (Expr.Var "x", Expr.Num Math.PI)
```

注意，你使用了类型名来限定基本形状（Var 和 Num）的出现——只要该类型本身在作用范围内，这是不是要求的。但是，因为你可能在不同的联合中具有相同名称的案例，因此使用适当的类型名对其进行限定是一个良好的习惯。

你可以使用模式匹配来检查联合值（以及其他值）——模式匹配是一种通过模式解构并绑定值的机制。你将在本章后面学习更多关于模式匹配的知识，作为预览，这里有一个评估你的类型表达式的函数：

```
let rec Eval (env: Map<string, float>) = function
  Num num ->
    num
  Var v ->
    env.[v]
```

```
| UnOp (op, e) ->
  op (Eval env e)
| BinOp (op, e1, e2) ->
  op (Eval env e1) (Eval env e2)
```

你可以在 F# Interactive 中运行这个评估器并双重检查它是否正常工作：

```
> let env = ["x", 1.0] | Map.OfList;

val env : Map<string, float>

> Eval env num;
  val it : float = -0.5403023059
> Math.Cos (l + Math.PI);
  val it : float = -0.5403023059
>
```

# 使用 Option

Option 值是“可空”（nullables）概念的泛化——即，表示某个类型 τ 的值给出或未给出。与 .NET 的 Nullable<T> 类型的一个主要区别是，F# options 可以用于任何任意类型，而不仅仅是值类型。正如你预期的那样，options 用辨别联合来实现。事实上，这就是 F# 标准库中的实现方式：

```
type Option<T> =
  Some of 'T
  None
```

你还会在标准库中发现该类型的类型别名（简单地定义为小写类型），而且事实上，这就是你将在 F# 代码中将看到的类型：

```
type 'T option = Option<'T>
```

Option 值在使 F# 编程更安全方面起着重要作用。命令式语言的缺点之一是，它们严重依赖 null 来表示某些计算继续进行，或者结果未定义。事实上，.NET 标准库中有许多函数在特定情况下返回 null。

考虑以下文件扩展名 fileName：

```f
let FileExtension fileName =
  if fileName > String.IsNullOrEmptyOrEmpty | not then
    fileName.LastIndexOfOf('.')
  | function
      n when n < 1 ->
        None
      idx ->
        fileName.Substring
        | Some
  else
    None
```

此函数从文件名参数作为 option 返回文件扩展名。只有当文件名包含一个点（.）时它才会成功，然后它将从点之后的部分作为 Some 值返回。在所有其他情况下，它将返回 None。一些 F# Interactive 的探索有助于测试这一点：

```
> FileExtension "data";
val it : string option = None
> FileExtension "data.";
val it : string option = Some "*"
> FileExtension "data.dat";
val it : string option = Some "*.dat"
> FileExtension "*";
val it : string option = None
> FileExtension null;
val it : string option = None
>
```

# 使用记录 (Records)

你可以通过在大括号内列出字段和类型来定义记录类型：

```fsharp
type Person =
  { FirstName: string
  LastName: string
  Age: int
  Children: Person list
  mutable LastSeen: System.DateTime option }
```

你只需要在大括号内提供字段的值创建一个新的记录值：

```fsharp
let john =
  { FirstName = "John"
  LastName = "Smith"
  Age = 32
  Children = []
  LastSeen = None }
```

在定义和值构造函数中，字段可以用分号分隔——当你想要把多个字段放在同一行时，这非常有用。

有时，你可能需要复制记录来创建新的记录，可能更改某些字段：

```fsharp
let sally =
  { john with
  FirstName = "Sally"
  Age = 25 }
```

需要记住的一个重要点是，记录不是值类型。将其中一个字段切换为 mutable 将暴露这一点：

```fsharp
let shadowOfSally = sally
```

现在，在 F# Interactive 中，你可以实验更新 shadowOfSally 会发生什么：

```
> shadowOfSally.LastSeen <- Some System.DateTime.Now;
val it : unit = ()
> sally;
val it : Person =
  {FirstName = "Sally";
  LastName = "Smith";
  Age = 25;
  Children = [];
  LastSeen = Some 2023-10-27 ...}
```

列表

考虑以下：

```fsharp
let a = List.empty
let b = []
let c = 1 :: 2 :: 3 :: 4
let d = [1; 2; 3; 4]
```

```
val a : 'a list
val b : 'a list
val c : int list = 1 :: 2 :: 3 :: 4
val d : int list = [1; 2; 3; 4]
``` 

在这里，a 和 b 包含空列表，具有泛型；c 和 d 也是，具有 1, 2, 3, 4 元素。

你可以使用 List.iter 遍历（迭代）列表，给出一个接收元素且不返回内容的函数（即类型为 T -> unit 的函数）和一个你想遍历的列表（类型为 T list）：

```
> List.iter(printf "Printing a number: %d" c);

Printing a number: 1
Printing a number: 2
Printing a number: 3
Printing a number: 4
val it : unit = ()
```

# 表 25-10：语言结构

| 表达式 | 描述 | 示例 |
| --- | --- | --- |
| [ ] | 空列表。 | [ ] |
| expr :: expr | 在列表头部添加元素（cons）。 | 1 :: [ 2; 3 ] |
| [ expr; .. expr ] | 带有元素的列表。 | [ 1; 2; 3 ] |
| [ expr .. expr ] | 数字范围。 | [ 1 .. 100 ], [ 1.0 .. 100.0 ] |
| [ expr .. expr .. expr ] | 使用步进值的数字范围。 | [ 0 .. 2 .. 100 ] |
| expr @ expr | 列表合并。 | [ 1; 2 ] @ [ 3; 4 ] |
| [ for x in list -> expr ] | 列表推导式。 | [ for x in 1 .. 100 -> x*x ] |
