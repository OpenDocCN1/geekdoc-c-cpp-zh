
数组中的最后一项始终是 `nil`。例如，要为 `.mov` 和 `.mp4` 文件定义数组，你的代码可能如下所示：

```objc
NSArray *fileTypes = [NSArray arrayWithObjects:@"mov",
@"mp4", nil];
```

2. 将数组传递给 `runModalForType`:

```objc
if ([openPanel runModalForTypes:fileTypes] ==
NSOKButton) {
// 加载电影的代码放在这里
}
```

3. 将文件路径传递给 `movieWithFile` 类方法以创建 `QTMovie`。

```objc
QTMovie *movie = [QTMovie movieWithFile:theFilePath
error:nil];
```

### QTMovieView

加载电影后，使用 `QTMovieView` 类来播放它。你可以在 Interface Builder 的库窗口中找到 `QTMovieView` 控件（见图 16-7），通过库窗口底部的搜索栏搜索“Movie View”。

![](img/ea40cad434a338535474e82c1a6ace20_326_0.png)

`QTMovieView` 有几个你可以手动在 Interface Builder 中设置的属性——见图 16-8——或者通过代码以编程方式设置。

![](img/ea40cad434a338535474e82c1a6ace20_326_1.png)

以下是你可以在 Interface Builder 中设置的属性：

- 显示颜色：控制未加载电影时 `QTMovieView` 的颜色。默认颜色是黑色，但你可以将其更改为你想要的任何颜色。
- 显示控制器：切换显示内置的 QuickTime 控制器，该控制器在你将电影加载到 `QTMovieView` 控件时出现在底部。如果你曾在 Web 浏览器或 QuickTime 播放器应用程序中查看过 QuickTime 电影，你会熟悉 QuickTime 控制器。该控制器允许用户使用一组熟悉的按钮来控制 QuickTime 内容的播放。除了开始和停止播放外，你还可以快进和快退电影的部分片段，并在播放期间调整音量。图 16-9 展示了一个典型的 QuickTime 电影控制器。
- 可编辑：默认情况下，可编辑的值是 `NO`（即在检查器窗口中未选中）。QuickTime 控制器会出现，如图 16-9 所示。当你在 Interface Builder 的检查器窗口中选中“可编辑”复选框将可编辑设置为 `YES`，然后在代码中加载电影时，你会看到如图 16-10 所示的控制器。

可编辑属性会导致 `QTMovieView` 显示一个略有不同的 QuickTime 控制器。你可以将这种类型的控制器用于不同的目的，例如选择电影的某一部分。正如你在图 16-11 中看到的那样，按住 Shift 键点击允许你在 `QTMovieView` 中选择电影的部分或全部。
- 音量：切换音量按钮控件的显示，该控件出现在 `QTMovieView` 的左边缘。当你通过在检查器窗口中点击“音量”复选框将此属性设置为 `YES` 时，音量按钮显示。当为 `NO`（未选中）时，音量按钮不显示。

![](img/ea40cad434a338535474e82c1a6ace20_327_0.png)

图 16-9：标准的 QuickTime 控制器提供简单的播放界面元素。

![](img/ea40cad434a338535474e82c1a6ace20_328_0.png)

图 16-10：

可编辑属性在播放和编辑界面元素之间切换。

![](img/ea40cad434a338535474e82c1a6ace20_328_1.png)

图 16-11：

在 QMovieView 中按住 Shift 键点击控制器以选择电影中的某部分。

在 Interface Builder 中设置好所需的 `QMovieView` 属性后，在 Xcode 中添加一些代码来播放电影。假设你已经使用 `QTMovie` 类将电影加载到内存中，通过添加以下代码在 `QMovieView` 中显示该电影：

```cpp
[moviePlayer setMovie:theMovie];
```

你可以使用代码设置播放的许多其他方面。除了你在 Interface Builder 中找到的属性外，你还可以在播放期间设置电影的音量。音量 1.0 表示*最大*音量，由系统最大音量级别定义。因此，音量 0.5 是系统最大音量级别的一半。

```
[*moviePlayer* setVolume:1.0];
```

或者，如果你愿意，可以静音声音：

```
[*moviePlayer* setMuted:YES];
```

### 构建一个简单的电影播放器

查看 Cocoa 中电影播放工作原理最简单的方法是构建一个播放器。按照以下步骤操作：

1. 启动 Xcode，通过选择 文件 > 新建项目 创建一个新的 Cocoa 应用程序项目。在 Xcode 中双击 `MainMenu.xib` 文件，使用 Interface Builder 打开它。
2. 从 `MainMenu.xib` 文件窗口，打开你的界面的主窗口，然后选择 工具 > 检查器 打开窗口的检查器。
3. 在检查器窗口中，将窗口的 *标题* 字段更改为合适的名称。从库窗口中添加一个 `QTMovieView` 控件和一个 `NSButton`（如图 16-12 所示）。

![](img/ea40cad434a338535474e82c1a6ace20_329_0.png)

4. 为此界面创建一个控制器类。

从库窗口中拖拽一个 `NSObject` 到 XIB 项目窗口。按下 ⌘+6 并将新对象命名为 `MyMovieController`。图 16-13 展示了新的类。

![](img/ea40cad434a338535474e82c1a6ace20_330_0.png)

5. 在检查器窗口中为新控制器类添加一个出口和一个操作。

将出口命名为 `moviePlayer`，将操作命名为 `loadMovie`。
6. 将 `MyMovieController` 实例连接到界面：

   - a. 从新的 `MyMovieController` 实例按住 Control 键并拖拽至你之前添加到窗口的 `QTMovieView`。
   - b. 在出现的黑色连接列表覆盖层中选择 `moviePlayer` 出口。
   - c. 从按钮按住 Control 键并拖拽至 `MyMovieController`，并将其连接到 `loadMovie` 操作。
7. 设计完界面后，在 XIB 项目窗口中选择 `MyMovieController` 实例，并选择 文件⥫编写类文件。编写类文件并将其添加到 Xcode 项目中。
8. 在 Xcode 中，将 `MyMovieController.h` 接口文件中的代码更改为如下所示：

```objc
#import <Cocoa/Cocoa.h>

@interface MyMovieController : NSObject {
    IBOutlet id moviePlayer;
}
- (IBAction)loadMovie:(id)sender;
@end
```

9. 在 `MyMovieController.m` 实现文件中添加以下代码：

```objective-c
#import "MyMovieController.h"
#import <QTKit/QTKit.h>

@implementation MyMovieController
- (IBAction) loadMovie:(id) sender {
    NSOpenPanel *openPanel = [NSOpenPanel openPanel];
    [openPanel setTitle:@"Choose a Movie"];
    [openPanel setCanChooseDirectories:NO];

    NSArray *fileTypes = [NSArray arrayWithObjects:@"mov", @"mp4", nil];

    if ([openPanel runModalForTypes:fileTypes] == NSOKButton)
    {
        NSString *theFilePath = [openPanel filename];
        [moviePlayer setMovie:[QTMovie
            movieWithFile:theFilePath error:nil]];
    }
}
@end
```

代码首先定义了一个用户可以打开的文件类型数组。在这种情况下，你限制用户只能打开 .mov 和 .mp4 电影文件：

```objective-c
NSArray *theFileTypes = [NSArray
    arrayWithObjects:@"mov", @"mp4", nil];
```

然后，代码呈现一个标准的 `NSOpenPanel`，用户可以在其中选择电影文件。当他们选择一个文件后，代码将电影加载到一个 `QTMovie` 中：

```objective-c
NSString *theFilePath = [openPanel filename];
[moviePlayer setMovie:[QTMovie
    movieWithFile:theFilePath error:nil]];
```

10. 选择 `Build::Build and Go` 来测试该项目。

## 当电影不仅仅是电影

播放电影很有用，但 QuickTime 还能做更多事情。大家都知道传统电影是一系列电影画面加声音的序列，但很少有人知道在 QuickTime 中，这只是电影的一种类型。QuickTime 将所有媒体类型都视为电影。

例如，如果你将自己喜欢的音频文件作为 QuickTime 电影打开，QuickTime 会忠实地播放该音频文件。由于音频文件没有视觉组件，因此除了控制器外，无需显示 `QTMovieView` 的任何部分。图 16-14 展示了一个加载到 `QTMovieView` 中的音频文件。

![](img/ea40cad434a338535474e82c1a6ace20_332_0.png)

你可以加载到 `QTMovie` 中的一些可能的媒体文件类型如下：

- 音频：AIFF、MP3、M4A、WAV
- 视频：MOV、AVI、MPEG-1
- 图形：JPEG、TIFF、PNG、BMP
- 3D：QTVR
- 动画：Flash

为了给用户加载其他媒体类型的选项，只需将它们添加到本章前面“构建简单的音频播放器”部分中的 `FileTypes` 数组中。例如，如果你想提供加载 QuickTime 电影或 TIFF 文件的选项，请更改代码如下：

```objective-c
NSArray *theFileTypes = [NSArray arrayWithObjects:@"mov", @"tiff", nil];
```

Cocoa（以及随后的 QuickTime）平等地对待这两种文件类型：作为 `QTMovie`。这意味着你可以加载和播放（或者加载和显示，如果是图像）许多种类的媒体，而无需特殊代码。这是 QuickTime 最强大的功能之一，所以经常使用它！图 16-15 展示了加载了图像的 `QTMovie` 的 `QTMovieView`。

![](img/ea40cad434a338535474e82c1a6ace20_333_0.png)

图 16-15：QuickTime 也可以显示图像。

# 第四部分

# 高级 Cocoa 主题

![](img/ea40cad434a338535474e82c1a6ace20_334_0.png)

## 在本部分……

Cocoa 使你能够轻松地编程简单的工程，但它能处理其他任务吗？当然可以！第四部分将带你超越简单的 Cocoa 编程，进入超级极客的领域。你将了解如何编写使用多个窗口的应用程序，以及如何利用 Mac OS X 命令行的强大功能。第四部分以对如何在 Cocoa 应用程序中利用功能强大的 Core Data 框架的讨论而结束。

# 第 17 章

# 基于文档的应用程序

- 构建基于文档的工程
- 构建你的界面
- 添加代码

在整个书中，你创建了简单的单窗口应用程序来查看 Cocoa 各个方面的运行情况。当你熟悉 Cocoa 时，单窗口应用程序对于测试你的技能来说是足够的。但当你熟练地操作 Cocoa 之后，你会想要独自开拓领域，创建一个货真价实的应用程序。创建演示工程是一回事，但创建完整的应用程序则是另一回事。

当你创建一个应用程序时，你不仅要考虑管理单个窗口。许多应用程序采用基于文档的方法，即用户创建一个文档并向其中添加某种内容。如果你曾经使用过文字处理程序或绘图程序，你可能熟悉这种类型的应用程序。在基于文档的应用程序中，用户还可以保存文档、稍后打开它或打印它。所有这些功能在自行实现时都需要大量的工作。幸运的是，Xcode 通过提供一个功能齐全的基于文档的工程作为你自己基于文档的应用程序的起点来帮助你。

本章指导你完成构建基于文档的应用程序所需的步骤。沿途，你将实现许多不同的功能，而不需要做太多工作。

## 创建一个基于文档的工程

要开始处理基于文档的应用程序，请在 Xcode 中按以下步骤创建新工程：

1. 选择 File::New Project，在左侧选择 Application，在右侧选择 Cocoa Document-Based Application，如图 17-1 所示。

![](img/ea40cad434a338535474e82c1a6ace20_337_0.png)

2. 点击 Choose 按钮，并将新工程保存到你以后可以找到的位置。

当新工程打开时，你会注意到它与本书其他地方的其他工程有很大的不同。这个工程包含一个 `MyDocument` 类，如图 17-2 所示。

![](img/ea40cad434a338535474e82c1a6ace20_337_1.png)

3. 点击 `MyDocument.h` 文件以查看其内容：

```objective-c
#import <Cocoa/Cocoa.h>

@interface MyDocument : NSDocument
{
}
@end
```

接口文件将 `MyDocument` 定义为 `NSDocument` 类的子类。这是你添加插座（outlets）和操作（actions）的地方。

4. 点击 `MyDocument.m` 文件以查看其内容：

```objective-c
#import "MyDocument.h"

@implementation MyDocument

- (id)init
{
    self = [super init];
    if (self) {
        // Add your subclass-specific initialization here.
        // If an error occurs here, send a [self release] message and return nil.
    }
    return self;
}

- (NSString *)windowNibName
{
    // Override returning the nib file name of the document
    // If you need to use a subclass of NSWindowController or if your document supports multiple NSWindowControllers, you should remove this method and override -makeWindowControllers instead.
    return @"MyDocument";
}

- (void)windowControllerDidLoadNib:(NSWindowController *) aController
{
    [super windowControllerDidLoadNib:aController];
    // Add any code here that needs to be executed once the windowController has loaded the document's window.
}
```

![](img/ea40cad434a338535474e82c1a6ace20_338_0.png)
