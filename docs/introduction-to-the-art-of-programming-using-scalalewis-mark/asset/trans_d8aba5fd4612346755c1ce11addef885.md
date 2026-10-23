

回到第 6.4 节我们看到如何通过向递归函数传递函数来使其更强大。这种方法正是 Scala 集合库中高阶函数所采用的方法。因此，从那以后我们自己并没有太多用到它。然而，不想为 case class 的每一种可能的排序都编写全新的排序或搜索函数的需求，促使我们再次提取这些想法。

如果你要编写一个新版本的冒泡排序，按降水量对 Weather 对象进行排序，你会发现唯一改变的是与元素比较相关的代码。为了得到一个可以按最高温度、降水量或与 Weather 类型相关的任何其他内容进行排序的排序，我们所要做的就是使其能够从外部改变比较。这可以通过传入一个执行比较的函数来实现。对于我们的排序，我们一直使用小于和大于进行比较，所以我们只需要传入一个代表其中之一的函数。我们在这里选择小于，但代码也可以很容易地用大于重写。更改后的排序代码如下所示。

```
def bubbleSortWeather(a:Array[Weather],lessThan:(Weather,Weather)=>Boolean) {
  for(j <- 0 until a.length-1) {
    for(i <- 0 until a.length-1-j) {
      if(lessThan(a(i+1),a(i))) {
        val tmp=a(i)
        a(i)=a(i+1)
        a(i+1)=tmp
      }
    }
  }
}
```

比较运算符被表示为一个函数，它接受两个 Weather 对象并返回一个 Boolean。在 if 语句中使用对该函数的调用。

使用这个修改后的版本，我们可以通过如下调用按最高温度排序。

```
bubbleSortWeather(weather,(w1,w2)=>{w1.tmax < w2.tmax})
```

或者，同样的方法也可以用来按降水量排序，调用如下。

```
bubbleSortWeather(weather,(w1,w2)=>{w1.precip < w2.precip})
```

更重要的是，使用这个版本的排序，很容易将其更改为从大到小排序，而不是标准的从小到大排序。在降水量的情况下，这是通过以下方式更改调用来实现的。

```
bubbleSortWeather(weather,(w1,w2)=>{w1.precip > w2.precip})
```

唯一改变的是比较运算符的方向。正如你所见，这种使用函数而不是硬编码比较运算符的抽象版本要灵活得多。

既然我们看到了在排序中使用它所带来的好处，很高兴能够以同样的方式启用搜索。如果你开始用相同的比较运算符编写搜索代码，你会发现有一个显著的问题，搜索需要的不仅仅是小于或大于。搜索需要我们能够判断两个事物是否相等。处理此问题的标准方法是使用返回 Int 而不是 Boolean 的函数。Int 为负数、零或正数分别表示小于、等于或大于。使搜索有点不同的另一个变化是函数只接受一个 Weather 对象，因为我们只想知道我们要查找的东西相对于我们正在搜索的这个值的相对位置。

将所有这些翻译成代码得到以下内容。

```
def binarySearchWeather(a:Array[Weather], comp:(Weather)=>Int):Int = {
    var start=0
    var end=a.length
    var mid=(end+start)/2
    var c=0
    while(end>start && {c=comp(a(mid)); c!=0}) {
        if(c<0) {
            end=mid
        } else {
            start=mid+1
        }
    }
    mid=(end+start)/2
    if(end <= start) -1 else mid
}
```

该函数名为 comp，它接受一个 Weather 并返回一个 Int。为了防止代码比需要的多调用 comp，我们引入了一个名为 c 的变量来存储最近比较的结果。我们在条件中的代码块中对其进行赋值。循环检查它是否不为零。if 检查它是否小于零。在我们计算新的 mid 之后，我们也进行新的比较。

现在问题是，我们如何使用这个搜索来查找数组中的不同元素。我们给出的第一个例子是重复我们上面搜索特定年份和月份的搜索。

```
binarySearchWeather(data,w => {
    if(w.year>1896) -1
    else if(w.year<1896) 1
    else if(w.month>2) -1
    else if(w.month<2) 1
    else 0
})
```

在这种情况下，我们正在搜索 1896 年的二月。这个版本使用一系列 if 表达式来确定元素 w 是否在那个时间之前或之后。通过一点数学，我们可以利用每年有 12 个月这一事实使其更简短。

```
binarySearchWeather(data,w => (1896*12+2)-(w.year*12+w.month))
```

基于日期的搜索数据变得更加复杂，因为它取决于两个值。如果我们使用灵活的排序按降水量重新排序数组，我们可以使用以下方法搜索降雨量为 1.43 英寸的月份。

```
binarySearchWeather(data,w => {
    val diff = 1.43-w.precip
    if(diff > 1e-8) 1
    else if(diff < -1e-8) -1
    else 0
})
```

编写此逻辑可能具有挑战性。值得庆幸的是，返回负数、零或正数的行为是一个常见的标准，Scala 库包含使用内置数字类型执行此操作的代码。因此，代码可以更简单地表示如下。

```
binarySearchWeather(data, w => 1.43 compare w.precip)
```

compare 调用实际上是我们可以在 Double 上调用的方法。由于句点对数字有其他含义，我们使用了运算符表示法而不是更标准的点和括号表示法来表示该方法。

## Bucket/Radix Sort（高级）

本章前面讨论的排序只需要比较元素的能力。存在一些情况，你对值有更多信息，可以利用它更有效地对它们进行排序。非通用排序的例子包括 BUCKET SORT 和 RADIX SORT。两者都使用有关正在排序的数据的知识来将它们分成组。

要理解其工作原理，请考虑你被要求按名称对大量文件夹进行排序并且你在一个大房间里的情况。许多人会先浏览堆栈并将其分成不同的堆。堆将用于字母表的不同部分。如果原始堆栈真的很大并且你有一个非常大的房间，你可能会为每个起始字母制作一个堆。你可以以这种方式继续分解，每次针对每个堆或在堆变小时切换到其他方法。这种通用方法称为桶排序，堆将被称为桶。桶排序实际上是一种将排序问题分解为更小、更易于管理的部分的通用方法。

基数排序使用类似的方法，但它是对整数值进行排序的特定算法。它一次组织一个数字的每一位。以一种违反直觉的方式，它从最低有效位开始。这之所以有效，是因为每次遍历都会保留元素的顺序。因此，如果 A 在一次遍历中的数字低于 B，并且下一次遍历将它们放在同一个 bin 中，A 将在该 bin 中排在 B 之前。

按照惯例，我们将使用十进制数字实现基数排序，使用十的幂的除法和取模。以下代码是一个相当高效的实现，它使用 Array[List[Int]] 作为 bin 对 Array[Int] 进行排序。请注意，将项目移动到 bin 不是原地操作。值在分箱后复制回数组，但它确实至少需要原地排序两倍的内存。

```
```scala
def radixSort(a:Array[Int]) {
  var max = a.max max a.min.abs
  var powerOf10 = 1
  while(max>0) {
    val byDigit = Array.fill(19)(List[Int]())
    for(num <- a) {
      val digit = num/powerOf10%10+9
      byDigit(digit) ::= num
    }
    var i = 0
    for(bin <- byDigit; num <- bin.reverse) {
```
```
