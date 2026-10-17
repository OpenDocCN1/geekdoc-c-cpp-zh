
Scala 语言内置了一个 XML 解析器，允许你直接在代码中编写 XML。你可以看到这个表达式的类型是 `scala.xml.Elem`。

# 使用 Scala 进行编程与问题解决简介

`scala.xml` 包包含了与 XML 相关的类型。我们在这里将介绍一些最重要的类型。

- `Elem` - 代表单个元素。它是 `Node` 的子类型。
- `Node` - 代表 XML 文档中更通用的节点。它是 `NodeSeq` 的子类型。
- `NodeSeq` - 代表 `Node` 序列。
- `XML` - 一个辅助对象，具有读取和写入 XML 文件的方法。

在 API 中你还可以看到相当少的其他类型，但我们将关注这些类型，因为它们为我们提供了目标所需的功能。

## 14.2.1 加载 XML

我们可以使用 `XML` 对象的方法从文件读取或写入到文件。`loadFile` 方法可用于读取文件。如果将第一个示例 XML 放在一个名为 `"grades.xml"` 的文件中，那么下面的代码将加载它。

```scala
scala.xml.loadFile("grades.xml")
```
`res4: scala.Elem =`
```xml
<course name="CS 1320">
  <student name="Bender" fname="Quinn">
    <grade grade="98"></grade>
    <grade grade="100"></grade>
    <grade grade="90"></grade>
    <test grade="94"></test>
    <assignment grade="100">
      Code compiled and runs.
    </assignment>
  </student>
<student name="Hughes" fname="Jason">
    <grade grade="85"></grade>
    <grade grade="78"></grade>
    <test grade="67"></test>
    <assignment grade="20">
      Code did not compile.
    </assignment>
</student>
</course>
```

显然，这就是我们创建的 XML 文件的内容。唯一缺失的是注释，那是为了人类阅读的，而不是让程序担心的。此外，空标签也被转换成了起始标签和结束标签，中间没有任何内容。这说明空标签也只是为了人类的方便，其意义与一对空的起始标签和结束标签相同。

## 14.2.2 解析 XML

一旦我们将这个 `Elem` 对象存储在 `res4` 中，问题就变成了如何从从中提取信息。`NodeSeq` 类型以及作为其子类型的 `Node` 和 `Elem` 类型声明了操作符 `\` 和 `\\`。这些操作符用于在 XML 内部搜索对象的内容。这两个操作符都接受第二个 `String` 类型的参数，表示你想要查找的名称。区别在于它们的搜索方式。`\` 操作符查找顶层内容，如果我们有一个 `NodeSeq`，则查找序列中的 `Nodes`；如果我们有一个 `Node` 或 `Elem`，则查找该节点的子节点。而 `\\` 操作符则查找当前层级匹配的任何内容。为了说明这一点，我们将做三个例子。

```scala
scala res4 \ "student"
```
`res5: scala.xml.NodeSeq =`
```xml
NodeSeq(<student name="Bender" name="Quinn">
  <quiz grade="88"></quiz>
  <quiz grade="100"></quiz>
  <quiz grade="90"></quiz>
  <test grade="94"></test>
  <assignment grade="100">
    Code compiled and runs free.
  </assignment>
</student><student name="Hughes" name="Jason">
  <quiz grade="85"></quiz>
  <quiz grade="78"></quiz>
  <test grade="67"></test>
  <assignment grade="20">
    Code did not compile.
  </assignment>
</student>)
```

```scala
scala res4 \ "test"
```
`res6: scala.xml.NodeSeq = NodeSeq()`

```scala
scala res4 \ "test"
```
`res7: scala.xml.NodeSeq = NodeSeq(<test grade="94"></test>, <test grade="67"></test>)`

这两个搜索都使用了 `\` 操作符。第一个搜索查找名称为 `"test"` 的元素。第二个搜索查找名称为 `"test"` 的标签，并返回包含这些标签的 `NodeSeq`。这个搜索返回了一个空的 `NodeSeq`。这是因为 `res4` 中虽然有名为 `"test"` 的标签，但它们深层嵌套在 `"student"` 元素内部，因此没有被 `\` 操作符找到。最后一个例子再次搜索了 `"test"` 标签名，但这次用的是 `\\`，它进行深度搜索，并返回了一个内部包含两个 `Node` 的 `NodeSeq`。

`\\` 操作符也可以用于从元素获取属性。要获取标签的属性索引，只需在搜索字符串的开头加上 `"@"` 即可。这里有三个例子来说明这一点。

```scala
scala res4 \ "name"
```
`res8: scala.xml.NodeSeq = CSCI 1320`

```scala
scala res4 \ "grade"
```
`res9: scala.xml.NodeSeq = NodeSeq()`

```scala
scala res4 \ "grade"
```
`res10: scala.xml.NodeSeq = NodeSeq(98, 100, 90, 94, 100, 85, 78, 67, 20)`

# 使用 Scala 进行编程与问题解决简介

第一个搜索使用 `\` 来获取顶层节点的名称。在顶层节点上查找 `@grade` 并不会带我们任何结果，而 `\\` 会返回文档中所有分值的值。

你真正想做的是将 XML 文件中的信息放入一个可以在程序中使用的结构中。根据我们所学的，这意味着我们想要将内容放入 `case class` 中。这个 XML 文件中的数据与我们在第 10 章中定义的 `Student` 类型非常接近。那个类看起来是这样的：

```scala
class Student(name:String,assignments:List[Double],tests:List[Double],quizzes:List[Double])
```

在本章中，我们将其解析为 `Students` 数组。现在我们现在演示如何使用 XML 实现同样的操作。我们将从一个接收 `Node` 并返回 `Student` 对象的函数开始。这样的函数可能看起来如下：

此函数构建了一个 `Student` 对象并传入了四个必需参数。第一个是名称，它由元素的 `fname` 和 `lname` 属性组成。之后，我们有三个分别代表作业 `assignments`、测试 `tests` 和测验 `quizzes` 成绩的列表。它们分别具有相似的形式。我们可能先搜索正确的标签名，并将结果映射到一个函数上，该函数将 `@grade` 的结果转换为 `Student` 的属性。调用它是必要的，因为结果是 `Node` 而不是 `String`，且 `Node` 类型没有 `toDouble` 方法。每种成绩类型的最后部分是 `toList`，这是必要的，因为 `map` 作用于 `NodeSeq` 并会给出一个 `Seq`，但 `student` 类型需要的是 `List`。

上面的 `studentFromXML` 形式很紧凑，但它可能不是可读性最高或最易操作的。在从 XML 解析时，为每个值引入新变量是有帮助的。以下代码显示了执行此操作的修改版本：

`map` 的使用起初可能没有注意到。希望到此时你已经习惯了它以及其他的排序方法。然而，如果你思考一下，你会发现令人惊讶的是，被调用的并不是 `List` 或 `Array`。相反，它是一个 `NodeSeq`。这之所以有效，是因为 `NodeSeq` 本身是 `Seq[Node]` 的子类型，这意味着我们在其他序列上使用的所有方法在这里同样适用。

这对于获取我们的学生数组同样有用。接下来的行显示了我们如何使用 `map` 和 `toArray` 来获得我们想要的，即 `studentFromXML` 函数的结果。

```scala
scala(res4) = \student\
```

再次，调用 `toArray` 返回的是所需的 `Array` 而不是更一般的 `Seq[Student]`。

我们在解析过程中使用了几次 `text` 方法。值得注意的是，应用在 `elem` 上的 `text` 方法将给你它内部以及所有子元素中的所有文本。调用 `text res` 会得到两条注释以及一行空白。要获取任何特定成绩的注释，你需要解析到那个特定的元素并调用 `text` 方法。

## 14.2.3 构建 XML

现在你知道如何将 XML 文件的内容获取到 Scala 中了。那么反过来操作呢？假设我们刚刚编写的代码被用于第 10 章中基于菜单的应用程序，并且进行了更改，现在我们想将结果写回文件。第一步就是构建表示数据的 `Node`。

我们上面看到可以直接将 XML 放入 Scala 程序或 REPL 中，它会被解析并理解。然而，这本身并不提供将程序中的值写回 XML 文件的能力。幸运的是，这也不难。嵌入 Scala 程序中的 XML 可以使用大括号来启用 Scala 表达式。我们将从一个简单的例子开始。

```scala
scala:<tag>4+5 is (4+5)</tag>
```
`res19: scala.elem = <tag>4+5 is 9</tag>`

在这里，表达式 `4+5` 被放在大括号中，你可以看到它求值为 `9`。你放在大括号内的代码可以复杂得多，用于构建额外的 XML 内容或。

我们将使用它编写一个函数，将 `Student` 对象解析为 XML 节点。这段代码如下：

```scala
def studentToXML(student:Student):xml.Node = {
val nameParts = student.nameParts(" ")
<student name=${nameParts(0)} name=${nameParts(1)}>
${student.quizzes.map(q => <quiz grade=${q.toString()}>) }
${student.tests.map(t => <test grade=${t.toString()}>) }
${student.assignments.map(a => <assignment grade=${a.toString()}>) }
</student>
}
```

第一行将学生姓名分成片段。假设第一个元素是名，第二个元素是姓。这些被用作 `student` 标签的属性。内部有三行代码，分别对应测验、测试和作业。这些每一行将相应的列表映射为带有 `grade` 属性的元素。

值得注意的是关于使用代码作为属性值的几点。首先，任何地方都没有写引号。当值是 Scala 代码时，引号会自动提供。其次，属性值的 Scala 代码类型必须是 `String`。这在成绩值上显而易见。它们是 `Double` 且必须显式转换为 `String`。

## 14.2.4 将 XML 写入文件

一旦你有了想要写入的 Node，写入过程就如调用 XML 对象的 `save` 方法一样简单。

```scala
xml.save("grades.xml",node);
```

第一个参数是你想要写入的文件名。第二个参数是你想要写入的 Node。

## 验证 XML（进阶）

XML 用于大型应用程序，因此，能够验证文件内容是否符合应用程序所需的格式至关重要。这一过程被称为验证 `validation`。在 XML 标准首次发布时，验证是通过文档类型定义 `DTDs` 来完成的。`DTD` 是一个文本文件，其格式相当简单，允许你指定文件中应该包含哪些类型的元素。对于每个元素，你可以规定它内部需要包含什么或者可能包含什么。这种能力不仅包括了属性，也包含了子元素。

`DTD` 通用被认为存在两个问题。首先，它们有些局限且过于简单。例如，你可以说一个元素必须包含某个属性，但不能对该属性的性质 `set` 任何限制。例如，你不能规定它必须是一个日期。此外，`DTD` 有它们自己的语法。`XML` 的目标是成为一种通用的数据格式，并通过使用某种格式来统一规定 XML 的内容。

出于这些原因，`XML schema` 被创建了。`XML schema` 是一个 XML 文档，使用标签来指定什么和不能进入其他文件。`XML schema` 需要是庞大且复杂的，但它们对 XML 文件的格式提供了极佳的控制。针对 `DTD` 和 `XML schema` 都有相应的工具可以遍历 XML 并告诉你它们是否遵循给定的规范。标准中还有一个名为 `scala.dtd` 的包可以帮助进行验证。

## 14.2.5 模式

我们已经在很多地方见过模式 `patterns`。在 XML 中我们还可以添加另一种。`XML` 不仅可以直接写入 Scala 语言中，还可以用于构建模式。这些模式看起来就像你想要的那样，你只需要在花括号中放入你想要的名称即可。有一个局限性：你不能在模式中放入属性。在下面的 REPL 示例中看到这种用法：

```scala
val personXML = <person><name>Kyle</name><gender>M</gender></person>
val monthXML = <month><name>Kyle</name><gender>M</gender></month>
val yearXML = <year><name>Kyle</name><gender>M</gender></year>
```

## 14.3 整合在一起

如果你决定使用模式来解析 XML，这可能会提供一种动力，让你将所有信息放在子元素而不是属性中。为了说明 XML 的真实威力，我们将编写一个更完整的程序，其中包含了之前的一些脚本以及编辑功能。最后一部分是之前强调过的，但它隐式地携带了赋予数据意义的能力。这使得插入不同类型的新信息变得非常困难。`XML` 可以根据需要添加新的标签。只要新标签与之前的标签不冲突，代码就能继续为你工作。我们又写了另一个脚本来确定“月度员工”。这两个脚本都处理员工和游乐项目，但所需的数据之间并没有 100% 的重叠，我们希望在这里编写的脚本能利用这两个脚本的功能，同时将所有信息保留在单个文件中。

代码如下。开头是多个用例类 `case classes` 的定义，然后是可以从 XML 构建这些类实例的函数。随后是之前章节中 schema 构建器的略微修改版本。

### 列表 14.1: ThemePark.scala

```scala
import scala.io.Source
import scala.xml._

case DayData(ride:String, dayOfWeek:String, operators: Array[String], numRiders:Int)
case MonthData(month:Int, days:List[DayData])
case YearData(year:Int, months:List[MonthData])
case RideData(name:String, numberOfOperators:Int, heavy:Int)
case EmployeeData(name:String, rides:List[String])

def parseDay(node: Node): DayData = {
  val ride = (node \ "ride").text
  val dow = (node \ "dayOfWeek").text
  val num = (node \ "numRiders").text.toInt
  val ops = (node \ "operator").map(_.text).toArray
  DayData(ride, dow, ops, num)
}

def toXML(data: DayData): Node = {
  <ride={data.ride} dayOfWeek={data.dayOfWeek} numRiders={data.numRiders}>
    <operators>{data.operators.map(op => <operator>{op}</operator>)}
  </ride>
}

def parseMonth(node: Node): MonthData = {
  val month = (node \ "month").text.toInt
  val days = (node \ "day").map(parseDay).toList
  MonthData(month, days)
}

def monthXML(month: MonthData): Node = {
  <month month={month.toString()}>
    {month.days.map(dayToXML)}
  </month>
}

def parseYear(node: Node): YearData = {
  val year = (node \ "year").text.toInt
  val months = (node \ "month").map(parseMonth).toList
```
