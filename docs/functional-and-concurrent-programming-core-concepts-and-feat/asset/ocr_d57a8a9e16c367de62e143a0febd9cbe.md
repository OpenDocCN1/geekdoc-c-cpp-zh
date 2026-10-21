one on the left tree and one on the right tree. To trigger the tail recursion optimization, you might be tempted to employ the same trick used for function `factorial`:

```
```scala
def size[A](tree: BinTree[A]): Int =
  def loop(tree: BinTree[A], sz: Int): Int = tree match
    case Empty                 => sz
    case Node(_, left, right)  => loop(right, loop(left, sz + 1))

  loop(tree, 0)
```
```

One recursive call to `loop` is now in tail position and could potentially be optimized, but the nested call `loop(left, ...)` still needs to use a stack frame: After controls returns from it, the `loop(right, ...)` call still needs to take place and still uses the current frame (to access local variable `right`).

A true tail recursive variant needs to make a single recursive call only. You can achieve this by introducing your own stack, as a list of trees:

```
```scala
def size[A](tree: BinTree[A]): Int =
  @tailrec
  def sizeSum(list: List[BinTree[A]], sum: Int): Int = list match
    case Nil                    => sum
    case Empty :: trees          => sizeSum(trees, sum)
    case Node(_, left, right) :: trees => sizeSum(left :: right :: trees, sum + 1)

  sizeSum(List(tree), 0)
```
```

Function `sizeSum` computes the sum of the sizes of a list of trees. It is tail recursive. When an empty tree is found in the list, it contributes nothing to the sum. When a node is taken out of the list, the sum accumulator is incremented by one, and the node’s children are added to the list of trees to be processed. The size of a tree is obtained by applying function `sizeSum` to a list that contains only this tree. In effect, the execution stack has been replaced with a regular list. As with factorial, tail recursion is achieved at the cost of a loss of elegance.

Seeking to replace general recursion with tail recursion involves trade-offs. While pushing and popping the execution stack is likely to be faster than list operations, stack space tends to be limited. By contrast, the added list in function `sizeSum` is allocated in heap memory alongside other objects. Heap memory is typically orders of magnitude larger than stack space.

Other approaches exist to optimize recursive calls and trade heap space for stack space. One notable technique, known as a *trampoline*, has been used to translate languages with tail-call optimization into languages without it. Trampolines are explored as a case study in Chapter 14.