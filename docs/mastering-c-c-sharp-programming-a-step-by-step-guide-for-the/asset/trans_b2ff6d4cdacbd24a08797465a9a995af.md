
线程涉及的内容相当多，我们没有篇幅深入讲解。相反，我们将探讨基础知识，以及你自己去查找更多信息时所需了解的内容。

## 线程任务

线程可用于处理很多事务，并且对于你能做什么、不能做什么并没有真正限制。不过，线程特别擅长的领域主要有两类。第一类是在后台执行任务，这意味着事情在发生的同时，你还可以继续更新 GUI 或同时做其他事情。这种情况很常见，通常会显示一个进度条，指示已完成或剩余的工作量。

第二类是当你有一大堆事情要做，并且可以将其分解为各自独立的部分时。多个线程将各自领取一部分并开始处理，同时不会妨碍其他线程。

正如我们所说，使用线程能做的事情实际上确实没有限制，但我们将使用第二类中的一个简单示例。假设我们有一个程序，其中包含一个 int 数组。我们想向该数组添加大量随机数，这些随机数在 0 到 99 之间。

如果我们不使用线程，程序可能会像这样：

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace Threading
{
    class Program
    {
```

```
static void Main(string[] args)
{
	int[] numbers = new int[10000];
	Random random = new Random();
	for (int index = 0; index < numbers.Length; index++)
	{
		numbers[index] = random.Next(100);
	}
}
```

然而，我们要做的是改变这段代码中的一些安排，以便我们能够使用线程。看一下代码；注意，尽管我们想用数字填充一个大列表，但每个数字都可以自行随机确定。它们都不依赖于其前一个或后一个数字。这使得创建多个线程变得非常容易，并且可以为每个线程提供一个数字块来处理。

## 为线程提取工作

我们需要做的第一件事是，把将要分配给线程的工作提取出来，并将其放到一个可以在单个线程上分配的位置。很快你就会发现，线程是通过一个方法启动的，它会在该方法中工作，但该方法不接受参数，也不会返回任何内容。因此，如果我们希望这些参数存在——这些参数实际上是我们希望它完成的工作——或者希望它返回某些内容，最好的办法是创建一个类，将工作和结果存储在其中，然后创建

一个不带返回值且不带参数的方法，供我们随后调用。

在我们开始之前，花几分钟坐下来思考这个类。它可能是什么样子？你认为其中应该包含哪些实例变量和属性？线程工作所在的方法会是什么样子？

以下是我想到的：

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace Threading
{
    public class GenerateNumbersTask
    {
        // This is done so that we have just one Random Class instance
        // being used, regardless of the number of tasks that we create.
        private static Random random = new Random();

        public int[] Numbers { get; set; }
        public int StartIndex { get; set; }
        public int Count { get; set; }

        public void GenerateNumbers()
        {
```

```
for (int index = StartIndex; index < StartIndex + Count; index++)
    {
        Numbers[index] = random.Next(100);
    }
}
}
}
```

这里我设置了三个属性。第一个名为 `Numbers`，它最终会有一个引用指向我们将要用随机数字填充的数组。我们还希望每个线程都能确切知道它要处理数组的哪一部分。为了便于实现，创建了 `StartIndex`——它告诉线程从哪个索引开始。最后，我们有 `Count`，它告诉线程将处理多少个数字。

假设我们创建 10 个线程，然后让每个线程生成 1000 个数字。每个线程都会有引用指向名为 `Numbers` 的数组，由于它们每个都生成 1000 个数字，`Count` 将完全相同。第一个线程的 `StartIndex` 为 0，第二个线程的 `StartIndex` 为 1000，依此类推。

最后，我们有一个名为 `GenerateNumbers` 的方法。生成随机数的工作就在这里完成，每个索引都在分配给它的范围内工作。请注意，`GenerateNumbers` 方法的返回类型为 `void`，这意味着不返回任何内容，而且它没有任何参数，因此我们可以开始使用它来启动线程。

## 启动线程

.NET 框架和 C# 内置了线程代码，你可以在 `System.Threading` 命名空间中找到它。要使用它，你需要将一个额外的语句放在代码的最顶部，与其他所有 “using” 语句放在一起：

并单独确保每个线程都完成任务后再继续处理下一个。这样说得通吗？等你看到相关的代码，可能就明白了：

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading;

namespace Threading
{
    class Program
    {
        static void Main(string[] args)
        {
            int[] numbers = new int[10000];

            // The list of threads and the list of tasks for the threads to get working on is prepared.
            int threadCount = 10;
            GenerateNumbersTask[] tasks = new GenerateNumbersTask[threadCount];
            Thread[] threads = new Thread[threadCount];

            for (int index = 0; index < threadCount; index++)
            {
```

```
// The task is created and it is set up with the correct
properties – these will be
    // our parameters.
    tasks[index] = new GenerateNumbersTask()
    {
        Numbers = numbers,
        Count = 1000,
        StartIndex = index * 1000
    };

    // Create the thread
    threads[index] = new
Thread(tasks[index].GenerateNumbers);

    // Start the thread running
    threads[index].Start();
}

// Wait and then join up with each of the threads in turn so
that
    // when we move on, we know that all of the work has been
done.
    for (int index = 0; index < threadCount; index++)
    {
        threads[index].Join();
    }
}
```

## 线程安全

以上涵盖了 C# 线程的基础知识，但现在我们将继续讨论与线程相关的更高阶内容。如果你已经用完了线程，那么完全可以直接进入下一节，但我认为我们将要讨论的内容非常重要。

在上一个例子中，我们的每个线程都有自己的工作要做，而且完全没有重叠。如果它们必须共享某些东西呢？请记住，所有线程都会在操作系统选择的时间被换出，而在那一刻，线程很可能正在做一些重要的任务。

试着想象你有一个游戏，里面有数百个对象，例如物体和由计算机控制的玩家。所有这些对象都必须更新。它们都放在一个数组中，并且有一个索引指示接下来要更新哪个对象。

我们可以把所有这些工作拆分开来，让不同的线程处理其中不同的部分——每个线程负责更新一部分对象。由于某些对象会快速更新，而另一些需要更长时间，我们需要考虑一种方法：工作线程一个接一个地更新对象，直到所有对象都更新完成。

当某个工作线程没有事情可做时，它会调用一个方法来帮助自己确定接下来该做什么。在该方法内部，线程可以获得需要处理的对象的引用，并将索引（指示需要处理哪个对象）推进到下一个对象。这样，当下一个线程调用该方法时，它就会拿到下一个对象。

然而，这并不像我们想象中那么轻松。如果一个线程拿到了更多工作，拾取了要处理的对象的引用，但在它能够将索引移到下一项之前，操作系统决定切换
