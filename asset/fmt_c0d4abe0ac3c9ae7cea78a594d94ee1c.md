
表达式的类型也可以用于赋值。因此我们可以更改存储在数组中的值。

```scala
arr(4) = 99
res9: Array[Int] = Array(7, 4, 6, 3, 99, 1)
```

在这里我们可以使用赋值来更改 `Array` 的一个元素的值。这可能会让你惊讶，因为最初 `arr` 应该是 `val`。之前我们说你不能更改由 `val` 创建的变量所指向的内容。这实际上并没有打破该规则；名称仍然指向同一个 `Array`。一个类比可能是 `Array` 是一个房子，而值是人。人们可能会离开房子，但房子本身没变。我们可以通过尝试更改 `arr` 来演示这一点。

```scala
arr = Array(2,7)
<console>: error: reassignment to val
arr:Array(2,5)
```

我们称 `Array` 类型为**可变（MUTABLE）**类型，因为它的值是可以更改的。内部值无法更改的类型被称为**不可变（IMMUTABLE）**类型。这种区别对我们 `Scala` 以及一般的编程中非常重要，因为它改变了我们处理数据的方式。由于我们在下一节中探讨的 `List` 类型恰好是不可变的。事实上，我们之前看到的所有类型都是不可变的。一旦创建，其值就永远不会改变。`Array` 是我们关于可变事物的第一个例子。

数组并不是所有属性都可以更改。正如我们所看到的，我们可以更改存储在数组中的值。然而，我们无法高效地更改数组中存储物品的数量。`Array` 持有的物品数量是长度。事实上，`Array` 类型有 `length` 和 `size` 方法为我们提供这些信息。

```scala
scala arr.length
res10: Int = 6
```

```scala
scala arr.size
res11: Int = 6
```

当你创建一个 `Array` 时，必须指定一个永远不会改变的长度。如果你使用 `var` 变量，你可以创建一个新的 `Array`。当你尝试使用负值或过大的索引时，`Scala` 会给出一个错误信息，说明你超出了 `Array` 的边界。我们可以看到当访问越界索引时是怎样的。

```scala
arr(100)
java.lang.ArrayIndexOutOfBoundsException: Index 100 out of bounds for length 6
```

# 138 使用 Scala 进行编程和解决问题的简介

修改内容。因此，不需要返回任何内容。该函数的结果存储在修改后的 `Array` 中。以下展示了该函数的用法。

```scala
scala val numbers = Array(0, 0, 0, 0)
numbers: Array[Int] = Array(0, 0, 0, 0)
```

```scala
scala fillArray(numbers, 0)
```

```scala
scala numbers
res12: Array[Int] = Array(2, 3, 4, 5)
```

创建了一个可以容纳四个值的整数数组。我们调用 `fillArray` 并输入值 2, 3, 4 和 5。完成操作后，我们可以检查 `numbers` 并查看它是如何存储这些值的。

现在，我们需要对 `Array` 的内容执行某种操作。我们将跳过仅为加法或乘法创建特殊函数的步骤，直接跳转到更抽象、更灵活的方法，即传递一个函数来操作内容。除了执行操作外，我们还需要一个 `Array` 和一个用于当前索引的整数。与上一章的操作不同，我们不需要传递基准情况，因为我们知道何时处于 `Array` 的开头或末尾。该函数可能如下：

```scala
def operateOnArray(arr:Array[Int],index:Int, func:(Int,Int)->Int):Int = {
  if (index < arr.length-1) {
    func(arr(index), operateOnArray(arr, index+1, func))
  } else {
    arr(arr.length-1)
  }
}
```

如果传入的索引位于 `Array` 最后一个元素或之后，该函数将返回数组的最后一个元素。否则，它将函数应用于当前元素以及对后续元素递归函数的结果。我们可以通过这些命令在之前定义的 `Array` `arr` 上看到它的运行情况。

```scala
scala val arr = Array(7,4,6,3,9,1)
res13: Array[Int] = Array(7, 4, 6, 3, 9, 1)
```

```scala
scala operateOnArray(arr, 0, _*)
res13: Int = 30
```

```scala
scala operateOnArray(arr, 0, _*)
res14: Int = 4536
```

这已经允许我们使用使用 `Array` 带来的额外能力。存储值使我们能够多次对它们进行操作，而无需多次输入它们。

# Scala 中的 Arrays 和 Lists

## 6.3 Lists

在大多数非函数式语言中，`Array` 是构建的集合的基础。`Array` 通常存储在内存块中。这使得在执行许多操作时既快速又高效。正如我们所见，`Array` 是可变的。函数式语言倾向于避免变和其他副作用。如果不允许变，`Array` 将变得非常高效。如果你想更改不可变 `Array` 中的单个值，你必须对 `Array` 进行完整拷贝。出于这个原因，函数式语言倾向于使用列表。从技术上说，`Scala` 中的 `List` 类型是不可变的单链表，这是你应该在随后的课程中会熟悉的数据结构。你不需要理解它的结构就可以使用它。

我们可以使用构建带初始值的 `Array` 的语法来构建 `List`。

```scala
scala List(7,4,6,3,9,1)
res15:List[Int] = List(7, 4, 6, 9, 1)
```

与 `Array` 类似，`List` 类型是参数化的，如果你使用这种语法，`Scala` 将推断出最佳类型。

与 `Array` 不同，`List` 的长度在创建时不是固定的。此外，当我们最初不知道将存储的所有值时，还有另一种方法将 `Lists` 组合在一起。如果我们向 `List` 的头部添加元素，就可以轻松地逐个构建 `Lists`。要向 `List` 中添加元素，我们使用 "cons" 操作符 `::`。以下向现有 `List` 添加单个元素的示例。

```scala
scala val lst = List(2,3,4)
lst:List[Int] = List(2, 3, 4)
```

我们首先创建一个包含 2, 3, 和 4 的 `List`，然后将 1 `cons` 到列表开头。此操作没有修改原始 `List`。它给了我们一个在开头多了一个额外元素的新列表。由于 `List` 的工作方式，它是高效的。它不需要拷贝 `List` 即可工作。我们可以再次查看 `lst` 发现它没有变化。

```scala
scala lst
res17:List[Int] = List(2, 3, 4)
```

如果你使用 `cons` 操作符构建 `List`，通常从一个空 `List` 开始。在 `Scala` 中表示空 `List` 有两种方法。一种不在括号内放入参数。另一种是使用 `Nil`。所以我们可以用同样的方式构建之前的那个列表。

```scala
scala 1::2::3::4::Nil
res18:List[Int] = List(1, 2, 3, 4)
```

你必须将 `Nil` 放在末尾，因为 `::` 操作符右侧需要有一个 `List`。注意，为了使之生效，`::` 操作符是右结合的。

> 这是我们首次讨论的 `val` 和 `var` 之间的区别。从一般规则来说，不包含变的程序更容易推理。包含变会通过引入错误使事情变得更复杂。因此，`1::2::` 等同于 `2::1` 与从左结合的普通数学运算符相反。在 `Scala` 中，任何以 `::` 结尾的操作符都是右结合的。我们可以使用 `cons` 操作符来写写一个从用户输入构建数字列表的函数。一直到 "quit" 对于 `Lists` 来说效果很好，因为我们可以轻松地向 `List` 中添加新元素。对于 `Arrays` 则不是这样，我们必须将大小减半。该方法非常简单。

```scala
def inputList():List[Int] = {
  val in = readLine()
  if (in == "quit") Nil else in.toInt::inputList()
}
```

当我们通过分行输入 3, 4, 5 和 "quit" 并运行它时，可以看到它的效果。

```scala
scala> inputList()
res19: List[Int] 
```

可以通过放置索引像访问 `Array` 一样访问 `List` 的元素。然而，对于 `List` 来说，这通常是低效的。首选的方法（特别是对于大型列表）使用 `head` 和 `tail` 方法。`head` 方法返回第一个元素。`tail` 方法返回剩余部分。

```scala
> lst.head
res20: Int = 2
```

```scala
> lst.tail
res21: List = 3
```

使用这些方法，我们可以写一个处理 `List` 的函数，own `Array`。

```scala
def operateList(lst:List[Int], func:(Int,Int)->Int):Int = {
  if (lst == Nil) 0 else func(lst.head, operateList(lst.tail, func))
}
```

你可能会发现使用 `match` 语句会更安全。

```scala
def operateList(lst:List[Int], func:(Int,Int)->Int):Int = {
  lst match {
    case Nil => 0
    case h::t => func(h, operateList(t, func))
  }
}
```

注意，为了让它工作，`::` 操作符是右结合的。我们可能会发现 `变` 。。。。 运行，， 看到为什么。

## 6.4 更大的 Arrays 和 Lists： Fill 和 Tabulate

简单的创建 `Arrays` 和 `Lists` 的语法对于短序列很好。在 `Lists` 中，你可以使用 `::` 和递归函数构建，但有更简单的方法。`fill` 方法的示例可能如下。

```scala
scala Array.fill(10)
res24:Array[Int] = Array(4, 4, 4, 4, 4, 4, 4, 4, 4, 4)
```

```scala
scala List.fill(6)(23)
res25:List[Int] = List(23, 23, 23, 23, 23, 23)
```

```scala
scala List.fill(6)("hi")
res26:List[String] = List("hi", "hi", "hi", "hi", "hi", "hi")
```

这里的 `Array` 和 `List` 指的是所谓的“伴对象”，像所有对象一样，它们拥有方法。可以使用补全查看各种方法。你可能会注意到 `fill` 是如何调用的。它接受两个参数，但不是在一个带有逗号的参数列表中传递，而是通过两个参数列表传递。这被称为柯化（CURRYING）。我们将在 7.8 节详细讨论。第一个参数是我们在结果序列中需要的值，第二个提供值的。

关于 `fill` 的另一个注意点是，第二个参数是以特殊方式传递的，“按名传递”（pass-by-name）。这是 `Scala` 的一个非常强大的功能，将在下一节 7.9 中涵盖。目前，我们只需简单展示为什么它很重要。考虑以下两个例子。

```scala
> List.fill(5)(math.random)
res27:List[Double] = List(0.34276326027921, 0.8128658516345523, 0.6149601139661, 0.53806172408777, 0.705727808692085)
```

```scala
> Array.fill(3)(readInt)
res28:Array[Int] = Array(1, 2, 3)
```

# 使用 Scala 进行编程与问题解决简介

这些示例的行为可能更显而易见。如你所见，在第二个示例中，你输入了 1、2和3 作为值。这就是我们在本章开始时做的：将值读取到 `Array`（数组）或 `List`（列表）中的函数。事实证明当我们知道有多少个元素时，可以使用 `fill` 通过一行代码完成这一操作。

为了了解这里是如何使用名传（pass-by-name）的，请考虑以下函数，它的目的是类似于第一个示例填充一个 `List`。

```scala
def fillList(n:Int,x:Double):List[Double] = if (n==1) Nil else x :: fillList(n-1,x)
```

我们调用此函数时，传递了我们在 `List` 中需要的数字数量以及我们想要使用的值。如果我们用 5 和 `math.random` 调用它，会发生以下情况。

```scala
scala> fillList(5,math.random)
res29:List[Double] = List(0.5701406699076761, 0.5701406699076761, 0.5701406699076761, 0.5701406699076761, 0.5701406699076761)
```

与 `fill` 不同，此 `List` 中的所有值都是相同的。如果我们调用 `readDouble`，那么整个过程中只会读取一个值，并且所有元素都将拥有那个值。名传正是 `fill` 能够在这些示例中获取不同值的原因。

```scala
scala> Array.fill(4){ println("Evaluating argument"); 5 }
Evaluating argument
Evaluating argument
Evaluating argument
Evaluating argument
res30:Array[Int] = Array(5, 5, 5, 5)
```

请注意，第二个参数只被放在了大括号中。作为一条通用规则，`Scala` 允许你对只有一个参数的数组列表这样做。这是 `fill` 被调用的原因之一。你可以添加额外的圆括号，但你仍然需要大括号，因为这是一个包含两个表达式的代码块。这个示例具有说明性，但并不十分有用。一个更有趣的示例使用了 `var`。

```scala
scala> var i=1
Int: Int = 1
scala> List.fill(5){ i::= i }
res31:List[Int] = List(2, 4, 8, 16, 32)
```

这里 `var` 初始化为 1。值参数将 `i` 乘以 2 并将值存回。然后它将其作为要使用的值返回。你可以看到在某些情况下这可能有用，但这种用 2 的幂填充数组的方法可能会让大多数阅读你代码的人困惑。

`fill` 的主要局限性是代码通常不知道正在生成序列中的哪一个元素。有时这些信息是有用的。这就是存在 `tabulate` 方法的原因。`tabulate` 方法创建一个新的列表或数组，通过你应用于它的函数将每个元素填充为它的索引。`tabulate` 与 `fill` 类似，其第二个参数不是名传变量，而是一个接收 `Int` 并产生序列应填充的类型的函数。一个简单的示例是填充一个 `List`，其元素为索引的平方。这可以通过以下代码生成。

```scala
scala> List.tabulate(5)(i => i*i)
```

# Scala 中的 Arrays 和 Lists

res32: List[Int] = List(0, 1, 4, 9, 16)

一个更复杂的示例是填充一个 `Array`，其值为对每个索引求多项式的的结果。

```scala
scala> Array.tabulate(6)(x => 3*x*x+5*x-7)
res33: Array[Int] = Array(-7, 1, 15, 35, 6, 93)
```
