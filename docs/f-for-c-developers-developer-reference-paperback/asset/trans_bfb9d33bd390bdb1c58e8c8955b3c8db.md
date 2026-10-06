
查找树直径
树是一个具有形状的结构，树直径是以下三个值中的最大值：

- 左子树的直径。
- 右子树的直径。
- 经过树根节点的最长路径。最长路径可以通过树的高度来计算。

示例树如图 7-14 所示，其代码如列表 7-29 所示。图中树的直径为 7。

![](img/63aaf94e22830ab98ce16c5946be8ef6_435_0.png)

图 7-14 用于测量直径的树

列表 7-29 树直径代码

```fsharp
type NodeType = int

type BinaryTree =
  | Nil
  | Node of NodeType * BinaryTree * BinaryTree

let createBinaryTree() =
  Node(1, Node(2, Node(4, Nil, Nil),
    Node(5,
      Node(6, Nil, Nil),
      Node(7, Nil, Nil)),
    Node(3,
      Nil,
      Node(8,
        Nil,
        Node(9, Nil, Nil))))
```

```fsharp
let rec treeHeight tree =
  match tree with
  | Nil -> 0
  | Node(v, left, right) ->
    let leftHeight = treeHeight left
    let rightHeight = treeHeight right
    (max leftHeight rightHeight) + 1

let rec treeDiameter tree =
  match tree with
  | Nil -> 0
  | Node(v, left, right) ->
    let leftHeight = treeHeight left
    let rightHeight = treeHeight right
    let leftDiameter = treeDiameter left
    let rightDiameter = treeDiameter right
    max (leftHeight + rightHeight + 1) (max leftDiameter rightDiameter)

treeDiameter(createBinaryTree())
```

注意：如果数据结构是一个 DU（联合类型），代码中经常看到许多 `match` 语句来解构该 DU。

查找最近公共祖先
给定二叉树中的两个节点，一种常用的操作是找到这两个节点的最近公共祖先（LCA）。例如，图 7-15 中节点 2 和 1 的祖先是 6 和 4，但 4 比 6 低，因此 2 和 1 的 LCA 是 4。列表 7-30 接收两个节点并返回这两个节点的 LCA。

![](img/63aaf94e22830ab98ce16c5946be8ef6_436_0.png)

图 7-15 在二叉树中寻找 LCA

# 列表 7-30 二叉树的 LCA

```fsharp
type NodeType = int

type BinaryTree =
  | Nil
  | Node of NodeType * BinaryTree * BinaryTree

let createBinaryTree() =
  Node(1, Node(2, Node(4, Nil, Nil),
    Node(5,
      Node(6, Nil, Nil),
      Node(7, Nil, Nil)),
    Node(3,
      Nil,
      Node(8,
        Nil,
        Node(9, Nil, Nil))))

let findLCA (node0, node1) root =
  let rec commonAncestor (node0, node1) root =
    match root with
  | Nil -> None
  | Node(v, left, right) ->
    match left with
    | Nil -> None
    | Node(v, _, _) when v = node0 || v = node1 -> Some root
    | _ ->
      let l = commonAncestor(node0, node1) left
      let r = commonAncestor(node0, node1) right
      match l, r with
      | None, _ -> None
      | Some(_), Some(_) -> Some root
      | Some(_) as n, None -> n
      | None, Some(_) as n -> n
  // ...
  match root with
  | Nil -> None
  | Node(v, left, right) when v=node0 || v=node1 -> Some root
  | Node(v, left, right) -> commonAncestor(node0, node1) root

let tree = createBinaryTree()
type ResultRecord = { Nodes : NodeType; Ancestor : NodeType }
let output pair =
  match pair with
  | Some(Node(v, _, _)) -> { Nodes = pair; Ancestor = v }
  | _ -> { Nodes = pair; Ancestor = -1 }

let pairsToFindAncestor = [
  (2, 3)
  (1, 8)
  (1, 2)
  (3, 8)
  (8, 7)
  (4, 6)
  (4, 7) ]

let r =
  pairsToFindAncestor 
  |> List.map(fun pair -> (pair, findLCA pair tree))
  |> List.map(fun (pair, result) -> output result)

# 执行结果

```text
[[Nodes = (2,3); Ancestor = 1};
 {Nodes = (1, 8); Ancestor = 1};
 {Nodes = (1, 2); Ancestor = 1};
 {Nodes = (3, 8); Ancestor = 1};
 {Nodes = (8, 7); Ancestor = 1};
 {Nodes = (4, 6); Ancestor = 2};
 {Nodes = (4, 7); Ancestor = 2;]]
```

> **注意** 为了更好的可读性，结果是从 FSI 输出并重新格式化的。

如果树是二叉搜索树（BST），寻找 LCA 会更容易，因为 LCA 是位于两个给定值之间的第一个节点。创建图 7-16 所示树的示例代码在列表 7-31 中寻找 LCA。

![](img/63aaf94e22830ab98ce16c5946be8ef6_438_0.png)

图 7-16 LCA 的树结构

# 列表 7-31 在 BST 中寻找 LCA

```fsharp
type NodeType = int

type BinaryTree =
  | Nil
  | Node of NodeType * BinaryTree * BinaryTree

let createBinaryTree() =
  Node(20, Node(8, Node(5, Nil, Nil),
    Node(12, Nil, Nil)),
    Node(15, Nil, Nil),
    Node(30, Node(21, Nil, Nil),
        Node(32, Nil, Nil))))

let tree = createBinaryTree()
let rec findCAInBST (n0, n1) root =
  match root with
  | Nil -> None
  | Node(v, left, right) ->
    if v > n0 && v <= n1 then v
    elif v > n0 && v > n1 then
      findCAInBST(n0, n1) left
    else
      findCAInBST(n0, n1) right

findCAInBST(3, 15) tree
```

验证所有子节点和
如果树有值，可以验证该值是否等于所有子节点和。示例见列表 7-32。

# 列表 7-32 检查节点值是否为子节点和

```fsharp
type NodeType = int

type BinaryTree =
  | Nil
  | Node of NodeType * BinaryTree * BinaryTree

let createBinaryTree() =
  Node(9, Node(4, Nil, Nil),
    Node(5, Nil, Nil),
    Node(6, Nil, Nil),
    Node(7, Nil, Nil))))

let rec checkTree root =
  match root with
  | Nil -> true, None
  | Node(v, left, right) ->
    let leftResult, leftSum = checkTree left
    let rightResult, rightSum = checkTree right
    let leftS = match leftSum with | Some n -> n | None -> 0
    let rightS = match rightSum with | Some n -> n | None -> 0
    let isValid = leftResult && rightResult && (v = leftS + rightS)
    isValid, Some (v + leftS + rightS)

createBinaryTree() |> checkTree | fst
```

计算树边界
树的边界可以使用列表 7-33 所示的代码计算（对于图 7-17定义的结构）。虚线显示了如何访问边界。

![](img/63aaf94e22830ab98ce16c5946be8ef6_440_0.png)

图 7-17 树边界

列表 7-33 计算树边界

```fsharp
type NodeType = int

type BinaryTree =
  | Nil
  | Node of NodeType * BinaryTree * BinaryTree

let createBinaryTree() =
  Node(1, Node(2, Node(4, Nil, Nil),
    Node(5),
    Node(6, Nil, Nil),
    Node(7, Nil, Nil)),
  Node(3,
    Nil,
    Node(8,
      Nil,
      Node(9, Nil, Nil))))

let mutable result = []
let add x =
  result <- result @ [x]
let visitLeaf root =
  match root with
  | Nil -> ()
  | Node(v, Nil, Nil) -> add v
  | Node(v, left, right) ->
    visitLeaf left
    visitLeaf right

let visitLeftBoundary root =
  match root with
  | Nil -> ()
  | Node(v, Nil, Nil) -> ()
  | Node(v, Nil, right) ->
    add v
    visitLeftBoundary right
  | Node(v, left, _) ->
    add v
    visitLeftBoundary left

let visitRightBoundary root =
  match root with
  | Nil -> ()
  | Node(v, Nil, Nil) -> ()
  | Node(v, left, Nil) ->
    visitRightBoundary left
    add v
  | Node(v, left, right) ->
    visitRightBoundary right
    add v

let getBoundary root =
  match root with
  | Nil -> ()
  | Node(v, left, right) ->
    add v
    getBoundary left
    visitLeaf left
    visitLeaf right
    visitRightBoundary right

let tree = createBinaryTree()
getboundary tree
```
