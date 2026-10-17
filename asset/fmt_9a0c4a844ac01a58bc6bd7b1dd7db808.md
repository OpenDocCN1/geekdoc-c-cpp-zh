
```fsharp
let findMedian (list0:int list) (list1:int list) =
    let totalCount = list0.Length + list1.Length
    let rec findFunction (list0:int list) (list1:int list) count =
        if count > 1 then
            match list0, list1 with
            | [], [] -> fail "not possible, check empty"
            | head::tail, [] -> findFunction tail [] (count - 1)
            | [], head::tail -> findFunction [] tail (count - 1)
            | h0::t0, h1::t1 ->
                if h0 < h1 then
                    findFunction t0 (h1::t1) (count - 1)
                else
                    findFunction (h0::t0) t1 (count - 1)
        else
            match list0, list1 with
            | [], [] -> fail "not possible, check empty"
            | head::tail, [] ->
                let pre = head
                let now = list1[0]
                if totalCount % 2 = 0 then (float (pre + now)) / 2.0
                else float now
            | [], head::tail ->
                let pre = head
                let now = list0[0]
                if totalCount % 2 = 0 then (float (pre + now)) / 2.0
                else float now
            | h0::t0, h1::t1 ->
                if totalCount % 2 = 0 then (float (h0 + h1)) / 2.0
                else float (max h0 h1)

    if list0.IsEmpty && list1.IsEmpty then
        failWith "please input valid data"
    findFunction list0 list1 (totalCount / 2)

findMedian [1] [2; 4; 5; 6; 7; 8; 10]
```

> 注意此示例使用了递归函数而不是 `for`/`while` 循环。对于某些人来说很容易理解，而另一些人并不认为如此。如果你想编写无副作用的代码，递归函数非常有用。

获取两个数组中位的另一种方法。如果两个位数相同，你就中奖了，位数就是最终结果。如果来自 `array0` 的位数（称为 `median0`）较小，最终结果应该更大，并且对大于或等于 `median0` 的元素继续搜索。如果位数较大，则应该对小于或等于 `median0` 的元素继续搜索，如列表 7-15 所示。

现在让我们回到我在列表 7-8 中提出的快速排序示例问题：如何以自定义的方式分解数据集？列表 7-15 中使用的 `Median` 模式将数组分为三部分：

- 左部分，包含所有小于中位的元素
- 中位数值
- 右部分，包含所有大于中位的元素

# 列表 7-15 从两个数组中寻找位数（版本 2）

```fsharp
let getMedian(list:float array) =
    let len = list.Length
    if len % 2 = 0 then
      (list.[len / 2 - 1] + list.[len / 2]) / 2.0
    else
      list.[len / 2]

let Median(list:float array) =
    let median = getMedian list
    let len = list.Length
    if len % 2 = 0 then
      (list.[0..len / 2], median, list.[len / 2..])
    else
      (list.[0..len / 2], median, list.[len / 2..])

let getMedianFromTwo(list0:float array) (list1:float array) =
    match list0, list1
    | [], [] -> 0.
    | [[a]], [[b]] -> (a + b) / 2.0
    | [[a0;..], [b0;..]] -> ((max a0 b0 + min a1 b1) / 2.0
    | Median(l0, m0, r0), Median(l1, m1, r1) ->
        if m0 = m1 then
            m0
        elif m0 < m1 then
            getMedianFromTwo r0 r1
        else
            getMedianFromTwo l0 l1

let list0 = [1..; 4.; 7.; 8.; 9.; 10..]
let list1 = [2..; 4.; 6.; 7.; 9.; 10..]
let c = getMedianFromTwo list0 list1
```

```fsharp
let dutchFlag(list: array, (low, high)) =
  let swap(i,j) =
    let temp <- list[i]
    list[i] <- list[j]
    list[j] <- temp

  let mutable i = 0
  let mutable lowPointer = 0
  let mutable highPointer = list.Length - 1

  while i <= highPointer do
    let value = low, list[i], high
    match compare value with
      | Lower ->
        swap(lowPointer, i)
        lowPointer <- lowPointer + 1
        i <- i + 1
      | Higher ->
        swap(highPointer, i)
        highPointer <- highPointer - 1
      | Middle ->
        i <- i + 1

let arr = [1; 9; 8; 2; 4; 3; 6; 7; 5; 0]
dutchFlag(arr, 3, 7)
```

**寻找最长递增序列** 确定最长递增序列（LIS），使用数组变量（命名为 `DP`）来存储到当前索引为止的 LIS。例如，如果 `DP.[10]` 的值为 3，则数组 `.[0..9]` 的 LIS 为 3。只有当新值（`DP.[j] + 1`）大于当前值（`DP.[i] < DP.[j] + 1`）且该值仍然递增时（`array.[i] > array.[j]`），才会更新 `DP.[i]` 的值。参见列表 7-17。

## 列表 7-17 最长递增序列代码

```fsharp
let list = [10; 22; 9; 31; 50; 41; 60; 80]
let DP = Array.create list.Length 1
let findMax() =
  let mutable maxLength = 1
  for i = 1 to list.Length - 1 do
    for j = i - 1 downto 0 do
      if list[i] > list[j] &&
        DP[i] < DP[j] + 1 then
          DP[i] <- DP[j] + 1

  maxLength <- max maxLength DP[i]

findMax()
```

* 星号*

## 创建树结构

树是计算机科学中的一种基础数据结构。它是由树形结构表示的层级结构，其中包含一些节点。典型的树结构如图 7-11 所示，后续章节描述了该结构的变体。

![](img/63aaf94e22830ab98ce16c5946be8ef6_423_0.png)

图 7-11 树结构

F# 树的表示与遍历 图 7-11 中树结构的 F# 表示如列表 7-18。该结构是通过判别联合（DU）帮助创建的。

### 列表 7-18 图 7-11 中树结构的树表示

```fsharp
type NodeType = int
type Tree =
  | Node of NodeType * Tree list

let createTree() =
  Node(1, [Node(2, [Node(4, []);]);
    Node(5, [])]);
    Node(3, [Node(6, []);]);
    Node(7, [Node(9, []))]);
    Node(8, []])
])
```

前序遍历和后序遍历是两种基本的树操作。前序遍历从当前节点开始处理树，然后从根节点开始处理子树。后序遍历从子树开始处理树，然后从根节点开始处理当前节点。列表 7-19 显示了这两个过程。

### 列表 7-19 前序和后序遍历

```fsharp
let rec preOrder visit tree =
  match tree with
  | Node(value, children) ->
    visit value
    children
    |> Seq.iter(preOrder visit)

let rec postOrder visit tree =
  match tree with
  | Node(value, children) ->
    children
    > Seq.iter(postOrder visit)

let mutable result = []
let sum v =
  result <- result @ [v]
preOrder sum (createTree())

result <- []
postOrder sum (createTree())
```

前序遍历执行结果

`val it : NodeType list = [4; 5; 2; 6; 9; 7; 8; 1]`

后序遍历执行结果

`val it : NodeType list = [1; 2; 4; 5; 3; 6; 7; 9]`

> **注意** 如前所述，可移植库不支持 `printf` 函数，你可以始终使用 FSI 来评估该函数。

> **注意** 在列表 7-17 中，二叉树是指每个节点最多有两个子节点，其中一个称为*左孩子*，另一个称为*右孩子*。图 7-11 所示的二叉树结构。

![](img/63aaf94e22830ab98ce16c5946be8ef6_423_0.png)

图 7-11 二叉树结构

二叉树的实现（由于此处原文截断）

删除树。你可以不使用递归来删除树，如列表 7-24 所示。执行后，所有节点都被标记为 0（零）。

### LISTING 7-24 不使用递归删除树

```fsharp
type NodeType = { mutable X: int }

type Tree =
  | Node of NodeType Tree list

let mutable stack : Tree list = []

let createTree() =
  Node(X=1), [Node(X = 2), [Node(X = 4), []];
  Node(X = 5), []];
  Node(X = 3), [Node(X = 6), []];
  Node(X = 7), [Node(X = 9),[]]];
  Node(X = 8), []]

let push x =
  stack <- [x] @ stack
let pop () =
  match stack with
  | [] -> None
  | head::tail ->
    stack <- tail
    Some head
let isEmpty() = Seq.exists(fun (x:NodeType) -> x.X < 0)

let deleteTree tree =
  push tree
  while not <| isEmpty() do
    let node : Tree option = pop()
    match node with
    | None -> ()
    | Some(Tree.Node(v, list)) ->
      list |> Seq.iter (fun v -> push v)

let tree = createTree()
deleteTree tree
```

> 注意：可迁移库支持 `System.Collections.Generic.Stack`。你可以用此结构替换堆栈。

> 优先使用递归版本，因为它允许消除可变变量。

410 第三部分 实际应用

### 根据前序和中序序列构建树

树的遍历结果不保留结构信息，但可以根据前序序列和中序序列构建二叉树。前序遍历首先访问根节点。中序遍历在完成左子树后产生根节点。前序中的根节点可以将中序序列划分为左子树序列和右子树序列。你可以轻松在前序序列中找到这些元素。前序序列可以显示根节点节点。重复此过程，直到序列中的所有元素都耗尽，最终就能构建出树。

以下序列是根据列表 7-22 中的树生成的。列表 7-25 根据前序序列和中序序列构建二叉树。

- 前序序列 `[6; 4; 2; 1; 3; 5; 7; 9]`
- 中序序列 `[1; 2; 3; 4; 5; 6; 7; 9]`

### LISTING 7-25 根据前序和中序序列构建二叉树

```fsharp
type NodeType = int
type BinaryTree =
  | Nil
  | Node of NodeType * BinaryTree * BinaryTree
let getLeftPart inorder head =
  inorder
  |> Seq.take(fun n -> n < head)
  |> Seq.toList
let getRightPart inorder head =
  inorder
  |> Seq.skipwhile(fun n -> n < head)
  |> Seq.skip 1
  |> Seq.toList
let getPreOrderLeftPart preorder inorderLeft =
  let len = inorderLeft | Seq.length
  preorder
  |> Seq.skip 1
  |> Seq.take len
  |> Seq.toList
let getPreOrderRightPart preorder inorderLeft =
  let len = inorderLeft | Seq.length
  preorder
  |> Seq.skip 1
  |> Seq.skip len
  |> Seq.toList
```

```fsharp
let rec buildTree inorder preorder =
  match preorder with
  | [] -> Nil
  | head::tail ->
    let inorderLeft = getLeftPart inorder head
    let inorderRight = getRightPart inorder head
    let preorderLeft = getPreOrderLeftPart inorderLeft
    let preorderRight = getPreOrderRightPart inorderRight
    Node(
      buildTree inorderLeft preorder,
      buildTree inorderRight preorder)
buildTree [1; 2; 3; 4; 5; 6; 7; 9] [6; 2; 1; 3; 5; 7; 9];
```

执行结果：

`BinaryTree = Node(6,4,Node(2,Nil,Nil),Node(3,Nil,Nil),Node(5,Nil,Nil), Node(7,Nil,Node(9,Nil,Nil)))`

**根据前序迭代列表构建 BST** 上一节的示例展示了如何构建二叉树。在这一节中，我将演示如何从前序迭代列表获取 BST（二搜索树）。构建树对于查找根节点、左子树和右子树很有用。因为左子树都小于根节点，前序迭代列表可以分为三部分（如列表 7-26 所示）：

- 根节点是迭代列表的第一个元素。
- 子树列表包含紧随根节点之后的元素。左子树节点小于根节点。
- 右子树列表包含左子树列表之后的元素。右子树节点大于根节点。

**LISTING 7-26** 根据前序迭代列表构建 BST
