# LISTING 7-23 BST validation

```
type NodeType = int

type BinaryTree =
  | Nil
  | Node of NodeType * BinaryTree * BinaryTree

let createBinaryTree() =
  Node(6, Node(4, Node(2,
    Node(1, Nil, Nil),
    Node(3, Nil, Nil),
    Node(5, Nil, Nil),
    Node(7,
      Nil,
      Node(9, Nil, Nil)))))

let checkInOrder value list =
  match list with
  | [] -> true
  | head::tail ->
    if value<head then
      checkInOrder tail
    else
      false

let rec inOrder visit tree =
  match tree with
  | Nil -> ()
  | Node(v, left, right) ->
    inOrder visit left
    visit v
    inOrder visit right

let mutable result = []
let sum v =
  result <- result @ [v]

inOrder sum (createBinaryTree())
```

> **Note** The *match* statement has an interesting advantage over the *if* statement: it can generate a warning if any unhandled paths are in your logic.

A tree is a complex structure. In addition to the common tree traversal operations I just described, there are other operations you can perform related to tree structures.