

# 其他特性

还有许多 Silverlight 功能尚未探讨。然而，由于本章仅是对 WPF 和 Silverlight 的介绍，这些功能仅会有几个段落的介绍，尽管其中某些功能完全可以写一整章（甚至一本书）。

## 离线浏览器 (OOB) 

Silverlight 应用主要以插件的形式存在于浏览器中。然而，Silverlight 支持在浏览器之外的桌面运行应用程序。安装离线浏览器（OOB）应用程序始终是一个由用户发起的过程——可以通过右键点击 Silverlight 应用并选择“将 <appname> 安装到此计算机”，或者通过点击开发者创建的调用 `Application.Install` 方法的 UI 。无论何种方式，系统都会提示用户是否真的要安装应用程序，以及安装程序是否应该在桌面或开始菜单上创建快捷方式。

默认情况下，OOB 运行在与浏览器相同的沙箱中，因此不需要用户账户控制（UAC）提示。OOB 应用同样适用于 OS X，因此这是一个在无需运行 Mac 的情况下创建 OS 桌面应用程序的绝佳方法！

某些功能仅在 OOB 模式可用。这些包括 WebBrowser 控制和 HtmlBrush 控制。WebBrowser 是一个功能完备的网络浏览器，可以作为 Silverlight 内部的一个矩形框架，用于显示任何网页或 HTML 内容（包括包含其他 Flash 插件的网站）。HTMLBrush 与 VideoBrush 类似。当它附加到 WebBrowser 控制时，它可以作为任何元素的画刷。然而，WebBrowser 控制保持交互性，并接受键盘和鼠标输入，而 VideoBrush 则处理交互性。

OOB 应用也可以以特权安装。图 8-36 显示了 Visual Studio 2010 中的 OOB 设置。特权允许启用跨域策略，并允许从文件和目录读取或向其发送信息；允许允许级别的 COM 互操作性，从而可以拒绝自动化。

![](img/5597c74e848b270d3051ae1066.png)
图 8-36：Visual Studio 中的 OOB 设置

## 打印

打印是 Silverlight 受请求最多的功能。Silverlight 中的打印基于回调模型：

```csharp
PrintDocument pd = new PrintDocument();
pd.DocumentName = "Silverlight";
pd.PrintPage += (obj, args) => {
    args.PageVisual = LayoutRoot;
    args.HasMorePages = false;
};
pd.Print();
```

在 `PrintPage` 处理程序中，可以定义一个 `UIElement`，它将被栅化并发送到打印机。`UIElement` 不一定非要在视觉树中；它可以在内存中动态构建。`MorePages` 属性告诉引擎是否还有更多页面——如果是，将再次调用 `PrintPage` 事件处理下一页。

## 位图效果

位图效果（或着色器）源于计算机图形，通常与图形处理器（GPU）绑定。在 Silverlight 中，用于创建着色的语言是高级着色语言（HLSL）。然而，在 Silverlight 应用中添加着色器会带来性能损失。尽管着色器程序是 JIT 编译并运行在可用核心上的，但它仍然会减慢应用程序。Silverlight 有两个内置着色器：模糊（Blur）和阴影（DropShadow）。两者都有允许精细调整的属性，并且具有使用 HLSL 创建自定义效果的能力，在不过使用的情况下，它们确实可以增加应用程序的视觉吸引力。

## 本地消息

如果多个 Silverlight 应用或插件在同一台计算机上，本地消息允许应用程序之间进行通信——即使它们没有运行在同一个网页或 OOB 中。本地消息通过消息通道工作，并具有相当简单的 API。

要发送消息，请创建一个带有消息通道名称的 `LocalSender` 对象并调用其 `SendAsync(string)`。要接收消息，必须以相同的方式创建一个 `LocalReceiver` 对象，并在消息到达时触发 `MessageReceived` 事件。接收器还可以使用 `MessageReceivedEventArgs.Response` 属性接收回复，发送者可以在 `SendAsyncCompleted` 事件中接收该回复。对于双向通信，应用程序可以设置两个通信通道——每个方向一个。

## GPU 加速

Silverlight 3 及更高版本支持有限的 GPU 加速。可以通过持有插件的 HTML 文件中的 `<object>` 标签为整个插件开启 GPU 加速，添加以下参数：

```html
<param name="enableGPUAcceleration" value="true" />
```

在 Mac OS X 上，GPU 加速仅全全屏有效。另一个要求是兼容 DirectX-9 的显卡或 Mac 兼容 OpenGL。

GPU 加速仅在某些情况下有所帮助。与 WPF（GPU 合成是默认设置）不同，Silverlight 并不总是非常明确何时以及如何使用 GPU。开发者必须通过将 `CacheMode` 属性设置为 `BitmapCache` 来管理 `UIElement`。

理解 Silverlight 中 GPU 加速工作原理的关键在于，它只是将指定 `UIElement` 的渲染位图传输到显存中，并完成剩余的合成。当渲染的 `UIElement`（及其子元素）的像素很少变化，因此缓存不需要失效时，GPU 加速就能提供帮助。

在 GPU 上进行合成可以将平移、缩放、矩形裁剪或旋转动画以及 Alpha 混合的工作卸给 GPU，释放 CPU 执行其他任务，提高整个应用程序的性能。Silverlight 还具有 GPU 加速视频的机制，使得即使使用今天的高分辨率显示器也能实现全屏 HD 视频。GPU 可以帮助加速透视变换，但在 Silverlight 4 中，像素着色器仍然由 CPU 执行。

> 要深入深入了解 Silverlight 的 GPU 加速，请阅读 Andrés Vallée 的博客：http://doctenees.net/blogs/vbandi/archive/2009/07/30/discovering-silverlight-3-deep-dive-into-gpu-acceleration.aspx。

## 隔离存储

隔离存储是用户计算机上的本地存储，可以作为本地缓存、存储用户偏好或其他数据。每个应用程序有 1 MB 的配额，当应用程序作为插件安装时，配额会增加到 25 MB。在用户同意的情况下可以增加配额。虽然隔离存储文件的物理存储位置是隐藏的，但实际内容并未加密，因此它不适合存储密码。隔离存储可以被视为一个虚拟文件系统。它还允许通过应用范围的 `ApplicationSettings` 或站点范围的 `SiteSettings` 实现键值对组合。

## 导航与搜索优化

随着 Silverlight（以及 RIA 技术）将网页与桌面融合，出现了一些可用性问题。选择桌面式体验还是 Web 式体验取决于 UI 设计师。但如果需要深度链接和后退支持，Silverlight 内置的导航框架可以帮助。Visual Studio 2010 包含名为 Silverlight Application 的模板。基于此模板创建项目将得到带有几个页面（首页和关于）的应用程序。点击导航链接就像点击浏览器——程序切换到“页面”，URL 发生变化（例如，关于页的 URL 末尾添加 #）。

这与传统浏览器导航的重要区别在于页面没有重新加载——Silverlight 保持运行，不会显示中间页面，就像 HTML 页面那样。导航中的后退和前进按钮，就像书签和深度链接。导航 API 的关键是 `System.Windows.Controls.Frame` 类。Frame 托管页面、处理导航并与浏览器集成。用于从查询字符串提取信息以及 URL 映射的设施。

那么搜索引擎优化（SEO）怎么办？如果搜索引擎无法读取信息，那么使用 Silverlight 构建一个完整的网站是不行的，因为访问者不会来到网站。SEO 技巧的两句话总结是：使用 ASP.NET 构建一个“镜像”，从相同数据源提取，并在托管页中 Silverlight `<object>` 标签的后备部分输出相关内容和导航。ASP.NET 应用程序还可以动态生成 `robots.txt` 站点 XML，以引导搜索引擎爬虫找到正确的内容。

> 要亲眼观察 Silverlight 的 SEO 效果，请访问你喜欢的搜索引擎并搜索“silverlight store mouse”。结果将带你进入一个展示了此处描述的 SEO 技术的 Silverlight 商店。

