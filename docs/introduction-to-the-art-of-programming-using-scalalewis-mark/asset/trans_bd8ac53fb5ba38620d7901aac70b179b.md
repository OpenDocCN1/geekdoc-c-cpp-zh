

## 16.1.4.5 The update Method

拥有一个 apply 方法对于许多情况已经足够了。例如，对于不可变集合来说，它就是所需要的一切。对于我们编写的 CourseSection 类来说，这也是我们想要的全部。然而，如果你想做类似对 Array 进行赋值的操作，它就不够了。基本上，它只是查找事物，并不会改变事物。要做到这一点，就要使用 update 方法。当 Scala 看到类似这样的表达式时

```
obj(args) = e
```

它会将其转换为如下形式的调用

```
obj.update(args,e)
```

因此，只需实现适当的 update 方法即可获得索引的赋值。

## 16.1.4.6 Overloading Methods

方法可以重载。这意味着你可以有两个名称相同但参数个数不同或参数类型不同的不同方法。重载方法的能力有时会很有用，但你不希望滥用它，因为它会使读者难以理解正在发生的事情，甚至可能使代码变得模糊而无法编译。对于特殊方法而言，由于必须具有特定的名称，重载是唯一能够使你在使用不同类型时获得所需功能的方法。

要理解这一点，请考虑你有一个代表数字网格的类，也许是用于电子表格。这是一个使用 apply 方法获取值的合适情况。然而，引用电子表格中的单元格有几种方式。在程序中最明显的方法是传递两个 Int 表示行和列。然而，当你运行电子表格程序时，通常使用字母表示列、数字表示行来引用单元格。你可能希望允许以 String 和 Int 传递（例如 "C", 13）或仅以 String 传递（例如 "C13"）。通过重载，你可以编写三个不同的 apply 方法和 update 方法，如下所示。

```
class Spreadsheet(rows:Int, columns:Int) {
  private val data = Array.fill(rows,columns)(0.0)

  def apply(c:Int, r:Int) : Double = data(r)(c)

  def update(c:Int, r:Int, v:Double) = data(r)(c)=v

  def apply(c:String, r:Int) : Double = data(r)(calcColumn(c))

  def update(c:String, r:Int, v:Double) = data(r)(calcColumn(c))=v

  def apply(cell:String) : Double = {
    val (c,r) = cell.partition(_.isLetter)
    data(r.toInt)(calcColumn(c))
  }

  def update(cell:String, v:Double) = {
    val (c,r) = cell.partition(_.isLetter)
    data(r.toInt)(calcColumn(c))=v
  }
}
```

```
private def calcColumn(c:String) : Int = {
  c.toLowerCase.foldLeft(0)((v,c) => v*26+(c-'a'))
}
```

使用这段代码，你可以做类似这样的事情。

```
val ss = new Spreadsheet(10,10)
ss("c5") = 14
ss(3,8) = 24
println(ss("c",5)+" "+ss("d8"))
```

这提供了一种非常自然的方式，使用任何方便的样式访问元素。通常，你最好不要在可以使用稍微不同的名称时重载方法。大多数情况下，不同的名称会导致代码更不易出错且更易读。

## 16.1.4.7 Vector Example

为了演示这些不同特性如何协同工作，我们将编写一个代表 3-D 向量的类。我们将为其提供 x、y 和 z 分量，然后定义我们希望能够对其执行的操作类型。我们为此必须做出的第一个重要设计决策是，我们是否希望向量对象是可变的还是不可变的。对于此示例，我们将采用不可变版本，因为它更好地展示了函数式设计，并且在这里效果更好。这种方法更耗内存，并且在某些应用中可能更慢，因为它不会改变向量。然而，它通常会产生更好、更可靠的代码，在某些应用中会更快，因为它防止了防御性拷贝。防御性拷贝是指在不想让自己的对象版本被更改时，将对象拷贝一份传递给其他代码。

我们将从包含 +、-、* 和 / 运算符的类声明开始。它还具有两个版本的 apply。最后有一个名为 toString 的方法，我们将在第 19 章中更详细地学习。该方法决定了当 Vect 类型的对象被打印出来时我们看到的内容。拥有一个有助于你了解正在发生的事情以纠正问题的形式是非常有用的。

```
class Vect(val x:Double, val y:Double, val z:Double) {
  def +(v:Vect):Vect = new Vect(x+v.x,y+v.y,z+v.z)

  def -(v:Vect):Vect = new Vect(x-v.x,y-v.y,z-v.z)

  def *(c:Double):Vect = new Vect(c*x,c*y,c*z)

  def /(c:Double):Vect = new Vect(c/x,c/y,c/z)

  def apply(i:Int):Double = i match {
    case 0 => x
    case 1 => y
    case 2 => z
  }

  def apply(is:Seq[Int]):Seq[Double] = {
    is.map(Array(x,y,z))
  }
}
```

```
override def toString = "<"+x+", "+y+", "+z+">"
}
```

第一个版本的 `apply` 让你可以索引不同的坐标。它是使用 match 表达式编写的，尽管当然还有其他方法可以实现。第二个版本的 `apply` 更不寻常。它允许你通过传入索引序列来将 x、y 和 z 值作为序列取回。²

写完这段代码后，我们可以实例化 `Vect` 类型的对象并对其执行指定的操作。

```
scala> val v1=new Vect(1,2,3)
v1: Vect = <1.0, 2.0, 3.0>
```

```
scala> val v2=new Vect(2,-4,7)
v2: Vect = <2.0, -4.0, 7.0>
```

```
scala> val v3=v1+v2
v3: Vect = <3.0, -2.0, 10.0>
```

```
scala> val v4=v3*8
v4: Vect = <24.0, -16.0, 80.0>
```

请注意，使用我们这里的代码，我们必须将标量放在乘法的右边。如果你尝试做 `8*v3` 你会得到一个错误。这是因为 Scala 将其视为 `(8).* (v3)`。值 8 是一个 `Int`，它没有适用于 `Vect` 的 `*` 版本。可以绕过这个问题，但它需要另一个更高级的概念，即隐式转换，我们现在不想考虑它。现在我们满足于将标量放在右边。

3-向量上的另外两个常见操作是点积和叉积。点积返回一个标量，叉积返回一个向量。编写它们时，我们必须做出一个重要的决定，我们希望它们是符号还是单词？我们不能对两者都使用 `*`，因为 Scala 无法弄清楚在任何给定时间我们指的是哪一个。同样，阅读代码的人也可能无法弄清楚。Scala 确实给了我们使用多运算符符号的较长符号名称的能力。所以也许 `**` 用于点积和 `**` 用于叉积。你不能使用 `*.*` 和 `*x*` 因为 `.` 和 `x` 不是运算符字符。这些中的 `+` 和 `-` 的选择来自于点积和叉积公式的知识，但两者都不能很好地契合，也不会让大多数人读起来像点积和叉积。因此，我们将坚持使用普通的字母方法名。

```
def dot(v:Vect):Double = x*v.x+y*v.y+z*v.z
def cross(v:Vect):Vect =
    new Vect(y*v.z-z*v.y, z*v.x-x*v.z, x*v.y-y*v.x)
```

我们仍然可以用运算符表示法使用它们。唯一的问题是字符的优先级低于乘法，因此为了强制执行运算顺序，必须使用括号。

由于这些是不可变的，因此没有提供 `update` 方法。理论上，你可以使它们可变并提供 `update`。你可能还想提供 `+=`、`-=`、`**=` 和 `/=` 运算符，使其变异而不是创建新拷贝。将其留作读者的练习。

²这种类型的索引是 MATLAB® 中的标准操作，在该语言中处理数组和矩阵是主要用途。

## 16.1.5 object Declarations

*Scala* 还有另一种与 **class** 在语法上相似但含义非常不同的类型声明。**object** 声明在当前作用域中创建一个单一对象，其中包含你放入其中的成员和方法。与 **class** 不同，你不能向 **object** 传递任何参数。这是因为你不会用 **new** 来创建 **object**。**object** 的声明就是使其存在的方式。

即使 **object** 声明不会创建新类型，我们仍使用名称的首字母大写来将其与普通实例化对象区分开。要使用 **object** 的成员或方法，使用 **object** 名称并像对 **class** 的实例一样调用它。**object** 声明可以在你想要一个 **object** 但只想要一个该类型对象的任何作用域中使用。在顶层，它们通常用作组织函数的场所，但其多功能性远不止于此。

### 16.1.5.1 Applications

你可以在不实例化的情况下使用 **object** 这一点非常重要。**objects** 在程序开始运行后就有效地存在了。你不需要有一行代码来新建一个。这在我们超越 REPL 和脚本进入完整应用程序时最为重要。顶层 **object** 声明如果包含一个名为 **main** 的方法，该方法接受 Array[String] 类型的参数并返回 Unit，则定义了应用程序的入口点。这里有一个简单的例子：

```
object FirstApp {
    def main(args:Array[String]) {
        println("My first application.")
    }
}
```

我们使用过的脚本可以通过在 **object** 中的 **main** 中放入代码来转换为应用程序。如果使用变量名 **args** 表示命令行参数，那么在脚本中对它们的引用甚至会正常工作。

脚本和应用程序之间的主要区别在于你在文件中组织代码的方式以及如何运行它们。按定义，脚本应该是小型程序。脚本的所有代码都放在单个文件中。当所需代码量变大时，就需要将其拆分并组织起来。在 *Scala* 中，几乎所有情况下你都应遵循的组织结构是，将每个顶层 **class** 或 **object** 放在一个单独的文件中，文件名是 **class** 或 **object** 的名称后跟 “.scala”。

考虑一个成绩簿应用程序的例子。我们可能会使用上面的 **Student** 类并将其放在名为 “Student.scala” 的文件中。上面的 **CourseSection** 类将放在 “CourseSection.scala” 中。最后，我们将有一个用于成绩簿的 **object** 声明，将放在 “Gradebook.scala” 中。除了具有 **main** 方法外，这将保存课程集合并提供我们想要的成绩簿的任何功能，无论是文本还是图形界面。

运行这样的应用程序是一个两步过程。首先你必须编译代码。这是用 scalac 命令完成的，代表 “*Scala* compiler”。你必须告诉 *Scala* 编译器你想要编译哪些文件。如果你组织代码，使应用程序的所有代码都在一个目录下，你可以执行类似 scalac *.scala 的操作。这将编译当前目录下所有以 “.scala” 结尾的文件。这样做时，如果有任何语法错误，它们将被找到并以与你作为脚本运行程序时相同的方式报告给你。一旦你找到并修复了所有语法错误，编译器将生成一组可以运行的编译后 BYTECODE 文件。这些文件将以 “.class” 扩展名结尾。要运行应用程序，你

