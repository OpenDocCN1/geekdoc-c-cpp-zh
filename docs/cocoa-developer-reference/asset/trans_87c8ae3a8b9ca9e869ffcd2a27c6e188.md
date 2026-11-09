
要移动查找指针，请使用

```objective-c
[aFileHandle seekToFileOffset: aLongInt];
```

对应的 writeData: 方法将数据写入文件。使用 synchronizeFile 方法刷新缓存和缓冲区，并确保文件内容正确更新。

![](img/2b293e29fc15b0797f113b85dd429b6e_260_0.png)

> **提示**
>
> 文件句柄也可用于数据传输。NSFileHandle 支持通过委托方法进行异步通信，这些委托方法在数据发送或传输时发布通知。有关详细信息，请参阅类参考。

## 使用文件管理器

你可以使用文件管理器对象来复制、移动和删除文件，以及列出目录内容。大多数应用程序不需要实现文件管理器。用户可以使用 Finder 处理单个文件，因此这些功能仅对批量文件操作的应用程序（例如备份/恢复应用程序）有用，或者当应用程序需要在关闭时删除临时文件时有用。文件打开/存储操作可以使用标准文件访问面板执行，而目录列表只有在创建自定义的等效功能时——或执行扫描目录结构的批量操作时——才有用。

但是，你可以使用文件管理器比较两个文件或更改应用程序的当前目录。

文件管理器类易于使用。要创建文件管理器对象，请使用

```objective-c
NSFileManager *thisManager = [NSFileManager defaultManager];
```

这会返回默认系统文件管理器，它是你的应用程序应使用的唯一管理器。

要比较两个文件，请使用

```objective-c
[thisManager contentsEqualAtPath: aPath andPath: anotherPath];
```

这会返回一个可用于测试相等性的 BOOL。复制/移动操作也同样简单直接

```objective-c
[thisManager copyItemAtPath: aPath
toPath: anotherPath error:&error];
```

要更改当前应用程序目录，请使用

```objective-c
[thisManager changeCurrentDirectoryPath: aNewPath];
```

## 创建和使用 URL

尽管 URL 与字符串路径在一定程度上可以互换，但它们更复杂。它们还支持附加功能。某些对象，例如用于向用户呈现文件选择器的 NSOpenPanel 和 NSSavePanel 对象，会自动返回 URL 路径。更常见的是，你从字符串路径创建文件访问 URL；例如：

```objective-c
NSURL *thisURL = [NSURL fileURLWithPath: aPath];
```

你也可以从 URL 中提取路径字符串：

```objective-c
NSString *thePath = [thisURL path];
```

![](img/2b293e29fc15b0797f113b85dd429b6e_261_0.png)

> **警告**
>
> NSURL 的 string 方法返回一种 URL 特定格式的字符串。它既不是有效的文件路径，也不是有效的 Web URL。如果你将其记录到日志中，会看到它看起来完全不像路径。另外，最好不要将 URLWithString: 和 initWithString: 方法用于文件路径——它们可能无法正确解析路径字符串。

### 理解路径与引用

NSURL 支持两种路径对象：文件路径和文件引用。创建文件 URL 时，你不需要指定类型，因为文件系统会在运行时检查类型并相应地解析 URL 数据。但了解这种区别是有用的。你可以通过对引用运行 filePathURL: 将其转换为路径。使用 fileReferenceURL: 将路径转换为引用。isFileReferenceURL 和 isFileURL 是返回类型的 BOOL 方法。

### 使用 URL 读写数据

大多数对象提供的方法与用于文件路径读写的方法相对应。例如，要加载字符串，请使用

```objective-c
NSString *textInTheFile =
[NSString stringWithContentsOfURL: aURL
encoding: anEncoding error: &error];
```

但与文件路径不同，URL 可以是远程的：

```objective-c
NSURL *aURL =
[NSURL URLWithString: @"http://www.asite.com/file.txt"];
```

如果你知道远程服务器上文件的地址，就可以使用此功能下载它，本章后面关于 Web API 的一节将对此进行讨论。

## 使用打开与存储面板

Cocoa 包含两个类，使用户能够在打开和存储文件时以可视方式选择文件并返回 URL。**NSOpenPanel** 创建如图 10.1 所示的类似 Finder 的窗口。**NSSavePanel** 创建如图 10.2 所示的更简单的窗口，不过它可以展开为如图 10.3 所示的更大面板。

**图 10.1** 标准 **NSOpenPanel**。该面板从应用程序窗口顶部滑下。此动画是自动的——它内置于该类中，无法更改。

![](img/2b293e29fc15b0797f113b85dd429b6e_262_0.png)

**图 10.2** 标准小型 `NSSavePanel`。你可以使用此面板输入文件名并将其存储到当前目录。

![](img/2b293e29fc15b0797f113b85dd429b6e_263_0.png)

通常，这些类包裹在加载和存储数据的代码周围，使用 Cocoa 数据收集类内置的功能或自定义 `NSCoder` 实现。你可以使用这些类来：

- 支持可配置的窗口标题、可选文本消息、返回按钮提示以及其他用户友好的标签功能。
- 打开文件时预选一种或多种文件类型。其他文件类型会变灰，无法选择或打开。
- 打开时允许多选。
- 存储时自动追加文件扩展名。
- 预选默认目录。
- 启用或禁用目录切换。
- 显示或隐藏隐藏文件。
- 启用文稿模态或应用程序模态显示。
- 动态刷新并重新验证文件视图。
- 返回“取消”或“好”状态。
- 以多种格式返回文件路径。（从 OS X 10.6 起，首选 URL。）

**图 10.3** 点击文件名框旁边的向下三角形，会显示 NSSavePanel 的较大视图，可完全访问目录。

![](img/2b293e29fc15b0797f113b85dd429b6e_264_0.png)

打开和存储面板以及 Cocoa 的面向对象数据功能，使得创建非常精简的应用程序成为可能，例如网站上提供的 Picopad 应用程序。Picopad 实现了一个非常简单的文本编辑器，具有文件存储/加载功能。该编辑器将文本存储在 NSTextView 中，而 NSTextView 位于 NSScrollView 内，如图 10.4 所示。

> **说明**
>
> 你可以在 www.wiley.com/go/cocoadevref 下载 Picopad 应用程序。

**图 10.4** Picopad 的 nib 文件。NSScrollView 包含一个 NSTextView 实例。在此示例中，你将忽略滚动条并直接链接到文本视图；不需要访问滚动视图的属性。

![](img/2b293e29fc15b0797f113b85dd429b6e_265_0.png)

NSWindow 被子类化为 TheWindow，并且它包含一对打开/存储方法 openADocument: 和 saveTheDocument:，它们链接到“打开”和“存储为”菜单项。TheWindow 还包含一个连接到文本视图的出口，以便应用程序可以读取和写入其文本。头文件以及其中一个链接如图 10.5 所示。

**图 10.5** TheWindow 的头文件包含一个连接到文本视图的出口以及一对用于打开和存储文件的方法。其中一个方法显示为链接到其对应的菜单项。另一个项（此处未显示）也已链接。

![](img/2b293e29fc15b0797f113b85dd429b6e_266_0.png)

存储和打开方法很容易实现。从 OS X 10.6 起，NSOpenPanel 和 NSSavePanel 使用内联块作为返回处理程序，而不是委托方法。TheWindow 的完整代码如下：

```objective-c
@implementation TheWindow
@synthesize theTextView;
- (void) saveTheDocument: (id) sender {
    //Create a panel
    NSSavePanel *savePanel = [NSSavePanel savePanel];
    savePanel.allowedFileTypes = [NSArray arrayWithObject:@"txt"];
    //Display it, and append the handler block
    [savePanel beginSheetModalForWindow:self
        completionHandler:^(NSInteger result) {
            //This is the handler block
            if (result == NSFileHandlingPanelOKButton) {
                //Save the file on OK, do nothing on Cancel
                [theTextView.string writeToURL: savePanel.URL atomically: YES
                    encoding: NSUTF8StringEncoding error:nil];
            }
        }]; //This is the end of the handler
}

- (void) openADocument: (id) sender {
    NSOpenPanel *openPanel = [NSOpenPanel openPanel];
    openPanel.allowedFileTypes = [NSArray arrayWithObject:@"txt"];
    [openPanel beginSheetModalForWindow:self
        completionHandler:^(NSInteger result) {
            if (result == NSFileHandlingPanelOKButton) {
                // If OK, load the file
                NSString *theText = [NSString stringWithContentsOfURL:openPanel.URL encoding: NSUTF8StringEncoding error:nil];
                [theTextView setString: theText];
            }
        }];
}
```

### 代码要点：

- 1. 第一行创建一个存储面板，并用一个预选 `.txt` 文件的数组初始化它。
- 2. 第二行显示该表单。它以模态方式运行，锁定应用程序的其余部分。
- 3. 结果处理程序位于一个块内。它检查返回按钮状态，如果用户取消则不做任何事。否则，它将以字符串形式把数据写入面板返回的 URL 所指向的文件。
- 4. 打开方法几乎相同，但它将所选文件中的数据加载到文本视图中。

你可以通过设置其他可选属性进一步自定义打开/存储面板。这个极简解决方案实现了一个完整的打开/存储应用程序，具有编辑、复制/粘贴以及文件存储和加载功能——所有这些只需几行代码。完成的应用程序如图 10.6 所示。

![](img/2b293e29fc15b0797f113b85dd429b6e_267_0.png)

> **警告**
>
> 如果你的 Mac 位于网络上，并且你连接到了任何远程服务器，打开和存储面板将扫描网络并 ping 服务器。这通常不是问题，但如果你使用像 Little Snitch 这样的网络监视器，当你的极简应用程序触发网络访问警告时，不要感到惊讶。

