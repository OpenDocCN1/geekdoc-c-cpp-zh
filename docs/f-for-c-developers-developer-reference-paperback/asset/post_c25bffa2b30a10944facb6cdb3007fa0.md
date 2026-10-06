
Find the tree diameter
The tree is a structure with a shape, and the tree diameter is the maximum value of the following three values:

- The diameter of the left tree.
- The diameter of the right tree.
- The longest path between nodes through the tree root. The longest path can be computed by the tree height.

A sample tree is shown in Figure 7-14, with code for it shown in Listing 7-29. The diameter for the tree shown in the figure is 7.

![](img/63aaf94e22830ab98ce16c5946be8ef6_435_0.png)

FIGURE 7-14 Tree for measuring the diameter

LISTING 7-29 Tree diameter code

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

Note If the data structure is a DU, it's common to see many match statements in the code to decompose the DU.

Find the lowest common ancestor
Given two nodes in a binary tree, one common operation is used to find the lowest common ancestor (LCA) for these two nodes. For example, the ancestors for 2 and 1 in Figure 7-15 are 6 and 4, but 4 is lower than 6, so the LCA for 2 and 1 is 4. Listing 7-30 takes two nodes and returns the LCA of these two nodes.

![](img/63aaf94e22830ab98ce16c5946be8ef6_436_0.png)

FIGURE 7-15 Finding the LCA in a binary tree

# LISTING 7-30 LCA for a binary tree

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
type ResultRecord = { Nodes : NodeType*NodeType; Ancestor : NodeType }
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

```fsharp
let r =
  pairsToFindAncestor 
  |> List.map(fun pair -> (pair, findLCA pair tree))
  |> List.map(fun (pair, result) -> output result)
```

# Execution result

```text
[[Nodes = (2, 3); Ancestor = 1};
 {Nodes = (1, 8); Ancestor = 1};
 {Nodes = (1, 2); Ancestor = 1};
 {Nodes = (3, 8); Ancestor = 1};
 {Nodes = (8, 7); Ancestor = 1};
 {Nodes = (4, 6); Ancestor = 2;};
 {Nodes = (4, 7); Ancestor = 2;]]
```

> **Note** The result is copied from the FSI output windows with some reformatting for better readability.

If the tree is a BST, finding LCA will be easier because the LCA is the first node whose value is between two given values. The sample code that creates the tree structure shown in Figure 7-16 and finds the LCA in it is shown in Listing 7-31.

![](img/63aaf94e22830ab98ce16c5946be8ef6_438_0.png)

FIGURE 7-16 BST structure for LCA

# LISTING 7-31 Finding the LCA in a BST

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

Validate the sum of all child nodes
If the tree has value, you can validate whether the value is the sum of all its children. The sample is shown in Listing 7-32.

# LISTING 72 Checking a node's value is the sum of child nodes

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

Calculate the tree boundary
tree's boundary can be calculated with code as shown in Listing 7-33 (for the tree structure defined in Figure 7-17). The dashed line shows how boundary is visited.

![](img/63aaf94e22830ab98ce16c5946be8ef6_440_0.png)

FIGURE 7-17 Tree boundary

LISTING 7-33 Calculating the tree boundary

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
  | Node(v, right) ->
    visitRightBoundary right
    add v

let getBoundary root =
  match root with
  | Nil -> ()
  | Node(v, left, right) ->
    add v
    visitBoundary left
    visitLeaf left
    visitLeaf right
    visitRightBoundary right

let tree = createBinaryTree()
getboundary tree
```

Execution result
> result;;
val it : NodeType list = [1; 2; 4; 6; 7; 9; 8; 3];

# Using String Operations

String is probably the most commonly used data type next to integer. Although .NET provides many built-in methods for processing strings, you may find it useful to see how string processing algorithms can be explicitly coded in F#.

Substring Listing 7-34 shows how to decompose a string into substrings consisting of one or more repeats of the same character. If the input is "34445", the function will return "3", "444", and "5".

LISTING 7-34 How to decompose a string into substrings

```fsharp
let str = "34445"
let getSub(str:string) =
  let result = ref ""
  for c in str do
    if result <> "" then
      result := string c
    elif (!result).EndsWith c then
      result := !result + string c
    else
      yield result
      result := string c
]
getSub str
```
