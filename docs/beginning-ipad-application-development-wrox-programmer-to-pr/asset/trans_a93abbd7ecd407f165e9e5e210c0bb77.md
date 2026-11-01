
## 7 使用表格视图

## 本章你将学到：

- 如何手动向视图添加表格视图，并将数据源和代理连接到您的视图控制器
- 如何处理表格视图中的各种事件以填充项目
- 如何处理表格视图中的各种事件，以便用户可以选择其中包含的项目
- 如何在表格视图的行中显示文本和图像
- 如何在基于拆分视图的应用程序中使用表格视图
- 如何在表格视图中显示属性列表中的项目
- 如何将表格视图中的项目分组到各节中
- 如何为表格视图添加索引
- 如何为表格视图添加搜索功能
- 如何向表格视图中的行添加披露指示符和复选标记

iPad 应用程序中最常用的视图之一是表格视图。它用于显示用户可以从中选择的项目列表，或点击以显示更多信息。图 7-1 显示了设置应用程序中正在使用的表格视图。

在第 4 章中，当你开发基于拆分视图的应用程序项目时，你第一次接触到表格视图。 该章节并未完全深入探讨表格视图的工作原理，并且刻意省略了很多细节。 表格视图是一个如此重要的主题，值得单独用一章来介绍。

在本章中，你将详细检查表格视图，并探索使其成为如此多功能视图的各种构建块。

- 2. 通过查看尺寸检查器窗口观察其大小和定位。 这里，其位置为 (20,20)，大小为 371 x 37 像素。
- 3. 通过点击窗口右上角的箭头图标旋转视图的方向。
- 4. 通过将其重新定位到视图窗口的右下角来重新定位圆角矩形按钮视图（参见图 6-5）。 同时观察并记录其位置。

![](img/744c5ec15e15ca7891c98be71dc25d13_210_0.png)

图 6-5

- 5. 在 ScreenRotationsViewController.h 文件中，添加以下以粗体显示的代码：

```
#import <UIKit/UIKit.h>

@interface ScreenRotationsViewController : UIViewController {
    IBOutlet UIButton *btn;
}
@property (nonatomic, retain) UIButton *btn;

@end
```

```
}
[self positionViews];
}
- (void)viewDidLoad {
    [self positionViews];
    [super viewDidLoad];
}
- (void)dealloc {
    [btn release];
    [super dealloc];
}
```

- 9. 保存项目并在 Xcode 中按 Command-R 将应用程序部署到 iPhone 模拟器。
- 10. 请注意，当 iPhone 模拟器处于纵向模式时，圆角矩形按钮视图显示在左上角。 但当你将方向更改为横向模式时，它会被重新定位到右下角（参见图 6-7）。

![](img/744c5ec15e15ca7891c98be71dc25d13_212_0.png)

图 6-7

## 工作原理

本项目说明了当设备更改方向时如何重新定位应用程序上的视图。 你首先创建一个出口并将其连接到视图窗口上的圆角矩形按钮视图。

当设备正在旋转时，你处理 willAnimateSecondHalfOfRotationFromInterfaceOrientation: 事件，因为这样做可以让你知道设备正在更改到的目标方向。 当此事件触发时，你可以使用当前视图（self）的 interfaceOrientation 属性获取目标方向，如下所示：

```
UIInterfaceOrientation destOrientation = self.interfaceOrientation;
```

使用此信息，你通过你已定义的 positionViews 方法更改其 frame 属性，根据目标方向定位视图：

```objc
-(void) positionViews {
    UIInterfaceOrientation destOrientation = self.interfaceOrientation;
    if (destOrientation == UIInterfaceOrientationPortrait || destOrientation == UIInterfaceOrientationPortraitUpsideDown) {
        //---if rotating to portrait mode---
        btn.frame = CGRectMake(20, 20, 371, 37);
    } else {
        //---if rotating to landscape mode---
        btn.frame = CGRectMake(633, 691, 371, 37);
    }
}
```

你还应该在 viewDidLoad 方法中调用 positionViews 方法，以便在加载视图窗口时正确显示圆角矩形按钮：

```objc
- (void)viewDidLoad {
    [self positionViews];
    [super viewDidLoad];
}
```

## 处理视图定位的属性

在前面的示例中，你使用 frame 属性在运行时更改视图的位置。 frame 属性定义了视图相对于其父视图（包含它的视图）所占用的矩形。 使用 frame 属性可以设置视图的定位和大小。 除了使用 frame 属性外，你还可以使用 center 属性，它设置视图的中心，也相对于其父视图。 你通常在执行某些动画并且只想更改视图位置时使用 center 属性。

## 本章你学到了什么

| 主题 | 关键概念 |
|---|---|
| 处理设备旋转 | 实现 `shouldAutorotateToInterfaceOrientation:` 方法 |
| 支持的四种方向 | `UIInterfaceOrientationPortrait`<br>`UIInterfaceOrientationLandscapeLeft`<br>`UIInterfaceOrientationLandscapeRight`<br>`UIInterfaceOrientationPortraitUpsideDown` |
| 设备旋转时触发的事件 | `willAnimateFirstHalfOfRotationToInterfaceOrientation:`<br>`willAnimateSecondHalfOfRotationFromInterfaceOrientation:`<br>`willRotateToInterfaceOrientation:`<br>`willAnimateRotationToInterfaceOrientation:` |
| 用于更改视图位置的属性 | 使用 `frame` 属性更改视图的定位和大小<br>使用 `center` 属性更改视图的定位 |

- 5. 右键单击表格视图并将 dataSource 出口连接到文件的所有者项（参见图 7-4）。 对 delegate 出口执行相同的操作（参见图 7-5）。

![](img/744c5ec15e15ca7891c98be71dc25d13_222_0.png)

图 7-2

![](img/744c5ec15e15ca7891c98be71dc25d13_222_1.png)

图 7-3

![](img/744c5ec15e15ca7891c98be71dc25d13_223_0.png)

图 7-4

![](img/744c5ec15e15ca7891c98be71dc25d13_223_1.png)

图 7-5

## 工作原理

你实际上在第 7 步通过创建一个名为 `listOfMovies` 的 `NSMutableArray` 对象来启动应用程序，其中包含电影名称列表。 存储在此数组中的项目将由表格视图显示。

```objc
- (void)viewDidLoad {
    //---initialize the array---
    listOfMovies = [[NSMutableArray alloc] init];
    
    //---add items---
    [listOfMovies addObject:@"Training Day"];
    [listOfMovies addObject:@"Remember the Titans"];
    [listOfMovies addObject:@"John Q."];
    [listOfMovies addObject:@"The Bone Collector"];
    [listOfMovies addObject:@"Ricochet"];
    [listOfMovies addObject:@"The Siege"];
    [listOfMovies addObject:@"Malcolm X"];
    [listOfMovies addObject:@"Antwone Fisher"];
    [listOfMovies addObject:@"Courage Under Fire"];
    [listOfMovies addObject:@"He Got Game"];
    [listOfMovies addObject:@"The Pelican Brief"];
    [listOfMovies addObject:@"Glory"];
    [listOfMovies addObject:@"The Preacher's Wife"];
    
    [super viewDidLoad];
}
```

为了用项目填充表格视图，你需要处理 `UITableViewDataSource` 协议中包含的几个事件。 因此，你需要确保你的视图控制器符合此协议：

```objc
@interface TableViewExampleViewController : UIViewController
<UITableViewDataSource> {
}
```

> **注意** 严格来说，如果你已将 `dataSource` 出口连接到文件的所有者项，则无需添加前面的语句。 然而，同时执行两者也不会造成任何伤害。 不过，添加 `<UITableViewDataSource>` 协议有一个优点——编译器会在你忘记在代码中实现任何强制方法时发出警告，有助于防止错误。

`UITableViewDataSource` 协议包含多个可用于向表格视图提供数据的事件。 本示例中处理的两个事件是：

- `tableView:numberOfRowsInSection:`
- `tableView:cellForRowAtIndexPath:`

