
图 17.1 显示了应用程序中的工具提示（tooltip）和状态提示（status tip）。

# 图 17.1. 显示工具提示和状态提示的应用程序

[查看全尺寸图像]

![](img/5a524abdf0b0d58fa99d30abb4463611_651_0.png)

在某些情况下，提供比工具提示或状态提示所能提供的更多关于组件的信息是有必要的。例如，我们可能希望提供一个复杂的对话框，其中包含每个字段的解释性文本，而无需强制用户调用独立的帮助窗口。“这是什么？”（What's This?）模式是解决此问题的理想方案。当窗口处于“这是什么？”模式时，光标会变为 ?，用户可以点击任何界面组件来获取其帮助文本。要进入“这是什么？”模式，用户可以点击对话框标题栏中的 ? 按钮（Windows 和 KDE 上），或按下 Shift+F1。

以下是一个在对话框上设置“这是什么？”文本的示例：

```
dialog->setWhatsThis(tr("<img src=\\images/icon.png\&nbsp;The meaning of the Source field depends on the Type field:
<<ul>
<li>Books</li> have a Publisher</li>
<li>Articles</li> have a Journal name with "volume and issue number"
<li>Theses</li> have an Institution name * and a Department name
</ul>

```

我们可以使用 HTML 标签来格式化“这是什么？”文本。在图 17.2 所示的示例中，我们包含了一张图片（在应用程序资源文件中列出）、一个项目列表以及一些粗体文本。Qt 支持的标签和属性在 http://doc.qt.com/4.3/richtext-html-subset 中指定。

# 图 17.2. 显示“这是什么？”帮助文本的对话框

![](img/5a524abdf0b0d58fa99d30abb4463611_652_0.png)

当我们在操作（action）上设置“这是什么？”文本时，当用户点击菜单项、工具栏按钮，或者在“这是什么？”模式下按下快捷键时，将显示该文本。当应用程序主窗口的界面组件提供“这是什么？”文本时，通常做法是在帮助菜单中提供一个“这是什么？”选项以及相应的工具栏按钮。这可以通过使用静态函数 `QWhatsThis::create()` 创建一个“这是什么？”操作，并将返回的操作添加到帮助菜单和工具栏中来实现。`QWhatsThis` 类还提供了静态函数，用于程序化地进入和离开“这是什么？”模式。

# 17. 提供在线帮助

![](img/5a524abdf0b0d58fa99d30abb4463611_653_0.png)

- 工具提示、状态提示和“这是什么？”帮助
- 使用 Web 浏览器提供在线帮助
- 使用 QtTextBrowser 作为简单的帮助引擎
- 使用 Qt Assistant 强大的在线帮助

大多数应用程序都会为用户提供在线帮助。有些帮助是简短的，例如工具提示、状态提示和“这是什么？”。当然，Qt 支持所有这些内容。其他帮助可以详尽得多，涉及许多页文本。对于这类帮助，你可以使用 `QTextBrowser` 作为简单的在线帮助浏览器，或者从你的应用程序中调用 `Qt Assistant` 或 HTML 浏览器。

# 工具提示、状态提示和“这是什么？”帮助

工具提示是一段短文本，当鼠标悬停在组件上一段时间后就会出现。工具提示以黄背景上的黑字形式呈现。它们的主要用途是为工具栏按钮提供文本描述。

我们可以在代码中使用 `QWidget::setToolTip()` 为任意组件添加工具提示。例如：

```
findButton->setToolTip(tr("Find next"));
```

要为可以添加到菜单或工具栏的 `QAction` 设置工具提示，我们可以简单地对该操作调用 `setToolTip()`。例如：

```
newAction = new QAction(tr("&New"), this);
newAction->setToolTip(tr("New document"));
```

如果我们没有显式设置工具提示，`QAction` 将自动使用操作文本。状态提示也是一段短描述文本，通常比工具提示长。当鼠标悬停在工具栏按钮或菜单选项上时，状态栏中会出现状态提示。调用 `setStatusTip()` 为操作或组件添加状态提示：

```
newAction->setStatusTip(tr("Create a new document"));
```

图 17.1 显示了应用程序中的工具提示和状态提示。

# 图 17.1. 显示工具提示和状态提示的应用程序

[查看全尺寸图像]

![](img/5a524abdf0b0d58fa99d30abb4463611_654_0.png)

在某些情况下，提供比工具提示或状态提示所能提供的更多关于组件的信息是有必要的。例如，我们可能希望提供一个复杂的对话框，其中包含每个字段的解释性文本，而无需强制用户调用独立的帮助窗口。“这是什么？”（What's This?）模式是解决此问题的理想方案。当窗口处于“这是什么？”模式时，光标会变为 ?，用户可以点击任何界面组件来获取其帮助文本。要进入“这是什么？”模式，用户可以点击对话框标题栏中的 ? 按钮（Windows 和 KDE 上），或按下 Shift+F1。

以下是在对话框上设置“这是什么？”的示例：

```
dialog->setWhatThis(tr("<img src=\/images/icon.png\&nbsp;The meaning of the Source depends on the Type field:\n<<ul>\n<li>Books</li> have a Publisher</li><li>Articles</li> have a Journal name with volume and issue number</li><li>Theses</li> have an Institution name * and a Department name name"));
```

我们可以使用 HTML 标签来格式化“这是什么？”文本。在图 17.2 所示的示例中，我们包含了一张图片（在应用程序资源文件中列出）、一个项目列表以及一些粗体文本。Qt 支持的标签和属性在 http://doc.trolltech.com/4.3/richtext-html-subset 中指定。

# 图 17.2. 显示“这是什么？”帮助文本的对话框

![](img/5a524abdf0b0d58fa99d30abb4463611_655_0.png)

当我们在操作（action）上设置“这是什么？”文本时，当用户点击菜单项、工具栏按钮，或者在“这是什么？”模式下按下快捷键时，将显示该文本。当应用程序主窗口的界面组件提供“这是什么？”文本时，通常做法是在帮助菜单中提供一个“这是什么？”选项以及相应的工具栏按钮。这可以通过使用静态函数 `QWhatsThis::create()` 创建一个“这是什么？”操作，并将返回的操作添加到帮助菜单和工具栏中来实现。`QWhatsThis` 类还提供了静态函数，用于程序化地进入和离开“这是什么？”模式。

# 使用 Web 浏览器提供在线帮助

大型应用程序可能需要更多的在线帮助，工具提示、状态提示和“这是什么？”帮助可以合理显示。解决此问题的简单方法是提供 HTML 格式的帮助文本并启动用户的浏览器。

包含帮助浏览器的应用程序通常在主窗口的帮助菜单和每个对话框中有帮助按钮。在本节中，我们将展示如何使用 `QDesktopServices` 类为这些按钮提供功能。

应用程序的主窗口通常有一个 `help()` 槽，当用户按下 F1 或点击帮助菜单选项时调用。

```
void MainWindow::url()
{
	QUrl url(directoryOf("doc").absoluteFilePath("index.html"));
	url.setScheme("file");
	QDesktopServices::openUrl(url);
}
```

在这个示例中，我们假设应用程序的 HTML 文件位于名为 `doc` 的子目录中。`QDir::absoluteFilePath` 函数返回带有给定名称的完整路径的字符串。我们首先创建一个指向帮助文件的 `QUrl` 对象。由于这是为主窗口提供的帮助，我们使用系统的 `index.html` 文件，所有其他文件都可以通过超链接访问。接下来，我们将 URL 的方案设置为 "file"，这样我们提供的文件将在本地文件系统中查找。最后，我们使用桌面服务的 `openUrl()` 静态便利函数启动用户的 Web 浏览器。

```
QDir MainWindow::directoryOf(const QString &subdir)
{
	QDir dir(QApplication::applicationDirPath());

#if defined(Q_OS_WIN)
	if (dir.dirName().toLower() == "debug"
		| dir.dirName().toLower() == "release")
		dir.cdUp();
```
