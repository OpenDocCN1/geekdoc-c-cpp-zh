# LISTING 7-57 Sum of the tree node values

```
type NodeType = int

type BinaryTree =
  | Nil
  | Node of NodeType * BinaryTree * BinaryTree

let tree n =
  let mutable subtree = Node(1, Nil, Nil)
  for i=0 to n do
    subtree <- Node(1, subtree, Nil)
  subtree

let deepTree = tree 1000000

module TreeModule =
  let rec sum tree =
    match tree with
    | Nil -> 0
    | Node(v, l, r) ->
      let sumL = sum l
      let sumR = sum r
      v + sumL + sumR

  sum deepTree

module TreeCPSModule =
  let rec sum tree cont =
    match tree with
    | Nil -> cont
    | Node(v, l, r) ->
      let afterLeft lValue =
        let afterRight rValue =
          cont (v + lValue + rValue)
        sum r afterRight
      sum l (afterLeft cont)

  sum deepTree id
```

Now I'll demonstrate how to convert from the recursive version to the CPS version; see Listing 7-58. During the conversion process, the intermediate code at some steps might not compile.

# LISTING 7-58 Converting a tree traversal to CPS

```
Step 1: Add a continuation function
module TreeModule =
  let rec sum tree cont =
    match tree with
    | Nil -> 0
```