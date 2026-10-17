
你可以像下面这样编写一个条件代码块：

```
#ifdef SOMEMACRO
    NSLog(@"This code will only be included if SOMEMACRO is defined...");
#endif
```

除非定义了 `SOMEMACRO`，否则 `NSLog()` 语句不会包含在编译后的代码中。`#ifdef` 指令并不在乎 `SOMEMACRO` 代表什么，只在乎它是否已定义。回想一下，你可以像这样定义 `SOMEMACRO`：

```
#define SOMEMACRO 1
```

## 在构建环境中定义宏

定义一个宏，然后检查它是否已定义，这很简单。一个宏是否被定义，也可以基于当前构建设置来决定，就像 `BETABUILD` 标志那样。

要亲自尝试这个场景，先将以下代码添加到 TestApp 委托类的 `-applicationDidFinishLaunching:` 方法的末尾：

```
#ifdef BETABUILD
    [[NSAlert alertWithMessageText:@"Beta Version"
        defaultButton:@"Ok"
        alternateButton:nil
        otherButton:nil
        informativeTextWithFormat:@"Warning: you are using a beta version of this application. Bad stuff might happen."]
        runModal];
#endif
```

```
#pragma mark NSApplicationDelegate Methods
- (void)applicationDidFinishLaunching:(NSNotification *)aNotification {
    // Load Google to demonstrate WebKit.framework's WebView
    NSURL * googleURL = [NSURL URLWithString:@"http://google.com"];
    NSURLRequest * request = [NSURLRequest requestWithURL:googleURL];
    [[webView mainFrame] loadRequest:request];

    // Create a Foo and a Bar to demo Foo.framework
    MyFoo * foo = [[[MyFoo alloc] init] autorelease];
    MyBar * bar = [[[MyBar alloc] init] autorelease];
    NSLog(@"Foo says: %@", foo);
    NSLog(@"Bar says: %@", bar);

    // Create a TestFoo to demo TestAppSharedFramework.framework
    TestFoo * testFoo = [[[TestFoo alloc] init] autorelease];
    NSLog(@"TestFoo says: %@", testFoo);

#ifdef BETABUILD
    // Display beta warning if built using Beta configuration
    [[NSAlert alertWithMessageText:@"Beta Version"
                     defaultButton:@"Ok"
                   alternateButton:nil
                       otherButton:nil
         informativeTextWithFormat:@"Warning: you are using a beta version of this application. Bad stuff might happen."]
     runModal];
#endif
}
```

**图19.8** 完整的 `-applicationDidFinishLaunching:` 方法

图19.8展示了完整的 `-applicationDidFinishLaunching:` 方法。`NSAlert` 代码块被包裹在 `#ifdef` 和 `#endif` 预处理指令中，仅当定义了名为 `BETABUILD` 的宏时才会被包含。

接下来，你需要在某处定义 `BETABUILD` 宏，并且你需要让构建环境来负责定义它。这可以通过为 beta 构建添加一个单独的构建配置，在目标的构建设置中（具体来说是“预处理器宏”设置）定义该宏，然后创建一个使用该 beta 构建配置的单独方案来实现。

**图19.9** TestApp 目标的“信息”标签页

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_332_0.png)

**图19.10** 复制 Release 配置

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_332_1.png)

为此，你首先要创建一个“beta”配置。转到 TestApp 项目，并在目标列表中选择 TestApp 目标。如果尚未选中，请点击“信息”标签页（图19.9）。

beta 配置应基于 Release 配置，因为你打算在应用程序的发布副本中显示 beta 警告。在“配置”部分中，选择 Release 配置。使用列表正下方的添加 (+) 按钮，从菜单中选择“复制‘Release’配置”（图19.10）。将名称从“Release copy”更改为“Beta Release”，然后按回车键。

**图19.11** 管理方案

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_333_0.png)

**图19.12** 编辑 Beta Release 方案的归档配置

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_333_1.png)

要使用单独的配置，你需要一个单独的方案。点击“方案”弹出菜单，并从菜单中选择“管理方案”。在方案管理器表单（图19.11）中，选择 TestApp 方案，然后点击添加 (+) 按钮并从菜单中选择“复制”。在出现的“方案编辑器”表单中，将方案名称设置为 TestApp (Beta)，然后选择“归档”操作。从“构建配置”弹出菜单中选择 Beta Release（图19.12），然后点击“好”。现在有两个构建 TestApp 的方案，但 beta 方案（在构建用于归档时）将使用你创建的 Beta Release 配置。

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_334_0.png)

**图19.13** 添加预处理器宏

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_334_1.png)

**图19.14** 最终的 `BETABUILD` 宏设置

最后一步是在 TestApp 目标的构建设置中，为 Beta Release 配置定义 `BETABUILD`。转到 TestApp 项目，然后选择 TestApp 目标并点击“构建设置”标签页。在设置中搜索“预处理器宏”设置。展开该设置，以便你可以看到三个配置（Debug、Release 和 Beta Release），如图19.13所示。

在 Beta Release 行中，双击值列（即 TestApp 的值），并添加宏名 **BETABUILD**。图19.14显示了正确配置后的设置。

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_335_0.png)

**图19.15** beta 警告

现在你可以测试它了。确保选择的是原始 TestApp 方案。从主菜单中，选择“产品”>“构建为”>“构建为归档”，然后等待构建完成。在项目导航器中，展开 TestApp 项目的“产品”组。右键点击 TestApp.app 产品，并从菜单中选择“在 Finder 中显示”。你应该会在其 Release 文件夹中看到正常发布构建的 TestApp 应用程序。双击启动它，并注意没有出现 beta 警告。退出 TestApp。

现在选择 TestApp (Beta) 方案。从主菜单中，选择“产品”>“构建为”>“构建为归档”，然后等待构建完成。再次在项目导航器中，右键点击“产品”组中的 TestApp.app 产品，并从菜单中选择“在 Finder 中显示”。你应该会在其 Beta Release 文件夹中看到 beta 发布构建的应用。启动它，并注意警告——这是一个 beta 版本（图19.15）。

> **提示：** 你还可以使用 Beta Release 配置来避免剥离调试符号。对于此配置，你可以禁用“在复制期间剥离调试符号”设置，这样更容易调试 beta 测试人员发现的问题。

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_335_1.png)

## 限制

理解*编译时间*或*构建时间*与*运行时间*之间的区别非常重要。C 预处理器在编译之前处理源文件。对源代码的所有影响发生在代码被*构建*时，而不是被*运行*时。例如，你不能使用预处理器条件，在应用程序运行于 Mac OS X 10.6 时运行一段代码，而在运行于 Mac OS X 10.5 时运行另一段代码。

> **提示：** 现在是回顾你在第17章中读到的两件事的好时机：“生成预处理文件”命令和助理编辑器的“生成输出”行为。

## 总结

你已经了解了如何使用 Xcode 的脚本挂钩来扩展和自动化各种任务。你还探索了 C 预处理器的能力：通过文本替换提供宏，并有条件地在源码中包含文本。掌握了这两个工具的基础知识后，你就可以扩展 Xcode 并将其集成到更庞大的工作流程中，自动化任务并降低人为错误的可能性。在下一章中，你将学习如何使用 Xcode 的配套应用程序 Instruments 来分析你的代码，以及更多内容。

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_336_0.png)

Instruments 是 Apple 为 DTrace 提供的前端（当然还有一些其他功能），DTrace 是一个动态跟踪系统，用于记录运行中程序的调试和性能信息。如果你以前从未使用过它，Instruments 将彻底改变你分析和调试应用程序的方式。一旦你被它惯坏了，你就会奇怪自己当初是如何从泄漏、僵尸对象和性能瓶颈的黑暗时代中熬过来的。

![](img/d4b18a89aece4a6ccac4cb886bdef5f7_339_0.png)
