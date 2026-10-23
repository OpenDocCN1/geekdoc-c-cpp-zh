
计算所需的信息被传入，这个函数只对数据进行计算，并返回一个数字。

现在我们可以把这些代码片段组合起来，编写一个脚本，它能告诉你最多四人的团队费用，包括购买套餐。我们将假设整个团队要么都带冷藏箱，要么都不带；所有人都要么去水上乐园，要么不去；并且他们都点某种规格的套餐。以下代码可以放在一个脚本中，与 `entryCost` 和 `itemCost` 函数一起使用。

```
def individualCost(cooler:Boolean, waterPark:Boolean): Double = {
  println("What is the person's age?")
  val age = readInt()
  println("What size combo are they ordering?")
  val size = readLine()
  entryCost(age,cooler,waterPark)+itemCost("Combo",size)
}
```

```
println("How many people are in your group? (1-4)")
val numPeople = readInt()
if(numPeople<1 || numPeople>4) {
  println("This script can not handle "+numPeople+" people.")
} else {
  println("Is the group bringing a cooler? (Y/N)")
  val cooler = readLine()=="Y"
  println("Will they be going to the water park? (Y/N)")
  val waterPark = readLine()=="Y"
  val totalCost = individualCost(cooler,waterPark) +
    (if(numPeople>1) individualCost(cooler,waterPark) else 0) +
    (if(numPeople>2) individualCost(cooler,waterPark) else 0) +
    (if(numPeople>3) individualCost(cooler,waterPark) else 0)
  println("The group cost is $"+totalCost+".")
}
```

请注意，这段代码不在函数中。当你编写脚本时，函数声明所做的正是这些：它们声明了一个函数。你需要在函数之外编写代码来让某些事情发生，通常是通过调用一个或多个已声明的函数。

这个脚本确实有一个重大局限：它只适用于1-4人。我们还不能让一段代码执行任意次数。我们将在下一章学习如何做到这一点。

## 运行 Scala 程序的方式（附注）

学生偶尔会遇到的一个难题是如何运行他们的 Scala 程序。运行 Scala 有三种不同的方式。你已经见过其中两种：REPL 和脚本。第三种方式——编译为应用程序——将在本书后半部分讨论。要使用 REPL，你可以在命令行中输入 `scala`，不指定要执行的文件。要运行脚本，你可以在命令行中输入 `scala`，并给它一个以 `.scala` 结尾的文件名。起初，这两种方式可能看起来完全不同。然而，REPL 有一个 `:load` 命令，你可以用它从 Scala 文件中加载代码。使用这个命令，你可以加载一个

4. 编写一个 if 语句。

## 5.9.2 概念总结

- 函数用于将问题分解成更小的部分。
  - 有助于解决问题。
  - 信息丰富的名称使代码更易理解。
  - 更小的函数更容易处理。
- 编程中的函数与数学中的函数类似。信息通过形式参数传入。参数的值在调用函数并传入实参时确定。
- 在 Scala 中，函数使用 `def` 声明。后面依次是函数名、参数列表、结果类型，然后是等号和函数表达式。结果类型可以省略并由编译器推断，但仍建议你显式包含它。
- 函数也可以写成 Scala 中的字面量。
  - 火箭记号用 `=>` 分隔参数列表和函数体。
  - 更简短的记法使用下划线表示参数。这只适用于某些函数。
- 仅因其副作用而被调用且不需要返回值的函数返回 `Unit`。这种情况很常见，因此有一种简化语法：省略冒号、结果类型和等号，花括号直接放在参数列表后面。
- 如果你的函数经常接受或返回元组，使用类型声明为元组提供更短、更有意义的名字会很有用。

## 5.9.3 自主学习

在 REPL 中输入以下语句，观察它们的作用。有些会产生错误。你应该弄清楚原因。尝试一些变体，以确保你理解正在发生的事情。

```
scala> def succ(n:Int):Int = n+1
scala> succ(1)
scala> succ(succ(1))
scala> var cnt = 0
scala> def inc { cnt=cnt+1 }
scala> cnt
scala> inc
scala> cnt
scala> inc
scala> inc
scala> cnt
scala> val f = (x:Double,y:Double)=>math.sqrt(x*x+y*y)
scala> f(3,4)
scala> def doThreeTimes(g:(Double)=>Double,x:Double) = g(g(g(x)))
```

```
scala> doThreeTimes(y=>y+1,1)
scala> doThreeTimes(y=>y+2,1)
scala> doThreeTimes(a=>a-5,100)
scala> doThreeTimes(_+1,1)
scala> doThreeTimes(_*2,1)
scala> def incChar(c:Char,offset:Int) = (c+offset).toChar
scala> incChar('a',1)
scala> incChar('a',2)
scala> incChar('z',-3)
scala> def tnp1(n:Int):(Int,Int) = {
  val odd = n%2
  (n/2*(1-odd),(3*n-1)*odd)
}
scala> odd
scala> var name = ""
scala> def introduction {
  println("What is your name?")
  name = readLine()
  println("Hello "+name)
}
scala> name
```

## 5.9.4 练习

1. 对于完成以下任务的函数，其参数和结果的类型分别是什么？（注意：你不必编写这些函数，只需说明它们的类型。）
   - 告诉你一个人的名字中有多少个单词。
   - 接受一个通常写法的人名，并以“姓, 名”的格式返回。
   - 接受三个单词，并返回它们的 TLA（三字母缩写）。
   - 接受二维空间中的十个点（x-y 坐标），并返回其中有多少个在单位圆内。
   - 接受一个数字，并告诉它有多少个不同的质因数。
   - 接受一个数字，并告诉它有多少个正因数。
   - 接受一个华氏温度值，并返回等效的摄氏温度。
   - 接受一个华氏温度值，并返回等效的摄氏温度和开尔文温度。

2. 编写函数，为练习1（第85页）的不同部分返回一个 Boolean。

3. 编写一个函数，接受一个 String 参数，并返回一个 Boolean，说明该参数是否为回文。

4. 为练习5（第86页）的解答编写一个函数。

5. 为练习6（第86页）的解答编写一个函数。

6. 为练习7（第86页）的解答编写一个函数。

7. 为练习8（第86页）的解答编写一个函数。

8. 将你为练习9（第86页）编写的代码转换为一个函数，该函数以 x 和 y 值作为参数，并返回一个 Boolean，指示该点是否在单位圆内。

9. 编写一个函数，将温度从华氏度转换为摄氏度。

10. 编写一个函数，将英里转换为公里。

11. 编写一个函数，将秒转换为年。

12. 编写一个函数，将 AU（天文单位）转换为英里。

13. 编写两个函数，接受四个数字并返回最小的一个。第一个可以使用 `min`，但第二个不能。

14. 编写一个函数，接受三个数字并返回中位数。

## 5.9.5 项目

1. 编写一组函数，对 Int 的二元组执行以下操作，就像它们是分数的分子和分母一样。
   (a) 加法
   (b) 减法
   (c) 乘法
   (d) 除法

2. 编写一组函数，对 Double 的三元组执行以下操作，就像它们是向量一样。
   (a) 加法
   (b) 减法
   (c) 点积
   (d) 叉积

3. 编写一组函数，对 Double 的二元组执行以下操作，就像它们是复数一样。
   (a) 加法
   (b) 减法
   (c) 乘法
   (d) 除法
   (e) 模

4. 使用你对练习3的解答来编写一个函数，该函数接受两个复数 z 和 c，并返回 z² + c 的值。

5. 编写一个函数来求解二次方程的实数值。你的解答应返回两个根的 (Double, Double) 元组。

6. 增强练习5的解答，使其返回一个 ((Double, Double), (Double, Double))。这是一个由两个二元组构成的二元组。它表示两个根，每个根都可以是一个以 (Double, Double) 表示的复数。
