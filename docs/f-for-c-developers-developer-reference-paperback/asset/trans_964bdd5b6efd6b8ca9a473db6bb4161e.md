

```sharp
if i % 3000 = 0
    syncContext.Post(fun _ -> myTrigger i, null)
a.Error.Add(fun _ -> printfn "something is wrong")
a.Start()
a)

// 添加事件处理器
Event.add(fun n-> printfn "%A message received") myEvent.Publish

// 向所有代理项发送消息
for agent in agents do
    agent.Post "hello"
```

你可以使用 `MailboxProcessor` 来模拟一个消息箱银行账户系统，其中存款和取款操作是异步执行的。示例见列表 6-92。

## 列表 6-92 使用 MailboxProcessor 的银行账户

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

