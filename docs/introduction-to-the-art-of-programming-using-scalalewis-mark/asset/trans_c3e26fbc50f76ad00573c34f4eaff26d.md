
```
ret
}

override def toString() : String = "ToD :\n"+
(for((o,i) <- values.zipWithIndex) yield i+" : "+o).mkString("\n")

private def hourFromTime(time:String) : Int = {
    time.substring(0,time.indexOf(':')).toInt +
    (if(time.endsWith("PM") && !time.startsWith("12")) 12 else 0)
}
}
```

这个类是参数化的。类名`ToDValues`后面跟着一个类型参数`[A]`。方括号将其与值参数区分开。习惯上使用单个大写字母，从`A`开始，作为类型参数的名称。这段代码可以这样使用。

```
val riders1 = new ToDValues[Int]
val riders2 = new ToDValues[Int]
val worker1 = new ToDValues[String]
val worker2 = new ToDValues[String]

riders1(12) = 5
riders1("8:24AM") = 10
riders1(14) = 7
riders2("2:13PM") = 8

worker1(12) = "Jason"

val totalRiders = riders1.combine(riders2,(o1,o2) => (o1,o2) match {
  case (None,None) => None
  case (Some(a),None) => Some(a)
  case (None,Some(b)) => Some(b)
  case (Some(a),Some(b)) => Some(a+b)
})

println(riders1)
println(totalRiders)
```

这段代码创建了该类的四个不同实例，两个存储`Int`，两个存储`String`。然后它向其中三个添加了一些值，并使用`combine`将骑手数量相加。

拥有参数多态意味着我们可以编写一个类，并让它与`Int`、`String`或我们想要的任何其他类型一起工作。这个类仍然有一些明显的局限性。首先，它很难初始化。如果你在其他序列中拥有想要的数据，并且想将其放入这里，除非编写代码手动逐元素复制，否则无法做到。`combine`方法也有些局限，因为我们只能合并相同类型的数据并返回该类型。例如，我们不能将工人与骑手合并。这种功能可能很有用，但它要求我们在方法上放置类型参数。

## 19.4.2 参数化函数和方法

在Scala中，让用户以不同方式创建某种类型对象的标准方法是创建一个伴生对象，其中包含接受所需不同参数的`apply`版本。然后我们让类本身接受适当的数据作为参数。下面是一个可能看起来像这样的示例。

```
object ToDValues {
  // First attempt that lacks type parameter and does not compile.
  def apply() : ToDValues = new ToDValues(Array.fill(24)(None))
}
```

正如注释所暗示的，这行不通。原因是`ToDValues`本身不是一个有效的类型。它必须有一个类型参数才能被完全指定。为了在那里获得一个类型，我们需要给方法一个类型参数。其语法很简单。我们只需在名称和值参数之间用方括号放置类型参数即可。这样做，我们可以创建两个如下所示的`apply`方法。

```
object ToDValues {
  def apply[A]() = new ToDValues[A](Array.fill(24)(None))
  def apply[A](a:A*) = {
    val d = a.map(Option(_)).toArray
    new ToDValues[A](if(d.length<24) d.padTo(24,None) else
      if(d.length>24) d.take(24) else d)
  }
}
```

第二个`apply`方法允许我们通过以下方式构造一个`ToDValues`对象。

```
val riders1 = ToDValues[Int]()
val riders2 = ToDValues(0,0,0,6,7,3,9)
```

这里你应该注意到的关键是，第二种用法没有指定类型参数。这是因为当它们与方法一起使用时，类型参数通常是推断出来的。只要类型出现在方法的参数中，你就不必告诉Scala要使用什么，它会自行推断。创建`riders1`的那一行要求我们指定`[Int]`，因为没有参数，但第二行可以推断出它是在使用`Int`类型。

这段代码之所以有效，是因为该类已设置为接受一个参数。这意味着声明将从上面显示的内容更改为类似这样的内容。

```
class ToDValues[A](private val values:Array[Option[A]]){
```

这里有一个非常大的问题：有可能创建一个带有不包含24个元素的数组的`ToDValues`对象。这显然是不良行为，我们需要防止它。一种防止方法是使该类拥有一个私有构造函数。这意味着只有与该类或其伴生对象相关联的代码才能对这个对象调用`new`。语法上，这是通过在值参数前放置`private`关键字来实现的，如下所示。

```
class ToDValues[A] private(private val values:Array[Option[A]]){
```

现在，外部代码唯一能实例化`ToDValues`对象的方式是通过伴生对象的`apply`方法，而且我们很容易确保这些方法总是使用包含24个元素的数组来创建实例。

我们想要做的另一个添加是增强`combine`方法，使其能够处理不同的类型。理想情况下，我们希望能够让输入类型成为两种不同的类型，而输出类型是第三种类型。我们可以通过在方法上引入两个类型参数来实现，如下所示。

```
def combine[B,C](o:ToDValues[B])(f:(Option[A],Option[B])=>Option[C]) :
    ToDValues[C] = {
new ToDValues((values,o.values).zipped.map((v1,v2) => f(v1,v2)))
}
```

现在我们可以做类似将工人与骑手合并的事情，以跟踪可能用于奖金的关联关系。

如果你仔细观察，会发现这里除了添加类型参数外，还有其他变化。不再是包含两个参数的一个值参数列表，而是两个列表，每个列表包含一个参数。你应该记得，这是一种称为柯里化的技术。这不是必需的，但它使方法的使用更加容易。下面是一个使用示例。

```
val totalRiders = riders1.combine(riders2)((o1,o2) => (o1,o2) match {
case (None,None) => None
case (Some(a),None) => Some(a)
case (None,Some(b)) => Some(b)
case (Some(a),Some(b)) => Some(a+b)
})
```

如果我们不对这个方法进行柯里化，Scala中的局部类型推断将不会自动推断出`o2`的类型，而我们将不得不在函数声明中用`(o1, o2: Int)`来指定它。

我们还有另一对任务可以通过类型参数受益，那就是排序和搜索。我们在第13章中编写的排序和搜索只适用于一种类型。当我们想处理不同类型时，必须复制它们并进行修改。现在我们知道我们希望有一个像`sort[A]`这样的方法，可以对任何我们想要的类型进行排序。一个简单的尝试会向我们展示一个我们尚未讨论的类型参数细节，它会引发问题。

```
object Sorts {
  def bubbleSort[A](a:Array[A]) {
    for(i <- 0 until a.length) {
      for(j <- 0 until a.length-1-i) {
        if(a(j)>a(j+1)) { // Error: > undefined for Any
          val tmp = a(j)
          a(j) = a(j+1)
          a(j+1) = tmp
        }
      }
    }
  }
}
```

这段代码中的注释描述了如果我们尝试编译这段代码会得到的错误。考虑到代码并没有显式使用`Any`类型，这可能会让你停顿一下。

小于或大于，这种方法是有益的。如果值相等，函数将返回0。如果第一个较小，它将返回一个负值。如果第一个较大，它将返回一个正值。我们将在后面的章节中看到这种对比较函数的使用。

这种使用第二个函数参数进行比较的方法的优势在于它使排序更加灵活。例如，在上面任何一个示例中，我们都可以通过简单地传入`>_`而不是`<_`，将数字从大到小排序，而不是从小到大。此外，它确实对类型`A`没有任何限制。这允许你根据任何想要的排序顺序对事物进行排序。例如，如果你有一个学生类型，你可能在某些上下文中想按姓氏排序，在另一些上下文中按成绩排序。这种方法允许你这样做，因为排序顺序并不依附于对象类型。这种方法的缺点是，调用排序方法的人每次想使用它时都必须编写一个比较函数。在上面的例子中，这并不是什么大问题，因为我们的比较很简单。然而，有时情况并非如此。

## 19.4.3 类型边界

正如我们刚刚看到的，一个普通的类型参数，比如`[A]`，当我们在代码中使用该类型的对象时，会被视为`Any`。虽然这是一种非常常见的用法，但肯定会有一些时候，你想限制类型参数中可以使用的类型，以便可以安全地调用除了`Any`可用的那一小部分方法之外的其他方法。做到这一点的方法是在类型上设置边界。

最常见的形式是在类型上设置上界。这是用`<:`符号完成的。为了理解为什么你可能想要这样做，让我们考虑一个使用之前关于水果的代码的示例。我们在本章开头编写的`makeBreakfastShake`函数只使用了一个水果。这通常不是它的工作方式。你可能希望能够包含多个水果，也许是不同类型的。一个常见的例子是同时含有香蕉和草莓的奶昔。为此，你可能会考虑使用如下代码，传入一个`Array[Fruit]`。

```
def makeBreakfastShake(fruits:Array[Fruit]) {
  for(fruit <- fruits) {
    if(!fruit.canEatSkin) {
      fruit.peel
    }
    blender += fruit
  }
  blender += juice
  blender += ice
  blender.blend
}
```

这段代码可能看起来没问题，而且在很多情况下它都会起作用。然而，它并不完美。下面是一个出现问题的地方的例子。

```
scala> val berries = Array(new Strawberry,new Strawberry)
berries: Array[Strawberry] = Array(Strawberry@51d36f77, Strawberry@103b1799)

scala> makeBreakfastShake(berries)
<console>:16: error: type mismatch;
found   : Array[Strawberry]
required: Array[Fruit]
```

