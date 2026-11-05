
## 其他流类

在 C# 中，流还用于在网络上读写数据，以及读写内存中的区域。NetworkStream 用于网络连接。MemoryStream 直接处理内存中的数据。

NetworkStream 类提供通过流套接字发送和接收数据的方法。本书不涉及对 NetworkStream 类的介绍。不过，该类用于同步和异步数据传输。该类具有与其他流类类似的方法，包括 Read 和 Write 方法。.NET 中还包含 MemoryStream 类。MemoryStream 类用于创建以内存（而不是磁盘或网络连接）作为后备存储的流。MemoryStream 类封装以无符号字节数组形式存储的数据，并可在内存中直接访问。内存流可以减少应用程序对临时缓冲区和文件的需求。建议查阅 MSDN 文档，详细了解如何使用 NetworkStream 和 MemoryStream 类。

流对象可以用 BufferedStream 类的对象包装。将无缓冲流对象传递给缓冲流类的构造函数，从而启用字符缓冲。这可以提高文件处理操作的速度和性能。通过将 BufferedStream 对象包装在文件流对象周围，可以将字符块（不止一条记录）带入内存以供检索。数据存储在内存后，该类的成员从缓冲区读取数据，从而减少对辅助存储设备的实际访问次数，而访问辅助存储设备会拖慢应用程序。

缓冲也可用于创建文件。此时，写入操作不是将每条记录物理写入辅助存储设备，而是将数据存储在内存缓冲区中。缓冲区包含指定数量的字符后，缓冲区会被写入实际文件。使用缓冲区所需的一切就是实例化 BufferedStream 类的对象，并将某个流类的对象作为参数传入。然后使用 BufferedStream 对象访问数据。建议查阅 MSDN 文档以获取示例。

使用 FileStream 类进行随机访问时，值可以按任意顺序处理，而不必从上到下按顺序处理。随机访问通过 Seek() 方法实现。Seek() 允许使用偏移参考参数将读或写位置移动到文件内的任何位置。偏移量可以相对于文件开头、当前位置或文件末尾来指定。

## FileDialog 类

使用过 Windows 应用程序后，您已经习惯浏览到特定位置来存储或检索文件。在应用程序中包含这类功能非常容易。不必像本章中大多数示例那样硬编码实际文件名和路径，您还可以添加对话框，允许用户在运行时输入名称。如果要访问文件进行输入，可以显示“打开”文件对话框，允许用户浏览到文件所在目录并选择文件。或者，如果要创建新文件，可以显示“另存为”对话框，允许用户在运行时键入或选择文件名。

这通过 OpenFileDialog 和 SaveFileDialog 类实现。这两个类都派生自 FileDialog 类。FileDialog 是一个抽象类，不能实例化，但为 OpenFileDialog 和 SaveFileDialog 类提供了许多功能。这些类属于 System.Windows.Forms 命名空间。FileDialog 类有一个名为 FileName 的属性，OpenFileDialog 和 SaveFileDialog 类都使用该属性来设置或获取对话框中的文件名。

要向应用程序添加对话框行为，请从工具箱将 OpenFileDialog 和/或 SaveFileDialog 控件拖到窗体上。释放鼠标时，控件会放置在窗体下方的组件托盘中，如图 13-13 所示。

![](img/e33ae760e23d89eac66541252ad65de8_842_0.png)

**图 13-13** 放置 OpenFileDialog 和 SaveFileDialog 控件

将 OpenFileDialog 控件放到窗体上时，FileName 属性的初始默认值为对象 `openFileDialog1` 的名称。您可以为 FileName 属性键入新值；或者，如果您希望名称没有值，可以清除 FileName 属性的值。这会使文件名的文本框变为空白。

将对话框控件放到窗体上后，使用 ShowDialog() 方法打开对话框。ShowDialog() 方法也是抽象 FileDialog 类的成员。这两个派生类都可以使用它。如果不更改对象名称而使用默认名称，则应在程序中希望显示对话框的位置包含以下语句：

```
openFileDialog1.ShowDialog();
```

或

```
saveFileDialog1.ShowDialog();
```

当使用 `openFileDialog1` 对象执行 ShowDialog() 方法时，将显示图 13-14 所示的“打开”文件对话框。

![](img/e33ae760e23d89eac66541252ad65de8_843_0.png)

**图 13-14** 执行 ShowDialog() 方法

当使用 SaveFileDialog 对象执行 ShowDialog() 方法时，将显示与图 13-14 所示类似的对话框。

要从对话框的文本框中检索文件名，请使用 FileName 属性。检索到的值可用作流对象实例化的参数。下面的 inFile 对象说明了这一点：

```
StreamReader inFile = new StreamReader(openFileDialog1.FileName);
```

此过程也适用于 `StreamWriter` 对象。以下两行会打开“另存为”对话框。用户可以浏览到文件应存储的位置，并键入新文件名或选择要替换的文件。

```
saveFileDialog1.ShowDialog();
StreamWriter outFile = new StreamWriter(saveFileDialog1.FileName);
```

执行这些行时，对话框的标题栏不会像图 13-14 那样显示“打开”字样，而是显示“另存为”字样。

## 编程示例：ICW WaterDepth 文件应用

在第 12 章中，设计了一个图形用户界面解决方案，使用户能够输入 ICW 沿岸的区域，这些区域因浅滩或浅水而建议划船者提高警惕。该图形用户界面使用户能够输入位置名称、州、英里标记编号，以及四个不同日期在低潮和高潮时的水深。输入有效数据后，会显示一条消息，展示该位置及其关联数据。然而，在处理并显示单个位置的数据后，输入第二个及后续位置时，这些数据就会丢失。没有可用于将数据从一次运行保存到另一次运行的机制。对于此编程示例，将修改第 12 章中给出的解决方案，以允许捕获并存储结果以供将来使用。

### 分析问题

应查看图 12-21 中的问题说明，并确保理解问题定义。必须向程序中输入多个值。该应用程序应允许输入多个位置，而不是只允许输入一组位置及相关水深。作为第 12 章所示编程示例解决方案的一部分，开发了一个 Windows 应用程序。运行 Windows 应用程序时，它处于进程循环中，可以处理多组值。需要进行少量修改，使窗体准备好接收第二组及后续输入值。

### 数据

为第 12 章中 `WaterDepth` 应用程序的解决方案设计了三个类。应查看表 12-4。它列出了 `ShoalArea` 类所需的数据字段成员。此类不需要新的数据成员。`TestOfStateException` 类不需要更改。`FrmWaterDepth` 类创建了用户界面，并显示一条消息，展示问题区域及其水深。在此类中，将创建 `StreamWriter` 类的对象。

