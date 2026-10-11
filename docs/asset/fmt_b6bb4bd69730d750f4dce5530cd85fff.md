
`type CommandType =`

`| Deposit`

`| Withdraw`

// 定义命令格式，包含一个命令类型和一个整数

`type TCommand =`

`| Command of CommandType * int`

// 可变变量 result

`let result = ref 7`

// 定义一个存款函数

`let deposit x = result := !result + x`

// 定义一个取款函数

`let withdraw x = result := !result - x`

// 根据命令类型执行操作的 Do 函数

`let Do cmd =`

    `match cmd with`

    `| Command(CommandType.Deposit, n) -> deposit n`

    `| Command(CommandType.Withdraw, n) -> withdraw n`

```
```fsharp

// 根据命令类型执行撤销操作的 Undo 函数

let Undo cmd =

    match cmd with

    | Command(CommandType.Deposit, n) -> withdraw n

    | Command(CommandType.Withdraw, n) -> deposit n

// 使用示例

let cmd = Command(CommandType.Deposit, 3)

Do cmd

printf("after deposit: %d" !result)

Undo cmd

printf("after undo: %d" !result)

```
```

```
```fsharp

// 在不检查零的情况下调用函数

try

    d.Invoke(1, 0) | ignore

    with e -> printf("without check, the error is %s", e.Message)

// 添加检查零函数然后调用除法函数

d.Function <- checkZero >> d.Function

try

    d.Invoke(1, 0) | ignore

    with e -> printf("after add check, error is %s", e.Message)

```
```

通过调用未检查的 decorate 函数，装饰器模式的执行结果为：尝试除以零。
添加检查后，错误为 a/b 且 b 为 0

# 使用代理模式 (Proxy Pattern)

代理使用一个作为另一个对象或函数的占位符或接口的类。它通常用于缓存、控制访问，或延迟在时间或资源上昂贵的对象的执行或创建。参见列表 13-16。`CoreComputation` 类包含两个名为 Add 和 Sub 的函数。该类还暴露了一个代理类，用户可以从该类访问计算。

**列表 13-16** 代理模式

```fsharp

// 定义核心计算

type CoreComputation() =

    member.Add(x) = x + 1

    member.Sub(x) = x - 1

    member.GetProxy name =

        match name with

        | "Add" -> this.Add, "add"

        | "Sub" -> this.Sub, "sub"

        | _ -> failwith("not supported")

// 代理实现

let proxy() =

    let core = CoreComputation()

    // 获取 add 函数的代理

    let proxy = core.GetProxy("Add")

    // 从代理获取计算函数

    let coreFunction = fst proxy

    // 获取核心函数名

    let coreFunctionName = snd proxy

```

```fsharp

// 执行核心函数计算

printf("performed calculation %s and get result = %A" coreFunctionName (coreFunction 1)

```

通过调用代理函数，代理模式示例的执行结果为：
执行计算 add 并得到结果 = 2

# 使用策略模式 (Strategy Pattern)

策略是一种软件设计模式，可以在运行时选择和使用算法。列表 3-17 使用一个函数来持有不同的策略。在运行时，可以修改策略。

- **列表 3-17** 策略模式

```fsharp

// 快速排序算法

let quicksort l = 

    printf("quick sort")

// 壳排序算法

let shellsort l = 

    printf("shell sort")

// 冒泡排序算法

let bubblesort l = 

    printf("bubble sort")

// 定义策略类

type Strategy() = {

    mutable sortFunction = fun _ -> ()

    member _.SetStrategy f = _.sortFunction <- f

    member _.Execute n = _..sortFunction n

}

let strategy() =

    let s = Strategy()

    // 将策略设置为快速排序

    s.SetStrategy quicksort

    s.Execute [1..6]

    // 将策略设置为冒泡排序

    s.SetStrategy bubblesort

    s.Execute [1..6]

```

通过调用策略函数，策略模式示例的执行结果为：
quick sort
bubble sort

> 注意：示例代码并没有实现三种排序算法。相反，代码仅仅输出了将要使用的算法名称。

列表 3-17 显示了如何使用 OOP 范式简洁地实现这种模式。然而，策略模式可以使用函数式方法更简洁地实现。列表 3-18 显示了如何使用名为 `executeStrategy` 的高阶函数通过函数式范式来实现这种模式。

# 列表 13-18 使用高阶函数的策略模式

```fsharp

// 快速排序算法

let quicksort l =

    printfn "quick sort"

// 壳排序算法

let shellsort l =

    printfn "shell sort"

// 冒泡排序算法

let bubblesort l =

    printfn "bubble sort"

let executeStrategy f = n

let strategy() =

    // 将策略设置为快速排序

    let s = executeStrategy quicksort

    // 整数列表执行

    [1..6] | s

    // 将策略设置为冒泡排序

    let s2 = executeStrategy bubblesort

    // 整数列表执行

    [1..6] | s2

```

# 使用状态模式 (State Pattern)

状态模式用于根据对象的状态来改变例的行为。这是一种对象在运行时部分更改其类型的整洁方式。列表 19 显示了利率是如何由内部状态决定的：余额越高，客户收到的利率越高。在示例中，我们还演示了如何使用单位度（unit-measure）功能。

# 列表 19 状态模式

```fsharp

// 定义状态

type AccountState =

    | Overdrawn

    | Silver

    | Gold

// 定义单位为美元

[Measure>] type USD

// 定义一个接受单位的账户

type Account<-[Measure>] 'u() =

    // 持有余额

    mutable balance = 0.0<_>

    // 状态属性

    member this.State

    with get() =

        match balance

            | when balance <= 0.0<_> -> Overdrawn

            | when balance > 0.0<_> && balance < 10000.0<_> -> Silver

```

## 列表 3-21 使用 function 关键字

```fs

// 定义两个类型

type Type =

| TypeA

| TypeB

// 使用 function 关键字检查

let checkWithFunction = function

| TypeA -> printf "type A"

| TypeB -> printf "type B"

// 使用 match 关键字检查

let checkWithMatch x =

match x

| TypeA -> printf "type A"

| TypeB -> printf "type B"

```

在列表 3-22 中，`factoryPattern` 内部的工厂实际上是一个函数。它是 `match` 语句的简写。列表 3-21 中的 `checkWithFunction` 和 `checkWithMatch` 函数是等的。

## 列表 3-22 工厂模式示例

```fs

// 定义接口

type IA =

  abstract Action : unit -> unit

// 定义两个类型

type Type =

| TypeA

| TypeB

let factoryPattern() =

// 根据输入对象类型创建对象的工厂模式

let factory = function

| TypeA -> { new IA with

member this.Action = printf "I am type A"

| TypeB -> { new IA with

member this.Action = printf "I am type B"}}

// 创建 A 类型对象

let obj1 = factory TypeA

obj1.Action()

// 创建 B 类型对象

let obj2 = factory TypeB

obj2.Action()

```

通过调用 `factoryPattern` 函数获取工厂模式示例的执行结果
Im type A
Im type B

工厂函数返回了一个不熟悉的对象。实际上，返回类型是所谓的对象表达式（object expression），这种轻量级语法可以显著简化你的代码。如果对象不涉及继承，你几乎可以使用对象表达式完全替代类定义。列表 23 显示了如何使用对象表达式创建接口 IA 的实例。

## 列表 23 使用对象表达式

```fs

// 定义接口

type IA =

  abstract Action : unit -> unit

let a = { new IA with

    member this.Action =

    printf "this is object expression" }

```

## 使用单例模式

单例模式（Singleton pattern）是一种用于限制类实例化次数的设计模式。当恰只需要一个对象来协调跨系统的操作时，这种模式非常有用。F# 中的值默认是不可变的，这保证了类只有一个实例。列表 24 显示了如何确保 F# 类是单例。

## 列表 24 单例模式示例

```fs

// 定义单例模式类

type A private =

    static let Instance = A()

    static member Instance = instance

    member this.Action() = printf "action from A"

// 单例模式

let singletonPattern() =

let a = A.Instance

a.Action()

```

## 使用组合模式

组合模式（Composite pattern）是一种结构模式。它描述了以相同方式处理对象的组。列表 25 显示了树结构。示例重点在于如何访问该树并返回结果。动态生成的对象可以像访问者一样。在示例代码中，CompositeNode 不仅定义了树，还定义了遍历方式。

## 列表 25 组合模式示例

```fs

// 定义访问者接口

type Visitor<'T> =

    abstract Do : 'T -> unit

// 定义组合节点

type CompositeNode<'T> =

    | Node of 'T

    | Tree of 'T * CompositeNode<'T>

    with

      // 中序遍历

      member this.InOrder f =

        match with

        | Tree(left, right) ->

            left.InOrder f

        | Node(n) -> f

      // 前序遍历

      member this.PreOrder f =

        match with

        | Tree(left, right) ->

            f

            left.PreOrder f

        | Node(n) -> f

      // 后序遍历

      member this.PostOrder f =

        match with

        | Tree(left, right) ->

            left.PostOrder f

            right.PostOrder f

        | Node(n) -> f

let invoke() =

    // 定义树结构

    let tree = Tree(Node(1), Node(2), Node(3))

// 定义访问者，获取节点汇总

let wrapper =

  let result = ref 0

  { new Visitor<int> with

    member this.Do n =

      result := result + n }

// 前序遍历树并打印结果

tree.PreOrder(printf("result = %d" !result))

```

通过调用 `invoke` 获取组合模式示例的执行结果
result = 3

## 使用模板模式

模板模式（Template pattern）顾如其名是一个算法骨架。在 F# 中，我们有高阶函数可以作为模板生成其他函数。列表 26 定义了一个名为 `TemplateF` 的模板函数。实际实现位于类之外，用户可以传入自己的版本。

## 列表 26 模板模式示例

```fs

// 模板模式接收三个函数并形成名为 TemplateF 的骨架

type Template(conn, queryF, disconnF) =

  member this.Execute(constr, queryStr) =

    this.TemplateF constr queryStr

  member this.TemplateF =

    let f queryStr =

      conn queryStr

      disconnF ()

// 连接数据库

let connectStr =

  printf("connect to database: %s" conStr)

// 使用 SQL 字符串查询数据库

let queryStr =

  printf("query database %s" queryStr)

// 从数据库断开

let disconnect () =

    printf("disconnect")

let template() =

let s = Template(connect, query, disconnect)

s.Execute("connection string", "select * from tableA")

template()

```

调用 `template` 函数获取模板模式示例的执行结果
connect to database: <connection string>
query database select * from tableA

注意：`connect`、`query` 和 `disconnect` 函数可以实现为类中的私有函数。类设计对于需要在 F# 项目中引用该设计模式实现的 C# 项目非常方便。然而，在纯 F# 的解决方案中，类并不是必要的。列表 27 显示了如何使用高阶函数来实现模板模式。

## 列表 27 使用高阶函数的模板

```fs

// 连接、查询和断开函数

let connect(conStr) = printf("connect using %s" conStr)

let query(queryStr) = printf("query with %s" queryStr)

let disconnect() = printf("disconnect")

// 模板模式

let template(connect, query, disconnect) (conStr:string)(queryStr:string)=

connect(conStr)

query(queryStr)

disconnect()

// 执行查询

let queryFunction = template(connect, query, disconnect)

// 执行查询
```
