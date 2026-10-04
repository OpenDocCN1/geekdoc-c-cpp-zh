

-   传递给 WaitAny 和 WaitAll 方法的数组不能超过 64 个元素，否则这些方法将抛出 `System.NotSupportedException` 异常。

-   你调用 WaitHandle 的 `Dispose` 方法来关闭底层内核对象句柄。在内部，这些方法调用 Win32 `CloseHandle` 函数。只有当你确切没有线程正在使用该内核对象时，你才可以在代码中显式调用 `Dispose`。如果你编写代码并设置它，会给你带来很大负担。因此，我强烈建议不要调用 `Dispose`；相反，让垃圾回收器 (GC) 来清理。GC 知道何时不再有线程使用该对象，并会将其移除。在某种意义上，GC 正在自动为你执行线程同步！

> 在某些情况下，当 COM 单线程单元线程阻塞时，该线程可以被唤醒并在内部泵消息。例如，被阻塞的线程将处理来自另一个线程的 Windows 消息。这样做是为了支持 COM 互操作性。对于大多数应用程序来说，这不是问题——事实上，这是一件好事。然而，如果你的代码在处理消息期间获取了另一个同步锁，则可能会发生死锁。正如你将在第 30 章中看到的，所有的混合锁在内部都会调用这些方法，因此在使用混合锁时也存在相同的优势或问题。

WaitOne 和 WaitAll 的版本不接受 `void` 返回类型的超时参数，而不是 `Boolean`。这是因为这些方法只返回 `true` 是因为隐含的超时是无限的（`System.Threading.Timeout.Infinite`）。当你调用这些任何一个方法时，不需要检查它们的返回值。

如所述，`AutoResetEvent`、`ManualResetEvent`、`Semaphore` 和 `Mutex` 类都派自 `WaitHandle`，因此它们继承了 `WaitHandle` 的方法和行为。然而，这些类引入了自己的额外方法，我现在将介绍它们。

首先，所有这些类的构造函数都会调用 Win32 `CreateEvent`（向 `bManualReset` 参数传递 `FALSE`）或 `CreateEvent`（向 `bManualReset` 参数传递 `TRUE`）、`CreateSemaphore` 或 `CreateMutex`。所有这些方法返回的句柄值都保存在 `WaitHandle` 基类定义的 `SafeWaitHandle` 字段中。

其次，`EventWaitHandle`、`Semaphore` 和 `Mutex` 类都提供了静态的 `OpenExisting` 方法，它们在内部调用 Win32 `OpenEvent`、`OpenSemaphore` 或 `OpenMutex`，并传递一个标识现有内核对象的 `String`。所有这些函数返回的句柄值都保存在 `OpenExisting` 方法返回的新构造对象中。如果不存在指定名称内核对象，将抛出 `WaitHandleOpenException`。

![](img/0ce3b788d061e3d3095fa554b1a34adf_805_0.png)

```csharp
public static class Program {
    public static void Main() {
        Boolean createdNew;
```

```csharp
// 使用指定的名称创建一个内核对象
using (new Semaphore(0, 1, "UniqueStringIdentifyingMyApp", out createdNew)) {
    if (createdNew) {
        // 创建了内核对象，因此此应用程序的其他实例
        // 正在运行。在此处运行应用程序的其他部分...
    }
    // 此线程打开了具有相同字符串名称的现有内核对象；
    // 现在此应用程序的另一个实例正在运行。
    // 在实例中无事可做，让我们直接从 Main 返回以终止
    // 此应用程序的第二个实例。
}
}
```

在此段代码中，我使用了 `Semaphore`，但如果我使用 `EventWaitHandle` 或 `Mutex`，效果也是一样的——我并没有实际上在创建任何类型的内核对象时使用内核提供的任何线程同步行为。然而，我正在利用某些线程同步行为来让我解释上述代码的工作原理。假设同时启动了此进程的两个实例。每个进程将有自己的线程，每个线程都会尝试创建一个相同名称（UniqueIdentifyingMyApp）的 Semaphore。Windows 确保只有一个线程创建了名称的内核对象；该线程的 `createdNew` 变量将设置为 `true`。

对于第二个线程，Windows 将看到已存在名称的内核对象；该线程不会创建另一个同名的内核对象，尽管此线程继续运行，它可以访问第一个进程的内核对象。这是不同进程通过单个内核对象进行通信的方式。然而，在示例中，第二个进程线程的 `createdNew` 变量被设置为 `false`。该线程现在知道另一个进程实例正在运行，第二个实例立即退出。

内核模式构造的一种常见用法是创建一个在任何时间只允许一个实例运行的应用程序。实例应用程序的示例有 Microsoft Outlook、Windows Live Messenger、Windows Media Player 和 Windows Media Center。以下是实现单实例应用程序的方法。

## 事件构造

事件是由内核维护的布尔变量。等待事件的线程在事件为 `false` 时阻塞，在事件为 `true` 时解除阻塞。有两种事件。当自动重置事件为 `true` 时，它会唤醒一个阻塞线程，因为内核在解除第一个阻塞后会自动将事件重置为 `false`。当手动重置事件为 `true` 时，它会唤醒所有阻塞线程，并保持为 `true`。

你可以使用事件来向其他线程发出事件已发生。例如，一个线程可能会等待资源可用，而另一个线程在资源就绪时发出事件。这是多线程编程中的常用模式。

使用事件有两种方法：

- 自动重置事件：当事件发出信号时，它会自动重置为 `false`。只有一个等待线程会被唤醒。
- 手动重置事件：当事件发出信号时，它保持为 `true`，直到被手动重置为 `false`。所有等待线程都会被唤醒。

你可以使用事件来协调线程之间的执行。例如，一个线程可以等待另一个线程完成任务后再继续执行。这确保了线程按正确的顺序执行。

