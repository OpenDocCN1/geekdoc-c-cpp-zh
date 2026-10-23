

```
scala> arr.size
res6: Int = 6
```

当你创建一个数组时，你必须指定一个长度，而且该长度永远不会改变。如果使用 var 风格的变量，你可以创建一个长度不同的新数组并让名称引用它，但这样做时你创建的是一个完全新的数组，你并没有改变旧数组的大小。

如果你尝试使用负数或过大的索引值，Scala 会给出错误信息，提示你已超出数组的边界。我们可以在这里通过尝试访问和更改越界索引来看到这种情况。

```
scala> arr(100)
java.lang.ArrayIndexOutOfBoundsException: 100
  at .<init>(<console>:7)
  at .<clinit>(<console>)
  at RequestResult$.<init>(<console>:9)
  at RequestResult$.<clinit>(<console>)
  at RequestResult$scala_repl_result(<console>)
  at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
  at sun...
```

```
scala> arr(100)=0
java.lang.ArrayIndexOutOfBoundsException: 100
  at .<init>(<console>:7)
  at .<clinit>(<console>)
  at RequestResult$.<init>(<console>:9)
  at RequestResult$.<clinit>(<console>)
  at RequestResult$scala_repl_result(<console>)
  at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
  at sun...
```

现在我们知道了使用数组的基本规则，我们就可以编写一些利用它们的有用函数。在上一章中，我们使用递归读取一组数字，然后对其进行操作。我们使用集合的一个动机是，我们无法存储值以便对其执行两个或多个操作。因此，两个有用的函数可能是：一个从用户输入填充数组，另一个执行我们之前所做的类型操作，但这次针对数组。

我们将从填充数组的函数开始，该函数从用户输入读取。这个函数需要传入它将要填充的数组。当使用数组时，最简单的方法是在开始时指定要读取的数字个数。这是因为数组大小固定。数组知道自己的大小，因此不需要传递该信息。需要传递的是下一个数字将被读入的索引。终止条件是我们尝试读取数组末尾之外的位置。该函数可能如下所示。

```
def fillArray(arr:Array[Int],index:Int) {
if(index<arr.length) {
  arr(index)=readInt()
  fillArray(arr,index+1)
}
}
```

这个函数很直接，但值得注意的是它不返回任何内容。数组是可变的，这意味着我们可以传入一个数组并让函数修改其内容。因此，无需返回任何内容。该函数的结果保存在修改后的数组内容中。以下展示了该函数的使用情况。

```
scala> val numbers=new Array[Int](4)
numbers: Array[Int] = Array(0, 0, 0, 0)
```

```
scala> fillArray(numbers,0)
```

```
scala> numbers
res3: Array[Int] = Array(2, 3, 4, 5)
```

创建了一个可以容纳四个值的整数新数组。我们调用 fillArray 并输入值 2、3、4 和 5。完成后，我们可以检查 numbers，看到它现在保存了这些值。

现在我们需要在数组内容上执行操作。我们将跳过为仅做加法或乘法制作特殊函数的步骤，直接进入更抽象、更灵活的方法，即传入一个用于操作内容的函数。除了执行操作的函数外，我们还需要一个数组和当前索引的整数。与上一章的做法不同，我们不需要传入基准值，因为我们知道何时到达数组的开头或结尾。该函数可能如下所示。

```
def operateOnArray(arr:Array[Int],index:Int,func:(Int,Int)=>Int):Int = {
  if(index<arr.length-1) {
    func(arr(index),operateOnArray(arr,index+1,func))
  } else {
    arr(arr.length-1)
  }
}
```

如果传入的索引位于或超出数组的最后一个元素，则此函数返回数组的最后一个元素。否则，它将函数应用于当前元素和对后续元素递归调用的结果。我们可以在之前定义的数组 arr 上通过以下命令看到其运行情况。

```
scala> operateOnArray(arr,0,_+_)
res0: Int = 30
```

```
scala> operateOnArray(arr,0,_*_)
res1: Int = 4536
```

这已经让我们看到了使用数组所带来的额外能力。值的存储使我们能够多次对其进行操作，而无需多次输入它们。

## 7.3 列表

数组是非函数式语言中最常用的内置集合。数组通常存储为一块连续的内存。这使得它们对许多操作来说快速且高效。但正如我们所见，数组是可变的。函数式语言倾向于远离突变和其他副作用。如果不允许突变，数组的效率会大大降低。如果你想更改数组中的单个值，就必须完整复制整个数组。因此，函数式语言更倾向于使用列表。严格来说，这些是链表，这是一种将在本书后面讨论的数据结构。你不需要详细了解其结构就能知道如何使用它。

我们可以使用与使用初始值构建数组相同的语法来构建列表。

```
scala> List(7,4,6,3,9,1)
res2: List[Int] = List(7, 4, 6, 3, 9, 1)
```

与数组类型一样，列表类型也是参数化的，如果使用这种语法，Scala 会推断出最佳类型。没有用于创建未初始化列表的语法。这是因为列表是不可变的。一旦创建了列表，其中的值就不能更改。因此，创建包含默认值的大列表意义不大。更改它需要创建一个新列表。

然而，当我们最初不知道将存储在其中的所有值时，还有另一种方法可以将列表组合起来。如果我们将元素添加到列表的前面，我们就可以高效地一次一个元素地构建列表。要向列表添加元素，我们使用“cons”运算符，::。以下是向现有列表添加单个元素的示例。

```
scala> val lst=List(2,3,4)
lst: List[Int] = List(2, 3, 4)
```

```
scala> 1::lst
res3: List[Int] = List(1, 2, 3, 4)
```

我们首先创建一个包含 2、3 和 4 的列表，然后将 1 cons 到列表的开头。此操作并未改变原始列表。相反，它给了我们一个在开头多了一个元素的新列表。由于列表的工作方式，这很高效。它实际上不需要复制整个列表即可实现。我们可以再次查看 lst，看到它没有改变。

```
scala> lst
res4: List[Int] = List(2, 3, 4)
```

如果使用 cons 运算符构建列表，通常会从空列表开始。在 Scala 中表示空列表有两种方法。一种是像我们之前那样使用它，但不向括号中放入任何参数。另一种是使用 Nil。因此，我们可以用这种方式构建之前相同的列表。

```
scala> 1::2::3::4::Nil
res5: List[Int] = List(1, 2, 3, 4)
```

你必须将 Nil 放在末尾，因为 :: 运算符需要在右手边有一个列表。请注意，要使其工作，:: 运算符是右结合的。所以 1::2::3::Nil 与 1::(2::(3::Nil)) 相同。这与通常的数学运算符相反，后者是左结合的。在 Scala 中，任何以冒号结尾的运算符都将是右结合的。

我们可以使用 cons 运算符编写一个从用户输入构建数字列表的函数。这是一个递归方法，它将读取数字直到遇到“quit”。使用“quit”作为结束条件对于列表来说效果很好，因为我们可以轻松高效地向列表添加新元素。对于数组来说并非如此，我们需要在开始时设置数组的大小。执行此操作的方法非常简单。

```
def inputList():List[Int] = {
```

