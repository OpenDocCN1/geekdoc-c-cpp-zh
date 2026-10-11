
前两个展示了我们在取列表和和结果后看到的内容。最后两个是差异（减法不是结合律），以及 `reduce` 方法是如何给我们 `(((7)-4)-(6)-3)-9` 的。`reduceRight` 给我们的是 `7-(4-(6-(3-(9)))`。

在上一章中，我们使用了一个递归方法，可以使用用户输入执行这些类型的操作。这与在本章中所做的不同，在本章中我们必须传递一个额外值在用户终止递归时使用。递归开启了其他可能性。我们没有对它做任何特殊处理。`reduce` 操作两个参数必须作用于集合的元素类型，因为函数的第一次调用使用了集合中的两个元素。如果我们指定了基值，我们

> 由于计算机内存存储 `List` 的方式，`reduceLeft` 方法在 `List` 上比 `reduceRight` 高得多。

> 还有一个通用的 `reduce` 方法，应该只使用结合律函数调用。

## Scala 153 中的数组与列表

`List(7, 4, 3)`
`List(7, 4, 9)`
`List(7, 4, 1)`
`List(7, 6, 3)`
`List(7, 6, 9)`
`List(7, 6, 1)`
`List(7, 3, 9)`
`List(7, 3, 1)`
`List(4, 6, 3)`
`List(4, 6, 9)`
`List(4, 6, 1)`
`List(4, 3, 9)`
`List(4, 3, 1)`
`List(4, 9, 1)`
`List(6, 3, 9)`
`List(6, 3, 1)`
`List(6, 9, 1)`
`List(3, 9, 1)`

- **`grouped(size:Int)`** – 遍历序列，将项目按指定的大小分组。

```scala
scala> lst1.grouped(2).foreach(println)

List(7, 4)

List(6, 3)

List(9, 1)
```
```scala
scala> lst1.grouped(3).foreach(println)

List(7, 4, 6)

List(3, 9, 1)
```

- **`inits`** – 提供一个从完整序列到空序列的迭代器，从末尾移除元素。正如其名，它与 **`init`** 方法有关，该方法返回一个不包含最后一个元素的序列。

```scala
scala> lst1.inits.foreach(println)

List(7, 4, 6, 3, 9, 1)

List(7, 4, 6, 3, 9)

List(7, 4, 6, 3)

List(7, 4, 6)

List(7, 4)

List(7)

List()
```

- **`permutations`** – 允许你遍历序列的所有排列。注意，这里的示例只对前三个元素进行排列，因为完整列表有 `6! = 720` 种排列。这同时也解释了为什么该方法返回一个 `Iterator`。如第 4 章所示，阶乘函数增长非常快，因此如果一次性创建所有排列，即使是对中等规模序列调用 **`permutations`**，消耗的内存也会超过任何计算机所拥有的内存。

```scala
scala> lst1.take(3).permutations.foreach(println)
```

## 154 使用 Scala 进行编程与问题解决

`List(7, 4, 6)`
`List(7, 6, 4)`
`List(4, 7, 6)`
`List(4, 6, 7)`
`List(6, 7, 4)`
`List(6, 4, 7)`

- **`sliding(size:Int)`** 提供一个迭代器，实现特定窗口在序列上滑动的效果。

```scala
scala= lst.sliding(2).foreach(println)

List(7, 4)

List(4, 6)

List(6, 3)

List(3, 9)

List(9, 1)
```
```scala
scala= lst.sliding(3).foreach(println)

List(7, 4, 6)

List(4, 6, 3)

List(6, 3, 9)

List(3, 9, 1)
```

- **`tails`** 提供一个迭代器，从完整序列开始，到空序列结束，每一步从左端移除一个元素。这基本上是 `inits` 的反向，并与 `tail` 方法密切相关。

```scala
scala= lst.tails.foreach(println)

List(7, 4, 6, 3, 9, 1)

List(4, 6, 3, 9, 1)

List(6, 3, 9, 1)

List(3, 9, 1)

List(9, 1)

List(1)

List()
```

如果你想对迭代器给出的值进行更复杂的操作，可以使用 `toList` 将其转换为 `List` 或 `Array`。然而，由于元素非常多（例如在 `permutations` 的情况所示），在转换之前你可能需要对其进行过滤或执行其他操作以缩小范围。例如，我们可以对 `lst` 的排列进行过滤，只保留那些具有最大值的排列。这过滤掉了大部分结果，因此它可以从 `Iterator` 转换为 `List`。

```scala
scala= lst.permutations.filter(_.take(3) > 20).toList

res100:List[List[Int]]=List(7, 6, 9, 4, 3, 1), List(7, 6, 9, 4, 1, 3), List(7, 6, 9, 3, 4, 1), List(7, 6, 9, 3, 1, 4), List(7, 6, 4, 9, 3, 1), List(7, 6, 4, 3, 9, 1), List(7, 6, 3, 9, 4, 1), List(7, 6, 3, 4, 9, 1), List(7, 6, 1, 9, 4, 3), List(7, 6, 1, 4, 9, 3), List(7, 6, 1, 3, 9, 4), List(6, 7, 9, 4, 3, 1), List(6, 7, 9, 3, 4, 1), List(6, 7, 9, 1, 4, 3), List(6, 7, 4, 9, 3, 1), List(6, 7, 4, 3, 9, 1), List(6, 7, 4, 1, 9, 3), List(6, 7, 3, 9, 4, 1), List(6, 7, 3, 4, 9, 1), List(6, 7, 3, 1, 9, 4), List(6, 6, 7, 9, 4, 3), List(6, 6, 7, 4, 3, 1), List(6, 6, 7, 3, 9, 4), List(6, 6, 7, 1, 9, 3), List(6, 6, 4, 9, 3, 1), List(6, 6, 4, 3, 9, 1), List(6, 6, 4, 1, 9, 3), List(6, 6, 3, 9, 4, 1), List(6, 6, 3, 4, 9, 1), List(6, 6, 3, 1, 9, 4), List(6, 6, 1, 9, 4, 3), List(6, 6, 1, 4, 9, 3), List(6, 6, 1, 3, 9, 4)
```

## Scala 中的数组

`List(9, 7, 6, 3, 4, 1), List(9, 7, 6, 3, 4, 1), List(9, 7, 6, 1, 4, 3),`
`List(9, 7, 6, 1, 3, 4), List(9, 6, 7, 4, 3, 1), List(9, 6, 7, 4, 1, 3), ...`

这些方法提供了一种对数据进行更有趣处理简单方法。例如，使用 `sliding`，你可以通过对填充了随机数的窗口取平均值来快速平滑噪声数据。注意输出永远不会低于 `0.4` 或高于 `0.82`，而原始随机数据的值更接近 `0.0` 和 `1.0`。

```scala
scala Array.fill(20)(math.random).sliding(5).map(_.sum/5).toArray

res101: Array[Double] = Array(0.406886956682401, 0.4201066221912837,

0.4600266221912837,
```

## Scala 中的数组与列表

打印菜单是一个显而易见的功能。我们已经看到，可以编写函数来计算简单平均值、排除最低分后的平均值，以及计算最终平均值。

这打破了功能的完整性。如果你走到键盘前并开始输入，你会很快发现 `significant`（变量）足以跳出设计范围：我们为什么要存储分数。有许多方法可以实现这一点，但考虑到我们唯一的功能是添加分数和计算平均值，解决方案是非常清晰的。我们唯一的选择是数组（`Arrays`）和列表（`Lists`）。数组的大小固定的，添加元素的效率低下。这对于本应用程序并不理想，因为我们将添加分数，且没有指定会有多少。所以列表（`Lists`）更合理。我们将使用三个列表来存储三种不同类型的成绩。如果我们使用命令式风格，列表将在递归函数之前用 `var` 声明。如果我们使用函数式风格，它们将传递给下一次调用进行迭代。我们将查看这两种方式以说明区别。大多数函数不会受到这种区别的影响。

这为我们的应用程序提供了一个相当不错的设计。现在我们转向实现。以下是使用命令式方法并对列表进行 `var` 声明的完整脚本列表。

### Listing 6: GradesImperative.scala

```scala
import io.StdIn._

def average(nums:List[Double]):Double = nums.sum/nums.length

def averageDropMin(nums:List[Double]):Double = (nums.sum-nums.min)/(nums.length-1)

def fullAverage(tests:Double, assignments:Double, quizzes:Double):Double = 0.4*tests + 
0.4*assignments + 0.2*quizzes

def courseAverage(tests:List[Double],assns:List[Double], quizzes:List[Double]):Double = {
  val testAve=average(tests)
  val aveAssn=average(assns)
  val aveQuiz=averageDropMin(quizzes)
  fullAve(testAve,aveAssn,aveQuiz)
}

def printMenu:Unit = {
  println("Select one of the following options:")
  1. Add a test grade.
  2. Add a quiz grade.
  3. Add an assignment grade.
  4. Calculate average.
  5. Quit("")
}

var tests = List[Double]()
var quizzes = List[Double]()
var assignments = List[Double]()

def mainGrades:Unit = {
  printMenu
  readInt() match {
    case 1 =>
      println("Enter a test grade.")
      tests = readDouble() :: tests
    case 2 =>
      println("Enter a quiz grade.")
      quizzes = readDouble() :: quizzes
    case 3 =>
      println("Enter an assignment grade.")
      assignments = readDouble() :: assignments
    case 4 =>
      println("The average is "+caseAverage(tests,assignments,quizzes))
    case 5 =>
      return
    case =>
      println("Unknown option. Try again.")
  }
  mainGrades
}

mainGrades
```

平均值的计算是由前四个函数完成的，从计算数字列表平均值的通用函数（以及排除最低分的平均值函数）开始。接下来是打印菜单的函数。这里唯一感兴趣点是使用三引号字符串，它可以使得字符串跨越多行。如果你不这样做，就必须使用 `\n` 来表示换行。

这些函数在命令式和函数式解决方案中是相同的。在这个命令式版本中，`printMenu` 函数之后是三个变量的声明。它们都是 `vars`，类型为 `List[Double]`。它们必须是 `vars` 是因为 `List` 是不可变的。因此，每当添加内容时，我们更改变量引用并指向一个新的 `List`。记住，这对于 `List` 类型可以高效完成，所以那行没问题。

如果你输入这些并尝试运行，你会发现表现得很糟糕。如果你在没有输入测试分数的情况下打印成绩，代码将会崩溃，因为 `List` 上的 `min` 方法至少一个元素来找到最小值。如果你在没有测试或作业，或只有一个测验分数时打印成绩，你可能会在询问平均值时得到如下输出：

The average is NaN

这应该会导致两个问题。首先，这叫什么 NaN？其次，是什么导致了这个问题？从技术上说，后者更，因为我们需要知道如何修复它。然而，知道第一个问题的答案可以帮助你在无法通过测试发现问题时解决它。`Double` 类型正如我们之前讨论过的，用于表示带有小数部分的数值。它具有很大的范围和良好的精度，但从技术上说它是固定精度的类型。你无法用它表示任何实数。此外，某些数学运算会产生未定义的结果。考虑以下情况。

```scala
scala> 1.0/0.0

res102: Double = Infinity

scala> -1.0/0.0

res103: Double = -Infinity
```

你应该在数学课上学过不能除以零。如果你对 `Int` 这样做，你会得到一个错误。但是，如果你对 `Double` 这样做，你会得到你看到的结果。

## Scala 中的数组与列表

这一切与 NaN 有什么关系？NaN 代表 "Not-a-Number"（不是数字），它是某些操作的结果。考虑这个：

```scala
scala> 0.0/0.0

res104: Double = Infinity
```

这就是导致我们错误的原因，它发生在没有输入任何测试或作业分数，或只输入了一个分数时。通常情况下，计算机不知道这是否会超出范围，因此它放弃了。函数返回 `(x-x)/(x-1)`，其中 `x` 是 `Double`。我们如何修复这个问题？我们需要让 `average` 和 `averageDropMin` 函数稍微特殊一点，以便我们有特殊它们不应执行除法的情况。我们可以通过在两者中放入表达式来实现。

```scala
def average(nums:List[Double]):Double = =
if (nums.isEmpty) 0 else nums.sum/nums.length

def averageDropMin(nums:List[Double]):Double = =
if (nums.isEmpty || nums.tail.isEmpty) 0 else
(nums.sum-nums.min)/(nums.length-1)
```

使用这些版本的函数，一切运行良好。现在来看函数式的替代方案。命令式版本在函数外部使用了 `var` 声明。这些声明可以被随后的任何内容看到。我们正式地称之为全局作用域（GLOBAL SCOPE）。对于小型脚本这可能不是问题，但我们不想养成把事物全局化的习惯，特别是当它是 `var` 或可变的时。大型程序中的全局变量可能会被任何行代码破坏，使得追踪某些类型的错误变得非常困难。最好将变量声明在局部作用域（LOCAL SCOPE），即函数内部。

如果我们简单地在 `mainGrades` 内部声明变量，当你进行递归调用时它将不起作用，你会得到所有局部变量的新版本。相反，我们将三个列表作为参数传递给函数。函数的参数的作用就像局部 `val` 声明，只是值是由调用代码提供的。这个版本不包含任何 `var` 声明，也不会有任何可变值，因为所有内容都存储在不可变列表中。所以除了打印之外，它是完全

# 使用 Scala 进行编程与问题解决介绍

函数式的。这样的函数看起来可能如下，以及我们如何调用它来使脚本工作。

```scala
def mainGrades(tests:List[Double],assignments:List[Double],
quizzes:List[Double]):Unit = {
  printMenu
  readInt() match {
    case 1 =>
      println("Enter a test grade.")
      mainGrades(readDouble() :: tests,assignments,quizzes)
    case 2 =>
      println("Enter a quiz grade.")
      mainGrades(tests,assignments,readDouble() :: quizzes)
    case 3 =>
      println("Enter an assignment grade.")
      mainGrades(tests,readDouble() :: assignments,quizzes)
    case 4 =>
      println("The average is "+courseAverage(tests,assignments,quizzes))
      mainGrades(tests,assignments,quizzes)
    case 5 =>
```
