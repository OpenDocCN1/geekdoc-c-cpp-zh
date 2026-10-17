
*(注：原文后部分存在大量 OCR 识别错误和重复，已在翻译中保留核心逻辑结构。)*

# 对象表达式 (Object Expressions)

你可以使用*对象表达式*来实例化接口：

```
let aud2000 =
    new ICar with
        member this.Name = "Audi"
        member this.Year = 2000
```

对象表达式用于动态实现接口。任何给定的表达式必须为所有接口成员提供实现方案：

```
let bmw525i2004 =
    new ICarModel with
        member this.Name = "BMW"
        member this.Year = 2004
        member this.Model = "525i"
```

你也可以定义实现接口的新类，数量随你意愿：

```
type Citroen(model: string, year: int) =
    interface ICar with
        member this.Name = "Citroen"
        member this.Year = year
        member this.Model = model
```

# 对象 (Objects)

普通类可以使用其构造函数和可选的*new* 关键字来实例化。

```
let aud2000 = Car("Audi", 2000)
let bmw525i2004 = new BMW("525i", 2004)
```

# 通过绑定对象状态 (Object State via Binding)

既然你已经学会了如何定义类和接口、对象表达式的工作，并且你可以实例化它们来创建对象，这里有一些额外的细节需要注意。

首先，你可以使用类定义中的*let* 绑定为对象添加构造时状态：

```
type Rectangle(height, width) =
    let area = height*width
    let diagonal = Math.Sqrt(height**2.0 + width**2.0)
    member this.Area = area
    member this.Diagonal = diagonal
```

这些*let* 绑定类似于类型/构造函数参数，在整个类型定义中可见，并且仅在对象构造时计算一次。它们需要放置在成员之前；否则将得到编译器错误。

# 对象初始化 (Object Initialization)

你还可以使用 `do` 关键字为类添加初始化代码。这些代码可以添加到 `let` 绑定之前或。通常，你可以使用初始化代码来检查构造对象时必须满足的各种约束。这里有一个拒绝构造负数维度矩形的示例：

```
type Rectangle2(height, width) =
    do if height < 0. || width < 0. then
        failwith("Can't construct rectangle with negative dimensions")
    let area = height*width
    let diagonal = Math.Sqrt(height**2.0 + width**2.0)
    member this.Area = area
    member this.Diagonal = diagonal
```

# Setter 和 Get器 (Setters and Getters)

在之前所有的类示例中，你定义的属性都是只读的。另一种编写这些属性的方法是显式地使用 getter：

```
...
member this.Area with get () = area
```

由于默认没有定义 setter，如果你尝试设置它们，将得到错误：

```
let r2 = Rectangle2(100,100)
r2.Area <- 100
// Error
```

添加 setter 是简单的，它通常与 getter 一起出现（除非你只需要一个 setter）：

```
type Rectangle2(height, width) =
    let mutable colorCode = 0
    ...
member this.ColorCode
    with get () = colorCode
    and set cc = colorCode <- cc
```

# 索引器 (Indexers)

你可以以 `object.[index]` 和 `object.[index] <- expr` 的形式为对象添加点符号。这些索引器属性是接受参数的特殊属性，可以像之前所示通过 getter 和 setter 定义为名为 `Item` 的特殊属性。

例如，你可能想要提供一种通过索引（从零开始）读取多边形中坐标的机制。你可以通过创建一个 `Polygon` 类来实现：

```
type Polygon(coords:int list) =
    ...
member self.Item
    with get idx =
        if Seq.length <= idx then
            Seq.nth idx
        else
            failwith("Index of bound")
```

你可以在 F# Interactive 中测试索引器属性：

```
> let p = new Polygon([1;2;3;4;5;6;7]);
> p.[2]
unit
```

# 命名和可选参数 (Named and Optional Arguments)

你可以通过命名参数和设置属性来让你的代码更具可读性。例如，你可以这样构造一个新的矩形：

```
let r2 = Rectangle(height=100., width=100., ColorCode=5)
```

你可以验证这种初始化是否正确：

```
> r2.ColorCode;
val it : int = 5
> r2.Area;
val it : float = 100.0
> r2.Diagonal;
val it : float = 141.42...
```

你还可以为构造函数添加可选参数：

```
type Circle(radius, y, ?color) =
    let setColor =
        match color with
        | None ->
        | Some c -> c
    member self.Everything = (radius, y)
```

在这里，`?color` 定义了 Circle 的可选参数。它被建模为接收一个 option 值，作为对象初始化的一部分进行赋值。你可以在 F# Interactive 中测试：

```
> let c1 = new Circle(radius=10, x=5, y=5);
val c1 : Circle
> let c2 = new Circle(10, 5, 5);
val c2 : Circle
> c1.Everything;
val it : int * int = (10, 5)
> c2.Everything;
val it : int * int = (10, 5)
```

# 匿名函数 (Anonymous Functions)

你可以创建一个匿名函数（C# 中的 lambda 表达式），即使用 `fun` 关键字列出形式参数和函数体：

```
fun x y -> Math.Sqrt(x + y)
```

你可以通过将其绑定到名称来命名函数：

```
let diag = fun x y -> Math.Sqrt(x + y)
```

这等同于：

```
let diag x y = Math.Sqrt(x + y)
```

如果你需要一个匹配其单一参数（你将在本节通过模式匹配学习），可以使用 `function` 关键字：

```
let onlyOne = function 1 -> 0
```

这定义了一个接收整数的函数，如果是1 则返回 1，否则返回 0。按照约定，每个模式匹配以管道符号 (`|`) 开始，第一个情况。

函数值可以从其他函数传递或返回。匿名函数特别有用的应用是编写延续（continuations），也称为延续风格（CPS）。你将在本节处理异步编程时遇到延续，其中表达式的评估是通过注册回调函数完成的（即一个接收计算值并继续处理结果的延续）。

关于显式延续的示例，考虑一个评估器的 CPS 版本（更多内容将在本节稍后的判别联合章节中）：

```
type Expr =
    | Number of float
    | Binop of (float -> float -> float) * Expr * Expr

static member Add (e1, e2) = Binop (+), e1, e2
static member Sub (e1, e2) = Binop (-), e1, e2
static member Mul (e1, e2) = Binop (*), e1, e2
static member Prod (e1, e2) = Binop (/), e1, e2

let rec Eval cont =
    match e with
    | Number n ->
        cont n
    | Binop (f, e1, e2) ->
        Eval (fun i1 ->
            Eval e2 (fun i2 ->
                f i1 i2 cont))
```

`Eval` 函数接收一个表达式和一个接收表达式结果的显式延续。当表达式是一个数字时，你只需将其传递给延续。如果表达式是一个二进制运算，你用一个评估第二个操作数的延续函数来评估第一个操作数，该函数本身获得一个接收两个评估结果的延续，对它们应用二进制运算，并将整体结果传递给原始延续。

CPS 是一种常见的函数模式，用于在不同表示之间进行转换或遍历数据类型。

# 使用元组 (Using Tuples)

元组是一种基础函数数据结构，这也是 F# 开发的标志。它们是一种多功能数据类型，NET 4.0 最终将其作为系统类型 `System.Tuple` 引入，受 F# 的开创和启发。

元组也被称为积类型（product types），因为它们构成了各个部分的笛卡尔积，而且在理论上，它们用星号表示（例如 `T1*T2*T3`）。正如你之前看到的，在 F# 类型签名中，元组用星号标记（例如 `T1*T2*T3`）。

你可以通过逗号连接值来构造元组：

- 1, "my string", 3

通常，你必须使用括号来避免优先级错误——例如，当你像在本节开头那样调用接收元组参数的函数时：

```
(1, "my string", 3) | MyFunction
```

在这里，函数调用（或管道运算符）的优先级高于逗号，如果不加括号，它将仅应用于元组中的值。

元组也被称为 n 元组（对于任意 n），元组分组了 n 个独立的值。你可以在元组中嵌套元组，因此以下是不同的值：

```
(1, "my string", 3)
(1, ("my string", 3))
((1, "my string"), 3)
```

你可以使用模式匹配来解构元组，你将在本节稍后看到。F# 还提供了一些处理元对的实用函数：

```
> fst (1, 2);
val it : int = 1
> snd (1, 2);
val it : int = 2
```

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
