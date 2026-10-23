

```
(elem \ "quiz").map(n => (n \ "@grade").text.toDouble).toList
```

这个函数构建一个 Student 对象，并传入四个必需的参数。第一个是姓名，由元素的 fname 和 lname 属性组成。之后依次是三个 List，分别对应作业、测试和测验的成绩。这些 List 的形式都很相似。它们首先搜索正确的标签名，并将结果映射到一个函数，该函数将 grade 属性的值转换为 Double。这里必须调用 text，因为 `\` 的结果是一个 Node，而不是 String，并且 Node 类型没有 toDouble 方法。每种成绩类型的最后一步是调用 toList。这是必需的，因为 map 操作的对象是 NodeSeq，返回的是 Seq，而 Student 类型要求的是 List。

你可能一开始并不会注意到这里使用了 map。希望到目前为止，你已经对 map 和其他高阶方法相当熟悉了。不过，如果你仔细想想，就会意识到这里有点令人惊讶，因为调用 map 的对象并不是 List 或 Array，而是 NodeSeq。这之所以可行，是因为 NodeSeq 本身是 Seq[Node] 的子类型，也就是说我们之前在其他序列上使用的所有方法也都可以在它上面正常工作。

这对于获取我们的学生数组也同样有用。下面的代码行展示了如何使用 map 和 toArray，通过 studentFromXML 函数得到我们想要的结果。

```
scala> (res4 \ "student").map(studentFromXML).toArray
res15: Array[Student] = Array(Student(Jason
Hughes,List(100.0),List(94.0),List(98.0, 100.0, 90.0)), Student(Kevin
Peese,List(20.0),List(67.0),List(85.0, 78.0)))
```

同样，调用 toArray 会返回我们想要的 Array[Student]，而不是更通用的 Seq[Student]。

将 text 方法应用于完整的 Elem，将得到它内部及其所有子元素中出现的全部文本。因此，对 res4 调用 text 会得到两条注释以及大量空白字符。如果只想获取某个特定成绩上的注释，就需要解析到那个特定元素，然后对其调用 text 方法。

## 14.2.3 构建 XML

现在你已经知道如何将 XML 文件的内容转换为 Scala 中有用的形式。那么反过来呢？假设我们刚刚编写的代码被用在了第 10 章的基于菜单的应用程序中，并且已经做了一些更改，现在我们希望把结果写回文件。第一步就是构建代表数据的 Node。

上面我们已经看到，可以将 XML 直接放入 Scala 程序或 REPL 中，它会被解析并理解。然而，仅凭这一点并不能让我们把程序中的值放回 XML 文件。幸运的是，这也不难做到。在嵌入到 Scala 程序中的 XML 里，你可以在花括号中嵌入 Scala 表达式。我们先从一个简单的例子开始。

```
scala> <tag>4+5 is {4+5}</tag>
res19: scala.xml.Elem = <tag>4+5 is 9</tag>
```

这里，表达式 4+5 被放在花括号中，正如你所看到的，它会计算得到值 9。你放在花括号中的代码可以复杂得多，并可以构建额外的 XML 内容或标签。

我们将利用这一点编写一个函数，把 Student 对象打包成 XML 节点。代码如下所示。

```
def studentToXML(stu:Student):xml.Node = {
  val nameParts=stu.name.split(" +")
  <student fname={nameParts(0)} lname={nameParts(1)}>
    {stu.quizzes.map(q => <quiz grade={q.toString}/>)}
    {stu.tests.map(t => <test grade={t.toString}/>)}
    {stu.assignments.map(a => <assignment grade={a.toString}/>)}
  </student>
}
```

第一行按空格将学生姓名拆分成多个部分。这里假定第一个元素是名字，第二个元素是姓氏。这两个部分被用作 student 标签的属性值。在该元素内部有三行代码，分别对应测验、测试和作业。每一行都将对应的 List 映射到一组带有 grade 属性的元素。

关于使用代码作为属性值，有两点值得注意。首先，引号不需要显式写出。当值是 Scala 代码时，引号会自动添加。其次，用于属性值的 Scala 表达式的类型必须是 String。这一点在成绩值上体现得很明显。它们是 Double 类型，必须显式转换为 String。

## 14.2.4 将 XML 写入文件

一旦你得到了想要写入的 Node，写入过程就如同调用 XML 对象的 save 方法一样简单。

```
xml.XML.save("grades.xml",node)
```

第一个参数是你要写入的文件名。第二个参数是你要写入的 Node。

## 验证 XML（高级）

当 XML 用于大型应用程序时，能够验证文件内容是否符合应用程序要求的格式非常重要。这一过程称为验证。当 XML 标准首次发布时，验证是通过文档类型定义（DTD）文件完成的。DTD 是一种文本文件，其格式相当简单，允许你指定文件中应包含哪些类型的元素。对于每个元素，你都可以规定其中必须包含什么，或者可以包含什么。这种能力涵盖了属性和子元素。

人们普遍认为 DTD 有两个问题。首先，它们有些局限且过于简单。例如，你可以规定一个元素必须包含某个属性，但无法对该属性的类型施加任何约束。你不能规定它必须是数字或日期。此外，DTD 有自己的语法。XML 的目标是成为一种通用的数据存储格式，但一些人觉得，必须使用另一种格式来指定 XML 文件的内容不太合适。

出于这些原因，人们创建了 XML schema。XML schema 是一种 XML 文档，它使用特定的标签来规定某个 XML 文件中可以包含什么和不能包含什么。XML schema 往往庞大而复杂，但它们能对 XML 文件的格式提供很强的控制力。

对于 DTD 和 XML schema，都有相应的工具可以对 XML 文件进行检查，并告诉你它们是否符合给定的规范。Scala 标准库中还有一个名为 scala.xml.dtd 的包，可以帮助使用 DTD 进行验证。

## 14.2.5 XML 模式

到目前为止，我们已经多次看到模式（pattern）的使用。借助 XML，我们还可以引入另一种模式。XML 不仅可以直接写入 Scala 语言，还可以用来构建模式。这些模式看起来与构建 XML 时使用的形式完全相同，只不过放在花括号中的内容应当是你希望绑定为变量的名字。有一个重要的限制：你不能在模式中包含属性。可以通过 REPL 中的下面这个小例子来理解这种用法。

```
scala> val personXML = <person><name>Mark</name><gender>M</gender></person>
personXML: scala.xml.Elem = <person><name>Mark</name><gender>M</gender></person>
```

```
scala> val <person><name>{name}</name><gender>{sex}</gender></person> = personXML
name: scala.xml.Node = Mark
sex: scala.xml.Node = M
```

## 14.3 综合应用

为了展示 XML 的真正威力，我们将编写一个更完整的主题公园程序，其中包含前面一些脚本的功能，以及编辑能力。所有信息都将存储在一个 XML 文件中。这最后一点是之前没有强调过的，但它本身就蕴含着给数据赋予含义的能力。在纯文本文件中，是文件中的位置赋予了数据含义。这使得插入不同类型的新信息变得非常困难。对于 XML 来说，这不是问题，因为可以根据需要添加新标签。只要新标签的名称不与原有标签冲突，原有代码就能继续正常工作。

在第 8 章中，我们编写了一个帮助制定排班的脚本。在第 13 章中，我们编写了另一个可用于评选月度员工的脚本。这两个脚本都涉及与员工和游乐设施相关的信息，但它们所需的数据并不完全重合，而且文件格式也大不相同。我们想在这里编写一个脚本，包含那两个脚本的功能，同时还能添加游乐设施和员工信息，并将所有信息存储在一个 XML 文件中。

下面给出了该脚本的代码。代码首先定义了许多 case class，然后是能够从 XML 构建这些 case class 的实例、或从这些实例构建 XML 的函数。在这些函数之后，有四行代码声明了程序的主要数据，同时从命令行指定的 XML 文件中读取这些数据。接下来是前几章中的排班构建器和员工排名器的略微修改版本。

```
import scala.io.Source
import scala.xml._
```

