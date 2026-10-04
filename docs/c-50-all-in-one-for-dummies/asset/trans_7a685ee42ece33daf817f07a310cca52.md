

# 使用 System.Net 命名空间 467

# 记录网络活动

这带我们进入了下一个主题，网络记录。活动问题非常难以调试和复现。微软构建了几个工具来管理跟踪活动。

更此外，虽然提供了 ASP.NET 追踪功能，但 System.Net 命名空间的追踪是完全通过配置文件管理的。为了使用这些功能，你不需要更改和重新编译代码。事实上，通过适当的管理，你可以通过管理所使用的配置文件来向用户显示调试信息。

每种应用程序都有不同的配置文件。对于你在这里使用的 Windows Forms 应用程序，该文件名为 `app.config`，存储在开发项目目录中。编译时，文件名将更改为应用程序的名称，并复制到 `bin` 目录以便运行。

如果你现在使用 `app.config` 文件，你会发现里面几乎什么都没有。这对于 .NET 来说是比较新的，因为它以前从不验证过任何配置。你将向配置中添加一些内容来开启追踪。

# 列表 4-3：默认的 app.config 文件

```xml
<xml version="1.0" encoding="utf-8" ?>
<configuration>
  <startup>
    <supportedRuntime version="v4.0" sku=".Framework,Version=v4.5" />
  </startup>
</configuration>
```

首先，你需要为 System.Net 命名空间添加一个新源。接下来，为你添加的源在 `Switches` 部分添加一个开关。最后，你在该部分添加了 `SharedListener` 并设置文件自动刷新追踪。

![](img/6df7bb88e9302e98442acc219cfbd7fc_492_0.png)

完成后的 `app.config` 文件（加粗新增部分）如列表 4-4 所示。它也出现在本书配套网站的示例代码中。

# 列表 4-4：完成的 app.config 文件

```xml
<xml version="1.0" encoding="utf-8" ?>
<configuration>
  <startup>
    <supportedRuntime version="v4.0" sku=".Framework,Version=v4.5" />
  </startup>
  <system.diagnostics>
    <sources>
      <source name="System.Net">
        <listeners>
```

(续)

# 列表 4-4 (续)

```xml
<add name="System.Net" />
</listeners>
</source>
</sources>
<switches>
<add name="System.Net" value="Verbose" />
</switches>
<sharedListeners>
<add name="System.Net"
type="System.Diagnostics.TextWriterTraceListener"
initializeData="my.log"/>
</sharedListeners>
<trace autoflush="true" />
</system.diagnostics>

</configuration>
```

再次运行应用程序并观察输出窗口。由于你对配置文件的更改，那里显示了高级日志信息。此外，还写入了一个日志文件。在开发环境中，它位于项目的 `bin/debug` 目录中。你可能需要点击解决方案管理器顶部的“显示所有文件”按钮才能看到它。

在文件夹中，你应该能看到名为 `my.log` 的文件，你在 `app.config` 文件中添加的 `Shared Listener` 将日志信息定向到了那里。我的文件副本如列表 4-5 所示——你的情况可能会有所不同。

# 列表 4-5：日志信息

```
System.Net Information: 0 : WebRequest::Create(ftp://ftp.csharpfordummies.net/sample.bmp)
System.Net Information: 0 : Exiting WebRequest::Create() -> FtpWebRequest#37460558
System.Net Information: 0 : FtpWebRequest#37460558::GetResponse()
System.Net Information: 0 : Exiting FtpWebRequest#37460558::GetResponse()
System.Net Information: 0 : Associating Message#5948790 with HeaderCollection#23085090
System.Net Information: 0 : HeaderCollection#23085090::Set(mime-version=1.0)
System.Net Information: 0 : Associating MailMessage#6964596 with Message#5948790
System.Net Information: 0 : SmtpClient::.ctor(host=24.123.157.3)
System.Net Information: 0 : Associating SmtpClient#17113003 with SmtpTransport#3054452
System.Net Information: 0 : Exiting SmtpClient::.ctor()
System.Net Information: 0 : SmtpClient#17113003::Send(MailMessage#6964596)
System.Net Information: 0 : SmtpClient#17113003::Send(DeliveryMethod=Network)
System.Net Information: 0 : Associating SmtpClient#17113003 with MailMessage#6964596
System.Net Information: 0 : Associating SmtpTransport#3054452 with SmtpConnection#4436549
System.Net Information: 0 : Associating SmtpConnection#4436549 with ServicePoint#7044526
System.Net Information: 0 : Associating SmtpConnection#4436549 with SmtpPooledStream#20390146
System.Net Information: 0 : HeaderCollection#3068939::Set(content-transfer-encoding=base64)
```

# 使用 System.Net 命名空间 469

```
System.Net.Information: 0 : HeaderCollection#3068939::Get(content-transfer-encoding=quoted-printable)
System.Net.Information: 0 : HeaderCollection#23085090::Remove(x-receiver)
System.Net.Information: 0 : HeaderCollection#23085090::Set(from@sempf.net)
System.Net.Information: 0 : HeaderCollection#23085090::Set(to:bill@sempf.net)
System.Net.Information: 0 : HeaderCollection#23085090::Set(date=Apr 2010 16:32:32 -0500)
System.Net.Information: 0 : HeaderCollection#23085090::Get(mime-version)
Success(1)
System.Net.Information: 0 : HeaderCollection#23085090::Get(from)
System.Net.Information: 0 : HeaderCollection#23085090::Get(to)
System.Net.Information: 0 : HeaderCollection#23085090::Get(date)
System.Net.Information: 0 : HeaderCollection#23085090::Get(subject)
System.Net.Information: 0 : HeaderCollection#3068939::Get(content-type)
encoding)
System.Net.Information: 0 : Exiting SmtpClient#17113003::Send()
```

读取此文件，你可以找到错误发生的地方。框架所有与图形和图像的方法都提供 `Graphics` 对象，使得编写变得简单得多。

# 使用 System.Net 命名空间 469

# 第 5 章：创建图像

## 本章

- 理解 System.Drawing 命名空间
- 了解绘图类如何适配框架
- 使用 System.Drawing 创建简单的应用程序

即使在最高层级，图形编程也由绘制多边形、填充颜色和用文本标记组成——这一切都在某种画布上完成。令人惊讶的是，这为你留下了四个构成你所写图形的核心对象：图形（graphics）、画笔（pens）、刷子和文本。

## 认识 .Drawing

通常来说，`Graphics` 类创建了一个作为你调色板的对象。它是画布。`Graphics` 对象的所有方法和属性都旨在让你绘制的区域更符合你的需求。

此外，框架中其他类的大多数与图形和图像的方法都提供 `Graphics` 对象作为输出。例如，你可以从 Windows Forms 应用程序调用 `System.Web.Forms.Control.CreateGraphics` 方法，并返回一个 `Graphics` 对象以便在表单控件中绘制。你还可以处理表单的 `Paint` 事件，并检查事件的 `Graphics` 属性。

`Graphics` 对象使用画笔和刷（在本章稍后的“Pens”和“Brushes”部分讨论）进行绘制和填充。`Graphics` 对象具有如下方法：

- DrawRectangle
- FillRectangle
- DrawCircle
- FillCircle
- DrawBezier
- DrawLine

# 画笔 (Pens)

你使用画笔绘制线条和曲线。复杂的图形由多边形组成，而多边形由线条组成，这些线条是由画笔生成的。画笔具有如下属性：

- Color
- DashStyle
- EndCap
- Width

