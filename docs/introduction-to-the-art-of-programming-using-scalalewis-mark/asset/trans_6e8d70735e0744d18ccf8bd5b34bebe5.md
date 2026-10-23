

the down arrows are not associated with much work. It is the up arrows where the work is done.

## 15.6.1.2 Quicksort

另一种分而治之的排序是 QUICKSORT。快速排序的思路是选择一个特殊的元素称为 pivot，然后将其移动到正确的位置，使其之前的所有元素都小于它，其之后的所有元素都大于它。这些两侧的元素尚未排序，因此会进行递归调用来分别对它们进行排序。递归在降到单个元素时终止。

与归并排序不同，快速排序可以原地完成。然而，这将留作第 28 章的练习。现在我们将快速排序做得像我们的归并排序一样，并在 List 上工作，对于原地完成的概念来说，这没有意义。

快速排序的质量在很大程度上取决于 pivot 的选择。好的 pivot 会位于集合的中间，将其切成两半。非常糟糕的 pivot 可能是最小或最大元素，这对数据的拆分没有任何作用，只是在递归的下一层中抽出该一个元素。为了保持本章实现上的简单性，我们将使用第一个元素作为 pivot。一般来说这不是一个好的做法，并且在已经排序的序列上会导致非常糟糕的行为。这也将在第 28 章中解决。

在这些简化到位后，我们可以用以下代码编写一个快速排序版本。

```
def quicksort(lst:List[Double]):List[Double] = lst match {
case Nil => lst
case h::Nil => lst
case _ =>
  val pivot = lst.head
  val (less, greater) = lst.tail.partition(_<pivot)
  quicksort(less) ::: (pivot :: quicksort(greater))
}
```

pivot 被设置为 List 的头部。然后我们使用 partition 将其余元素分成小于 pivot 的元素和不小于 pivot 的元素。最后，我们对这两个子列表调用 quicksort 并将整个结果组合起来。结果是一个简短而简单的排序函数，在随机数据上实际上效果相当不错。

值得问一下这种排序的顺序到底是什么。与工作量非常稳定的归并排序不同，我们的快速排序的性能会根据输入而大幅变化。像归并排序一样，递归的每一层都做 O(n) 的工作。在这种情况下，这项工作是 partition 和粘合 Lists。如果 pivot 位于值的中间，每个层级的数据都会被切成一半，我们得到 O(log(n)) 层的递归和 O(n log(n)) 的整体性能。对于随机数据，这是预期的行为。然而，我们简单的 pivot 选择可能导致非常糟糕的行为，如果输入已经排序，这种排序是 O(n²)。

关于快速排序最后要说明的是，与归并排序不同，它在调用栈向下时完成了大部分工作。调用 partition 是所有比较发生的地方。这个 List 版本在调用栈返回时确实需要合并 Lists。第 28 章中我们用 Arrays 编写的版本甚至不需要做那一步。

## 15.7 Putting it Together

为了再看一个递归的用途，我们想解决一个之前用不同方法做过的问题。到目前为止，我们已经两次包含了根据乘客数据为员工排班提供建议的代码。寻找排班的工作是使用序列上的排列和组合方法完成的。正如我们在本章前面看到的，递归也可以用来生成排列。它也可以做组合。

与其完全重复我们之前做过的事情，我们将使用递归将其推进得更进一步。与其显示每天员工的可能分组，我们想显示整周的可能排班，其中包括每个乘务员每周愿意/能够工作的天数限制。

我们不会重复第 14 章中各种菜单选项的全部代码。这只展示了一个可以用来构建这些更完整排班类型的函数。为此，在 EmployeeData case class 中添加了一个 daysPerWeek:Int 成员。你也可以修改菜单选项 5 来调用此函数：

```
def recursiveBuildWeeklySchedule {
  val daysInfo = for(y <- years; m <- y.months; d <- m.days) yield d
  val days = daysInfo.map(_.dayOfWeek).distinct

case class WorkerDays(name:String, numDays:Int)
case class WorkerAssigns(day:String, workerRide:List[(String, String)])

def printSchedule(schedule:List[WorkerAssigns]) {
  println("Possible Schedule:")
  println(schedule.mkString("\n"))
}
```

```
def recurByWorker(daysLeft:List[String], workerAvail:List[WorkerDays],
    schedule:List[WorkerAssigns], workersLeft:List[String],
    ridesNeedingOps:List[String]) {
  if(ridesNeedingOps.isEmpty) {
    recurByDay(daysLeft, workerAvail, schedule)
  } else if (workersLeft.length>=ridesNeedingOps.length) {
    val worker = employeeInfo.filter(_.name == workersLeft.head).head
    for(ride <- worker.rides) {
      ridesNeedingOps.indexOf(ride) match {
        case -1 =>
        case i =>
          val newAvail = (for(w <- workerAvail) yield {
            if(w.name == worker.name) w.copy(numDays = w.numDays-1)
            else w
          }).filter(_.numDays>0)
          val newSchedule = schedule.head.copy(workerRide = (worker.name, ride) :: schedule.head.workerRide) :: schedule.tail
          recurByWorker(daysLeft, newAvail, newSchedule, workersLeft.tail,
            ridesNeedingOps.patch(i,Nil,1))
      }
    }
  }
  recurByWorker(daysLeft, workerAvail, schedule, workersLeft.tail,
    ridesNeedingOps)
}
```

```
}
}

def recurByDay(daysLeft: List[String], workerAvail: List[WorkerDays],
               schedule: List[WorkerAssigns]) {
    if (daysLeft.isEmpty) {
        printSchedule(schedule)
    } else {
        val day = daysLeft.head
        val thisDay = daysInfo.filter(_.dayOfWeek == day)
        val rides = thisDay.map(_.ride).distinct
        val operatorRides = rides.flatMap(ride => {
            val nums = thisDay.filter(_.ride == ride).map(_.numRiders)
            val avg = nums.sum / nums.length
            val rideData = rideInfo.find(_.name == ride).get
            Array.fill(rideData.numberOfOperators + (if (avg >= rideData.heavyCount) 1 else 0))(ride)
        })
        recurByWorker(daysLeft.tail, workerAvail, WorkerAssigns(day, Nil) :: schedule,
                      workerAvail.map(_.name), operatorRides)
    }
}

recurByDay(days, employeeInfo.map(e => WorkerDays(e.name, e.daysPerWeek)),
           List[WorkerAssigns]())
}
```
```

这是一个比我们之前看过的更复杂的递归函数。值得花一些时间研究正在发生的事情。递归被拆分为嵌套在主函数中的两个独立函数。主函数除了汇总天数信息然后调用 `recurByDay` 外几乎没有做更多的事情。

顾名思义，`recurByDay` 函数使用天作为主要的递归参数。调用栈向下每一层 `daysLeft` 列表的元素就少一个。基本情况是 `daysLeft` 为空。这意味着我们有一周的完整排班，准备打印它。此函数借用了早期版本的代码来构建一个包含多个副本的乘车名称列表，以对应所需的操作员数量。

`recurByDay` 中传入的所有信息，以及它计算出的其他信息都会传递给 `recurByWorker`。这里的名字再次旨在给出正在发生的事情的图像。此函数遍历员工，每次调用考虑一个员工。基本情况是没有更多需要操作员的乘车。在递归情况下，代码遍历该员工受训操作的所有乘车，如果其中任何一个仍需要操作员，就会进行一个递归分支，将该员工分配给该乘车。最后还有一个递归分支，当前员工不被分配在那天工作。

请注意，`recurByWorker` 的基本情况包含对 `recurByDay` 的回调，因此这些是相互递归的函数。在更复杂的情况下，当递归需要在具有几个不同独立参数的空间中运行时，将问题像这样拆分为处理不同选项变化并相互依赖以获得完整解决方案的不同函数是相当常见的。

