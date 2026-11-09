

```objc
- (void)connectionDidFinishLoading:(NSURLConnection *)connection
{
    // Process the data here
}
```

代码的主要特性包括：

- 该连接需要两个对象：一个 URL 请求和一个 URL 连接。
- NSURLRequest 对象定义连接的属性，包括 URL 和超时时间间隔。如果请求在超时时间间隔结束前未完成，请求就会失败。
- 请求对象还定义缓存策略。这里，缓存被设置为每次尝试都重新加载，因为缓存 API 返回结果可能有风险，尤其是当远程数据是临时的时候。
- 请求被传递给 NSURLConnection 对象，由它发起连接。它为连接指定一个委托对象，该对象监视连接状态并在数据到达时接收数据。
- 四个委托方法管理该连接。
- `connection:didReceiveResponse:` 由一个活跃的新连接触发，并重置数据接收器对象。
- `connection:didReceiveData:` 在数据到达时将其追加到数据对象。
- `connection:didFailWithError:` 报告错误代码。
- `connectionDidFinishLoading:` 在数据成功接收后触发。

尽管这是字节级的 Web 访问——你可以以通用方式使用 NSData 接收任意格式的数据——但你可以用这段代码管理几乎任何异步 Web 请求。

## 使用 Cocoa 的 XML 类

Cocoa 的 XML 实现很复杂，部分原因是 XML 本身可能很复杂。核心类是 NSXMLDocument，可以使用 initWithData: 方法加载。虽然可以将数据提取到 NSXMLElement 和 NSXMLNode 等支持数据类型中，但对于简单任务（例如获取两个标签之间的文本）来说，这并非必要。可以使用名为 XPath 的查询框架直接扫描 XML 文档，该框架内置于 NSXMLDocument 中。

XPath 是一种标准 Web 技术。所有标准 Web 浏览器都内置了 JavaScript 版本。XPath 搜索假定 XML 文件中的数据以类似路径的结构格式化。查询将路径传递给文档，搜索返回该路径处的数据。

![](img/2b293e29fc15b0797f113b85dd429b6e_282_0.png)

### 注意

NSXMLDocument 和 nodeForXPath: 在 iPhone 上都不可用。请改用 NSXMLParser——一个动态解析器类，它接收 XML 字符串并在扫描时触发各种委托方法。NSXMLParser 比 NSXMLDocument 更轻量，但不太方便。要提取特定元素，必须向委托方法添加显式 switch 或条件测试。

以下是从 url 标签中提取文本字符串的示例代码：

```objc
theDocument = [[NSXMLDocument alloc] initWithData:theData
    options:NSXMLDocumentTidyXML error:&theError];

if (theDocument) {
    // We have a valid document
    NSLog(@"The XML doc: \r%@", theDocument);
    // Get the text string within the url tags
    NSArray *someNodes = [theDocument
        nodesForXPath:@"/response/data/url/text()"
        error:&theError];
    // This is the string we're looking for
    bitlyURL.stringValue = [someNodes objectAtIndex:0];
} else {
    bitlyURL.stringValue = @"Doc error";
    return;
}
```

代码的主要特性包括：

- 文档使用 NSXMLDocumentTidyXML 选项创建，该选项会整理文档格式，并可以消除轻微错误。
- nodesForXPath 数组返回搜索路径处的元素。
- 访问 text() 元素会返回一个文本对象，可以从数组中读取。无需进一步处理或提取。
- 项目代码包含一个旋转活动指示器，这是一个非常简单但有效的补充，用于显示下载状态。

![](img/2b293e29fc15b0797f113b85dd429b6e_282_1.png)

### 提示

要找到所需的路径，请查看原始 XML 中缩进标签的顺序。XPath 可以执行许多技巧，包括读取具有相同标签的多个返回值。更多信息，请参阅 www.w3schools.com/xpath/xpath_examples.asp 上的 XPath 教程。

## 使用 WebView

如果不介绍 WebView（Cocoa 的 Web 浏览器），任何关于 URL 的讨论都不完整。你可以使用 WebView 向任何应用添加浏览器窗口，完全控制 URL、窗口大小（滚动条会根据需要自动出现）以及前进和后退按钮等标准浏览器功能。

创建一个新项目，并将其保存为 WebView。右键单击 Frameworks，从出现的列表中选择 WebKit.framework，然后单击 Add，如图 10.14 所示。

### 图 10.14

在创建 WebView 之前添加 WebKit 框架。WebKit 包含一组非常丰富的功能，用于在 Objective-C 和 JavaScript 应用中进行 Web 管理。

![](img/2b293e29fc15b0797f113b85dd429b6e_283_0.png)

在 Interface Builder 中，从库中向 Content View 对象添加一个 WebView。设置其自动调整大小选项，如图 10.15 所示。

按如下方式编辑 WebViewAppDelegate.h 文件：

```objective-c
@class WebView;

@interface WebViewAppDelegate : NSObject <NSApplicationDelegate> {
    NSWindow *window;
    WebView *webView;
}

@property (assign) IBOutlet NSWindow *window;
@property (assign) IBOutlet WebView *webView;

@end
```

### 图 10.15

为 WebView 设置自动调整大小选项会强制其跟随窗口大小。如果不设置此功能，WebView 的大小将保持固定，这有时是理想的属性，但通常并非如此。

![](img/2b293e29fc15b0797f113b85dd429b6e_284_0.png)

保存文件。在 IB 中，将 WebView 输出口连接到 WebView 对象。然后，按如下方式编辑 WebViewAppDelegate.m 文件：

```objc
#import "WebViewAppDelegate.h"
#import <WebKit/WebKit.h>

@implementation WebViewAppDelegate

@synthesize window, webView;

- (void)applicationDidFinishLaunching:(NSNotification *)aNotification
{
    WebFrame *mainFrame = [webView mainFrame];
    NSURL *url = [NSURL URLWithString:@"http://www.apple.com"];
    NSURLRequest *aRequest = [NSURLRequest requestWithURL:url];
    [mainFrame loadRequest:aRequest];
}

@end
```

构建并运行应用，等待页面加载。然后点击 Store 链接。你应该会看到图 10.16 所示的结果。

### 图 10.16

WebView 在其窗口中运行。你可以点击活动链接进行导航。

![](img/2b293e29fc15b0797f113b85dd429b6e_285_0.png)

这段代码比看起来稍微不那么直观。关键特性是 `mainFrame` 属性是活动浏览器窗口；`WebView` 是一个或多个 Web 框架的包装器。`mainFrame` 是最重要的活动框架。在大多数应用中，你可以忽略其他框架。

`WebView` 是一个非常复杂的类。你可以添加浏览器必备功能，例如前进、后退和刷新按钮，还可以使用各种委托方法实现受控下载。甚至还有一个 `estimatedProgress` 方法可以驱动进度条。

作为一个简单的练习，你可以尝试添加 URL 栏，并在用户输入新 URL 时下载新页面。也可以实现更复杂的应用。

### 提示

大多数应用使用 `WebView` 访问网页。由于 URL 可以是本地地址，你可以使用 `WebView` 访问本地 HTML、CSS 或图像内容。

## 总结

在本章中，你了解了文件路径、URL 以及它们的异同。你探索了 Cocoa 的 File Manager 类，并发现了如何比较文件以及将可用的打开/保存面板构建到应用中。你还学习了如何从本地文件系统加载和保存数据、如何创建和查找有效路径，以及如何开始使用 Cocoa 数据对象的文件功能。

接下来，你详细探索了 NSURL，并了解了如何使用 URL 对象将在线数据加载到 Cocoa 对象中。你试验了 bit.ly Web API，并学习了如何组装简单的基于文本的请求，以及从 XML 返回中提取信息的复杂异步请求。

最后，你认识了 WebKit 中的 WebView 对象，并看到了向任何项目添加简单 Web 浏览器是多么容易。

