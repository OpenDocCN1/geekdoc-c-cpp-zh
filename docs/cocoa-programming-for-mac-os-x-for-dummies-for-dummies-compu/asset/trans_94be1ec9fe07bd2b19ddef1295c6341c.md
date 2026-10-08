
9. **在 _MyMovieController.m_ 实现文件中添加以下代码：**

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

然后，代码呈现一个标准的 _NSOpenPanel_，用户可以在其中选择电影文件。当他们选择一个文件后，代码将电影加载到一个 _QTMovie_ 中：

```objective-c
NSString *theFilePath = [openPanel filename];
[moviePlayer setMovie:[QTMovie
    movieWithFile:theFilePath error:nil]];
```

10. 选择 **Build::Build and Go** 来测试该项目。

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

**图 16-15：** QuickTime 也可以显示图像。

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

当新工程打开时，你会注意到它与本书其他地方的其他工程有很大的不同。这个工程包含一个 MyDocument 类，如图 17-2 所示。

![](img/ea40cad434a338535474e82c1a6ace20_337_1.png)

3. 点击 MyDocument.h 文件以查看其内容：

```objective-c
#import <Cocoa/Cocoa.h>

@interface MyDocument : NSDocument
{
}
@end
```

接口文件将 MyDocument 定义为 NSDocument 类的子类。这是你添加插座（outlets）和操作（actions）的地方。

4. 点击 MyDocument.m 文件以查看其内容：

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

```objective-c
- (NSData *)dataOfType:(NSString *)typeName error:(NSError **)outError
{
    // Insert code here to write your document to data of the specified type. If the given outError != NULL, ensure that you set *outError when returning nil.

    // You can also choose to override -fileWrapperOfType:error:, -writeToURL:ofType:error:, or -writeToURL:ofType:forSaveOperation:originalContentsURL:error: instead.

    // For applications targeted for Panther or earlier systems, you should use the deprecated API -dataRepresentationOfType:. In this case you can also choose to override -fileWrapperRepresentationOfType: or -writeToFile:ofType: instead.

    if (outError != NULL) {
        *outError = [NSError errorWithDomain:NSOSStatusErrorDomain code:unimpErr userInfo:NULL];
    }
    return nil;
}

- (BOOL)readFromData:(NSData *)data ofType:(NSString *)typeName error:(NSError **)outError
{
    // Insert code here to read your document from the given data of the specified type. If the given outError != NULL, ensure that you set *outError when returning NO.

    // You can also choose to override -readFromFile&wrapper:ofType:error: or -readFromURL:ofType:error: instead.

    // For applications targeted for Panther or earlier systems, you should use the deprecated API -loadDataRepresentation:ofType:. In this case you can also choose to override -readFromFile:ofType: or -loadFileWrapperRepresentation:ofType: instead.
}
```

