
## 使用 BackgroundWorker 控件

因为线程是在 Windows 编程中非常常见的编程任务，Microsoft 提供了一个方便的解决方案来实现线程：用于 Windows 应用程序的 BackgroundWorker 控件。BackgroundWorker 控件使您能够运行长时间的后台任务，例如网络访问、文件访问等，并持续接收任务进度的反馈。它在单独的线程上运行。

本节创建一个简单的 Windows 应用程序，展示 BackgroundWorker 组件如何帮助使您的应用程序更具响应性。

首先，启动 Visual Studio 2008 并创建一个新的 Windows 应用程序。用以下控件填充默认的 Windows 窗体（见图 10-12）。

| 控制 | 名称 | 文本 |
|---|---|---|
| 标签 |  | 数字 |
| 标签 | lblResult | label2 |
| 标签 |  | 进度 |
| 文本框 | txtNum |  |
| 按钮 | btnStart | 开始 |
| 按钮 | btnCancel | 取消 |
| 进度条 | ProgressBar1 |  |

![](img/a977a875c7c627b45d939729705a252e_338_0.png)

图 10-12

从工具箱拖放 BackgroundWorker 组件到窗体上。BackgroundWorker 是一个非可视控件，因此它出现在窗体下方的组件区域中（见图 10-13）。

第一部分：C# 基础

![](img/a977a875c7c627b45d939729705a252e_339_0.png)

图 10-13

右键单击 BackgroundWorker 组件并选择属性。将 WorkerReportsProgress 和 WorkerSupportsCancellation 属性设置为 True，以便组件可以报告线程的进度并且可以在线程进行到一半时被中止（见图 10-14）。

![](img/a977a875c7c627b45d939729705a252e_339_1.png)

图 10-14

以下是应用程序的工作方式。用户在 TextBox 控件（txtNum）中输入一个数字并单击开始按钮。然后应用程序将从 0 到该数字的所有数字求和。页面底部的进度条显示求和的进度。进度条更新的速度取决于输入的数字。对于较小的数字，进度条会非常快速地填满。为了真正看到求和在后台线程中如何工作，请尝试一个大数字并观察进度条自行更新。请注意，求和进行时窗口仍然有响应。要中止求和过程，请单击取消按钮。求和完成后，结果会打印在标签控件（lblResult）上。

```csharp
{
    int percentDone = (int)((i / number) * 100);
    //---update the progress bar if there is a change---
    if (percentDone > lastPercent)
    {
        worker.ReportProgress(percentDone);
        lastPercent = percentDone;
    }
}
    return sum;
}
```

它接收三个参数——要求和到的数字、BackgroundWorker 组件和 DoWorkEventArgs。在 for 循环中，您通过检查 CancellationPending 属性的值来检查用户是否单击了取消按钮（该事件在本章稍后定义）。如果用户已取消进程，请将 e.Cancel 设置为 True。每隔 10 次迭代，您就会计算到目前为止完成的进度。如果有进度（当当前进度百分比大于上次记录的进度时），您将通过调用 BackgroundWorker 组件的 ReportProgress() 方法来更新进度条。请不要不必要地调用 ReportProgress() 方法，因为频繁调用会冻结应用程序的 UI。

需要注意的是，在此方法中（由 DoWork 事件调用），您不能直接访问 Windows 控件，因为它们不是线程安全的。尝试这样做会触发运行时错误，这是 Visual Studio 2008 中的一个有用功能。

每当调用 ReportProgress() 方法时，就会调用 ProgressChanged 事件。在此情况下，您使用它来更新进度条。要为 ProgressChanged 事件生成事件处理程序，请切换到设计视图并查看 BackgroundWorker 组件的属性。在属性窗口中，选择事件图标并双击 ProgressChanged 事件（见图 10-15）。

![](img/a977a875c7c627b45d939729705a252e_341_0.png)

图 10-15

按如下方式为 ProgressChanged 事件编码事件处理程序：

```csharp
private void backgroundWorker1_ProgressChanged(
    object sender, ProgressChangedEventArgs e
)
{
    //---updates the progress bar and label control---
    progressBar1.Value = e.ProgressPercentage;
    lblResult.Text = e.ProgressPercentage.ToString() + "%";
}
```

现在双击 RunWorkerCompleted 事件以生成其事件处理程序：

```csharp
private void backgroundWorker1_RunWorkerCompleted(
    object sender, RunWorkerCompletedEventArgs e
)
{
    if (e.Error != null)
        MessageBox.Show(e.Error.Message);
    else if (e.Cancelled)
        MessageBox.Show("Cancelled");
    else
    {
        lblResult.Text = "Sum of 1 to " +
            txtNum.Text + " is " + e.Result;
    }
    btnStart.Enabled = true;
    btnCancel.Enabled = false;
}
```

当线程（在此情况下为 SumNumbers()）完成运行时，会触发 RunWorkerCompleted 事件。在这里您相应地打印结果。

最后，当用户单击取消按钮时，您通过调用 CancelAsync() 方法来取消进程：

```csharp
private void btnCancel_Click(object sender, EventArgs e)
{
    //---Cancel the asynchronous operation---
    backgroundWorker1.CancelAsync();
    btnCancel.Enabled = false;
}
```

### 测试应用程序

要测试应用程序，请按 F5，输入一个大数字（例如 9999999），然后单击开始按钮。进度条应开始更新。进程完成后，结果会打印在标签控件中（见图 10-16）。

![](img/a977a875c7c627b45d939729705a252e_343_0.png)

图 10-16

## 摘要

本章解释了线程的理由以及它如何提高应用程序的响应性。线程是一个复杂的话题，在应用程序中使用线程之前需要仔细规划。例如，您必须识别关键区域，以便确保访问关键区域的不同线程是同步的。最后，您看到 Windows Forms 控件不是线程安全的，并且在从另一个线程更新 UI 控件时需要使用委托。

## 文件和流

在开发周期的某个阶段，您需要将数据存储在某种持久介质上，以便在计算机重新启动后数据仍然可用。在大多数情况下，您要么将数据存储在数据库中，要么存储在文件中。文件基本上是存储在存储介质（如硬盘、U盘等）上的字符序列。当谈到文件时，您需要了解另一个相关的术语——流。流是数据从一个点传递到另一个点的通道。在 .NET 中，流分为各种类型：用于永久存储上文件的 file 流、用于跨网络传输数据的 network 流、用于内部存储中数据的 memory 流等。

使用流，您可以执行各种任务，包括压缩和解压缩数据、序列化和反序列化数据以及加密和解密数据。本章将讨论：

- 操作文件和目录
- 如何快速读写文件数据
- 流的概念
- 使用 BufferedStream 类提高从流中读取数据的应用程序性能
- 使用 FileStream 类读写文件
- 使用 MemoryStream 类将内部内存存储用作缓冲区
- 使用 NetworkStream 类进行网络编程
- .NET 中可用的各种加密类
- 对流进行压缩和解压缩
- 将对象序列化为二进制和 XML 数据并反序列化

### 使用文件和目录

.NET Framework 中的 System.IO 命名空间包含大量允许同步和异步读写流和文件数据的类。在以下各节中，您将探索用于处理文件和目录的各种类。
