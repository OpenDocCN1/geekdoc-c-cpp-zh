
## **图 11.34** 带有预览附件组件的文件对话框

```java
class ImagePreviewer extends JLabel
{
    public ImagePreviewer(JFileChooser chooser)
    {
        setPreferredSize(new Dimension(100, 100));
        setBorder(BorderFactory.createEtchedBorder());
    }
    public void loadImage(File f)
    {
        var icon = new ImageIcon(f.getPath());
        if(icon.getIconWidth() > getWidth())
            icon = new ImageIcon(icon.getImage().getScaledInstance(
                getWidth(), -1, Image.SCALE_DEFAULT));
        setIcon(icon);
        repaint();
    }
}
```

这里只有一个挑战。我们希望在用户选择不同文件时更新预览图像。文件选择器使用“JavaBeans”机制，在其某个属性发生变化时通知感兴趣的监听器。选中的文件是一个属性，你可以通过安装 `PropertyChangeListener` 来监视它。以下是你捕获通知所需的代码：

```java
chooser.addPropertyChangeListener(event ->
{
    if (event.getPropertyName() == JFileChooser.SELECTED_FILE_CHANGED_PROPERTY)
    {
        var newFile = (File) event.getNewValue();
        // update the accessory
        . . .
    }
});
```

### javax.swing.JFileChooser 1.2

- `JFileChooser()`  
  创建一个可用于多个窗口的文件选择器对话框。
- `void setCurrentDirectory(File dir)`  
  设置文件对话框的初始目录。
- `void setSelectedFile(File file)`, `void setSelectedFiles(File[] file)`  
  设置文件对话框的默认文件选择。
- `void setMultiSelectionEnabled(boolean b)`  
  设置或清除多选模式。
- `void setFileSelectionMode(int mode)`  
  允许用户仅选择文件（默认）、仅选择目录，或同时选择文件和目录。模式参数是 `JFileChooser.FILES_ONLY`、`JFileChooser.DIRECTORIES_ONLY` 和 `JFileChooser.FILES_AND_DIRECTORIES` 之一。
- `int showOpenDialog(Component parent)`, `int showSaveDialog(Component parent)`, `int showDialog(Component parent, String approveButtonText)`  
  显示一个对话框，其中确认按钮标记为“打开”、“保存”，或使用 `approveButtonText` 字符串作为标记。返回 `APPROVE_OPTION`、`CANCEL_OPTION`（如果用户选择了取消按钮或关闭了对话框），或 `ERROR_OPTION`（如果发生错误）。
- `File getSelectedFile()`, `File[] getSelectedFiles()`  
  获取用户选中的文件（如果用户未选择任何文件，则返回 null）。
- `void setFileFilter(FileFilter filter)`  
  设置文件对话框的文件掩码。所有使 `filter.accept` 返回 true 的文件都将显示。此外，将该过滤器添加到可选择的过滤器列表中。
- `void addChoosableFileFilter(FileFilter filter)`  
  将文件过滤器添加到可选择的过滤器列表中。
- `void setAcceptAllFileFilterUsed(boolean b)`  
  在过滤器组合框中包含或禁止“所有文件”过滤器。
- `void resetChoosableFileFilters()`  
  清除可选择的过滤器列表。除非显式禁止，否则只保留“所有文件”过滤器。
- `void setFileView(FileView view)`  
  设置文件视图，以提供有关文件选择器所显示文件的信息。
- `void setAccessory(JComponent component)`  
  设置附件组件。

### javax.swing.filechooser.FileFilter 1.2

- `boolean accept(File f)`  
  如果文件选择器应显示此文件，则返回 true。
- `String getDescription()`  
  返回此文件过滤器的描述——例如，“图像文件 (*.gif,*.jpeg)”。

### javax.swing.filechooser.FileNameExtensionFilter 6

## 第 12 章 并发

本章内容

- 12.1 什么是线程？
- 12.2 线程状态
- 12.3 线程属性
- 12.4 同步
- 12.5 线程安全的集合
- 12.6 任务与线程池
- 12.7 异步计算
- 12.8 进程

你可能熟悉*多任务*——操作系统能够使多个程序看起来在同一时间工作。例如，你可以在编辑或下载电子邮件的同时进行打印。如今，你的计算机很可能拥有多个 CPU，但并发执行的进程数量并不受 CPU 数量的限制。操作系统为每个进程分配 CPU 时间片，从而营造出并行活动的印象。

多线程程序将多任务的思想进一步扩展了一层：单个程序看起来会同时执行多个任务。每个任务都在一个*线程*中执行，线程是“控制线程”的简称。能够同时运行多个线程的程序被称为*多线程*程序。

那么，多个*进程*和多个*线程*之间有什么区别？本质区别在于，每个进程都拥有自己完整的一套变量，而线程共享相同的数据。这听起来有些风险，事实上也确实可能如此，你将在本章后面看到。然而，与进程间通信相比，共享变量使线程间通信更高效，也更易于编程。此外，在某些操作系统上，线程比进程更“轻量”——创建和销毁单个线程的开销比启动新进程更小。

多线程在实践中极其有用。例如，浏览器应能够同时下载多张图片。Web 服务器需要能够处理并发请求。图形用户界面（GUI）程序有一个单独的线程，用于从宿主操作环境中收集用户界面事件。本章将向你展示如何为 Java 应用程序添加多线程能力。

友情提醒：并发编程可能变得非常复杂。本章涵盖应用程序员可能需要的所有工具。不过，对于更复杂的系统级编程，我们建议你参考更高级的资料，例如 Brian Goetz 等人所著的 *Java 并发编程实战*（Addison-Wesley Professional，2006）。

### 12.1 什么是线程？

让我们先看一个使用两个线程的简单程序。这个程序在银行账户之间转移资金。我们使用一个 Bank 类来存储给定数量账户的余额。transfer 方法将一笔金额从一个账户转移到另一个账户。实现见[代码清单 12.2](#listing-12.2)。

在第一个线程中，我们将资金从账户 0 转移到账户 1。第二个线程将资金从账户 2 转移到账户 3。

以下是在单独线程中运行任务的简单步骤：

1. 将任务的代码放入实现 `Runnable` 接口的类的 `run` 方法中。该接口非常简单，只有一个方法：

   ```
   public interface Runnable
   {
      void run();
   }
   ```

   由于 Runnable 是函数式接口，你可以用 lambda 表达式创建实例：

   ```java
   Runnable r = () ->
   {
       task code
   };
   ```

2. 根据 Runnable 构造一个 Thread 对象：

   ```
   var t = new Thread(r);
   ```

3. 启动线程：

   ```
   t.start();
   ```

要为转账创建一个单独的线程，我们只需将转账代码放入 Runnable 的 run 方法中，然后启动一个线程：

```java
Runnable r = () ->
{
    try
    {
        for (int i = 0; i < STEPS; i++)
        {
            double amount = MAX_AMOUNT * Math.random();
            bank.transfer(0, 1, amount);
            Thread.sleep((int) (DELAY * Math.random()));
        }
    }
    catch (InterruptedException e)
    {
    }
};
var t = new Thread(r);
t.start();
```

对于给定的步数，该线程会转移一个随机金额，然后休眠一段随机延迟。

我们需要捕获 sleep 方法可能抛出的 `InterruptedException`。我们将在第 757 页的[12.3.1 节“中断线程”](#)中讨论这个异常。通常，中断用于请求线程终止。因此，当发生 `InterruptedException` 时，我们的 run 方法会退出。

我们的程序还启动第二个线程，将资金从账户 2 转移到账户 3。运行此程序时，你会得到类似下面的输出：

```
Thread[Thread-1,5,main]  606.77 from 2 to 3 Total Balance:  400000.00
Thread[Thread-0,5,main]   98.99 from 0 to 1 Total Balance:  400000.00
Thread[Thread-1,5,main]  476.78 from 2 to 3 Total Balance:  400000.00
Thread[Thread-0,5,main]  653.64 from 0 to 1 Total Balance:  400000.00
Thread[Thread-1,5,main]  807.14 from 2 to 3 Total Balance:  400000.00
Thread[Thread-0,5,main]  481.49 from 0 to 1 Total Balance:  400000.00
Thread[Thread-0,5,main]  203.73 from 0 to 1 Total Balance:  400000.00
Thread[Thread-1,5,main]  111.76 from 2 to 3 Total Balance:  400000.00
Thread[Thread-1,5,main]  794.88 from 2 to 3 Total Balance:  400000.00
. . .
```

如你所见，两个线程的输出交错在一起，表明它们并发运行。事实上，当两行输出交错时，有时输出会稍显混乱。

就是这样！现在你知道了如何并发运行任务。本章余下部分将介绍如何控制线程之间的交互。

