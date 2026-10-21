

operation: 其耗时与索引的值成正比。此外，要更改索引 n 处的值，你必须从列表中丢弃 n 个元素，并分配一个长度为 n 的新列表。例如，如果索引指向列表 [P,l,a,t,o] 中的第一个“a”，并且你想将其替换为“u”以生成 [P,l,u,t,o]，你需要创建一个新的列表 [P,l,u]：

![](img/74309e2bdd93f68d2e94338a3d73517f_95_0.png)

拉链是一种巧妙的数据结构，可以避免这种缺点。它被实现为一对列表 (left, right)：第二个列表包含光标右侧的元素；第一个列表包含光标左侧的元素，但顺序是反的。所有必要的操作——向左或向右移动光标，以及查询和更新光标下的元素——都可以以常数时间实现。

为了帮助可视化拉链，再次考虑列表 [P,l,a,t,o]，当前元素为“a”。它被表示为此拉链：

```
(List('l', 'P'), List('a', 't', 'o'))
```

将光标向右移动会产生新的拉链：

```
(List('a', 'l', 'P'), List('t', 'o'))
```

要实现拉链，首先定义 Zipper 类型为一对列表。拉链值是从非空元素列表构造的：

```
type Zipper[A] = (List[A], List[A])

def fromList[A](list: List[A]): Zipper[A] = (Nil, list)
```

Listing 5.10: List zipper definition and construction.

当你从列表构造拉链时，光标位于最左侧位置（左列表中没有元素）。拉链始终包含至少一个值（当前元素），并且一对中的右列表永远不会为空（fromList 的正确实现会以异常拒绝空列表参数）。

右列表的头部是光标下的元素。它可以被高效地查询和更新：

```
def get[A](zipper: Zipper[A]): A = zipper match
  case (_, x :: _) => x

def set[A](zipper: Zipper[A], value: A): Zipper[A] = zipper match
  case (left, _ :: right) => (left, value :: right)
```

Listing 5.11: List zipper getting and setting.

函数 get 使用匹配第二元素为非空列表且头部为 x 的对的模式。此头部是光标下的值并被返回。由于拉链是不可变的，函数 set 通过生成新的拉链来更新光标下的值。模式 _ :: right 匹配右列表非空且头部未指定的情况。通过使用头部为 value 参数的新右列表构建新的拉链。由于函数列表中的数据共享，set 和 get 都是常数时间操作。此外，函数 set 产生的新的拉链也与用作参数的拉链共享数据——所有第一个列表和第二个列表的大部分。

要将光标向左移动，你需要函数 moveLeft 将光标左侧的第一个列表中最右边的元素移动到第二个列表。由于光标左侧的元素以相反顺序存储，要移动的元素是第一个列表的头部，它需要成为第二个列表的头部：x :: left 变为 left，right 变为 x :: right。在前面的示例中，(List('a','l','P'), List('t','o')) 变为 (List('l','P'), List('a','t','o'))。如果光标已在最左侧位置，则拉链保持不变。此情况由下划线模式捕获：

```
def moveLeft[A](zipper: Zipper[A]): Zipper[A] = zipper match
  case (x :: left, right) => (left, x :: right)
  case _                 => zipper

def moveRight[A](zipper: Zipper[A]): Zipper[A] = zipper match
  case (left, x :: right) if right.nonEmpty => (x :: left, right)
  case _                                    => zipper
```

Listing 5.12: List zipper navigation.

将光标向右移动是类似的：取第二个列表的头部并将其移动到第一个列表的头部。然而，你还需要避免将光标移动到最右边元素之后，因为这会留下没有当前值的拉链。函数 moveRight 的第一个模式中的条件保证了新拉链中的第二个列表是非空的。两个光标移动都以常数时间实现。

与其使用条件，你可以使用模式 "_ :: _" 来确保 right 非空：

```
val alpha = bits >>> 8
(alpha, r, g, b)
```

Listing 5.14: Example of an extractor (RGB values).

在 Scala 中，函数的名称 unapply 具有特殊作用。只要对象 ARGB 在作用域中，你现在就可以使用模式匹配将一个数字拆分为其颜色元素：

```
val ARGB(a, r, g, b) = 0xABCDEF12
```

这将变量 a 设置为 0xAB，变量 r 设置为 0xCD，等等。

对象 ARGB 被称为提取器。许多提取器在 Scala 标准库中定义。例如，你可以使用模式匹配检索正则表达式中的捕获组：

```
val Phone: Regex = """(?(?:\+1\s)?([2-9]\d{2})[\s-]([2-9]\d{2})-?\d{4})""".r

def formatNumber(str: String): Option[String] = str match
  case Phone(npa, nxx, number) => Some(s"($npa) $nxx-$number")
  case _                       => None

formatNumber("603 5551234")     // Some("(603) 555-1234")
formatNumber("+1 603-555-1234") // Some("(603) 555-1234")
formatNumber("6035551234")      // None
```

Listing 5.15: Example pattern matching on a regular expression.

## 5.8 Summary

- Pattern matching 是函数式编程语言的常见特性。在最简单的形式中，你可以将其视为一种强大的 switch 表达式形式。它可用于测试布尔条件，将值与常量进行比较，或检查运行时类型。
- 然而，模式匹配的真正威力来自于用于处理代数数据类型。它所特有的类型是按其他类型的替代（也称为和）和聚合（也称为积）定义的。模式匹配可用于在替代之间切换，并从聚合类型中提取组件。

> 3In Scala, the r method creates a regular expression out of a string. Also, the s prefix enables interpolation in string literals: s"$x" is a string that contains the value of x.

This page intentionally left blank

actually remove anything from an immutable collection, you would need to replace the action processOne with a function¹ that processes an element and returns a new collection with that element removed:

```
// processes one element, and returns a collection with this element removed
def processOne[A](collection: ImmutableCollection[A]): ImmutableCollection[A] = ...
```

So far, so good. Now, you need a way to use this function to process an entire collection, one element at a time. The same approach as before will not do: If collection.nonEmpty is true, processOne(collection) will not change that—the collection is immutable. Therefore, collection.nonEmpty will remain true, and the loop will never terminate. Can a loop be used at all? Yes, and this program would work:

```
def processCollection[A](collection: ImmutableCollection[A]): Unit =
  var remaining = collection
  while remaining.nonEmpty do
    remaining = processOne(remaining)
```

This gets the job done, but at the cost of reintroducing mutation through an assignment statement: Something in the body of the loop must have some side effect, and since collection cannot change, a mutable variable remaining is introduced. (The same approach was used in Section 3.6 to implement a mutable state in terms of an immutable data structure.) The loop-based solution works only because there is mutation. To achieve a fully immutable style—no var—you need to take a different route.

If a function f is free of side effects, the repetition f(x); f(x); f(x) is pointless. Think of code that executes Math.sqrt(4.0); Math.sqrt(4.0); Math.sqrt(4.0). What is the point? Instead, the output of f must be used, typically as the input to further computing. Instead of loops, what you need is a mechanism that can arbitrarily nest function calls. This mechanism is recursion.

Let’s go back to the problem of processing an entire immutable collection. A function needs to process one element from the collection and then process, in the same fashion, a new collection with that one element removed. In other words, you need to invoke processOne on the value produced by a previous call to processOne. Since processCollection is designed to invoke processOne, all you need to do is to call processCollection again on the output of processOne:

```
def processCollection[A](collection: ImmutableCollection[A]): Unit =
  if collection.nonEmpty then processCollection(processOne(collection))
```

Listing 6.1: Nesting function calls through recursion.

An initial call to processCollection processes the first element of a collection, and produces a new, reduced collection. This collection is then processed in the same way

¹This function is not pure because processing an element must have some side effect. However, it has no side effect on the collection itself, which is all that matters for the purpose of this illustration.

