

- 如果一个操作被阻塞（例如在等待 I/O 完成时），你如何检测到这种情况并安排处理器运行不同的操作而不是空闲等待？
- 如何确定一个或多个并发操作已完成？

对于应用程序开发人员来说，第一个问题是应用程序设计的问题。剩余的问题取决于程序化基础设施。Microsoft 在 System.Threading.Tasks 命名空间中提供了 Task 类和一组相关类型，以帮助解决这些问题。

## Important

关于应用程序设计的一点是根本性的。如果一个应用程序不是以多任务为目标来实现的，那么无论你投入多少处理器核心，它运行的速度都不会比在单核机器上更快。

## Tasks, threads, and the ThreadPool

Task 类是对并发操作的抽象。你创建一个 Task 对象来运行一段代码。你可以实例化多个 Task 对象，并在有足够处理器或处理器核心可用时并行启动它们。

### Note

从现在开始，我将使用术语 processor 来指代单核处理器或多核处理器上的单个处理器核心。

在内部，Windows Runtime（WinRT）使用 Thread 对象和 ThreadPool 类来实现任务并安排其执行。多线程和线程池自 .NET Framework 1.0 版本以来就已可用，如果你正在构建传统的桌面应用程序，可以直接在代码中使用 System.Threading 命名空间中的 Thread 类。然而，Thread 类不适用于通用 Windows 平台（UWP）应用；相反，你使用 Task 类。

Task 类提供了强大的线程抽象，你可以轻松地区分应用程序中的并行化程度（任务）和并行化单元（线程）。在单处理器计算机上，这些项目通常是相同的。然而，在具有多个处理器或多核处理器的计算机上，它们是不同的。如果你直接基于线程设计程序，你会发现你的应用程序可能无法很好地扩展；程序将使用你显式创建的线程数量，并且操作系统将只调度该数量的线程。这可能导致过载和响应时间差，如果线程数量远远超过可用处理器数量，或者如果线程数量少于处理器数量，则会导致效率低下和吞吐量差。

WinRT 优化了实现一组并发任务所需的线程数量，并根据可用处理器数量高效地调度它们。它实现了一种排队机制，将工作负载分配到分配给线程池的一组线程中（使用 ThreadPool 对象实现）。当程序创建一个 Task 对象时，该任务将被添加到全局队列中。当一个线程可用时，任务将从全局队列中移除并由该线程执行。ThreadPool 类实现了许多优化，并使用工作窃取算法来确保线程被高效调度。

![](img/16f6e3fe08f01ddadb2741a92c392b0e_607_0.png)

### Note

ThreadPool 类在 .NET Framework 的早期版本中可用，但在 .NET Framework 4.0 中得到了显著增强，以支持 Tasks。

你应该注意，创建来处理你的任务的线程数量不一定与处理器数量相同。根据工作负载的性质，一个或多个处理器可能忙于为其他应用程序和服务执行高优先级工作。因此，你应用程序的最佳线程数可能少于机器中的处理器数量。或者，应用程序中的一个或多个线程可能在等待长时间运行的内存访问、I/O 或网络操作完成，从而使相应的处理器空闲。在这种情况下，最佳线程数可能多于可用处理器数量。WinRT 遵循一种迭代策略，即 hill-climbing algorithm，以动态确定当前工作负载的理想线程数。

重要的是，你在代码中要做的全部工作就是将应用程序划分为可以并行运行的任务。WinRT 负责根据计算机的处理器架构和工作负载创建适当数量的线程，将你的任务与这些线程关联并安排它们高效运行。即使你将工作划分为过多的任务也没关系，因为 WinRT 将尝试仅运行实际可行的并发线程数量；事实上，鼓励你过度划分工作，因为这将有助于确保你的应用程序在移动到具有更多可用处理器的计算机时能够扩展。

## Creating, running, and controlling tasks

你可以通过使用 *Task* 构造函数创建 *Task* 对象。*Task* 构造函数是重载的，但所有版本都期望你提供一个 *Action* 委托作为参数。第 20 章“Decoupling application logic and handling events”说明了 *Action* 委托引用一个不返回值的方法。*Task* 对象在被调度运行时调用此委托。以下示例创建一个使用委托运行名为 *doWork* 的方法的 *Task* 对象：

Click here to view code image

```
Task task = new Task(doWork);
...
private void doWork()
{
    // The task runs this code when it is started
    ...
}
```

![](img/16f6e3fe08f01ddadb2741a92c392b0e_608_0.png)

### Tip

默认的 *Action* 类型引用一个不带参数的方法。*Task* 构造函数的其他重载接受一个 *Action<object>* 参数，表示引用带有一个 *object* 参数的方法的委托。通过这些重载，你可以将数据传递到任务运行的方法中。以下代码显示了一个示例：

Click here to view code image

```
Action<object> action;
action = doWorkWithObject;
object parameterData = ...;
Task task = new Task(action, parameterData);
...
private void doWorkWithObject(object o)
{
    ...
}
```

创建 *Task* 对象后，你可以使用 *Start* 方法将其启动，如下所示：

```
Task task = new Task(...);
task.Start();
```

*Start* 方法是重载的，你可以可选地指定一个 *TaskCreationOptions* 对象以提供有关如何调度和运行任务的提示。

### More info

有关 *TaskCreationOptions* 枚举的更多信息，请参阅随 Visual Studio 提供的描述 .NET Framework 类库的文档。

创建和运行任务是一个非常常见的过程，*Task* 类提供了静态 *Run* 方法来合并这两个操作。*Run* 方法接受一个指定要执行操作的 *Action* 委托（与 *Task* 构造函数类似），但会立即启动任务运行。它返回对 *Task* 对象的引用。你可以像这样使用它：

Click here to view code image

```
Task task = Task.Run(() => doWork());
```

当任务运行的方法完成时，任务结束，用于运行任务的线程可以被回收以执行另一个任务。

当任务完成时，你可以通过创建 *continuation* 来安排另一个任务立即被调度。为此，调用 *Task* 对象的 *ContinueWith* 方法。当 *Task* 对象执行的操作完成时，调度程序会自动创建一个新的 *Task* 对象来运行 *ContinueWith* 方法指定的操作。延续指定的方法期望一个 *Task* 参数，调度程序将传递对已完成的任务的引用到该方法中。*ContinueWith* 返回的值是对新的 *Task* 对象的引用。以下代码示例创建一个运行 *doWork* 方法的 *Task* 对象，并指定一个延续，在第一个任务完成后在新任务中运行 *doMoreWork* 方法：

Click here to view code image

```
Task task = new Task(doWork);
task.Start();
Task newTask = task.ContinueWith(doMoreWork);
...
private void doWork()
{
    // The task runs this code when it is started
    ...
}
...
private void doMoreWork(Task task)
{
    // The continuation runs this code when doWork completes
    ...
}
```

*ContinueWith* 方法是高度重载的，你可以提供一个

