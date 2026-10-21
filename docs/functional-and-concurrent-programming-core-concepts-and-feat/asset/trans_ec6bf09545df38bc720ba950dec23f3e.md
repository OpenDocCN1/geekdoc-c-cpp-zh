

这个示例启动了一个 1 秒的任务和一个 2 秒的任务，并在每个任务上注册了一个简单的回调。它会产生如下形式的输出：

```
main at XX:XX:33.413: START
main at XX:XX:33.465: END
pool-1-thread-3 at XX:XX:34.466: Success(42)
pool-1-thread-3 at XX:XX:35.465: Failure(java.lang.NullPointerException)
```

你可以看到主线程会立即终止——回调注册几乎不花费时间。一秒后，第一个回调运行并打印一个 Success 值。再过一秒，第二个回调运行并打印一个 Failure 值。在此输出中，两个回调都在同一个线程上运行，但不能保证这种情况总会发生。

你可以在广告获取场景中使用回调。与在 26.2 节的示例中等待自定义广告来组装页面不同，你指定一个操作作为广告一旦可用时要执行的操作：

```
val futureAd: Future[Ad] = Future(fetchAd(request))
val data: Data = dbLookup(request)
futureAd.onComplete { ad =>
  val page = makePage(data, ad.get)
  connection.write(page)
}
```

清单 26.3：带回调的未来广告获取示例。

在连接处理线程完成数据库查找后，它在广告获取任务上注册一个回调操作，而不是等待任务完成。回调操作从 Try 值中提取自定义广告（假设没有错误），将数据和广告组装成页面，并像之前一样将其作为回复发送回去。与清单 26.2 的主要区别在于，不涉及任何阻塞。

## 26.3 Future 上的高阶函数

通过使用回调来组装和发送页面，你避免了阻塞，从而消除了死锁的风险。然而，由于 onComplete 的函数参数是一个操作，该操作是为了其副作用而执行的，因此丢失了一些早期的函数式风格。请回忆在清单 25.2 中的服务器完整版本中，组装好的页面还用于统计保持函数。如果作为未来产生的值需要在多个地方使用，使用回调来处理这些使用可能会变得复杂。如果该值

是异步使用的，你甚至可能需要回调中的回调，这很难编写，也更难调试。更好的解决方案是将回调的非阻塞特性带入保持更函数式风格的代码中。

在我们重访 26.5 节中的广告获取示例之前，考虑这个基于回调的函数：

```
Scala
def multiplyAndWrite(futureString: Future[String], count: Int): Unit =
  futureString.onComplete {
    case Success(str) => write(str * count)
    case Failure(e)   => write(s"exception: ${e.getMessage}")
  }
```

在某处，一个输入字符串正在异步生成。它作为未来传递给函数 multiplyAndWrite。该函数使用回调来重复字符串多次并写入结果——在 Scala 中，“A” * 3 是 “AAA”。这种方法要求你在回调操作中指定你想对字符串 str * count 做的一切，而该字符串在回调之外不存在。这是可能复杂性和模块化丧失的来源。用某种方式返回字符串 str * count 并使其可供任何需要它的代码使用的 multiply 函数来替换 multiplyAndWrite 可能会更有优势。

然而，在这个 multiply 函数内部，可能还没有要乘的字符串可用——它的计算可能仍在进行中。你也不能等待它，因为你想避免阻塞。相反，你需要将乘法的字符串本身作为未来返回。因此，multiply 的返回类型不是 String，而是 Future[String]。要返回的未来可以使用承诺创建，如清单 25.4 所示：

```
Scala
def multiply(futureString: Future[String], count: Int): Future[String] =
  val promise = Promise[String]()
  futureString.onComplete {
    case Success(str) => promise.success(str * count)
    case Failure(e)   => promise.failure(e)
  }
  promise.future
```

你创建一个承诺来保存乘法的字符串，并创建一个回调操作来兑现该承诺。如果未来 futureString 产生一个字符串，回调会将其乘以并成功兑现承诺。否则，承诺会失败，因为没有可用于乘法的字符串。

现在有趣的部分来了。从概念上讲，前面的代码与字符串和乘法关系不大。它真正做的是转换未来产生的值，以便创建一个新的未来。当然，我们以前见过这种模式——例如，将函数应用于选项的内容——以高阶函数 map 的形式出现。不是关注字符串乘法的特殊情况，你可以编写一个通用的未来上的 map 函数：

```
def map[A, B](future: Future[A], f: A => B): Future[B] =
  val promise = Promise[B]()
  future.onComplete {
    case Success(value) => promise.complete(Try(f(value)))
    case Failure(e)     => promise.failure(e)
  }
  promise.future
```

该函数是为通用类型 A 和 B 定义的，而不是字符串。与函数 multiply 的唯一有意义的区别是 f 可能会失败并且在 Try 内部被调用。因此，承诺可能因两个原因之一而失败：没有产生类型 A 的值来应用 f，或者函数 f 本身的调用失败。

提出 map 的好处在于它带我们进入一个熟悉的世界，即高阶函数，如第 9 章和第 10 章以及第一部分中讨论的那样。事实上，Try 类型本身有一个 map 方法，你可以使用它来简化未来上 map 的实现：

```
def map[A, B](future: Future[A], f: A => B): Future[B] =
  val promise = Promise[B]()
  future.onComplete(tryValue => promise.complete(tryValue.map(f)))
  promise.future
```

清单 26.4：在未来上重新实现高阶函数 map。

注意错误情况是如何透明地处理的，这要归功于 Try 类型（参见第 13.3 节，了解 Try 上 map 的行为）。

函数作为值和高阶函数构成了函数式编程的一个基本方面。第 25 章介绍了未来作为一种方式，通过依赖于适用于产生值的任务的机制，使并发编程更具函数式。一旦你选择函数式，就不应该对高阶模式开始出现感到惊讶。但故事并没有止步于 map。未来上的各种高阶函数催生了一种强大的并发编程风格，它既是函数式的又是非阻塞的。

你不需要在未来上重新实现 map：Scala 未来已经有一个 map 方法。你可以简单地按如下方式编写 multiply 函数：

```
def multiply(futureString: Future[String], count: Int): Future[String] =
  futureString.map(str => str * count)
```

最后两个函数可能比 flatMap/map 变体更容易阅读。尽管如此，你应该牢记 flatMap 的基本性质。事实上，zip 和 zipWith 可以使用 flatMap 实现。

一位经验丰富的 Scala 程序员可能会这样编写 multiply：

```
def multiply(futureString: Future[String], futureCount: Future[Int]): Future[String] =
  for str <- futureString; count <- futureCount yield str * count
```

请回忆第 10.9 节，Scala 中的 for-yield 是作为 map 和 flatMap（以及 withFilter）的组合实现的。该代码将被编译器转换为之前的 flatMap/map 版本。for-yield 语法非常好用，尤其是在处理未来时。我鼓励你在 Scala 编程时使用它。然而，正如前面注释中提到的，出于教学原因，我将在本书的示例中继续偏爱显式使用 map 和 flatMap。

通过使用 flatMap、zip 或 zipWith 将两个未来合并为一个，你可以将清单 26.1 的并行快速排序示例重写为非阻塞函数：

```
def quickSort(list: List[Int])(using ExecutionContext): Future[List[Int]] = list match
  case Nil => Future.successful(list)
case pivot :: others =>
  val (low, high) = others.partition(_ < pivot)
  val lowFuture  = Future.delegate(quickSort(low))
  val highFuture = quickSort(high)
  lowFuture.flatMap(lowSorted =>
    highFuture.map(highSorted => lowSorted ::: pivot :: highSorted)
  )
```

清单 26.5：并行快速排序的非阻塞实现。

为了避免阻塞，函数的返回类型从 List[Int] 改为 Future[List[Int]]。与之前一样，排序低值的任务被委托给线程池。你也可以等价地写成 lowFuture = Future(quickSort(low)).flatten。对高值使用直接递归调用，并将两个未来合并，遵循与函数 multiply 相同的模式。这种快速排序变体不涉及任何阻塞，与清单 26.1 相比，不可能发生死锁。¹

¹此实现仍然效率低下。其主要弱点是它为非常小的列表一直到空列表创建单独的排序任务。更现实的实现会在某个点停止并行化，并在当前线程内对短列表进行排序。例如，Java 的 Arrays.parallelSort 函数，一旦子数组的元素数少于或等于 8192 就会停止将其分发到单独的线程。

