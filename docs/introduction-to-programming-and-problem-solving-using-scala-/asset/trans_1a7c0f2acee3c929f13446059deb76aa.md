

## 14.2.4 将 XML 写入文件

一旦你有了想要写入的 Node，写入过程就如调用 XML 对象的 `save` 方法一样简单。

```
xml.save("grades.xml",node);
```

第一个参数是你想要写入的文件名。第二个参数是你想要写入的 Node。

## 验证 XML（进阶）

XML 用于大型应用程序，因此，能够验证文件内容是否符合应用程序所需的格式至关重要。这一过程被称为验证（validation）。在 XML 标准首次发布时，验证是通过文档类型定义（DTDs）来完成的。DTD 是一个文本文件，其格式相当简单，允许你指定文件中应该包含哪些类型的元素。对于每个元素，你可以规定它内部需要包含什么或者可能包含什么。这种能力不仅包括了属性，也包含了子元素。

DTD 通用被认为存在两个问题。首先，它们有些局限且过于简单。例如，你可以说一个元素必须包含某个属性，但不能对该属性的性质set任何限制。例如，你不能规定它必须是一个日期。此外，DTD 有它们自己的语法。XML 的目标是成为一种通用的数据格式，并通过使用某种格式来统一规定 XML 的内容。

出于这些原因，XML schema 被创建了。XML schema 是一个 XML 文档，使用标签来指定什么和不能进入其他文件。XML schema 需要是庞大且复杂的，但它们对 XML 文件的格式提供了极佳的控制。针对 DTD 和 XML schema 都有相应的工具可以遍历 XML 并告诉你它们是否遵循给定的规范。标准中还有一个名为 `scala.dtd` 的包可以帮助进行验证。

## 14.2.5 模式

我们已经在很多地方见过模式（patterns）。在 XML 中我们还可以添加另一种。XML 不仅可以直接写入 Scala 语言中，还可以用于构建模式。这些模式看起来就像你想要的那样，你只需要在花括号中放入你想要的名称即可。有一个局限性：你不能在模式中放入属性。在下面的 REPL 示例中看到这种用法：

```scala
val personXML = <person><name>Kyle</name><gender>M</gender></person>
val monthXML = <month><name>Kyle</name><gender>M</gender></month>
val yearXML = <year><name>Kyle</name><gender>M</gender></year>
```

## 14.3 整合在一起

如果你决定使用模式来解析 XML，这可能会提供一种动力，让你将所有信息放在子元素而不是属性中。为了说明 XML 的真实威力，我们将编写一个更完整的程序，其中包含了之前的一些脚本以及编辑功能。最后一部分是之前强调过的，但它隐式地携带了赋予数据意义的能力。这使得插入不同类型的新信息变得非常困难。XML 可以根据需要添加新的标签。只要新标签与之前的标签不冲突，代码就能继续为你工作。我们又写了另一个脚本来确定“月度员工”。这两个脚本都处理员工和游乐项目，但所需的数据之间并没有 100% 的重叠，我们希望在这里编写的脚本能利用这两个脚本的功能，同时将所有信息保留在单个文件中。

代码如下。开头是多个用例类（case classes）的定义，然后是可以从 XML 构建这些类实例的函数。随后是之前章节中 schema 构建器的略微修改版本。

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
  YearData(year, months)
}

def yearToXML(year: YearData): Node = {
  <year year={year.toString()}>
    {year.months.map(monthToXML)}
  </year>
}

def parseRideData(node: Node): RideData = {
  val name = (node \ "Name").text
  val numOps = (node \ "numberOfOperators").text.toInt
  val heavy = (node \ "heavyCount").text.toInt
  RideData(name, numOps, heavy)
}

def rideData(rd: RideData): Node = {
  <ride name={rd.name} numberOfOperators={rd.numberOfOperators} heavyCount={rd.heavy}>
    <operators>{rd.operators.map(op => <operator>{op}</operator>)}
  </ride>
}

def parseEmployeeData(node: Node): EmployeeData = {
  val name = (node \ "Name").text
  val rides = (node \ "rides").map(_.text).toList
  EmployeeData(name, rides)
}

def employeeXML(ed: EmployeeData): Node = {
  <employee name={ed.name}>
    {ed.rides.map(r => <ride>{r}</ride>)}
  </employee>
}
```

