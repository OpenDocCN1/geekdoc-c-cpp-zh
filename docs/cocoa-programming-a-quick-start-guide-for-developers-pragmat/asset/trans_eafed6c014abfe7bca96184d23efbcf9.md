
![](img/9355405953264484a02198b0e3d25b7e_33_0.png)

将另一个按钮的标题设置为 Forward，并将其键盘等效项设置为 ⌘ →。接下来，选择 Window，并将其标题设置为 SimpleBrowser。

最后，让我们为用户提供一个默认值，并提示如何使用我们的浏览器。将文本字段的标题设置为 http://pragprog.com，可以双击它，也可以选中它并在 Attributes inspector 中设置 title 字段的值。还要使用文本字段的 Attributes inspector 中的下拉列表，将 Action 的值设置为 Sent on Enter Only。这会配置文本字段，使其在用户按下 Enter 时发送其值。

当用户按下 Enter 时，文本字段的值会发送到哪里？我们还没有设置这一点。

现在，你已经完成了 SimpleBrowser 界面所有可视元素的创建。使用 Cocoa Simulator 再查看一下浏览器，并调整窗口或任意组件的大小。你的浏览器仍然不做任何事情——但我们将在下一节修复这一点。

## 读取 Nib

到目前为止你所做的所有工作都以 XML 形式存储在 MainMenu.xib 文件中。你没有理由直接读取或更改你生成的 XML。这是一种旨在由 Interface Builder 创建和解释的格式。出于好玩，你也许想用最喜欢的文本编辑器打开该文件并四处看看。你可以找到文本字段、两个按钮和 web 视图。它并不好看，你也不会想以这种方式与你的 GUI 设置交互，但令人安心的是，如果你愿意，这种格式是你可以探究的。悄悄关闭文件，不要保存任何更改。在本章结束前，我们会再来看一次 MainMenu.xib。

## 2.5 连接组件

你已经使用 Interface Builder 选择并配置了将在此应用程序中使用的可视元素。你把它们放入窗口，更改了外观，设置了默认值，调整了大小，并设置了它们在窗口大小变化时如何调整。现在你准备好将它们连接起来。

例如，你想将 Back 按钮连接到 web 视图。当你点击该按钮时，你希望 web 视图显示上一个 URL 的内容。普通按钮对 web 视图一无所知。然而，web 视图应该知道如何在其历史中后退，并且应该由某个外部来源触发。所以，你只需要将 web 视图的后退能力连接到这个按钮的点击。

类似地，文本字段不应该知道 URL 和 web 视图。如果文本字段必须知道它可以为其提供文本的所有东西，API 就会庞大而脆弱。但 web 视图应该知道如何从某个其他元素的字符串中获取 URL。所以，你只需要将 web 视图的“从字符串获取 URL”能力连接到提供该字符串的组件。

这并不总是奏效，但思考谁知道什么会有帮助。在这种情况下，大部分知识都在 web 视图中。许多……

回看连接检查器。你在 goBack: 旁边点击的圆圈现在已被填充。此外，goBack: 现在在视觉上连接到 Push Button (Back)。看到 Push Button (Back) 左侧的 x 了吗？点击它。你刚刚断开了连接。

你可以像之前一样重新连接 goBack: 和 Back 按钮，或者你可以右键单击或 ^-单击（即 Control-单击）web 视图，以调出浮窗显示版本。和之前一样，点击 goBack: 旁边的圆圈，并拖到 Back 按钮。松开鼠标，你就重新连接了 goBack: 和 Back 按钮。

![](img/9355405953264484a02198b0e3d25b7e_36_0.png)

我们还有两个连接要做。再次选择 WebView，并使用连接检查器或浮窗显示。

- 1. 将 goForward: 接收的动作连接到 Forward 按钮。这将使用户能够点击 Forward 按钮，在浏览器历史中向前移动。
- 2. 将 takeStringUrlFrom: 接收的动作连接到文本字段。这使用户可以在文本字段中输入 URL，并点击 Enter 加载网页。

完成后，连接检查器应该像这样：

![](img/9355405953264484a02198b0e3d25b7e_37_0.png)

仿佛你的选项还不够多，你也可以按相反方向建立这些连接。例如，选择 Back 按钮并查看它的连接检查器。在 Sent Actions 区域，你应该看到单个条目 selector:⁶ 选中它，将连接拖回 WebView，然后松开。应该会出现一个包含 web 视图所有动作的灰色框。

选择 goBack:。你现在已经成功地按相反方向建立了连接。你很快就会围绕自己最喜欢的方法和方向形成节奏。坚持使用你最 comfortable 的方式。

## 在模拟器中测试浏览器

保存你的工作，并在 Cocoa Simulator 中打开它。点击文本字段，然后按 ↵。Pragmatic Programmer 主页应该会出现。输入另一个 URL，然后按 ↵。尽管这基本可行，但我有几点简短说明：

- 不要忘记包含 http://，因为这只是一个非常基础的 web 浏览器。

⁶. 选择器是被调用方法的名称，冒号表示该方法接受单个参数。你将在第3章*方法与参数*第48页学到更多关于选择器的内容。

- 不要选择过于复杂的页面或需要身份验证的页面。这是一个非常基础的 web 浏览器。
- 一旦第二个页面出现，你可以点击 Back 和 Forward 按钮，在两个页面之间来回导航。

这很棒！至少在这里的模拟器中，你有一个可工作的 web 浏览器。

我们的浏览器没有一些你即使在最简陋的浏览器中也可能期望看到的功能。例如，页面加载时你得不到任何反馈。当你第一次运行 SimpleBrowser 时，你可能会以为什么也没发生，直到停顿之后页面出现。此外，当你点击 Back 和 Forward 时，URL 不会改变。如果你加载 http://pragprog.com，然后加载 http://apple.com，然后点击 Back 按钮，你会看到 Pragmatic Programmer 的主页，尽管 URL 仍会显示 http://apple.com。我们将在接下来几章中处理这些问题。

## 2.6 修复构建

感觉你已经完成了。你可以在 Cocoa Simulator 中玩你的应用程序。你在 Interface Builder 中的所有工作都正确且完整，而且这个 SimpleBrowser 项目没有代码要写。然而，你还没有一个可以交给别人在其机器上运行的应用程序。你需要回到 Xcode 并创建一个发布版本。

在 Xcode 中，点击 Build & Run。构建成功，看起来 SimpleBrowser 开始加载。图标在 Dock 中弹跳了一会儿，但什么也没发生。取决于你的设置，你可能会发现自己身处调试器中，看到堆栈跟踪和一条警告。

啊——。点击 Stop 按钮，或选择 Run > Stop。⁸ 我们需要添加 WebKit.framework。

我之前提到过我们必须把它链接进来。我们本可以在将 WebView 从 Library 拖到窗口时完成。现在你看到了可能出现的问题，很可能你会更容易记住它。请参阅本页的*Joe 问……*，了解你如何自行诊断该问题的解释。

⁷ 这个示例的重点不是构建一个健壮的 web 浏览器，而是使用 web 浏览器作为示例应用程序，让我们向你介绍 Cocoa 编程。例如，目前你还无法加载包含 Flash 的页面。

⁸ 如果你安装的 Xcode 看起来和我的不一样，你总是可以通过选择 View > Customize Toolbar... 来自定义工具栏。此外，你可以从 Xcode > Preferences 进行许多调整。

![](img/9355405953264484a02198b0e3d25b7e_39_0.png)

## Joe 问……

### 我怎么会知道要添加 WebKit 框架？

首先使用 Run > Debugger 或 ⇧⌘Y 打开调试器。取决于你如何配置 Xcode，你可能还会看到一个看起来像杀虫喷雾的图标，可以点击。在 Xcode 窗口左上角，你会看到警告：应用程序正在

```
TERMINATING DUE TO UNCAUGHT_EXCEPTION
```

堆栈跟踪不太有帮助，但如果你查看 Console，你很快就会看到问题。使用 ⇧⌘R 或 Run > Console 打开 Console。你会看到一个 gdb 提示符。向上滚动越过堆栈列表。就在这上面，你会看到一系列行，每一行都以时间戳、单词 SimpleBrowser 以及包含进程号的标识符周围的括号开头。一旦你解析掉所有这些信息，你应该会得到类似这样的内容：

```
An uncaught exception was raised
-[NSKeyedUnarchiver decodeObjectForKey:]
        cannot decode object of class (WebView)
Terminating app due to uncaught exception
        'NSInvalidArgumentException'
```

啊哈！问题在于解归档一个 WebView 对象。你的 nib 本质上是对象及其连接的归档。你需要加载 WebKit 框架，以便 WebView 能够成功重建。

当我们从库中拖出 WebView 实例时，我们看到它是 WebKit 框架的一部分，而不是 Cocoa 框架的一部分。我本以为 Xcode 会自动将 WebKit 框架添加到相应项目中进行链接，但它不会。你需要自己做这件事。

从项目视图中，选择 SimpleBrowser 组中的 Frameworks 文件夹。你应该看到已经有四个框架添加到了项目中，但如果你查看最右列，你会看到只有 Cocoa.framework 对我们的目标处于活动状态。

