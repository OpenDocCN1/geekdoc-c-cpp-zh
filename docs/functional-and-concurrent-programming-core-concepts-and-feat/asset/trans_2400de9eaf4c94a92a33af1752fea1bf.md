

在 2.5 节，我们讨论了扩展方法，这是一种使函数看起来像方法的机制。这里，我们需要的是相反方向的转换，以便把方法当作函数来使用。

这个概念的正式名称是 η-变换。在 λ-演算中，它表明 f 与 λx. f x 是等价的。更直白地说，你可以把它看作 greaterThan90 与 x => greaterThan90(x) 之间的等价。作为计算单元，两者执行相同的任务：判断一个整数是否大于 90。鉴于 find 的参数类型必须是 Int => Boolean，而 greaterThan90 是一个从 Int 到 Boolean 的方法，表达式 temps.find(greaterThan90) 的意图十分清晰，编译器能够插入必要的 η-变换。

其他语言也提供了类似的桥梁，支持从方法中创建函数，有时依赖更显式的语法。例如，在 Java 中，lambda 表达式 x -> target.method(x) 可以用方法引用 target::method 替换。Kotlin 使用类似的语法。

## 9.5 单抽象方法接口

在混合语言中，函数是对象，lambda 表达式是创建这类对象的便捷方式。事实上，lambda 表达式的语法非常方便，许多语言允许你用它来创建函数以外类型的实例。

单抽象方法（SAM）接口是恰好包含一个抽象方法的接口。例如，在 Scala 中，类型 Function[A,B]（或者等价地，A => B）就是具有单个抽象方法 apply 的 SAM 接口。我们在代码示例中使用 lambda 表达式创建 Function[A,B] 的实例，但事实证明，所有 SAM 类型都可以使用 lambda 表达式实例化，即使是那些与 Function 无关的类型：

```
Scala
abstract class Formatter:
  def format(str: String): String
  def println(any: Any): Unit = Predef.println(format(any.toString))
```

类 Formatter 只定义了一个抽象方法 format，因此它是一个 SAM 接口。它可以用 lambda 表达式来实现：

```
Scala
val f: Formatter = str => str.toUpperCase
f.println(someValue)
```

注意，方法 println 是如何在被定义为 lambda 表达式的对象 f 上被调用的。这之所以可行，只是因为 f 被声明为 Formatter 类型；表达式 (str => str.toUpperCase).println("foo") 没有任何意义。

## 9.6 部分应用

许多 Java 接口都可以用 lambda 实现，尽管它们早于 Java 的 lambda 表达式语法，并且与函数式编程关系不大：

```
val absComp: Comparator[Int] = (x, y) => x.abs.compareTo(y.abs)
val stream: IntStream = ...
val loggingStream: IntStream = stream.onClose(() => logger.info("closing stream"))
```

Comparator 是一个 Java 2 的 SAM 接口，带有一个抽象方法 compare。Stream 的 onClose 方法接受一个类型为 Runnable 的单一参数，Runnable 是 Java 1 的 SAM 接口，带有一个抽象方法 run。Comparator 和 Runnable 都可以用 lambda 表达式实现。

## 9.6 部分应用

除了 lambda 表达式、柯里化和 η-变换之外，部分应用是另一种用于创建函数值的机制。在 Scala 中，它采用下划线占位的形式，用来代替表达式的一部分。这会生成一个函数，当该函数被应用时，会用其参数替换给定表达式中的下划线。例如，以下代码在一个摄氏温度列表中查找大于 90（华氏度）的温度：

```
celsiusTemps.find(temp => temp * 1.8 + 32 > 90)
```

你不需要使用 lambda 表达式，而是可以通过将表达式 temp * 1.8 + 32 > 90 中的 temp 替换为下划线来构建所需的函数参数：

```
celsiusTemps.find(_ * 1.8 + 32 > 90)
```

表达式 _ * 1.8 + 32 > 90 表示一个布尔函数，它将 temp 映射到 temp * 1.8 + 32 > 90，就像 lambda 表达式 temp => temp * 1.8 + 32 > 90 定义的函数一样。之前用 lambda 表达式编写的搜索可以改用部分应用：

```
temps.find(_ > 90)
projects.find(_ .id == 12345L)
```

通过在同一个表达式中使用多个下划线，部分应用被推广到多参数函数。例如，_ * 1.8 + 32 > _ 是一个双参数

迫使你为在 then 和 else 块内声明的变量选择不同的名称。

虽然通常每个代码块都定义自己的作用域，但并非所有语言都遵循这一规则。例如，JavaScript 和 Python 会为函数体引入新作用域，但不会为条件语句的 then 和 else 分支或循环体引入新作用域。当你习惯了更主流的作用域规则时，这可能会令人困惑。作为示例，请考虑以下 Python 程序：

```
```python
x = 1
def f():
  x = 2
  if x > 0:
    x = 3
    y = 4
  print(x)  # prints 3
  print(y)  # prints 4

f()
print(x)  # prints 1
print(y)  # error: name 'y' is not defined
```
```

函数 f 的函数体定义了自己的作用域，但 if 内部的代码块却没有。相反，x=3 是对在函数作用域中声明的变量 x（初始值为 2）的赋值，而 y=4 在同一个作用域中引入了变量 y。特别地，这个变量 y 在 if 语句之后仍然存在，其值为 4。函数 f 内部的 print(x) 语句打印函数作用域中变量 x 的值，即 3；而函数 f 外部的 print(x) 语句打印最外层作用域中变量 x 的值，即 1。最后的 print(y) 语句会触发错误，因为在函数作用域之外没有声明 y 变量。在 JavaScript 中行为也是如此。对比 Scala 中的情况：

```
```scala
var x = 1
def f() =
  var x = 2
  if x > 0 then
    var x = 3
    var y = 4
  println(x) // prints 2
  println(y) // rejected at compile-time
```
```

```
f()
println(x) // prints 1
println(y) // rejected at compile-time
```

大多数语言现在使用静态作用域，但在哪些编程语言结构会引入新作用域上存在差异。相比之下，动态作用域容易出错，已不那么流行。它曾被用于最初的 Lisp，并且在现代版本的该语言中仍然作为一个选项存在。它也被用于一些脚本语言，最著名的是 Perl 和各种 Bourne Shell 实现。

作为示例，这个 Scala 程序遵循静态作用域规则：

```
Scala
var x = 1

def f() =
  x += 1
  println(x) // prints 2

def g() =
  var x = 10
  f()

g()
println(x) // prints 2
```

函数 g 定义了一个局部变量 x，然后调用 f。然而，函数 f 内部使用的变量 x 是在程序第一行声明的那个，即函数 f 定义处作用域内的那个。函数 g 内部定义的同名局部变量不参与其中。等效的 Java、Kotlin、C 或任何其他使用静态作用域的语言编写的程序，行为也是一样的。

对比下面这个 Bash 实现：

```
Bash
x=1

f() {
```

```
(( x++ ))
printf "%d\n" $x # prints 11
}

g() {
  local x=10
  f
}

g
printf "%d\n" $x # prints 1
```

在 Bash 中，函数 f 内部使用的变量 x 不是 f 定义处作用域内的变量，而是函数 f 被调用处作用域内的变量。这个变量等于 10，被递增到 11。程序开头声明的变量 x 从未被修改。

动态作用域可用于用局部变量覆盖全局变量，从而改变函数的行为。这有时很有用，而在 Scala 中可以通过隐式参数实现类似的行为。例如，通过复用 9.5 节的 Formatter 类型，可以定义一个函数，使用作用域内的默认格式化器来打印对象：

```
Scala
def printFormatted(any: Any)(using formatter: Formatter): Unit =
  formatter.println(any)

printFormatted("foo") // uses the default formatter in scope (there must be one)
```

在函数内部——或任何引入自身作用域的代码块中——可以指定不同的格式化器：

```
Scala
given UpperCaseFormatter: Formatter = str => str.toUpperCase

printFormatted("foo") // prints "FOO"
```

这种技术带回了动态作用域的一些灵活性，但安全得多：函数 printFormatted 明确允许局部定义的格式化器影响其行为。

本书中的代码示例并不太依赖隐式参数，除了在第二部分偶尔使用。特别是，Scala 倾向于使用隐式参数来指定执行并发活动的线程池。

