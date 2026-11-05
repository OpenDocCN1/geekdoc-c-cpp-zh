
打印机。借助这个 Graphics 对象，你可以使用 Graphics 类提供的方法，例如 DrawString。随附代码取自 MainForm 模块，用于将 RichTextBox 的内容打印到打印机。

你完全可以使用相同的代码，将 RichTextBox 控件的文本内容打印到任何其他设备上下文（Device Context），例如窗体本身。

如果需要支持打印机设置，请使用 PageSetupDialog。PageSetupDialog 允许用户更改给定文档的 PageSettings 和 PrinterSettings。要使用 PageSetupDialog 控件，请将 PageSetupDialog 控件单击并拖到应用程序上，然后将 PageSetupDialog.Document 属性设置为 PrintDocument 控件，即 AssemblyViewer 中的 printDocument1。

要显示 PageSetupDialog，请调用 ShowDialog 方法。所做的更改将应用到与 PageSetupDialog 关联的 PrintDocument。（有关展示这两个控件的示例，请参阅 AssemblyViewer 中的 MainForm.cs 模块。）

## 嵌入式资源文件管理

资源文件用于将内容（例如字符串数据）外部化。通过将字符串数据放入资源文件，你可以提供资源文件的不同语言版本，从而更轻松地实现内容国际化。

要向应用程序添加资源文件，请在解决方案资源管理器中右键单击项目。在项目的上下文菜单中，选择“添加/新建项”。在“添加新项”对话框中，选择“程序集资源文件”模板，如图 2-4 所示。

在解决方案资源管理器中选择该资源文件后，将显示资源管理器，如图 2-5 所示。你可以使用编辑器向资源文件添加资源内容。如图所示，字符串资源条目以包含名称、值、注释、类型和 mimetype 数据的表格形式呈现。这与资源文件类似。最大的区别在于，.NET 中的资源文件存储为 XML 文档，而不是纯文本。单击 XML 选项卡（如图 2-5 所示）即可查看该 XML。

Utility.cs 模块展示了如何使用 ResourceManager 从资源 (.resx) 文件读取数据。要从资源文件读取字符串数据，请创建 System.Resources 命名空间中定义的 ResourceManager 类的实例，并调用 GetString 方法。下面的代码清单展示了如何使用在 Utility.cs 模块中实现的 ResourceManager。

ResourceManager 必须知道你要加载的资源文件以及包含该资源文件的程序集。在此示例中，我们加载的是执行程序集中默认命名的资源文件。

## 多线程

最后，我们来讨论多线程。多线程是一个复杂的主题。多线程涉及多个方面，因此本节将只讨论它用于帮助实现 AssemblyViewer 的方式。

AssemblyViewer 在加载应用程序时使用单独的线程显示启动画面。这无疑是一种奢侈，但如果启动画面以线性方式执行，它还有什么意义呢？也就是说，当启动画面正在加载时，并没有发生真正的初始化，而且我从来不喜欢把初始化代码交给启动画面。（不过，你很可能会发现，许多启动画面实际上确实包含初始化代码。）

在我们的示例应用程序中，启动画面运行在单独的线程上。在 .NET 中，有四种不同的方式可以模拟看似异步的行为。Timer 控件和 Application.Idle 事件提供事件驱动的同步行为。控件支持异步的 BeginInvoke 和 EndInvoke。

ThreadPool 类提供可用线程池，而 Thread 类使你能够自行启动和管理线程。

AssemblyViewer 使用来自 ThreadPool 类的一个线程；因此，这里介绍的是线程处理的这一方面。

## 线程池线程处理

ThreadPool 是一个为你管理线程池的类。在 ThreadPool 中使用线程进行多线程处理，与创建 Thread 对象相同。不过，你的工作负担会有所减轻，而且从池中获取线程通常比创建 Thread 类的实例更快一些，因为池中可能已经有一个线程在等待你给它分配工作。

要使用 ThreadPool 中的线程，你只需以委托的形式给 ThreadPool 一些工作去做。在此示例中，委托充当表示线程要执行的工作的方法。线程处理的其他部分与你自行启动 Thread 对象没有区别。要记住的最重要的一点是，ThreadPool 线程需要与 Thread 实例同样谨慎对待，尤其是在涉及 Windows Forms 控件时。Windows Forms 控件不是线程安全的；因此，从线程与 Windows Forms 控件交互时，你应格外小心。

### 在线程池中排队工作项

委托至关重要：没有委托，事件处理程序就无法工作；而且除非理解委托，否则你无法在任何 .NET 语言中使用多线程。简而言之，委托包含一个或多个方法的地址。线程处理的工作方式是：给线程一个委托，其中包含表示该线程要完成的工作的方法。

在清单 2-3 中，静态方法 Splash 创建 Opacity 为 0 的 Splash 窗体。当 Form.Opacity 为 0 时，窗体是透明的；1 表示不透明窗体。当 Opacity 值介于 0 和 1 之间时，窗体为半透明。Splash 窗体最初是透明的，线程会逐渐增大 Opacity 值，直到窗体变为不透明，此时该线程便完成了工作。

### 方法调用

Show 方法在清单 2-3 的第 11 行至第 26 行中定义。

GDI+ 就像一位老态龙钟的祖父，什么都记不住。（我们稍后会再讨论字体和画笔。）这意味着你需要替 GDI+ 记住这些信息。换句话说，每次绘制文本时，你都必须告诉 GDI+ 使用什么字体和画笔来绘制文本。GDI+ 不仅会忘记你刚刚使用的字体和画笔，也不会跟踪你上次写入文本的位置，甚至还会忘记屏幕尺寸。信不信由你，如果画布尺寸在你上次请求 Graphics 对象（可以理解为 DC）与下次使用该 Graphics 对象之间发生变化，GDI+ 不会更新有关画布尺寸的信息。

无状态意味着，每当代码与设备上下文交互时，程序员都必须显式提供字体、画笔、钢笔、颜色和位置等信息。在 .NET 中也不应存储 DC。像下面这样的代码是不可取的。

前面的代码定义了一个继承自 Form 的类 CacheGraphics。构造函数创建一个新的 Graphics 对象，并将其存储在 graphics 字段中。

尽管 Graphics 对象是包含 DC 的类的名称，但清单中所示的两件事——直接创建 Graphics 对象并缓存该 Graphics 对象——都是错误的。由于 GDI+ 是无状态的，对 DC 的更改不会传播到你缓存的 Graphics 对象。例如，如果你调整窗体大小，那么你的 Graphics 对象所表示的区域就不会精确反映你的 DC。此外，应调用工厂方法 CreateGraphics 来获取 Graphics 对象的实例。

正如你将在本章中发现的，不应存储 Graphics 对象；每次需要时都应使用 CreateGraphics 请求它。每次需要时，都应使用工厂方法 CreateGraphics（或从事件处理程序获取 Graphics 对象参数）；并且每次执行绘制操作时，都应传入状态数据，例如字体和画笔。

## 检查 PlayControl

图中所示的 PlayControl 显示自定义图形 UI。从图中你可以
