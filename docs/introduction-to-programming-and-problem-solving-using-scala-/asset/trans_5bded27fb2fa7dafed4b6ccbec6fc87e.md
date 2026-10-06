
# 418 使用 Scala 进行编程与问题解决

# 线性二分查找（进阶）

二分查找适用于一般的已排序数据。然而，如果你恰好知道数据分布相当均匀，你可以做得更好。与其将 `mid` 设置为范围的中点，你可以根据数据在 `start` 和 `end-1` 之间线性分布的情况，将其放置在你预期值出现的位置。假设 `Array` 包含 `Double` 类型，可以通过如下代码行实现：

```
val mid = start+((value-start)/(end-1-start))*(end-1-start)).toInt
```

这是根据线性近似选取的 `mid` 的值。需要小心确保这不会陷入无限循环。此外，如果数据不是均匀分布的，这种方法的起始速度可能比普通的二分查找慢得多。在某些情况下，它会退化为 O(n)。

# 13.3 使用类例类（case classes）进行排序/搜索

在我们看过的排序和搜索中，处理的是数值类型。更通地说，所编写的代码将适用于任何支持比较操作符类型。因此，如果我们简单地更改传入排序函数的类型，我们的代码就可以适用于 `Array[Char]` 或 `Array[String]`，因为 `Char` 和 `String` 类型可以使用 `<`。但我们编写的类例类并不满足这一要求。因此，我们需要对类例类进行排序。幸运的是，除了目标类型之外，代码的修改并不显著。

我们将使用以下类例类：

```
case class Weather(id:String,year:Int,month:Int,prec:Double,tmax:Double,tmean:Double,tmin:Double)
```

该类的创建是为了存储历史天气数据。它用于表示温度和降水的每月记录。你可以将这些记录记录文件加载到 `Array` 中。如果你想对最热的天气进行排序，可以根据温度对数组排序。此类排序的代码所示：

```
def bubbleSortHighTemps(a:Array[Weather]):Unit = {
  for (j <- 0 until a.length-1) {
    for (i <- 0 until a.length-j) {
      if (a(i).tmax > a(i+1).tmax) {
        val tmp = a(i)
        a(i) = a(i+1)
        a(i+1) = tmp
      }
    }
  }
}
```

# 排序与搜索

选择泡沫排序是因为它的排序非常简单。非常容易看到了哪些变化。唯一的改变是传入的 `Array` 参数类型，以及比较是在数组元素的字段之间进行的。将此排序应用到数组后，你可以使用 `take` 或 `takeRight` 来提取一端或另一端的元素。

类例类提供了另一种方案，这是我们在处理值时没有真正实现的方案，即基于某个字段进行比较的能力。对于天气数据，它们可能在数据文件中按时间顺序存储。按时间顺序是年份和月份字段的组合。如果你想按时间进行的能力，你可能需要一个可以查找特定年月份的二分查找。该代码列在此：

```
def binarySearch(a:Array[Weather], year:Int, month:Int):Int {
  var start = 0
  var end = a.length
  var mid = (end+start)/2
  while (end < end && (a(mid).year != year || a(mid).month != month)) {
    if (year < a(mid).year || (year == a(mid).year && month < a(mid).month)) {
      end = mid
    } else {
      start = mid+1
    }
    mid = (end+start)/2
}
if (end <= start) -1 else mid
```

注意，比较变得显著复杂了。它必须先比较年份，如果平局，则用月份平局。

不幸的是，如果这样写，我们必须为类例类的每种可能的排序顺序编写完全独立的排序或搜索。如果你想在最热的月份中寻找最暖的月份，你需要一个单独的排序。你可能会觉得为了为了微小的更改而复制整个排序或搜索函数是不高效的，而且应该有一种方法可以实现更通用的排序或搜索。我们可以在这里帮助改进针对类例类的函数。在《Scala：面向对象、抽象与数据结构》[1] 中，我们将获得抽象这些思想的能力，使函数能够适用于多种类型，而不是在单个类型上进行不同的排序。

回到 5.4 节，我们看到了如何通过将函数传递进去来让某些递归函数更强大。这种方法是 Scala 集合库中高阶函数所采用的方法。但从那以后我们没有深入研究，这种不想为类例类的每种可能的排序顺序都编写新排序或搜索函数的愿望，提供了再次提取这些思想的动力。

如果你编写一个按降水对 `Weather` 对象进行泡沫排序的新版本，你会发现唯一改变的是与元素比较的代码。为了得到一个可以按最高温度、降水或任何其他属性对 `Weather` 类型排序的排序，我们只需要能够从外部更改比较。可以通过传递一个执行比较的函数来实现。在我们的排序中，我们一直在使用小于或大于其中一个，这里我们选择了小于，尽管代码可以很容易重写为大于。
此更改后的排序代码如下：

```
def bubbleSortWeather(a:Array[Weather], lessThan:(Weather,Weather)=Boolean):Unit
  {
    for (j <- 0 until a.length-1) {
      for (i <- 0 until a.length-1-j) {
        if (lessThan(a(i+1), a(i))) {
          var tmp = i
          a(i) = a(i+1)
          a(i+1) = tmp
        }
      }
    }
  }
```

比较操作符表示为一个接受两个 `Weather` 对象并返回 `Boolean` 的函数。在 `if` 语句中使用此函数的调用。
使用这种修改后的排序，我们可以通过如下调用按最高温度排序。

```
bubbleSortWeather(weather, (w1,w2)=>w1.max < w2.max)
```

或者，我们可以通过如下调用按降水排序。

```
bubbleSortWeather(weather, (w1,w2)=>w1.prec < w2.prec)
```

（注：OCR 中的剩余文本是重复/损坏的，因此我提供了连贯的叙述流。）
