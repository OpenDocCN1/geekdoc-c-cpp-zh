
```cpp
void Thread::run()
{ 
    while (!stopped)
        std::cerr << QPrintable(messageStr);
    stopped = false;
    std::cerr << std::endl;
}
```

run() 函数被调用以开始执行线程。只要 `stopped` 变量为 `false`，该函数就会持续向控制台打印指定的的消息。当控制离开 `run()` 函数时，线程终止。

```cpp
void Thread::stop()
{
    stopped = true;
}
```

stop() 函数将 `stopped` 变量设置为 `true`，通知 `run()` 停止向控制台打印文本。此函数可以在任何线程的任何时间被调用。为了本示例的目的，我们假设对 `bool` 的赋值是一个原子操作。考虑到 `bool` 只有两种状态，这是一个合理的假设。我们将在本节稍后的部分介绍如何使用 `QMutex` 来保证对变量的赋值是原子操作。

Thread 提供了一个 `terminate()` 函数，可以在线程仍在运行时终止其执行。不建议使用 `terminate()`，因为它可能在任何点停止线程，并且没有给线程留下清理工作的机会。像我们这里这样使用 `stopped` 变量和 `stop()` 函数总是更安全的。

现在我们将展示如何在一个小型 Qt 应用程序中使用 `Thread` 类，该程序除了主线程外还使用了两个线程 A 和 B。

```cpp
class ThreadDialog : public QDialog
{
    Q_OBJECT

public:
    ThreadDialog(QWidget parent = 0);

protected:
    void closeEvent(QCloseEvent event);

public slots:
    void startOrStopThreadA();
    void startOrStopThreadB();

private:
    Thread threadA;
    Thread threadB;
    QPushButton threadAButton;
    QPushButton threadBButton;
    QPushButton *quitButton;
};
```

`ThreadDialog` 类声明了两个 `Thread` 类型的变量以及一些提供用户界面的按钮。

```cpp
ThreadDialog::ThreadDialog(QWidget *parent)
 : QDialog(parent)
{
    threadA.setMessage("A");
    threadB.setMessage("B");

    threadAButton = new QPushButton(tr("Start A"));
    threadBButton = new QPushButton(tr("Start B"));
    quitButton = new QPushButton(tr("Quit"));
    quitButton->setDefault(true);

    connect(threadAButton, SIGNAL(clicked()),
           this, SLOT(startOrStopThreadA()));
    connect(threadBButton, SIGNAL(clicked()),
           this, SLOT(startOrStopThreadB()));
    ...
```

在构造函数中，我们调用 `setMessage()` 让第一个线程反复打印 'A'，第二个线程打印 'B'。

```cpp
void ThreadDialog::startOrStopThreadA()
{
    if (threadA.isRunning()) {
        threadA.stop();
        threadAButton->setText(tr("Start A"));
    } else {
        threadA.start();
        threadAButton->setText(tr("Stop A"));
```

当用户点击线程 A 的按钮时，`startOrStopThreadA()` 会在线程正在运行时运行时停止它，否则启动它。它还会更新按钮的文本。

```cpp
void ThreadDialog::startOrStopThreadB()
{
  if (threadB.isRunning()) {
    threadB.stop();
    threadBButton->setText(tr("Start B"));
  } else {
    threadB.start();
    threadBButton->setText(tr("Stop B"));
  }
}
```

`startOrStopThreadB()` 的代码在结构上相同。

```cpp
void ThreadDialog::closeEvent(QCloseEvent *event)
{
  threadA.stop();
  threadB.stop();
  threadA.wait();
  threadB.wait();
  event->accept();
}
```

如果用户点击“退出”（Quit）或关闭窗口，我们会停止任何正在运行的线程并等待它们完成（使用 `QThread::wait()`），然后再调用 `QCloseEvent::accept()`。这确保了应用程序以整洁的状态退出，尽管在这个示例中这并不重要。

如果你运行应用程序并点击“Start A”，控制台将充满 'A'。如果你点击“Start B”，它现在将充满交替的 'A' 和 'B' 序列。点击“Stop A”，现在它将只打印 'B'。
[/content]

---

### 第二部分：第 4 章 多线程（开头）

[content]
# 4. 多线程

![](img/5a524abdf0b0d58fa99d30abb4463611_541_0.png)

- 创建线程
- 线程同步
- 与主线程通信
- 在辅助线程中使用 Qt 类

传统的 GUI 应用程序只有一个执行线程，并且一次只执行一个操作。如果用户从用户界面调用了耗时操作，界面在操作进行期间通常会冻结。第 7 章介绍了解决此问题的一些解决方案。多线程是另一种解决方案。

在多线程应用程序中，GUI 运行在自己的线程中，额外的处理发生在一个或多个其他线程。这使得应用程序在密集处理时也能保持响应良好的 GUI。在单处理器上运行时，多线程应用程序可能比单线程对应程序运行得慢，因为存在多线程开销。但在日益常见的多处理器系统中，多线程应用程序可以在不同的处理器上执行，从而获得更好的性能。

在本章中，我们将首先展示如何子类 QThread 以及如何使用 `QMutex`、`QSemaphore` 和 `QWaitCondition` 来同步线程。然后我们将查看如何在辅助线程与主线程通信。最后，我们将回顾哪些类可以在辅助线程中使用。

> Qt 4.4 将提供更的线程 API，补充此处介绍的线程类，使编写多线程应用程序不易出错。

多线程是一个大课题，有很多专门介绍该主题的书——例如 Bill Lewis 和 Daniel J. Berg 的《Threads Primer: A Guide to Multithreaded Programming》（Prentice Hall, 1995）以及 Gregory Andrews 的《Multithreaded, Parallel, and Distributed Programming》（Addison-Wesley, 2000）。在这里假设你已经理解多线程编程的基础，因此重点在于解释如何开发多线程应用程序而非主题本身。

# 创建线程

在 Qt 应用程序中提供多个线程是简单的：只需子类 QThread 并实现 `run()` 函数。为了展示它是如何工作的，我们将首先回顾一个非常简单的反复在控制台打印字符串的 QThread 代码。应用程序的用户界面如图 14.1 所示。

```cpp
class Thread : public QThread
{
    Q_OBJECT

public:
    Thread();

    void setMessage(const QString &message);
    void stop();

protected:
    void run();

private:
    QString messageStr;
    volatile bool stopped;
};
```

# 图 14.1 Threads应用程序

![](img/5a524abdf0b0d58fa99d30abb4463611_542_0.png)

Thread 类派自 QThread 并实现了 `run()` 函数。它提供了两个额外的函数：`setMessage()` 和 `stop()`。`stopped` 变量被声明为 `volatile`，因为它从不同的线程访问，我们想要确保每次需要时都能读取最新值。如果我们忽略了 `volatile` 关键字，编译器可能会对变量访问进行优化，可能导致错误的结果。

```cpp
Thread::Thread()
{
    stopped = false;
}
```

我们在构造函数中将 `stopped` 设置为 `false`。
