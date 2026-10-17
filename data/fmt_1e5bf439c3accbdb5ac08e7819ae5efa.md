
这填充了数组 `$3x^2-7$` 的值，其中 `$x$` 是索引：0, 1, 2, 3, 4 和 5。

> 注意：你也可以通过调用 `new` 创建更大的 `Array`。如果你有其他语言的经验，你可能熟悉这种方法。在 Scala 中，这通常不是推荐的方法，因为它容易导致某些类型的异常。

## 6.5 标准方法

现在你知道如何创建 `Arrays` 和 `Lists`。为了对它们进行操作，你需要知道可以使用哪些方法。Scala 集合的优势之一是它们拥有丰富的接口。接口是一组用于构建软件应用程序的协议、例程和工具。Scala 的接口包含许多不同的方法。我们查看了 `Array` 的 `length` 和 `size`，以及 `List` 的 `head` 和 `tail`，但这仅仅是冰山一角。你实际上可以在 `Lists` 或 `Arrays` 上调用它们。然而，`length` 和 `size` 对于 `Array` 来说高效的，而 `tail` 在 `Array` 上是低效的。在本节中，我们将列出处理 `Lists` 和 `Arrays` 时可以使用其他方法。我们将从基础开始。

### 6.5.1 基础方法

我们根据功能将方法分为几组。在每组中，方法都会返回一个与调用类型相同的新集合。因此，如果你在 `Array` 上调用它们，就会得到 `Array`；如果你在 `List` 上调用它们，就会得到 `List`。

- `drop(n)`：返回排除前 `$n$` 个元素的集合。
- `take(n)`：返回前 `$n$` 个元素的集合。
- `head`：返回集合的第一个元素。
- `tail`：返回排除第一个元素的集合。
- `init`：返回排除最后一个元素的集合。
- `last`：返回集合的最后一个元素。
- `size`：返回集合中的元素数量。
- `length`：返回集合中的元素数量。
- `slice(from, to)`：返回从 `from` 到 `to` 的集合子集。
- `contains(elem)`：如果集合包含该元素则返回真。
- `startsWith(seq)`：如果集合以指定的序列开头则返回真。
- `endsWith(seq)`：如果集合以指定的序列结尾则返回真。
- `isEmpty`：如果集合没有元素则返回真。
- `nonEmpty`：如果集合至少包含一个元素则返回真。
- `filter(p)`：返回仅包含满足谓词 `p` 的元素的集合。
- `map(f)`：返回一个每个元素都经过函数 `f` 的新集合。
- `fold(z, f)`：使用初始值 `z` 和二元函数将集合归约为单个值。
- `foldLeft(z, f)`：从左到右归约集合。
- `foldRight(z, f)`：从右到左归约集合。

`mkString` - 可以带零、一个或三个参数调用。它根据元素的字符串表示构建一个单一的长字符串。如果没有提供任何参数，则元素之间将无任何内容。如果指定了一个参数，它应该是一个用于分隔元素的字符串。如果指定了三个参数，中间的那个是分隔符，第一个和最后一个是放在元素之前和之后的字符串。

```scala
scala = lst.mkString
res55: String = 746391
```

```scala
scala = lst.mkString(" ")
res56: String = 7; 6; 3; 9; 1
```

```scala
scala = lst.mkString("[", ", "]")
res57: String = "[7, 4, 6, 3, 9]"
```

`patch` - 这一强大的方法允许你生成新的序列，这些序列是从原始序列中移除并插入的。它接受三个参数：开始补丁的索引、要放入补丁的元素、以及要用补丁替换的元素数量。如果替换项为空集合，它将简单地移除指定数量的元素。如果给定的元素为 0，则它仅会在给定位置插入新元素。

```scala
scala = lst.patch(3,Nil,2)
res58: List[Int] = List(7, 4, 6, 1)
```

```scala
scala = lst.patch(3,List(10,11,12),0)
res59: List[Int] = List(7, 4, 6, 10, 11, 12, 3, 9, 1)
```

```scala
scala = lst.patch(3,List(10,11,12),3)
res60: List[Int] = List(7, 4, 6, 10, 11, 12)
```

`reverse` - 接受参数并按反序产生一个新的集合。

```scala
scala = lst.reverse
res61: List[Int] = List(1, 9, 3, 6, 7)
```

`toArray` - 不接受参数，并根据当前集合中的元素创建一个指定类型的新集合。

```scala
scala = lst.toArray
res62: Array[Int] = Array(7, 4, 6, 3, 9)
```

`zip(that:Iterable[B])` - 接受另一个集合作为参数，并产生一个元组集合，其中第一个元素来自此集合，第二个元素来自传入的集合。结果的为两者中较短的一个。

```scala
scala = lst.zip(lst.reverse)
res63: List[(Int, Int)] = List((7,1), (4,9), (6,3), (3,6), (9,4), (1,7))
```

```scala
scala = lst.zip(Array(1, 2, 3, 4))
res64: List[(Int, Int)] = List((7,1), (4,2), (6,3), (3,4))
```

# Scala 中的数组和列表

- `zipIndex` – 接受参数并产生一个新的元组集合，其中第一个是集合中的元素，第二个是它的索引。

```scala
scala> lst.zipIndex
res65: List[(Int,Int)] = List((7,0), (4,1), (6,2), (3,3), (9,4), (1,5))
```

上述列出的方法适用于任何类型的序列。因此，它们可以适用于 `List[Int]`、`List[String]` 或 `Array[Double]`。有少数方法对元素类型有特殊要求（需要某些操作），这些是 `min`、`sum` 和 `product`。`min` 和 `max` 方法适用于可以排序的类型。它们包含了 `Int` 和 `Double`，还包括许多其他类型，而这些类型中 `sum` 和 `product` 方法要求集合是数值类型。我们可以像这里这样直接调用 `sum` 或 `product` 方法。

```scala
scala> lst.sum
res66: Int = 30
```

```scala
scala> lst.product
res67: Int = 45
```

值必须是数值类型的限制意味着你不能使用 `+` 来连接它们。对于 `List[String]` 或 `Array[String]`，你应该使用 `mkString` 来连接这些值。

## 6.5.2 高阶方法

虽然你可能觉得这里展示的方法列表很长，且并赋予了我们许多能力，但所有这些方法都是通过为参数添加普通值来实现的。就像我们的第一个方法一样，通过添加一些抽象并使它们成为高阶方法，它们可以变得强大。下面列出了许多属于 `List` 或 `Array` 中的类型 `B` 的方法。再次，这些示例使用了 `val lst = List(7,4,6,3,9)`。

- `count(p:(A)=>Boolean)` – 接受一个作用于元素并返回布尔值的函数。返回集合中所有返回 true 的元素数量。

```scala
scala> lst.count(_ > 5)
res68: Int = 3
```

- `dropWhile(p:(A)=>Boolean)` – 产生一个新的集合，包含从第一个返回 false 的元素开始的所有元素。

```scala
scala> lst.dropWhile(_ < 3)
res69: List[Int] = List(3, 9, 1)
```

# 编程与问题解决简介

- `exists(p:(A)=>Boolean)` - 接受一个作用于元素并返回布尔值的函数。如果集合中某个元素使函数结果为 true，则其值为 true。

```scala
scala lst.exists(_ 5 == 0)
res70: Boolean = true
```

- `filter(p:(A)=>Boolean)` - 接受一个作用于元素并返回布尔值的函数。产生一个包含所有使函数返回 true 的元素的新集合。

```scala
scala lst.filter(_ < 5)
res72: List[Int] = List(3, 9, 1)
```

```scala
scala lst.filter(x > 4)
res73: List[Int] = List(7, 4, 6)
```

- `filterNot(p:(A)=>Boolean)` - 接受一个作用于元素并返回布尔值的函数。产生一个包含所有使函数返回 false 的元素的新集合。

```scala
scala lst.filterNot(_ < 5)
res75: List[Int] = List(7, 6)
```

```scala
scala lst.filterNot(_ > 7)
res76: List[Int] = List(3, 9, 1)
```

- `flatMap(f:(A)=>Seq[B])` - 接受一个作用于元素并返回集合的函数。从所有函数返回的集合中构建一个新的集合。

```scala
scala lst.flatMap(n => if (n<6) n else Nil)
res78: List[Int] = List(7, 4, 6, 3, 9)
```

```scala
scala val str = "test"
scala lst.flatMap(str.take)
res79: List[Char] = List(t, e, s, t)
```

- `forAll(p:(A)=>Boolean)` - 接受一个作用于元素并返回布尔值的函数。如果集合中所有元素使函数结果为 true，则其值为 true。传入 `flatMap` 的返回类型实际上比 `Seq[B]` 更通用，但差别并不大。

```scala
scala lst.forall(_ > 2)
res80: Boolean = false
```

```scala
scala lst.forall(_ < 10)
res81: Boolean = true
```

- `foreach(f:(A)=>Unit)` – 接受一个作用于元素并应用于集合中所有元素的函数。返回类型为 `Unit`。此方法用于副作用。

```scala
scala lst.foreach(n=>println(n))
14
8
18
2
```

- `indexWhere(p:(A)=>Boolean)` - 接受一个作用于元素并返回布尔值的函数。返回第一个使函数返回 true 的元素的索引值。

```scala
scala lst.indexWhere(_ 2 == 0)
res82: Int = 1
```

```scala
scala lst.indexWhere(_ > 7)
res83: Int = 4
```

- `lastIndexWhere(p:(A)=>Boolean)` – 接受一个作用于元素并返回布尔值的函数。返回最后一个使函数返回 true 的元素的索引值。

```scala
scala lst.lastIndexWhere(_ 2 == 0)
res84: Int = 2
```

- `map(f:(A)=>B)` – 接受一个作用于元素并产生结果的函数。产生一个包含将函数应用于集合所有内容后的结果的新集合。

```scala
scala lst.map(_ + 1)
res85: List[Int] = List(8, 5, 7, 4, 10, 2)
```

```scala
scala lst.map(_ * 2)
res86: List[Int] = List(14, 8, 12, 6, 18, 2)
```

```scala
scala lst.map(i => i * i)
res87: List[Int] = List(49, 16, 36, 9, 81, 1)
```

# 使用 Scala 进行编程与问题解决

```scala
scala lst.partition(_ < 5)
res88:(List[Int], List[Int]) = (List(4, 3, 1),List(7, 6, 9))
```

```scala
scala lst.partition(_ % 2 == 0)
res89:(List[Int], List[Int]) = (List(4, 6),List(7, 3, 9, 1))
```

- `takeWhile(p:A)=>Boolean` - 接收一个作用于元素并返回布尔值的函数。产生一个包含所有该函数为真的开头元素的新列表。

```scala
scala lst.takeWhile(_ < 3)
res90:List[Int] = List(7, 4, 6)
```

虽然第一组方法直观易懂，但这组方法需要更多的解释。我们将关注 `map` 和 `filter`，因为它们在函数式编程世界中非常标准。假设我们有一个人名的列表或数组。这个列表可能很长，但为了我们的示例，我们只需要使用几个来演示。名字采用人们书写的普通格式：“名 姓”，中间名是可选的或者可能有多个名字。为了编程目的，我们希望格式是“名 姓 中间名”，因为我们经常关心姓氏。我们在这里描述了应用一个函数来获取一个带有修改后元素的新序列。这正是 `map` 方法为我们所做的。我们都必须弄清楚如何写一个函数来进行转换，然后用 `map` 使用它。我们想要做的转换是取名字中的最后一个单词并将其移动到前面，在它和名字之间加上逗号和空格。基本上，我们想根据最后一个空格分割字符串。如果上述列的方法作用于 `String`，它们可以很好地完成这一点。事实证明，我们可以视为字符序列。因此，我们可以使用 `indexOf` 找到空格并使用 `split` 生成两个 `String`。我们可以在这里特定的字符串上看到这一点。

```scala
scala val name="Mark C. Lewis"
name: String = "Mark C. Lewis"
```

```scala
scala name.split(name.lastIndexOf(' ')+1)
res91:(String, String) = ("Mark C. ", "Lewis")
```

现在我们只需要以相反的顺序并加上逗号和空格将它们重新组合。
如果我们频繁地重命名名字，可以将这段代码放在一个独立函数中。如果没有，我们可以使用函数字面量来定义它。在这个示例中，我们将使用后一种方法。

```scala
scala val names=List("Mark C. Lewis", "Lisa L. Lacher", "Jason C. Hughes", "Glen R. Stewart","Jen Hogan")
names: List[String] = List("Mark C. Lewis", "Lisa L. Lacher", "Jason C. Hughes", "Glen R. Stewart", "Jen Hogan")
```

```scala
scala val names=names.map(n =>
  val (rest,last)=n.splitAt(n.lastIndexOf(' ')+1); last+", "+rest.trim())
names: List[String] = List("Lewis, Mark C.", "Lacher, Lisa L.", "Hughes, Jason C.", "Stewart, Glen R.", "Hogan, Jen")
```

# Scala 中的数组和列表

因此，`map` 的使用允许我们以快速快捷的方式完成任务，而如果使用其他方法可能需要大量的代码。

如果你有一个这些名字的列表，你可能想做一些事情，比如找到所有姓氏以特定字母开头的人。例如，我们可能想找到所有姓氏以 'H' 开头的人。为此，我们想要使用 `filter` 函数。`filter` 函数将筛选出满足某些条件的元素并给我们一个只包含这些值的序列。

```scala
scala names= names.filter(_.startsWith("H"))
```

多亏于 `filter` 和 `startsWith` 方法，这是一个非常简单的单行代码。

## 6.5.3 reduce 和 fold

还有其他没有在上面列出的方法，因为它们需要更多的解释。如果你一直跟到这里，理解它们应该并不困难，因为它们与在本章中通过 `operateArray` 和 `operateOnList` 函数所的操作完全相同。我们将从 `reduce` 方法开始，`reduceLeft` 和 `reduceRight`。这些方法接收一个作用于序列元素并返回类型值结果的函数。`reduce` 方法反复地将函数应用到连续元素上，与 `operateArray` 和 `operateOnList` 方法相同。两者的区别在于它们是从左到右还是从右到左应用操作。如果操作是结合律的（例如加法或乘法），则不会影响结果，可能会影响效率。对于非结合律操作，这可能会很重要。这里是使用我们定义的第一个变量 `List(7,4,6,3,9,1)` 的几个示例。

```scala
scala= lst.reduceLeft(_ + _) // Means 7+4+6+3+9+1
res93: Int = 30
```

```scala
scala= lst.reduceLeft(_ * _) // Means 7*4*6*3*9
res94: Int = 4536
```

```scala
scala= lst.reduceLeft(_ - _) // Means 7-4-6-3-9-1
res95: Int = -16
```

```scala
scala= lst.reduceRight(_ - _ ) // Means 7-(4-(6-(3-(9-1)))))
res96: Int = 14
```
