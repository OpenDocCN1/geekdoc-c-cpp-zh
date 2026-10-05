
点击此处查看代码

```
Circle c = new Circle(42);
object o = c; // 不需要装箱，因为 Circle 是引用变量
int i = (int)o; // 编译通过但在运行时会抛出异常
```

下面的图表说明了这种情况：

![](img/4f6c1423ece9eeb79a4a4e5db8b1746d_351_0.png)

你将在后面的练习中用到装箱（boxing）和拆箱（unboxing）。请记住，装箱和拆箱是非常耗资源的操作，因为它们需要大量的检查并且分配额外的堆内存。装箱有其用处；但如果不当使用会严重损害程序的性能。你将在第 17 章“引入泛型”中看到装箱的替代方案。

## 安全地转换数据

通过使用类型转换（cast），你可以指定根据你认为，对象引用的数据具有特定类型，并且使用类型引用该对象是安全的。这里的关键短语是“你认为”。C# 编译器不会检查这一点，而是由运行时检查。如果内存中对象的类型与转换类型不匹配，运行时将抛出上一节描述的 `InvalidCastException`。你应该准备好在发生此类异常时捕获它并进行恰当的处理。

然而，当对象的类型不是你预期的类型时，捕获异常并尝试恢复是一种相当繁琐的方法。C# 提供了两个非常有用的运算符，可以帮助你以更优雅的方式执行转换：`is` 和 `as` 运算符。

## is 运算符

你之前可能见过 `is` 运算符（在检查空值时用过），但它实际上允许你检查任何引用对象的类型。你可以使用 `is` 运算符来验证对象的类型是否如你的预期，如下：

点击此处查看代码

```
var wi = new WrappedInt();

object o = wi;
if (o is WrappedInt) {
    WrappedInt temp = (WrappedInt)o; // 这是安全的；o 是一个 WrappedInt
}
```

`is` 运算符接受两个操作数：左侧是对象的引用，右侧是类型名称（或 `null`）。如果堆上引用的对象类型与 `is` 运算符指定的类型匹配，则 `is` 结果为 `true`；否则，结果为 `false`。前面的代码仅在确定转换将成功时，才会尝试将引用转换为对象变量 `o`。

`is` 运算符的另一种形式允许你通过将类型检查和赋值结合来简写这段代码，如下：

```
WrappedInt wi = new WrappedInt();
...
object o = wi;
...
if (o is WrappedInt temp) {
    ... // 在此处使用 temp
}
```

在这个示例中，如果 `WrappedInt` 类型测试成功，`is` 运算符会创建一个新的引用变量（名为 `temp`）并将 `WrappedInt` 对象的引用赋值给它。

## as 运算符

`as` 运算符的作用与 `is` 类似，但方式略有简化的。你可以这样使用 `as` 运算符：

```
WrappedInt wi = new WrappedInt();
...
object o = wi;
WrappedInt temp = o as WrappedInt;
if (temp is not null)
{
    ... // 转换成功
}
```

与 `is` 一样，`as` 运算符接受一个对象和一个类型作为其操作数。运行时尝试将对象转换为指定的类型。如果转换成功，则返回结果，并在示例中将其赋值给 `WrappedInt` 变量 `temp`。如果转换失败，`as` 运算符将返回 `null` 值并将其赋值给 `temp`。

> 注意
> `is` 和 `as` 运算符的内容比这里描述的更多；第 12 章将更详细讨论它们。

## 重温 switch 语句

如果你需要检查一个引用相对于多个类型，可以使用一系列 `if...else` 语句结合 `is` 运算符。下面的示例假设你已经定义了 `Circle`、`Square` 和 `Triangle` 类。构造函数接受几何形状的半径（radius）或边长（side）作为参数：

```
var c = new Circle(42);      // 半径为 42 的圆
var s = new Square(55);      // 边长为 55 的正方形
var t = new Triangle(33);   // 边长为 33 的等边三角形
...
object o = s;
...
if (o is Circle myCircle)
{
  ... // o 是 Circle，在 myCircle 中可以使用引用
} else if (o is Square mySquare)
{
  ... // o 是 Square，在 mySquare 中可以使用引用
} else if (o is Triangle myTriangle)
{
  ... // o 是 Triangle，在 myTriangle 中可以使用引用
}
```

与任何长度的 `if...else` 语句一样，这种方法可能会迅速变得繁琐且难以阅读。幸运的是，在这种情况下你可以使用 `switch` 语句，如下：

```
switch (o)
{
  case Circle myCircle:
    ... // o 是 Circle，在 myCircle 中可以使用引用
  case Square mySquare:
    ... // o 是 Square，在 mySquare 中可以使用引用
  case Triangle myTriangle:
    ... // o 是 Triangle，在 myTriangle 中可以使用引用
}
```

`switch` 语句中也支持 `when` 表达式来进一步限定条件，例如下面的语句显示了不同的形状：

```
switch (o)
{
  case Circle myCircle when myCircle.Radius > 10:
    ...
    break;
  case Square mySquare when mySquare.SideLength == 100:
    ...
    break;
  case Triangle myTriangle when myTriangle.Side == 33:
    ...
    break;
  default:
    throw new ArgumentException("未识别的形状");
}
```

## 指针与不安全代码

此侧边栏仅供参考，针对熟悉 C 或 C++ 的开发者。如果你是编程初学者，可以忽略这些信息。

如果你已经使用 C 或 C++ 等语言编写过程序，本章关于对象引用的讨论可能让你很熟悉，这些语言有一种提供类似的功能：指针。指针是持有内存地址或引用（在堆或栈上）的变量。

使用特殊的语法来标识变量为指针。例如，下面的语句声明了一个整数的指针：

```
int *pi;
```

虽然变量 `pi` 被声明为指针，但在初始化之前，它并不指向任何地方。例如，为了让 `pi` 指向整数变量 `i`，可以使用以下语句和地址运算符 (`&`)：

```
int *pi;
int i = 99;
...
```

你可以通过指针变量访问并修改变量 `i` 存储的值：

```
*pi = 100;
```
