
`def distinct(list: List[A]): List[A]`

// 从此构建一个包含任何重复元素的新序列。

`def first(list: List[A]): List[A]`

// 选择除第一个元素以外的所有元素。

`def drop(n: Int): List[A]`

// 选择至少存在一次的元素。

`def dropIf(p: Boolean): List[A]`

// 忽略满足谓词的元素。

`def endsWith(s: Seq[B]): Boolean`

// 如果此序列以给定的序列结尾，则返回 true。

图 7.2 显示了 `List` 类的 API。

在 Scala 程序中，默认情况下你可以使用某些内容，而无需使用 `import` 语句。虽然我们没有进入细节，但你已经看到了 `scala.io` 包。我们在脚本最顶部的 `import io.stdin_` 语句中使用了它的部分。Scala 中的导入是嵌套的，因此由于 `scala` 包已经过导入，我们可以直接说 `io.stdin_` 而不是 `scala.io`。如果你愿意，可以使用较长的版本。两者的效果一样好。你可以查看 `scala.io` 包，或者在 API 顶部的搜索栏中输入 "Stdin" 来查看 `Stdin` 对象。点击它，你将看到你一直在使用的各种读取方法。

图 7.2 显示了从 `scala.collection.immutable` 包中选择 `List` 并向下滚动到方法后的 API。在可见部分，你可以看到第 6 章中引入的许多方法，包括 `distinct`、`drop`、`exists` 和 `filter`。点击这些任何一个方法都将显示带有更多信息的详细描述。

API 包含许多超出我们目前对 Scala 知识的内容。它是一个非常有用的资源，如果遇到你不理解的地方，不必并在那里担心。在你编写代码时，应该参考它们。注意，作为程序员，你的目标不是记忆整个 API。那实际上是非常浪费时间的。你想要对 API 中包含的内容留有直觉，这样你就能大致了解那里有什么，并在你需要使用某些你不熟悉的内容时能够快速查阅。你将熟悉你经常使用的部分，而无需背诵。事实上，用该语言练习编程的主要优点之一，就是它将帮助你在无需通过背诵的情况下学习细节。

# Option 类型

如果你开始深入研究 API，你会发现位于顶层 `scala` 包中的 `Option` 类型经常出现。`Option` 类型的构造思想是，当你不确定是否有一个值时，应该使用它。`Option[A]` 既可以是 `Some[A]` 也可以是 `None`。如果是 `Some`，它将拥有一个可以通过 `get` 获取的值。如果没有值，那么你就会得到 `None` 并知道它没有值。其中一个实现此功能的方法示例是 `find` 方法。你可以在 `List` 或 `Array` 上调用 `find`，并传递一个接收元素并返回 `Boolean` 的函数。`find` 方法预期返回函数结果为 `true` 的第一个元素。这听起来足够简单，但如果没有一个呢？如果 `find` 遍历了整个序列但没有任何让函数返回 `true` 会发生什么？由于这个原因，`find` 方法返回 `Option[A]`，其中 `A` 是序列中包含的类型。如果什么都不适用，它可以返回 `None`。

让我们运行两个示例来看它是如何工作的，使用声明 `val lst = List(7, 4, 6, 9, 3, 1)`。

```scala
scala lst.find(_ < 4)
res0: Option[Int] = Some(3)
```

```scala
scala lst.find(_ < 1)
res1: Option[Int] = None
```

列表包含小于 4 的元素。其中第一个是 3，所以我们得到了 `Some(3)`。然而，它不包含任何小于 1 的内容，因此返回 `None`。你可能会奇怪如何使用这种类型的结果。实际上有几种不同的方法可以使用。这取决于你想对结果做什么，或者根据结果想做什么。

最简单的方法是使用 `Option` 类型的 `getOrElse`。正如该方法的名称所示，如果在 `Some` 上调用它，它将获取存储的值；如果对 `None` 调用，它将返回某个默认值。在这里我们可以看到如何使用我们之前的两个 `find` 示例来这样做。

```scala
scala lst.find(_ < 4).getOrElse(0)
res2: Int = 3
```

```scala
scala lst.find(_ < 1).getOrElse(0)
res3: Int = 0
```

如果你在未找到任何内容的情况下有一个良好的默认值，这种方法是有效的。这也是符合 Scala 惯用法的。然而，如果你想在有值的情况下执行额外的逻辑，或者想根据是否有值来做不同的事情，这种方法就并不好。在你有 `Some` 的情况下应该发生更多处理时，你可以使用 `Option` 的 `map` 或 `flatMap` 方法。在 `Some` 上调用 `map` 会将函数应用于存储的值，并产生一个带有该函数结果的 `Some`。在 `None` 上调用 `map` 则什么都不做并产生 `None`。这种行为与如果 `Some` 是包含一个元素的 `List` 而 `None` 是 `Nil` 的预期完全一致。

# 类型基础与参数传递

假设我们想对找到的值进行平方，但仅在我们找到它时。那么 `map` 就很合适。

```scala
scala lst.find(_ < 4).map(_ * _)
res4: Option[Int] = Some(9)
```

```scala
scala lst.find(_ < 1).map(_ * _)
res5: Option[Int] = None
```

正如你所，`map` 或 `flatMap` 的挑战在于你返回的是另一个 `Option` 类型的对象。你可以经过多次 `map` 甚至是 `filter`，但在某些时刻你可能需要使用其他方法之一来解包。如果你实际上想在有 `None` 的情况下做些什么，在 Scala 中更惯用的方法是使用 `match`。它接收 `find` 的结果并告诉我们发现了什么。

```scala
scala lst.find(_ < 4) match {
  case Some(i) => "Found "+i
  case None => "Nothing found"
}
res6: String = "Found 3"
```

注意，这是在使用模式匹配功能来获取 `Option` 的值。`Option` 类型还有 `isEmpty`，它对 `None` 为 `true`，对 `Some` 为 `false`，以及一个 `get` 方法，它将返回 `Some` 中的值，或者在为 `None` 时崩溃。这是处理 `Option` 最不惯用的方法，通常是不被鼓励的。与 `match` 相同功能的代码像这样：

```scala
val result = lst.find(_ < 4)
res7: Option[Int] = Some(3)
if(result.isEmpty) "Nothing found" else "Found " + result.get
```

注意，调用 `find` 的结果需要给它命名，因为代码中使用了两次模式匹配，调用两次它会效率很低。

## 7.3 参数化函数

`List`、`Array` 和 `Option` 等类型不是唯一可以参数参数。函数也可以有参数。这是我们还没有深入细节的内容，但你已经看到过泛型包了。函数也可以有参数，这在书中并不常用，但在后续课程中很重要，它展示了泛型泛的语法。

# 使用 Scala 编程的介绍

泛型函数最简单的例子是这里的 `ident` 方法。

```scala
def ident[A](a:A)=a
ident: A
```

该方法接收任何类型的参数并返回它。泛型只需要在函数名和普通参数列表之间放置类型参数。

```scala
scala ident(3)
res1: Int = 3
```

```scala
scala ident("3.3")
res2: String = 3.3
```

首先，这个函数对于 `Int`、`Double` 和 `String` 都能正常工作。甚至更好的是，不需要告诉它类型。泛型函数几乎可以推断参数的类型。这里有一个更复杂的示例，它并没有做什么，一个接收两个参数并返回包含两个值的元组的函数。

```scala
def makeTuple[A,B](a:A,b:B) = (a,b)
makeTuple: (a:A, b:B) => (A, B)
```

这展示了函数如何拥有多个参数。它们在方括号中以逗号的形式出现。一个简单的例子是具有三个元素的函数。

```scala
def threeList[A](a1:A,a2:A,a3:A) = List(a1,a2,a3)
threeList: (a1:A, a2:A, a3:A) => List[A]
```

引入此点的主要原因是它帮助我们理解我们在上一章看到的内容，即 `fold` 方法。我们说 `fold` 类似于我们在上一章编写的一个递归函数，在那里我们传入一个基值和一个函数。然而，`fold` 适用于任何类型的序列，而且，它们可以返回不同的类型。通过参数类型，我们可以编写一个具有相同能力的函数。

```scala
def ourFold[A,B](list:List[A],base:B)(f:(A,B)=>B):B = {
  if (list.isEmpty) base
  else f(list.head,ourFold(list.tail, base))
}
```

就像 API 中一样，这个方法是柯化的，这是一个我们将在第 7.8 节详细讨论的话题。事实证明这样做有助于类型推断，并允许我们不必在函数上指定类型。我们可以看到使用两个不同的处理函数对 `lst` 进行工作。

```scala
scala ourFold(List(1,0), _+)
res0: Int = 30
```

# 类型基础与参数传递

```scala
scala>ourFold(lst,"+")"_+_"
res2: java.lang.String = 7 4 6 3 9 1
```

第一个示例正如我们已经多次看到的那样，取的是和。这并没有真正练习处理类型的能力，因为涉及的是 `Int`。然而，第二个示例将这些 `Int` 转换成 `String`，有效地利用了第二种类型。

我们之前看过的另一个例子可以从参数类型（parametric types）中获益。在第 4 章中，我们查看了向下组合。当时我们只处理数学函数，并将限制在 `Double` 类型上。到此为止，你应该看到函数远比数字复杂得多。只要 `g` 的输出是一个我们可以传递给 `f` 的类型，我们就可以组合两个函数 `f` 和 `g`。因此，我们传递给 `f` 的是：这里涉及的类型、传递给 `g` 的类型、`g` 返回的类型以及 `f` 返回的类型。多亏了参数类型，我们可以用一行 Scala 代码写出这样的函数。

```scala
def compose[A,B,C](f:(B)=>A,g:(C)=>B):(C)=>A = (x)=>f(g(x))
```

## 7.4 子类型

我们一直一直在讨论类型，就好像它们是完全独立且不相关的。我们写了可能适用于 `Int`、`String` 或元组（Tuple）的函数。这种情况的例外出现在 7.2 节，在那里很明显 `Option`、`Some` 和 `None` 在某种程度上是相关的。通过添加参数，我们能够创建处理任何类型的函数，但这仍然并不意味着类型之间存在任何关系。实际上，Scala 与大多数面向对象的的语言一样，支持**子类型（SUBTYPING）**。如果在任何我们想要使用类型为 `A` 的对象的地方都可以使用类型为 `B` 的对象，那么类型 `B` 就是类型 `A` 的子类型。

子类型的概念在《Object-Orientation, Abstraction, and Data Structures Using Scala [1]》的继承章节中有详细讨论，但现在你应该记住这个术语，因为以后会遇到它。我们的第一个例子：如果我们写一个接受 `Option[Int]` 作为参数的函数，我们可以传递一个 `Some[Int]` 或一个 `None` 并且它可以工作，因为 `Some` 和 `None` 是 `Option` 的子类型。

Scala 中的一些通用子类型关系如图 7.3 所示。这是一个 UML^3 图。箭头从子类型指向超类型。

顶部有一个称为 `Any` 的最终子类型。Scala 中的每个对象都是 `Any` 的实例。Scala 中的所有值，所有内容无论是直接还是间接地都是 `Any` 的实例。我们在第 2 章学到的 `Int` 和 `Double` 类型位于图 7.3 的左侧，在类型 `AnyVal` 下方，`AnyVal` 是 `Any` 的子类型。右侧有另一个名为 `AnyRef` 的类型，它下面有一系列未指定的类型。我们在书中将讨论的所有其他类型都在 `AnyRef` 的某个地方。

> 统一建模语言（UML）是一种用于面向对象软件开发的通用目的建模语言。

![](img/06d4e84f27a8884ea40ba6182ec7c778_202_0.png)

**图 7.3：** Scala 中通用子类型关系图。此图改编自 Odersky, Spoon 和 Venners 编写的 *Programming in Scala* [3] 中的类似图表。

# 类型基础与参数传递

在图右侧底部是一个名为 `Null` 的类型。它是所有 `AnyRef` 类型的子类型。这的一个影响是，任何 `AnyRef` 类型，或任何结果为 `AnyRef` 子类型的函数/方法，都可以有一个为 `null` 的值。这在 Scala 中存在是为了与 Java 保持向后兼容性。然而，作为一条一般规则，你应该尽量避免在程序中使用 `Null`，因为它们非常容易导致崩溃。

在图的最底端是一个名为 `Nothing` 的类型，它是 Scala 中所有其他类型的子类型。`Nothing` 没有存在的值，它的存在是为了使类型系统完备，并处理函数不产生任何结果的情况。我们不会在这一代码块中进行任何需要你显式使用 `Nothing` 的操作，但在某些时候它可能会出现，理解它将帮助你弄清楚发生了什么。考虑以下创建空列表和空数组的示例：

```scala
scala> List()
res8: List[Nothing] = List()
scala> Array()
res9: Array[Nothing] = Array()
```

注意，类型是由 Scala 推断的。看到它时不要惊慌。相反，请替换代码中的某些内容，那里可能没有给 Scala 提供足够的类型信息来推断出其他内容。

## 7.5 变长度参数列表

你是否好奇过我们如何通过这样的调用来构造列表和数组？

```scala
val lst = List(7,4,6,3,9,1)
val lst2 = List(1,2,3)
```

到底发生了什么？事实证明，这种用法下的 `List` 是 7.1 节中提到的单例对象之一，你其中放入了代码，允许它像函数一样被调用。对我们现在更重要的是，我们能够在此调用中传递变数量的参数。在我们看到的第一个例子中，对于任何其他数量也是一样。我们写的函数不能做到这一点。到为止，我们拥有的都是包含特定数量值的参数。我们如何让我们的函数允许传递变数量的参数呢？在 Scala 中，这并不难。这将允许调用者传递零个或多个该类型以创建一个**变长度参数列表（VARIABLE LENGTH ARGUMENT LIST）**。这样做的一个方便地方是平均值函数，比如我们可能用于计算成绩。这样的方法可能像这样：

```scala
def average(nums): ???
```

> 这些被称为更短的名称。

## 使用 Scala 进行编程和问题解决简介

这将允许我们以以下任何方式调用函数，或使用更多更少的参数：

```
average(1,2)
average(2,3,5,7)
average(100,95,63,78)
```

问题是，我们如何使用。答案是，我们对待 `nums` 就像对待 `List` 或 `Array` 一。技术上讲，它是一个 `Seq`，第 6 章中使用的所有方法都在它上面。这些方法将使编写平均函数变得非常容易。

```scala
def average(nums): nums.sum/length
```

如果我们想要带最小值的平均值呢？并没有并没有增加复杂度，因为有一个我们可以调用的 `min` 方法。我们可以将其结合第 6.6 节来创建一个修订版的 `courseAverage`：

```scala
def courseAverage(nums): nums.sum/length
```

（注：此处原文逻辑似乎不完整或存在重复，翻译已根据上下文对齐）

如果如果我们想要带最小值的平均值呢？并没有并没有增加复杂度，因为有一个我们可以调用的 `min` 方法。我们可以将其结合第 6.6 节来创建一个修订版的 `courseAverage`：

```scala
def courseAverage(nums): nums.sum/length
```

（注：此处原文逻辑似乎不完整或存在重复，翻译已根据上下文对齐）

如果如果我们想要带最小值的平均值呢？并没有并没有增加复杂度，因为有一个我们可以调用的 `min` 方法。我们可以将其结合第 6.6 节来创建一个修订版的 `courseAverage`：

```scala
def courseAverage(nums): nums.sum/length
```

（注：此处原文逻辑似乎不完整或存在重复，翻译已根据上下文对齐）

如果如果我们想要带最小值的平均值呢？并没有并没有增加复杂度，因为有一个我们可以调用的 `min` 方法。我们可以将其结合第 6.6 节来创建一个修订版的 `courseAverage`：

```scala
def courseAverage(nums): nums.sum/length
```
