

## 21.3 不同类型的线程池

概念上，线程池由一个任务队列和一组工作线程组成。我们已经见过 newCachedThreadPool，它使用无限数量的线程且没有队列，³ 以及 newFixedThreadPool，它使用固定数量的线程和一个无界 FIFO 队列。JVM 线程池在类 ThreadPoolExecutor 中实现，该类高度可定制。特别是，你可以指定线程创建的工厂、在任务进入队列前保持活跃的最小线程数、当队列已满时创建的额外线程的最大数量、当不需要时这些额外线程被从池中移除前的时长、要使用的队列类型（例如有界或无界、FIFO 或优先级），以及当队列已满且已达到最大活跃线程数时如何处理资源耗尽。你还可以使用各种“钩子”来指定在任务开始或结束时、或线程池关闭时运行的自定义代码。

作为示例，下一个示例自定义了多个线程池元素：

```
object exec extends ThreadPoolExecutor(
  4,
  16,
  3, MINUTES,
  ArrayBlockingQueue(128),
  ThreadPoolExecutor.CallerRunsPolicy()
):
  override def beforeExecute(thread: Thread, task: Runnable): Unit =
    logger.info(() => s"${thread.getName} starts task $task"
```

池维护最少四个工作线程，准备运行任务。如果全部四个线程都忙，任务会被排入一个基于数组的容量为 128 的队列。如果该队列已满，则最多创建 12 个额外线程，使最大池大小达到 16。之后，这些额外线程在空闲 3 分钟后会被终止。如果全部 16 个线程都忙，队列已满，并且提交了一个新任务，则提交任务的线程会运行它。CallerRunsPolicy 是一种方便的方式，可以在同时减少任务创建速率的情况下引入额外的 worker；在服务器示例中，这将使监听线程在一段时间内运行连接处理代码。最后，每次任务开始运行时都会记录信息。

为方便起见，通常会为创建任务的代码提供一个默认线程池。你可以在 Scala 中将其作为 scala.concurrent.ExecutionContext.global 访问，在 Java 中作为 java.util.concurrent.ForkJoinPool.commonPool 访问。其大小通常基于（但不一定等于）运行时可用核心的数量。因为

³更准确地说，池使用一个零容量队列，该队列始终为空。

该线程池不会被关闭，其线程以守护模式启动，以便不阻止 JVM 终止（参见第 17 章，脚注 3）。⁴

除了标准线程池之外，类 ScheduledThreadPoolExecutor 扩展了 ThreadPoolExecutor，并提供了用于计划任务的机制。它定义了若干方法来延迟和/或重复任务执行，因此可作为计时器使用。例如，你可以修改字母打印示例以使用计划线程池：

```
println("START")
val exec = Executors.newScheduledThreadPool(2)

exec.schedule(() => println('A'): Runnable, 5, SECONDS)
exec.scheduleAtFixedRate(() => println('B'), 3, 10, SECONDS)
exec.scheduleWithFixedDelay(() => println('C'), 3, 10, SECONDS)

println("END")
```

清单 21.5：使用计时器池进行计划执行的示例。

字母 A 被安排在 5 秒后显示。⁵ 字母 B 和 C 被安排在 3 秒后显示，然后每隔 10 秒重复显示一次。典型的输出如下所示：

```
main at 09:23:41.514: START
main at 09:23:41.517: END
pool-1-thread-1 at 09:23:44.518: B
pool-1-thread-2 at 09:23:44.518: C
pool-1-thread-1 at 09:23:46.517: A
pool-1-thread-2 at 09:23:54.521: B
pool-1-thread-1 at 09:23:54.521: C
pool-1-thread-2 at 09:24:04.517: B
pool-1-thread-1 at 09:24:04.522: C
...
```

执行在 09:23:41 开始。三秒后，在 09:23:44，字母 B 和 C 被打印。两秒后——从开始算起 5 秒——字母 A 被打印。在 09:23:54，即首次显示后 10 秒，字母 B 和 C 再次被打印，之后重复。

B 和 C 下一次显示之间轻微的时间差异说明了 scheduleAtFixedRate 和 scheduleWithFixedDelay 的区别。字母 B 的显示每 10 秒启动一次（固定速率），而字母 C 的显示在同一事件上一次出现后 10 秒启动（固定延迟）。由于显示字母需要时间，字母 C 会在字母 B 之后几毫秒打印。这种差异会随时间累积。字母 B 总是在 09:23:44 加上 10 秒的倍数的时间显示；字母 C 总是在上一次显示后 10 秒打印，与开始时间无关。稍后时间的输出显示 B 和 C 之间的时间差异已经增加：

```
...
pool-1-thread-2 at 10:15:14.524: B
pool-1-thread-1 at 10:15:15.526: C
pool-1-thread-2 at 10:15:24.521: B
pool-1-thread-1 at 10:15:25.531: C
...
```

程序启动 52 分钟后，字母 C 比字母 B 晚了整整一秒。你在任务完成时间异常时也可能观察到固定速率调度和固定延迟调度的区别。例如，如果出于某种原因打印单个 B 被延迟并花费整整一分钟完成，随后会以快速连续的方式进行多次 B 的显示，以维持期望的速率。相比之下，如果 C 的打印被延迟，则会跳过错过的运行，下一次显示在 10 秒后进行。

> ⁴这种方法往往使默认池不适合小型说明性示例，因为 JVM 会过早终止。出于这个原因，我在这本书中很少使用它，而是依赖于非守护线程的自定义池。

> ⁵由于另一个重载的 schedule 方法，需要类型标注 :Runnable。

## 21.4 并行集合

清单 21.4 中的并行服务器是无缝并发编程的示例，前提是方法 handleConnection 必须是线程安全的。如果服务器的请求相互独立且无需相互交互，则更容易实现。这与通常情况一样，共享越少，并行化越容易。

基于此精神，并发库提供服务，通过在隐藏底层线程池的同时并行处理独立数据。以下示例说明了这一点：

```
Scala
println("START")

def distinctWordsCount(url: URL): Int =
  println(s"start $url")
  val count =
    Using.resource(Source.fromURL(url)(UTF8)) { source =>
      source
        .getLines()
        .flatMap(line => line.split("""\b"""))
        .map(word => word.filter(_.isLetter).toLowerCase)
        .filter(_.nonEmpty)
        .distinct
```

```
.size
}
println(s"end $url")
count

val urls: List[URL] = ...

val counts = urls.map(distinctWordsCount)
println(counts.max)

println("END")
```

该程序的想法是对 URL 列表应用函数 distinctWordsCount 以找到产生的最大值。函数计算源中不同单词的数量，其实现细节并不重要（参见第 12.6 节，了解更多此类流水线计算的示例）。

在十本经典书籍的列表上运行此程序会产生以下形式的输出：⁶

```
main at XX:XX:03.586: START
main at XX:XX:03.620: start https://gutenberg.org/files/13951/13951-0.txt
main at XX:XX:09.000: end https://gutenberg.org/files/13951/13951-0.txt
main at XX:XX:09.000: start https://gutenberg.org/files/2650/2650-0.txt
main at XX:XX:12.715: end https://gutenberg.org/files/2650/2650-0.txt
main at XX:XX:12.715: start https://gutenberg.org/files/98/98-0.txt
main at XX:XX:15.634: end https://gutenberg.org/files/98/98-0.txt
main at XX:XX:15.635: start https://gutenberg.org/files/1342/1342-0.txt
main at XX:XX:18.336: end https://gutenberg.org/files/1342/1342-0.txt
main at XX:XX:18.336: start https://gutenberg.org/files/76/76-0.txt
main at XX:XX:20.840: end https://gutenberg.org/files/76/76-0.txt
main at XX:XX:20.841: start https://gutenberg.org/files/4300/4300-0.txt
main at XX:XX:26.460: end https://gutenberg.org/files/4300/4300-0.txt
main at XX:XX:26.460: start https://gutenberg.org/files/28054/28054-0.txt
main at XX:XX:33.829: end https://gutenberg.org/files/28054/28054-0.txt
main at XX:XX:33.829: start https://gutenberg.org/files/6130/6130-0.txt
main at XX:XX:37.955: end https://gutenberg.org/files/6130/6130-0.txt
main at XX:XX:37.955: start https://gutenberg.org/files/2000/2000-0.txt
main at XX:XX:45.789: end https://gutenberg.org/files/2000/2000-0.txt
main at XX:XX:45.789: start https://gutenberg.org/files/1012/1012-0.txt
main at XX:XX:48.152: end https://gutenberg.org/files/1012/1012-0.txt
main at XX:XX:48.155: 29154
main at XX:XX:48.155: END
```

所有源都由主线程顺序处理。整个计算大约需要 45 秒。然而，对 URL 进行单词计数是完全独立的

⁶该应用程序是 I/O 密集型的，计算机速度很快。在本节的示例输出中，单词处理被人为放慢，以便观察更有意义且可预测的时间。

