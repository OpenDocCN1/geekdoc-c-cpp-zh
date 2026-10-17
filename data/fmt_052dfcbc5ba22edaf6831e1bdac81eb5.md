
```fsharp
open System
let ( AllEmpty | StrNotEmpty | Both ) (str0, str1) =
  let b0 = String.IsNullOrEmpty(str0)
  let b1 = String.IsNullOrEmpty(str1)
  match b0, b1 with
  | true, true -> AllEmpty
  | false, true -> StrNotEmpty
  | true, false -> StrNotEmpty
  | false, false -> Both

  let mutable result = []
  let add x =
    result <- result @ [x]

  let interleaving str0 str1 =
    let rec interleaving str0 str1 current =
      match str0, str1 with
      | AllEmpty _ -> ()
      | StrNotEmpty _ -> add (current+str1)
      | StrNotEmpty -> add (current+str0)
      | Both ->
        interleavingStrs (str0.Substring(1)) str1 (current + string str0.[0])
        interleavingStrs str0 (str1.Substring(1)) (current + string str1.[0])

    interleavingStrs str0 str1 ""

interleaving "ab" "cd"

在 `FSI` 中的执行结果

> result;
val it : string list = ["abcd"; "acbd"; "acbd"; "cabd"; "cadb"; "cdab"]
```

KMP 假设你有两个字符串，并且你想找到目标字符串的所有出现位置。KMP 字符串搜索算法是一种你可以用来实现此目的的算法。搜索复杂度为 `O(n)`，其中 `n` 是字符串的长度。除了演示算法外，代码还展示了如何使用 F# 记录（record）、类型别名和扩展方法。还要注意 `match` 语句的使用，其中分支逻辑完全通过 `when` 实现；所有模式的守卫符均为 `_`。示例代码在列表 7-38 中。

### 列表 7-38 KMP 字符串搜索算法

```fsharp
type List = System.Collections.Generic.List<int>

let kmp (w: string) =
  let t = List([1..w.Length])
  let mutable pos = 2
  let mutable cnd = 0
  t[0] <- -1
  t[1] <- 0

  while pos < w.Length do
    match pos cnd with
    | when w.[pos - 1] = w.[cnd]
      cnd <- cnd + 1
    | t.[pos] < cnd
      pos <- pos + 1
    | when cnd > 0 ->
      cnd <- t[cnd]
    | ->
      t.[pos] <- 0
      pos <- pos + 1

  let t | List.ofSeq

type ResultType =
  { mutable Result : int; mutable Found : bool }
  with
    member this.Set
```

有了图结构，我现在可以实现几种图算法了。

## 深度优先搜索

深度优先搜索（DFS）是一种搜索算法，它在回溯之前会尽可能地沿着树的单个分支向下遍历。DFS 图的示例代码如列表 7-41 所示。在图 7-18 的图上执行的代码生成的生成如 `[Node("1"); Node("2"); Node("3"); Node("4"); Node("5"); Node("6")]`。

![](img/63aaf94e22830ab98ce16c5946be8ef6_449_0.png)

图 7-18 DGML 格式的示例图

### 列表 7-41 图上的 DFS

```fsharp
Portable Class Library Project 中的 DFS 代码
type NodeStack = System.Collections.Generic.Stack<Node>
type VisitedList = System.Collections.Generic.List<Node>

let stack = NodeStack()
let visited = VisitedList()

let visit node =
    visited.Add(node)

let (| Visited | _ ) node =
    if visited.Contains(node)
        Some node
    else
        None

let dfsGraph graph(start:Node)=
    stack.Push(start)
    visited.Clear()

while stack.Count > 0 do
    let currentNode = stack.Pop()
    match currentNode with
        | Visited() ->
        | _ ->
            visit currentNode
            let nodes =
                currentNode.OutgoingEdges
                |> Seq.map (fun edge -> edge.Node)
                |> Seq.distinctBy (fun node -> node.ID)
                |> Seq.toList
            nodes
            |> Seq.iter (fun node -> stack.Push node)

// 调用代码
```

```fsharp
let g = DGML.Graph.DGMLReader(new System.IO.StreamReader("C:\My\ConsoleApplication\Graph1.dgml"))

let (Some startNode) = g.Graph.FindNode("1")

DGMLGraph.DfsGraph g startNode

printf("%A", (Seq.toList DGMLGraph.visited))
```

广度优先搜索（BFS）与 DFS 的区别仅在于存储节点的方式。DFS 使用栈，而 BFS 使用队列。列表 7-42 提供了一个 BFS 示例。

### 列表 7-42 BFS 图示例

```fsharp
type NodeQueue = System.Collections.Generic.Queue<Node>

type VisList = System.Collections.Generic.List<Node>

let queue = NodeQueue()

let visited = VisList()

let visit node =
    visited.Add(node)

let (| Visited | _ ) node =
    if visited.Contains(node) then
        Some node
    else
        None

let bfs graph (start:Node)=
    queue.Enqueue start
    visited.Clear()

while queue.Count <> 0 do
    let currentNode = queue.Dequeue()
    match currentNode with
    | _ ->
        visit currentNode
        let nodes =
            currentNode.OutgoingEdges
            |> Seq.map (fun edge -> edge.ToNode)
            |> Seq.distinctBy (fun node -> node.ID)
            |> Seq.toList
        |> Seq.iter (fun node -> queue.Enqueue node)
```

## 查找图中的所有路径

表示图的另一种方法是使用矩阵。列表 7-43 展示了如何访问图并找到从一点到另一个点所有可能的路径。如果矩阵中的元素为 1，则表示通路；如果矩阵中的元素为 0，则表示障碍物。示例代码找到了从 `(0,0)` 到 `(4,2)` 的所有路径。

### 列表 7-43 查找图中的所有路径

```fsharp
type Location = { X : int; Y : int }

type Path = { Location list }

let graph = {
    [1:1:1;1:0]
    [0:1:0;1:0]
    [0:0:1;1:1]
    [0:1:1;1:0]
    [0:1:0;1:0]
}

let getNeighbors(point:Location) =
    let getLeft(point:Location) =
        if point.X = 0 then None
        else { X = point.X - 1; Y = point.Y }
    let getTop(point:Location) =
        if point.Y = 0 then None
        else { X = point.X; Y = point.Y - 1 }
    let getRight(point:Location) =
        if point.X = 4 then None
        else { X = point.X + 1; Y = point.Y }
    let getBottom(point:Location) =
        if point.Y = 4 then None
        else { X = point.X; Y = point.Y + 1 }
    let result =
        [getLeft point;
         getTop point;
         getRight point;
         getBottom point]
        |> List.filter(fun n -> match n with Some _ -> true | None -> false )
        |> List.map(fun n -> n)
```

```fsharp
rec findAllPath(startPoint:Location)(endpoint:Location)(path:Path)=
    if startPoint = endpoint then
        [ path ]
    else
        let neighbours =
            getNeighbors startPoint
        |> List.filter(fun n -> not (path |> List.exists(fun x -> x=n)))
        for n in neighbours do
            for path in findAllPath n endpoint (n::path) do
                if path.Length > 0 then
                    yield path
```

```fsharp
let start = { X = 0; Y = 0 }
let endpoint = { X = 4; Y = 2 }
let path = [start]
```

> 注意：在 Portable Class Library 中，`List<T>` 仍然存在。你可以用 F lists 来利用不可变性。

A* 算法（读作 A star）是另一种图算法。图用矩阵表示，其中 0 无法通过。存在 `openList` 和 `closedList`。`openList` 用于跟踪未访问的节点，`closedList` 用于跟踪已处理的节点。在通目的地的途中，H 值在决定靠近还是远离目的地时起作用。这就是 A* 的工作原理。算法从具有起始点且 `TotalCost` 设置为 0 的 `openList` 开始。在每次迭代中，从 `openList` 中取出 `TotalCost` 最小的节点并标记为 `currentNode`。只要邻居节点未被访问且不在 `closedList` 中，就将其放入 `openList`。邻居的 `MoveCost` 值根据当前节点计算。如果小于当前值，则将节点的 `PreviousNode` 设置为 `currentNode`。当所有目标节点都关闭或 `openList` 为空时，如列表 7-44 所示。

### 列表 7-44 A* 算法示例

```fsharp
type Location = { X : int; Y : int }

type Node() as this =
    member IsBlock = false
    member val PreviousNode: Node option = None
    member val Location = { X = 0; Y = 0 }
    member val H = 0
    member val MoveCost = 1000
    member this.TotalCost = this.MoveCost + this.H

type Path = Location list

let graph = [
    [1:1:1:1:1:1]
    [1:1:1:0:1:1]
    [1:1:1:0:1:1]
    [1:1:1:0:1:1]
    [1:1:1:1:1:1]
    [1:1:1:1:1:1]
]

let nodeGraph = (
  graph
  |> List.map (fun x ->
    |> List.map (fun y ->
      let loc = {X = x; Y = y}
      Node(IsBlock=(if y = 1 then false else true), Location = loc)))
let rightMax = 6

let getNeighbors(point:Location) =
    let getLeft(point:Location) =
        if point.X = 0 then None
        else { X = point.X - 1; Y = point.Y }
    let getTop(point:Location) =
        if point.Y = 0 then None
        else { X = point.X; Y = point.Y - 1 }
    let getRight(point:Location) =
        if point.X = rightMax then None
        else { X = point.X + 1; Y = point.Y }
    let getBottom(point:Location) =
        if point.Y = rightMax then None
        else { X = point.X; Y = point.Y + 1 }
    let getLeftTop(point:Location) =
        if point.X = 0 || point.Y = 0 then None
        else { X = point.X - 1; Y = point.Y - 1 }
    let getRightTop(point:Location) =
        if point.X = rightMax || point.Y = 0 then None
        else { X = point.X + 1; Y = point.Y - 1 }
    let getRightBottom(point:Location) =
        if point.X = rightMax || point.Y = rightMax then None
        else { X = point.X + 1; Y = point.Y + 1 }
    let getLeftBottom(point:Location) =
        if point.X = 0 || point.Y = rightMax then None
        else { X = point.X - 1; Y = point.Y + 1 }
    let result =
        [(10, getLeft point); (10, getTop point); (10, getRight point); (10, getBottom point);
```
