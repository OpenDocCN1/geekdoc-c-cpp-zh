

```
Employee newEmp1 = (Employee)newXs.Deserialize(fs);
if (newEmp1 != null) {
    listBox1.Items.Add(newEmp1.ID);
    listBox1.Items.Add(newEmp1.Name);
    listBox1.Items.Add(newEmp1.Salary);
}
fs.Close();
```

在前面的代码片段中，我们创建了 FileStream 类的对象来读取序列化对象，即 employee.xml XML 文件。之后，我们通过指定 Employee 的类型信息创建了 XmlSerializer 类的对象。然后，我们调用 XmlSerializer 对象的 Deserialize() 方法，并传入 FileStream 对象，并借助显式类型转换将 Deserialize() 方法返回的值赋给 Employee 类的引用变量。Employee 对象的数据已添加到列表框中。最后，我们调用了 FileStream 对象的 Close() 方法。

8. 按 F5 键运行 ObjectSerializationInXMLWithoutSCA 应用程序。在最终输出中，您可以单击 Serialize Data 按钮以在 Web 浏览器中显示 XML 文件 newEmployee.xml 的数据。当您单击 Deserialize Data 按钮时，Employee 对象的数据会显示在列表框中。图 30.12 显示了最终输出：

![](img/e073a4882197be4ab61103cbe0bcb394_1487_0.png)

图 30.12：显示 ObjectSerializationInXMLWithoutSCA 应用程序的输出

现在，让我们总结一下本章讨论的主要主题。

## Summary

在本章中，您学习了 XML 以及它如何与 .NET 结合在 Web 上交换不同类型的数据。您还学习了 System.Xml 命名空间，其中包含处理 XML 文档的类。接下来，您学习了如何在 .NET Framework 4.0 中使用流式 XML 并实现 DOM。您还学习了 XPath，它用于导航到 XML 文档的不同部分；以及用于将 XML 文档转换为其他格式的 XSLT。您还学习了 XML 如何与 ADO.NET 结合使用。此外，您还学习了如何通过使用 XML 进行对象序列化来序列化或反序列化对象。

在下一章中，您将学习 C# 2010 中的线程。

## 31

## Threading in C# 2010

| if you need an Immediate Solution to: | See page: |
|---|---|
| Creating a Thread | 1454 |
| Starting a Thread | 1454 |
| Putting a Thread to Sleep | 1455 |
| Suspending a Thread | 1456 |
| Resuming a Thread | 1457 |
| Stopping a Thread | 1458 |
| Creating a Multithreaded Application | 1460 |
| Setting Priority of a Thread | 1461 |
| Determining State of a Thread | 1463 |
| Joining Threads | 1465 |
| Synchronizing Threads | 1467 |

## In Depth

线程是一系列必须按特定顺序执行的指令，以便在程序内执行特定任务。正在执行的程序称为进程，线程可以是正在执行程序的一部分。进程在操作系统（OS）中执行；而线程在进程内执行。因此，线程也被称为轻量级进程。线程与进程之间一个主要区别是，进程彼此完全隔离。这意味着一个进程的运行不会影响操作系统中运行的另一个进程的运行。然而，线程可以与同一应用程序中运行的其他线程共享内存。例如，一个线程可以在后台获取数据，而另一个线程可以同时显示由第一个线程接收到的数据。进程的执行从 Main() 线程开始，该线程在进程执行时自动启动；而其他线程需要通过传递 Thread 类的方法来启动。如果一个进程包含一个以上的线程，则称为多线程。多线程应用程序能够同时执行多个任务，例如在同一操作系统上创建应用程序、下载电影和收听音乐。为了确保线程在多线程环境中的顺畅运行，您需要根据线程需要执行的任务为线程分配优先级级别。

在本章中，您将学习 Thread 类及其方法和属性。接下来，本章讨论了多线程的概念，该概念促进了在进程中同时运行多个任务。您还将学习可以分配给线程的各种优先级级别。本章随后继续讨论线程的各种状态。最后，您将学习如何在多线程环境中同步线程以避免任何死锁情况。

## The Thread Class

在 C# 中，线程（Main() 线程）在由公共语言运行时（CLR）和操作系统（OS）自动创建的进程中启动。要在 C# 程序中启用线程，您必须添加 System.Threading 命名空间，如下所示：

```
using System.Threading;
```

Thread 类是一个包含各种方法和属性的类，用于创建和控制线程、设置其优先级并获取其状态。表 31.1 列出了 Thread 类的一些值得注意的公共方法：

### Table 31.1: Noteworthy Public Methods of the Thread Class

| Name | Description |
|------|-------------|
| Abort() | 终止当前线程并在调用它的线程上引发 ThreadAbortException 异常 |
| AllocateDataSlot() | 在所有线程上分配一个未命名的数据槽。此方法使用标记有 ThreadStaticAttribute 属性的字段以获得更好的性能。 |
| AllocateNamedDataSlot() | 在所有线程上分配一个命名的数据槽。此方法使用标记有 ThreadStaticAttribute 属性的字段以获得更好的性能。 |
| BeginThreadAffinity() | 通知主机托管代码即将执行依赖于当前操作系统线程的线程。 |
| EndThreadAffinity() | 通知主机托管代码已完成对依赖于当前操作系统线程的线程的执行。 |
| FreeNamedDataSlot() | 删除名称与所有线程进程中的槽之间的关联。此方法使用标记有 ThreadStaticAttribute 属性的字段。 |
| GetApartmentState() | 返回指示 ApartmentState 对象状态的值。 |
| GetData() | 从当前线程检索值。此方法使用标记有 ThreadStaticAttribute 属性的字段。 |

### Table 31.1: Noteworthy Public Methods of the Thread Class

| Name | Description |
|------|-------------|
| GetDomain() | 返回当前线程正在运行的当前域。 |
| GetDomainID() | 返回唯一的应用程序域标识符。 |
| GetHashCode() | 返回当前线程的哈希码。 |
| GetNamedDataSlot() | 查找命名数据槽。此方法使用标记有 ThreadStaticAttribute 属性的字段。 |
| Interrupt() | 中断处于 WaitSleepJoin 线程状态的线程。 |
| Join() | 阻塞调用线程，直到正在执行的线程终止。 |
| ResetAbort() | 重置为当前线程请求的终止操作。 |
| Resume() | 恢复已挂起的线程。 |
| SetData() | 设置当前运行线程的数据。此方法使用标记有 ThreadStaticAttribute 属性的字段。 |
| SetProcessorAffinity() | 设置托管线程的处理器亲和性。处理器亲和性决定线程在哪些处理器上运行。 |
| Sleep() | 阻塞当前线程指定的毫秒数。它是一个重载方法。 |
| SpinWait() | 导致线程等待 iterations 参数定义次数。 |
| Start() | 导致线程被调度执行。它是一个重载方法。 |
| VolatileRead() | 读取字段的值。此值对所有正在运行的进程可见。 |
| VolatileWrite() | 将值写入字段。此值一旦写入就会对所有正在运行的进程可见。 |

表 31.2 列出了 Thread 类的公共属性：

### Table 31.2: Public Properties of the Thread Class

| Name | Description |
|------|-------------|
| CurrentContext | 获取线程正在执行的当前上下文 |
| CurrentCulture | 获取或设置线程的文化 |
| CurrentPrincipal | 获取或设置当前线程的主体 |
| CurrentThread | 获取当前正在运行的线程 |
| CurrentUICulture | 获取或设置线程的用户交互文化 |
| ExecutionContext | 获取包含当前线程信息的 ExecutionContext 类的对象 |
| IsAlive | 获取指示当前线程执行状态的值 |
| IsBackground | 获取或设置指示线程是否为后台线程的值 |
| IsThreadPoolThread | 获取指示线程是否属于线程池的值 |
| ManagedThreadId | 获取当前线程的唯一标识符 |
| Name | 获取或设置线程的名称 |
| Priority | 获取或设置指示线程调度优先级的值 |
| ThreadState | 获取指示当前线程状态的值 |

