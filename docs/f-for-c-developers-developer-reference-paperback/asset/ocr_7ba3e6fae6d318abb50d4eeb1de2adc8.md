```
let rec buildTree inorder preorder =
  match preorder with
  | [] -> Nil
  | head::tail ->
    let inorderLeft = getLeftPart inorder head
    let inorderRight = getRightPart inorder head
    let preorderLeft = getPreOrderLeft inorderLeft
    let preorderRight = getPreOrderRight inorderRight
    Node(
      buildTree inorderLeft preorder,
      buildTree inorderRight preorder)
buildTree [1; 2; 3; 4; 5; 6; 7; 9] [6; 2; 1; 3; 5; 7; 9];
```

Execution result

BinaryTree =
Node(6,4,Node(2,Nil,Nil),Node(3,Nil,Nil),Node(5,Nil,Nil),
Node(7,Nil,Node(9,Nil,Nil)))

**Build a BST from a pre-order iteration list** The sample in the previous section shows how to build a binary tree. In this section, I demonstrate how to get a BST from a pre-order iteration list. Building a tree is useful for finding the root, left subtree, and right subtree. Because the left subtrees are all smaller than the root, the pre-order iteration list can be divided into the three parts (as shown in Listing 7-26):

+   - The root is the first element of the iteration list.

+   - The subtree list contains elements immediately following the root node. The left subtree nodes are smaller than the root node.

+   - The right subtree list contains elements listed after the left subtree list. The right subtree nodes are larger than the root node.

**LISTING 7-26** Building a BST from a pre-order iteration list

```
type NodeType = int

type BinaryTree =
| Nil
| Node of NodeType * BinaryTree * BinaryTree

let rec buildBSTFromOrder (l:NodeType list) =
  match l with
  | [] -> Nil
  | [a] -> Node(a, Nil, Nil)
```