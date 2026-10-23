

现在我们将学习 Set、Map 和 Buffer 类型。这些类型能显著提升你的编程效率，并使某些任务的完成变得容易得多。

## 20.2 Set

集合（Set）的概念源自数学。Set 类型与 Seq 类型之间有两个主要区别。最重要的一点是 Set 不允许包含重复值。如果你向一个 Set 添加某个元素，而其中已经有一个与之相等的元素，那么它不会添加新值，最终集合的大小与之前相同。另一个区别是 Set 中元素的顺序是不保证的。¹ 我们可以在下面的一系列 REPL 命令中看到这两种效果。

¹ 如果你碰巧使用的是 SortedSet，那么对象的顺序将与类型的自然顺序一致，但这属于例外情况而非普遍规律。

```scala
scala> Set(1,2,3)
res0: scala.collection.immutable.Set[Int] = Set(1, 2, 3)

scala> res0 + 4
res1: scala.collection.immutable.Set[Int] = Set(1, 2, 3, 4)

scala> res1 + 2
res2: scala.collection.immutable.Set[Int] = Set(1, 2, 3, 4)

scala> res1 + -10
res3: scala.collection.immutable.Set[Int] = Set(-10, 4, 1, 2, 3)
```

这里从一个包含值 1、2 和 3 的集合开始。与 List 和 Array 类型一样，Scala 会推断出这是一个 `Set[Int]`。你还可以从推断出的类型中看到，默认情况下我们得到的是一个不可变集合。

你可以使用 `+` 向集合中添加元素，你会得到一个新集合，其中包含了加号后面的那个元素。第二条语句返回的集合在 1、2、3 之外还包含了 4。在第三条命令中，我们向这个新集合添加了一个 2。结果看起来与添加 2 之前的集合相同。这是因为集合不能包含重复元素。

最后一条语句将值 -10 添加到了 res1 的集合中。由于之前没有 -10，这个值被加入了结果集合。然而，结果显示集合中并不保留顺序。将 -10 加入集合不仅把它放到了开头这个奇怪的位置，还改变了 4 在集合中的位置。由此你可以看出，当你关心的是元素的唯一性而非获取它们的顺序时，才应该使用集合。

顺序可能改变这一事实意味着，像我们对 Array 或 List 所做的那样对集合进行“索引”意义不大。你可以对 Set 执行此类操作，但含义略有不同。请考虑以下示例。

```scala
scala> res3(2)
res4: Boolean = true

scala> res3(5)
res5: Boolean = false

scala> res3(-10)
res6: Boolean = true
```

对集合进行这种操作不会返回某个特定位置的值。相反，它返回一个 Boolean，告诉你指定的值是否在集合中。如果集合包含的是 Int 以外的值，这种方式也同样有效。请考虑以下情况。

```scala
scala> val strSet=Set("Mark","Jason","Kevin")
strSet: scala.collection.immutable.Set[java.lang.String] = Set(Mark, Jason, Kevin)

scala> strSet("Jason")
res7: Boolean = true

scala> strSet("Bill")
res8: Boolean = false
```

在这个示例中，集合包含 String，“索引”通过传入 String 来完成。两种方式的含义相同。如果传入的参数在集合中，返回值就是 true，否则就是 false。要理解为什么是这样，请到 Scala API 中查看 Set 的某个版本。它们都有一个名为 A 的类型参数，并定义了以下方法。

```scala
def apply (elem: A): Boolean
```

记住，apply 是一个特殊方法，当对象以函数调用语法使用时会被调用。因此 Scala 中的 f(5) 会被展开为 f.apply(5)。这里的 apply 接收一个参数 elem，其类型必须为 A。这是整个集合的类型参数，所以你必须传入一个集合所包含类型的对象。然后该方法返回一个 Boolean，告诉你该值是否在集合中。

### 20.2.1 遍历集合

除了 map、filter 和 foreach 等标准高阶方法（这些方法对 Set 和之前使用过的序列都可用）之外，Set 类型同样可以很好地与 for 循环配合使用。

```scala
scala> for(v <- res3) println(v)
1
2
-10
3
4
```

事实上，你无法真正使用 while 循环来遍历 Set，因为你不能按位置索引。而且，循环遍历集合值的顺序也是你无法预测的。它甚至不必与 Set 被转换为字符串打印时值的显示顺序一致。

### 20.2.2 可变与不可变

上面的示例展示的是默认的不可变 Set 类型。与我们之前见过的 List 类型一样，不可变集合在创建之后不会改变。当我们使用 `+` 运算符向集合添加元素时，我们得到一个新集合，原集合保持不变。我们可以通过重新调用原集合来证明这一点。

- `--=(xs : TraversableOnce[A])` - 从集合中移除 xs 中的所有元素。
- `add(elem : A) : Boolean` - 向集合添加指定元素。如果在调用之前不存在该元素则返回 true，否则返回 false。
- `clear() : Unit` - 从集合中移除所有元素。
- `remove(elem : A) : Boolean` - 从集合中移除指定元素，如果该元素存在并被移除则返回 true，否则返回 false。
- `retain(p : (A) => Boolean) : Unit` - 从集合中移除所有不满足谓词的元素。

可变集合还可以使用赋值来进行更新。这基本上是我们之前用 apply 看到的“索引”操作的逆操作。索引是你正在集合中调整的值，而赋值要么是 true 要么是 false。要了解其工作原理，请考虑以下示例。

```scala
scala> mset(7)=true

scala> mset(2)=false

scala> mset
res14: scala.collection.mutable.Set[Int] = Set(1, 4, 7, 3)
```

第一行将 7 添加到集合中，而第二行移除了 2。这是可行的，因为 `scala.collection.mutable.Set` 类型定义了一个如下所示的 update 方法。

```scala
def update (elem: A, included: Boolean): Unit
```

因此 `mset(7)=true` 这一行会被展开为 `mset.update(7,true)`。

本节前面提到过，map 和 filter 等标准方法在可变集合上的行为与在不可变集合上相同。这是有意为之的。像这样的子类型上的相同操作始终应该具有相同的外部表现和显著效果。这降低了程序员犯低级错误的几率。如果你想修改集合，就必须调用相应的专用方法。例如，你应该调用 retain 而不是 filter。如果你意外地对不可变类型使用这些操作之一，代码将无法编译。如果同名操作具有不同的行为，程序员就很容易引入逻辑错误，因为他/她认为一个对象是某种类型而实际上却是另一种类型，或者后来程序员改变了赋给变量的具体类型时也会引入 bug。

### 20.2.3 使用集合

为了了解 Set 类型的实用性，我们将编写一个函数，它告诉我们文本文件中所有唯一的单词。该函数将文件名作为参数，并返回一个包含所有小写单词的 `Set[String]`。与任何具有一定复杂度的函数一样，实现方式有很多种。我们将大量使用 Scala 的集合方法来完成。由于我们使用了集合方法，使用 Source 比使用 Scanner 更为合理。下面是可以实现此功能的代码。

```scala
def uniqueWords(fileName:String):Set[String] = {
  val source = io.Source.fromFile(fileName)
  val words = source.getLines.toSeq.flatMap(_.split(" +"))
    .map(_.filter(_.isLetter).toLowerCase).toSet
  source.close()
  words
}
```

使用所描述的签名定义了一个函数。该函数只包含四条语句。函数中的第一条和第三条语句负责打开和关闭文件。最后一条语句只是一个表达式，返回从源数据创建的集合。第二条语句完成了所有主要工作，值得详细研究。

这一行声明了变量 words，并使其等于一个单词集合。为此，它从 Source 中获取行并将它们转换为序列。toSeq 调用使类型与 flatMap 更好地配合。你可能还记得，getLines 返回一个 Iterator。Iterator 类型是一种只能遍历一次的集合，在遍历过程中它会被消耗殆尽。通过将其提升为序列，我们得到的东西能更好地与 split 方法返回的 `Array[String]` 配合。

行被转换为序列之后，有一个对 flatMap 的调用。这是集合上标准的高阶方法之一。我们之前用得不多，所以值得花一点时间讨论一下。从名称可以看出，flatMap 与 map 密切相关。map 方法对集合中的每个元素应用某个函数，并创建一个包含该函数应用结果的新集合。flatMap 做的事情基本相同，只是它期望传入的函数返回集合。与 map 返回集合的集合不同，flatMap 会将所有内部集合展开成一个长的集合。如果你对行的序列使用 map 并使用相同的映射函数，你会得到一个 `Seq[Array[String]]`。序列中的每个元素将包含该行单词的数组。然而，这并不是我们想要的。我们想要的是一个简单的单词序列，而不是单词数组的序列。这正是 flatMap 为我们做的事情。它将每个数组首尾相接放入新序列中，从而得到一个 `Seq[String]`。

如果我们知道文件只包含简单的小写单词，就可以到此为止了。然而，大多数文本文件还会包含大写字母和标点符号。这会打乱集合，因为“Hi”不等于“hi”，当我们只想要一个时，两者都会出现在结果中。类似地，如果单词恰好出现在标点符号之前，单词“dog”也会与“dog.”或“dog,”不同。第二条语句的第二行包含了处理这一问题的逻辑。文件被拆分出的每个单词都会经过一个 map。该 map 过滤掉任何非字母字符，并将结果字符串转换为小写。过滤非字母字符的做法可能过于激进，因为它会移除缩略词中的撇号等内容，但它提供的结果对于我们当前的目的而言已经足够正确了。

第二条语句中最后做的事情是将序列转换为 Set。这给了我们想要的类型，并凭借 Set 的特性移除了所有非唯一元素。

## 20.3 Map

另一种极其有用的集合类型是 Map，在大多数程序中它可能比 Set 更常用。与 Set 一样，术语 Map 也起源于数学。数学中的映射是指从一个集合中取值并返回另一个集合中的值。数学中的函数在技术上就是一种映射。Map 集合类型与此并没有太大不同

