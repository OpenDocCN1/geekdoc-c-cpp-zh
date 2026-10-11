
```sharp
open Microsoft.FSharp

[<Measure>] type USD

// 定义账户状态
type AccountState =
| Overdrawn
| Silver
| Gold

// 定义操作：存款和取款
type Operation =
| Deposit of decimal<USD>
| Withdraw of decimal<USD>

// 定义账户类
type Account() =
    let mut balance = 0.0m<USD>

    // 定义一个 MailboxProcessor<Operation>(fun inbox ->
    let bank =
        let rec loop () =
            async {
                let! msg = inbox.Receive()
                match msg with
                | Deposit n -> balance <- balance + n
                | Withdraw n -> balance <- balance - n
                return loop ()
            }
        loop ()
    loop ()

    //  MailboxProcessor 实例
    do
        let _ = bank.Start()

    // 定义将消息发送到 MailboxProcessor的操作
    member this.Deposit(args) =
        bank.Post(Deposit(args))
    member this.Withdraw(args) =
        bank.Post(Withdraw(args))

    member this.State =
        get() {
            match balance
            | when balance <= 0.0mUSD -> AccountState.Overdrawn
            | when balance > 0.0mUSD && balance < 10000.mUSD -> AccountState.Silver
            | _ -> AccountState.Gold
        }
    member this.PayInterest() =
        while bank.CurrentQueueLength > 0 {
            System.Threading.Sleep(100)
            printf("current state is %A", this.State)
            match this.State {
                | AccountState.Overdrawn -> this.Deposit(balance * 0.01)
                | AccountState.Gold -> this.Deposit(balance * 0.02)
            }
        }
    member this.ShowBalance() =
        while bank.CurrentQueueLength > 0 {
            System.Threading.Sleep(100)
            printf("current balance is %A", balance)
        }

let account = Account()
account.Deposit(1000.mUSD)
account.Deposit(10000.mUSD)
account.PayInterest()
account.ShowBalance()

FSI 中的执行结果
current state is Gold
current balance is 11220.00M
```

## 使用计算表达式（Computation Expressions）

我在“异步工作流”章节的第 4 章中介绍了 `query` 和 `async`。当你查看 Visual Studio 编辑器窗口中蓝色的 `async` 和 `query` 语法时，你可能会认为它们是关键字，就像 C# 中的 `this` 关键字一样。然而，如果是那样，这些关键字就不能用作变量名。例如，列表 6-93 中的代码是如何编译的？

## 列表 6-93 将 async、seq 和 query 作为变量

```sharp
let async = 0
let seq = 1
let query = 2
```

实际上，代码之所以能够编译，是因为 `async`、`seq` 和 `query` 并不是关键字。相反，它们是一种称为计算表达式（computation expressions）的 F# 特性。MSDN 文档（https://msdn.microsoft.com/en-us/library/dd231832.aspx）对计算表达式给出了很好的定义：

F# 中的计算表达式为编写计算提供了一种方便的语法，可以使用控制流结构和绑定进行排序和绑定。它们可以用于为单子（monads）提供方便的语法，这是一种函数编程特性，用于管理函数式程序中的数据、控制和副作用。

F# 提供了计算表达式以便扩展语言。你之所以可以将代码放在 `seq` 中，是因为它是一个计算表达式。列表 6-94 重新审视了第 1 章讨论过的序列生成代码。

## 列表 6-94 使用引用单元生成序列

```sharp
// 序列生成代码
let indices = [1, 2; 3; 4; 5; 6 ]

let newIndices = seq {
  let currentCell = ref 0
  for a, b in indices
    yield currentCell, a
    yield a, b
    currentCell := b
  yield !currentCell, 100
}

执行结果
> newIndices;
val it : seq<int> = seq [[0, 1); (1, 2); (2, 3); (3, 4); ...]
```

> 注意：此示例代码还演示了如何使用引用单元（reference cell）。在计算表达式中使用可变变量（mutable variable）是无效的。在这种情况下定义可变变量的方法是使用引用单元。

除了对可变变量的限制，计算表达式还有另一个限制。在计算表达式中使用 `base` 是无效的。（参见列表 6-95。）解决方法只是直接使用 `this`。

等等，扩展 .NET 语言似乎是一个令人兴奋的可能性。

## 列表 6-95 在计算表达式中使用 this

```sharp
// 列表 6-95 示例
```

```fsharp
module TestModule =
// 将重试限制设置为 4
let retry = Retry 4

// 计算表达式返回布尔值
let a = retry {
do! (fun () -> printfn "let us try";
    failwith("test failure") // 故意让进程失败
)

printf "result is %A" a
```

## 执行结果

let us try

failed with test failure, 1 times

let us try

failed with test failure, 2 times

let us try

failed with test failure, 3 times

let us try

failed with test failure, 4 times

result is false

计算表达式（computation expression）创建了一个具有自己语言的小区域，并且可能有它自己的执行计算的语言。如果你反复编写相同的代码，计算表达式是一个可以提供极大帮助的东西。

## 使用计算表达式属性 (Using Computation Expression Attributes)

如果 `query` 和 `seq` 都是计算表达式，你可能在好奇 `where` 等其他关键字是如何定义的。它们是通过属性（attributes）定义的。让我们从一个简单的示例开始，`SimpleSequenceBuilder`。列表 6-99 显示了一个简单的序列生成器以及它将被翻译后的代码。这是展示如何像 `where` 一样添加自定义操作起点。

### 列表 6-99 简单序列生成器

```fsharp
// 定义序列生成器类
type SimpleSequence() = class
member this.For(seq<'a>, f:'a -> seq<'b>) =
    seq { for n in source do yield! n }
member this.Yield(n) = seq { yield n }
seq
```

let mySeq = SimpleSequence()

let r = mySeq { for i in 1..10 do yield i * i }

翻译结果

let b = mySeq

b.For ([1..10], fun i -> b.Yield(i * i))

```

`where` 操作是通过 `CustomOperation` 属性引入的，如列表 6-100 所示。第二个参数上的 `ProjectionParameter` 有助于简化函数的定义。缺少此属性，计算表达式中的 `where` 部分必须写成 `fun i -> explicitly`。当自定义操作和 `ForEach` 之间存在 `let` 绑定时（如列表 6-101 所示），`ProjectionParameter` 就非常有用。

### 列表 6-100 使用 CustomOperation 和 ProjectionParameter 属性

```fsharp

type SimpleSequence2() = 

  member.For(source:seq<'a>, f:a -> seq<'b>) =

    seq (n in source yield! f n)

  member.Yield(n) = seq { yield n }

[CustomOperation('where')>=

  member.Where(source:seq<'a>, [ProjectionParameter])f:a -> bool) =

    source | Seq.Filter f

```

```fsharp

let mySeq2 = SimpleSequence2()

let r2 = mySeq2 {

  for i in 1..10 do

    where (i > 3)

}

```

```fsharp

翻译结果

let b2 = mySeq2

b2.Where (b.For([1..10], fun i -> b.Yield(i)), fun i-> i)

```

### 列表 6-101 ProjectParameter 和 let绑定

```fsharp

let r3 = mySeq2 {

  for i in 1..10 do

    let j = i + 3

    where (i > 5 && j < 10)

}

```

```fsharp

翻译结果

let b3 = mySeq2

b3.Where(b.For([1..10], fun i ->

  let j = i + 3

  b.Yield(i, j)),

fun (i, j) -> i > 5 && j < 10)

```

`CustomOperation` 属性中有两个属性。`MaintainsVariableSpace` 属性支持类似于 `where i>5 & j<=10` 的语句，在此处所示：

```fsharp

where (i<5)

where (j<10)

```

示例代码在列表 6-102 中。另一个属性是 `AllowIntoPattern`。正如其名所示，它支持列表 6-103 所示的语法。

### 列表 6-102 CustomOperation 属性中的 MaintainsVariableSpace

```fsharp

type SimpleSequence() {

  member.For(source:seq<'a>, f:'a -> seq<'b'>) =

    seq { for n in source yield! n }

  member.Yield(n) = seq { yield n }

  [CustomOperation("where", MaintainsVariableSpace=true)]

  member.Where(source:seq<'a>, [ProjectionParameter])f:'a -> bool) =

    source | Seq.filter f

```

```fsharp

let mySeq3 = SimpleSequence()

let r4 = mySeq3

  for i in 1..10 do

    let j = i + 3

    where (j > 5)

    where (j < 10)

```

翻译结果
let b4 = mySeq3
b4.Where(
  b4.For([1..10], fun i ->
      let j = i + 3
      b4.Yield(i, j)),
    fun (i, j) -> i > 5,
  fun (i, j) -> j < 10)
```

> 注意上述代码生成了一个警告，可以通过在末尾添加 `| ignore` 来消除该警告。

![](63aaf4e2283ab98ce1c944be8ef6370.png)

### 列表 6-103 CustomOperation 属性中的 AllowIntoPattern

```fsharp
type SimpleSequence() =
  member.For(source:seq<'a>, f:'a -> seq<'b>) =
    seq { for n in source do yield! n }
  member.Yield(n) = seq { yield n }
  [CustomOperation("", AllowIntoPattern=true)]
  member.Where(source:seq<'a>, [ProjectionParameter])f:'a -> bool) =
    source |> Seq.filter f

let mySeq4 = SimpleSequence()
let mySeq4 {
  for i in 1..10 do
    where (i > 5) into j
    where (j < 10)
}
```

翻译结果

let b5 = mySeq4

b5.Where(

  b5.For([1..10], fun i -> b5.Yield(i)),

  fun i -> i > 5,

  fun j -> b5.Yield(j)

) j < 10)

> 注意上述代码生成了一个警告，可以通过在末尾添加 `| ignore` 来消除该警告。

除了 `MaintainsVariableSpace` 属性外，另一个名为 `MaintainsVariableSpaceBinding` 的属性可用于将变量向下传递，这是一种不同的方式。示例在列表 6-104 中所示。

### 列表 6-104 CustomOperation 属性中的 MaintainsVariableSpaceBinding

```fsharp
type SimpleSequence5() =
  member.For(source:seq<'a>, f:'a -> seq<'b>) =
    seq { for n in source do yield! n }
  member.Yield(n) = seq { yield n }
  [CustomOperation("", AllowIntoPattern=true, MaintainsVariableSpaceBinding=true)]
  member.Where(source:seq<'a>, [ProjectionParameter])f:'a -> bool) =
    source |> Seq.filter f
  member.Bind(value) = value

## F# 的独特特性

```fsharp

let mySeq5 = SimpleSequence5()

let r6 = mySeq5 (

  for i in 1..10 do

    where (i > 5 && i + 3 < 10) into j

    yield j

)

翻译结果

let b6 = mySeq5

b6.Bind(

  b6.For([1..10]),

  fun i -> i > 5 && i + 3 < 10,

  fun j -> j

)

)

```


```fsharp

if finalBalance > 0 then

    account.Balance <- finalBalance

    account

else

    printfn "not enough found"

    account

```

[<Measure>] type USD
let account = Account<USD>()
let bank = Bank<USD>(account)

```fsharp

let transaction =

    bank {

        deposit 100.<USD>
