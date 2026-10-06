
此函数还展示了大多数 while 循环中常见的另一个元素，它可能导致常见的 bug。`i += 1` 这一行是循环的递增器（迭代器）。它从循环中的一个情况移动到下一个，以便循环最终终止。常见的 bug 是不小心遗漏迭代器。考虑一下这样做会发生什么。如果没有 `i += 1` 这一行，`i` 的值将永远不会改变。结果就是条件永远不会改变，如果初始为真，它将一直保持为真。这会导致无限循环，即永远不会退出的循环。在 while 循环中很容易代码代码引入这种错误，因为循环的结构中没有包含任何提醒你包含递增器的内容。while 循环需要变量变更，且容易出现 bug，这意味着我们只有在发现有充分理由时才会使用它。通常的理由是我们需要多次执行某些操作，但在循环开始之前，我们不知道要执行多少次，而且我们不想写递归函数¹

## 8.2 do-while 循环

Scala 提供了第二个与 while 循环密切相关的构造结构。它是 do-while 循环。do-while 循环的语法如下。

```
do {
  statements
} while (condition)
```

在技术上这里大括号不是必须的，但很少看到不带大括号的 do-while 循环。再次，语句的作用完全如其名称描述的那样。当条件为真时，它将执行语句。

鉴这看起来与普通的 while 循环如此相似，你可能会想知道区别在哪里。区别体现在布局上。普通的 while 循环在执行循环体内的语句之前检查条件。do-while 循环在执行循环体之后检查条件。结果是，do-while 循环体始终会至少执行一次。

do-while 循环在编程中并不常用。它只在循环的“事后检查”（POST-check）性质很有帮助，且你希望循环内容始终发生一次的情况下才会使用。一个常见的例子是：你需要读取用户想要什么然后对其进行操作的应用。循环是否应该执行取决于用户选了哪个选项。

第 6 章末尾的 `mainGrades` 函数就是这样一个例子。在本章中，我们使用递归编写了程序，因为那是我们唯一知道让程序以未知次数重复执行相同代码的方法。这个函数可以转换为使用 do-while 循环，结果可能如下：

```
def printMenu():Unit = {
  println("Select one of the following options:")
  1. Add a test grade.
```

> 如果递归函数不是“尾递归的”，那么当操作发生几千次时，while 循环将更优。

# 使用 Scala 进行编程与问题解决简介

- 2. 添加测验成绩。
3. 添加作业成绩。
4. 计算平均分。
5. 退出("")

``````
def mainGrades {
  var tests = List[Double]()
  var assignments = List[Double]()
  var quizzes = List[Double]()
  var option = 0

  do {
    printMenu
    option=readInt()
    option match {
      case 1 =>
        println("Enter a test grade.")
        tests ::= readDouble()
      case 2 =>
        println("Enter a quiz grade.")
        quizzes ::= readDouble()
      case 3 =>
        println("Enter an assignment grade.")
        assignments ::= readDouble()
      case 4 =>
        println("The average is "+courseAverage(tests,assignments,quizzes))
      case 5 =>
      case =>
        println("Unknown option. Try again.")
    } while (option != 5)
}
```

使用这种写法还是第 6.6 节的代码，主要是一个风格问题。大多数开发者可能默认编写这个版本，但那主要是因为大多数开发者具有命令式编程背景，并出于熟悉的原因而倾向于这种方法。习惯于函数式编程的程序员会更倾向于递归的形式。和 while 循环一样，do-while 循环需要变量变更，并且容易出现忘记递增的问题，从而导致无限循环。

## 8.3 for 循环

while 循环在逻辑上是最简单的循环，但它并不是语言中最常用的循环。在那些提供了 for 循环的语言中，它通常是最常用的循环。Scala 中的 for 循环与许多其他语言中提供的略有不同，但你可能会发现，当你要在代码中引入迭代时，你会求助于它。
在语言中，for 循环的自然用法是计数，因此我们将从这里开始

# 循环 207

一个从 1 计数到 10 并打印值的 for 循环在 Scala 中的写法如下。

```
for (i <- 1 to 10) {
  println(i)
}
```

名字 `i` 是一个变量名，就像你在 Scala 中使用 `val` 声明的一样。因此，你可以称它任何名字。对于计数循环，使用 `i`、`j` 和 `k` 作为名字非常常见。然而，任何名字都可以，但在使用其他变量名时，如果你的选择能向阅读代码的人传达信息，方便他们理解会更好。在变量名之后是一个由连字符和减号组成的向左箭头。你会在 Scala 所有的 for 循环中看到它。你可以将其读作“in”。之后是一个你应该能够读懂的良好表达式。我们将详细讨论这具体意味着什么。你可以将该 for 循环读为类似“在 1 到 10 之间”。

正如我们在第 6 章看到的，Scala 集合中的索引不是从零开始计数的。因此，你不会从 1 计数到 10。相反，我们通常从 0 计数到 9。这在 Scala 中可以通过将 `1 to 10` 替换为 `0 to 9` 来。然而，从零开始并表示你想遍历的元素数量是非常常见的。出于这个原因，你可以使用 `until` 代替 `to`，这在 Scala 中同样有效。

```
for (i <- 0 until 10) {
  println(i)
}
```

使用 `until` 会导致计数在列出的最后一个值之前结束。
Scala 中的 `for-in` 不仅仅是计数。事实上，这种用法在 Scala 中某种程度上是一个特例。通常情况下，Scala 中 for 循环中读取 `<-` 的表达式可以评估任何类型的集合。在其他语言中，这种遍历集合元素的循环类型通常被称为 `FOR-EACH`（对于每个）循环，因为它对集合中的每个元素都执行了某些操作。这可能会让你联想到第 6.5 节中的 `foreach` 方法。这不仅仅是表面上的相似。

为了说明 for 循环的这种用法，考虑 REPL 中的以下代码：

```
scala> List.tabulate(10)(i => i*i)
res0: List[Int] = List(0, 1, 4, 9, 16, 25, 36, 49, 64, 81)
scala> for (elem <- res0) {
  println(elem)
}
```

- 0
1
4
9
16
25
36
49
64
81

在这种情况下，for 循环实际上执行的操作与 `foreach` 完全相同，并且在列表的每个不同元素上运行循环内部的代码。你在 for 循环中看到的代码 

# 208 使用 Scala 进行编程与问题解决简介

在 for 循环中可以是任意复杂的。这里显示的 `println` 语句只是简单的例子。

对 for 循环语法的更通用的描述如下——

```
for (name <- collection) statement
```

`name` 可以是任何有效的 Scala 名称。`collection` 可以是产生集合的任何表达式。`statement` 可以是你想要的任何内容。经常使用代码块来执行多项式。我们将使用 `Array[Double]` 作为多项式，其中每个元素都是多项式中的系数。例如，多项式 $3x²+6x²-4x+7$ 表示为 `Array(3.0,6.0,-4.0,7.0)`。我们要针对特定的 $x$ 值评估该多项式。我们将用三种方法编写。第一种将计数循环。

```
def evalPolyCount(coefs:Array[Double],x:Double):Double =
  var ret = 0.0
  for (i <- 0 until coeffs.length)
    ret += coeffs(i)*math.pow(x,coeffs.length-1-i)
  ret
```

这种方法行得通，但它特别低效。使用小指数效率非常低。使用索引遍历 Array 并不糟糕，如果我们决定使用 `List` 来处理会变化的系数的话。

记住，for 循环旨在遍历集合的元素。因此，我们可以直接遍历 `coeffs` 的元素并进行数学计算。这里的唯一挑战是，我们同样使用了索引 `i` 来计算 $x$ 的幂。如果我们简单地反向遍历 Array，就可以去掉这一点并移除 `pow` 的使用。将该逻辑放入代码产生：

```
def evalPolyReverse(coefs:Array[Double],x:Double):Double =
  var ret = 0.0
  var power = 1.0
  for (c <- coeffs.reverse)
    ret += c**power
    power *= x
  ret
```

这个版本没有使用索引计数。相反，它遍历数组元素。Array 中的每个值都被放入 `c` 中，并增加返回值。创建了一个单独的变量 `power`，初始值为 1.0，并且每次乘以 `x`。这为我们提供了 $x$ 的运行幂次，并消除了调用 `math.pow` 的需要。

这个函数也是完全正确的。它的主要缺点是，为了反转 $x$ 的幂 Array，会创建一个全新的 Array 并在反向顺序上复制元素。虽然这样效率较低，但这允许我们很好地说明使用 for 循环遍历任何集合，即使是通过对其他集合的操作创建的集合。这个循环也是非常命令式的，因为我们有两个正在变更的 `var` 声明。到此为止我们

