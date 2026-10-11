
![](img/ea40cad434a338535474e82c1a6ace20_283_0.png)

删除一个文件，它就消失了！永久地。确保你的用户知道将发生删除操作，并始终给他们提供退出选项。做到这一点的一种方式是一个警告：

```objective-c
NSOpenPanel *theOpenPanel = [NSOpenPanel openPanel];
[theOpenPanel setTitle:@"Choose a File or Folder to Delete"]; 
[theOpenPanel setCanChooseDirectories:YES];

if ([theOpenPanel runModal] == NSOKButton) {
    NSString *theFilePath = [theOpenPanel filename];
    NSFileManager *theManager = [NSFileManager defaultManager];

    NSInteger n;
    n = NSRunAlertPanel (NSLocalizedString(@"Are you sure you want to delete the file?",nil), 
    NSLocalizedString(@"You cannot undo this deletion.", nil),
    NSLocalizedString(@"Yes", nil),
    NSLocalizedString(@"No", nil),
    nil);

    if (n == NSAlertDefaultReturn) {
        [theManager removeFileAtPath:theFilePath
        handler:nil];
    }
}
```

该代码使用 `NSOpenPanel` 询问用户要删除哪个文件。在创建 `theFilePath` 和 `theManager` 对象后，代码通过调用 `NSRunAlertPanel` 函数显示一个 Alert 面板。`NSRunAlertPanel` 接受五个参数，分别对应 Alert 的标题、Alert 上的消息、默认按钮上的文本、替代按钮上的文本，以及第三个按钮的文本，这次你通过传递 `nil` 来忽略它。如果 `NSRunAlertPanel` 返回 `NSAlertDefaultReturn` 值，这对应于 Alert 中的默认按钮，则代码使用 `removeFileAtPath` 方法删除文件。

## 创建文件夹

要在你的硬盘上创建一个文件夹，请使用 `NSFileManager` 的 `createDirectoryAtPath` 方法。你需要传递两个参数：

- 第一个参数是你希望创建文件夹的路径。
- 第二个参数允许你设置文件夹的各种属性。你很少会使用这个第二个参数，所以可以简单地将其设置为 `nil`。

为了展示 `createDirectoryAtPath` 方法的作用，请遵循以下步骤：

1. **将以下代码添加到 `FileInfoController.m` 中，以在桌面上创建一个名为 `MyNewFolder` 的文件夹：**

```objective-c
- (IBAction) createAFolder: (id) sender
{
NSString *theDestination = [ [NSHomeDirectory()
 stringByAppendingPathComponent:@"Desktop"]
 stringByAppendingPathComponent:@"MyNewFolder"
 ];
[theManager createDirectoryAtPath:theDestination
attributes:nil];
}
```

如果你使用了 `createAFolder` 操作，别忘了在头文件中定义它：

```objc
– (IBAction) createAFolder: (id) sender;
```

**2. 为 `FileInfoController` 添加一个操作，并将其连接到 Interface Builder 中的一个新 `NSButton`。**

图 13-9 展示了完成的界面。

有时，直接在 Xcode 的项目和 Interface Builder 的 `.nib` 文件中添加操作和出口（outlets）是最简单的方法，而不是依赖这两个应用程序之间的相互通信。

**3. 为了测试你的工作，回到 Xcode 并按下 ⌘+R。**

![](img/ea40cad434a338535474e82c1a6ace20_285_0.png)

# 第 14 章

## 使用 Cocoa 打印

### 本章内容

- 理解 Cocoa 中的打印过程
- 调整页面设置
- 运行打印任务
- 打印到 PDF 文件

![](img/ea40cad434a338535474e82c1a6ace20_286_0.png)

虽然 Cocoa 在屏幕上显示图形和文本的能力是世界级的，但这并不意味着 Apple 忘记了打印功能。Apple 数十年来一直作为推动 PostScript 和激光打印等技术采用的创新力量而闻名，并继续这一传统，通过为 Cocoa 添加易于实现的打印功能。本章向你展示了如何为你的 Cocoa 应用程序添加打印功能。虽然打印在过去对程序员来说是一个棘手的话题，但 Cocoa 使得在你的项目中实现一些复杂的打印功能变得简单。你会爱上 Apple 作为开发者为你提供的一致性，而你的用户也会爱上你的应用程序实现的专业打印结果。

要开始处理打印，请复制本章的起始源代码到你的硬盘。（要下载代码，请访问 www.dummies.com/go/cocoa.fd。）本章的打印项目基于第 12 章末尾完成的项目。因为你可以使用任何视图进行打印，所以你可以使用第 12 章中的图形视图作为你的可打印画布。

### Cocoa 中的打印工作原理

为了帮助你实现能够满足所有打印需求的良好结果，Cocoa 提供了一组用于在 Mac OS X 中打印的重要类。你将这些类组合在一起为你的应用程序添加打印功能：

- **`NSView`**：向页面打印就像在 `NSView` 中绘制文本和图形一样简单。本章的示例基于第 12 章中的图形示例。
- **`NSPageLayout`**：这个类负责显示“页面设置”面板。通常，当用户选择“文件” → “页面设置”时，应用程序会显示此面板。你的用户将调用“页面设置”面板来选择打印页面的方向。他们还可以在该面板中设置纸张大小。当用户完成调整 `NSPageLayout` 对象的打印属性后，`NSPageLayout` 对象会将结果保存在一个 `NSPrintInfo` 对象中。
- **`NSPrintInfo`**：`NSPrintInfo` 是一个存储类，保存打印的设置和选项。`NSPrintInfo` 存储来自“页面设置”面板的设置，以及出现在 `NSPrintPanel` 中的页数、边距和其他项目。
- **`NSPrintPanel`**：当你从大多数应用程序中选择“文件” → “打印”时，你会看到 `NSPrintPanel` 的一个示例。`NSPrintPanel` 负责管理打印任务的设置。`NSPrintPanel` 将其设置存储在 `NSPrintInfo` 对象中。
- **`NSPrintOperation`**：这个类负责创建打印的页面。它显示“打印”面板并执行打印任务。

为了帮助你设想 Cocoa 中打印过程的工作原理，以下是相关步骤的简要说明：

1. 向视图绘制文本和图形。
   这种绘制可以发生在任何视图中，无论是图形应用程序中的视图、文字处理程序，甚至是窗口的背景。Cocoa 可以从所有这些地方进行打印。
2. 用户选择“文件” → “页面设置”。
   你的应用程序显示“页面”面板。
3. 用户选择打印任务的格式和比例。
   图 14-1 显示了“页面”面板的样子。
4. 用户关闭面板。
   你的应用程序将设置存储在一个 `PrintInfo` 对象中。
5. 用户选择“文件” → “打印”。
   你的应用程序显示“打印”面板，用户在那里调整打印任务的设置。图 14-2 显示了一个典型的“打印”面板。当用户完成准备打印任务时，他可以通过点击“取消”来关闭面板，或通过点击“确定”来开始打印任务。
6. 用户打印视图。
   你的应用程序使用存储在 `PrintInfo` 对象中的“页面”和“打印”面板设置来设置打印操作。视图的 `drawRect` 负责绘制图形或文本，就像在屏幕上一样。

![](img/ea40cad434a338535474e82c1a6ace20_288_0.png)

![](img/ea40cad434a338535474e82c1a6ace20_288_1.png)

### 调整页面设置

你打印旅程的第一步从“页面”面板开始，你的用户可以在这里选择项目任务的刻度和格式。

如果你可以访问多台打印机，你还可以选择一个“针对格式”选项以获得可打印区域的尺寸。这些尺寸有助于你避免在边缘被裁剪。

![](img/ea40cad434a338535474e82c1a6ace20_289_0.png)

打开本章的 Xcode 项目。双击 `MainMenu.xib` 文件在 Interface Builder 中打开此项目的界面 XIB 文件。XIB 文件打开后，请按照以下步骤向项目中添加打印控制器：

1. **创建一个新的控制器类：**
   a. *打开 Library 窗口并搜索 `NSobject`。*
   b. *将新对象拖到项目窗口中。*
   c. *按 ⌘+6 并将新的 `NSobject` 命名为 `MyPrintController`。*

图 14-3 显示了新命名的对象。

![](img/ea40cad434a338535474e82c1a6ace20_289_1.png)

图 14-3：`MyPrint Controller` 对象承担打印任务。

2. **为 `MyPrintController` 添加一个出口和两个操作。**
   a. 按 ⌘+6 打开 Identity Inspector 窗口，并为 `MyPrintController` 类添加一个 `View` 出口。
   b. 通过点击 Identity Inspector 的 Class Actions 部分下方的 + 按钮，为控制器添加两个操作。
   c. 将这些操作命名为 `printOnePage:` 和 `showPagePanel:`。

`showPagePanel` 操作负责显示“页面”面板并存储其设置。`printOnePage` 操作显示“打印”面板，然后执行打印任务。

图 14-4 显示了 `MyPrintController` 的出口和操作。

3. **将 `MyPrintController` 实例连接到用户界面。**
   a. 从 `MyPrintController` 实例 Control-drag 到主窗口中的视图。在出现的小黑色连接列表覆盖层中，选择 `canvasView` 出口。

![](img/ea40cad434a338535474e82c1a6ace20_290_0.png)

![](img/ea40cad434a338535474e82c1a6ace20_290_1.png)

![](img/ea40cad434a338535474e82c1a6ace20_290_2.png)

   b. *将这两个操作连接到该项目的菜单项：从 MainMenu 菜单栏中的 Page Setup 菜单项 Control-drag 到 `MyPrintController` 实例。在出现的小黑色连接列表覆盖层中，选择 `MyPrintController` 中的 `showPagePanel` 操作。对 Print 菜单项和 `printOnePage` 操作重复此步骤。*

图 14-5 显示了 Identity Inspector 窗口中的 `MyPrintController` 出口和操作连接。

4. **创建 `MyPrintController` 的文件。**
   在 XIB 项目窗口中选择 `MyPrintController`。选择 *File* ‡ *Write Class Files* 以将头文件和实现文件添加到你在 Xcode 中的项目中。

5. **通过选择 *File* ‡ *Save* 保存你的界面项目，并通过选择 *Interface Builder* ‡ *Quit* 退出 *Interface Builder***。

6. **返回 Xcode 并选择 `MyPrintController.h` 文件以查看其内容。将你的 `MyPrintController.h` 文件修改为如下内容：**

```objc
/*  MyPrintController  */

#import  <Cocoa/Cocoa.h>

@interface MyPrintController : NSObject
{
IBOutlet  id canvasView;
NSPrintInfo  *thePrintInfo;
}
```

![](img/ea40cad434a338535474e82c1a6ace20_291_0.png)

除了将 `MyPrintController` 定义为 `NSObject` 之外，唯一的其他添加就是下面这一行：

```objc
NSPrintInfo *thePrintInfo;
```

这一行声明了一个指向 `NSPrintInfo` 对象的指针，作为实例变量，帮助你存储用户在“页面设置”和“打印”面板中所做的设置。

### 7. 选择 `MyPrintController.m` 文件，并将其代码修改为如下所示

```objc
#import "MyPrintController.h"

@implementation MyPrintController

- (IBAction) showPagePanel:(id) sender {
	int i;
	thePrintInfo = [NSPrintInfo sharedPrintInfo];
	NSPageLayout *pageLayout = [NSPageLayout
		pageLayout];
	i = [pageLayout runModalWithPrintInfo: (NSPrintInfo *)thePrintInfo];
}

@end
```

代码的运行逻辑如下：

- 1. `showPagePanel` 方法首先使用 `NSPrintInfo` 值填充 `thePrintInfo` 变量，该值由所有应用程序共享。
- 2. 代码创建一个 `NSPageLayout` 实例，并使用 `runModalWithPrintInfo` 方法将其显示出来。

通过将 `thePrintInfo` 传递给 `runModalWithPrintInfo` 方法，当用户关闭“页面设置”面板时，该面板会在 `thePrintInfo` 中保留其设置。

目前，这段代码是可以运行的，但并不是特别有趣。你可以运行它，然后选择“文件”→“页面设置”来查看并操作“页面设置”面板中的设置。

### 设置打印任务并打印视图

若要添加打印功能，你只需要实现上一节中 `MyPrintController` 中定义的 `printOnePage` 操作即可。在 Xcode 中点击 `MyPrintController.m` 文件，并将其代码修改为如下所示

```objc
#import "MyPrintController.h"

@implementation MyPrintController

- (IBAction)showPagePanel:(id)sender {
    int i;
    thePrintInfo = [NSPrintInfo sharedPrintInfo];
    NSPageLayout *pageLayout = [NSPageLayout pageLayout];
    i = [pageLayout
         runModalWithPrintInfo:(NSPrintInfo *)
             thePrintInfo];
}

- (IBAction)printOnePage:(id)sender
{
    thePrintInfo = [NSPrintInfo sharedPrintInfo];
    NSPrintOperation *thePrintOperation;

    thePrintOperation =
        [NSPrintOperation printOperationWithView:
         myCanvasView printInfo:thePrintInfo];

    [thePrintOperation setShowPanels: YES];
    [thePrintOperation runOperation];
}

@end
```

`printOnePage` 方法以这种方式处理运行“打印”面板并执行打印任务：

- 1. 它使用类方法 `printOperationWithView` 创建一个 `NSPrintOperation` 实例。
- 2. 你向 `printOperationWithView` 方法传递要打印的视图和一个 `NSPrintInfo` 实例。
- 3. `printOperationWithView` 方法返回一个 `NSPrintOperation` 实例。
- 4. （可选，但在大多数应用程序中很常见）如果你希望显示“打印”面板，请调用 `setShowPanels`，并传入布尔值 `YES`。
- 5. `NSPrintOperation` 对象的 `runOperation` 方法执行打印任务。

Cocoa 会为你处理其余的一切，包括关闭“打印”面板和打印视图。

## 打印到除打印机以外的位置
