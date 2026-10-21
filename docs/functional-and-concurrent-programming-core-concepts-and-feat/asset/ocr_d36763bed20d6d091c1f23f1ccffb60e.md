value and two children, typically named left and right, which are themselves binary trees:⁵

```
enum BinTree[+A]:
  case Empty
  case Node(value: A, left: BinTree[A], right: BinTree[A])
```

On such a tree, you can compute the number of values recursively:

```
def size[A](tree: BinTree[A]): Int = tree match
  case Empty          => 0
  case Node(_, left, right) => 1 + size(left) + size(right)
```

Listing 6.7: Recursive implementation of size on binary trees.

The empty tree contains no value, and a non-empty tree contains as many values as in its combined children, plus one for the root. Many other computations on binary trees can proceed recursively, using the empty tree as a terminal, non-recursive case. Binary trees are the focus of a case study in Chapter 8.

Recursive structures are also sometimes defined in terms of mutually recursive types: Type A depends on type B, which depends on type A, for instance. This leads to code that uses mutually recursive functions, also called co-recursive functions. For instance, you can define N-ary trees, in which nodes have zero, one, or more children, in terms of two types: Tree and Forest. On the one hand, a forest is a list of non-empty trees; on the other hand, a non-empty tree consists of a root value and a forest of children:

```
enum Tree[+A]:
  case Empty
  case Node(value: A, trees: Forest[A])

type Forest[A] = List[Tree.Node[A]]
```

You can then calculate the size of a tree by relying on the size of its forest, and the size of a forest by relying on the sizes of its trees:

```
def treeSize[A](tree: Tree[A]): Int = tree match
  case Empty      => 0
  case Node(_, trees) => 1 + forestSize(trees)
```