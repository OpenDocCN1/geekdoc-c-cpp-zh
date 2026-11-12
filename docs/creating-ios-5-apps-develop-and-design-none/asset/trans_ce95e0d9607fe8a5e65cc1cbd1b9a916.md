

**图 4.18** 带有圆角的“完成”按钮

![](img/fe9fea534a8e7868f811f7cd33da015f_213_0.png)

再次运行应用程序。现在当你按下单位按钮时，我们的模态视图中的“完成”按钮看起来很漂亮（图 4.18）。

这在竖屏模式下运行良好，但如果旋转视图，你会注意到我们的渐变没有拉伸以填满按钮。问题在于，我们无法自动调整这些图层的大小。相反，我们需要在系统布置我们的视图时手动调整它们的大小。为此，请在视图控制器中实现 `viewDidLayoutSubviews` 方法。

```objective-c
- (void)viewDidLayoutSubviews {
    CALayer* layer = self.doneButton.layer;
    CGFloat width = layer.bounds.size.width;
    for (CALayer* sublayer in layer.sublayers) {
        if ([sublayer.name hasSuffix:@"Gradient"]) {
            CGRect frame = sublayer.frame;
            frame.size.width = width;
            sublayer.frame = frame;
        }
    }
}
```

这个方法在系统布置完所有子视图后立即被调用。在这里，我们只是获取 `doneButton` 图层及其宽度的引用。然后遍历所有子图层。如果子图层的名称以 “Gradient” 结尾，我们就将其宽度调整为按钮的宽度。这样，我们的自定义图层将被调整大小，但不会改动按钮的任何其他图层。

试试看。在“输入体重”和“选择单位”视图之间来回切换。将界面旋转到所有不同的方向。如果一切正常，提交我们所有的更改。下一站，历史视图。

## 核心动画与性能

虽然我们使用 `CALayer` 为按钮添加了圆角，但同样的技术也可以应用于任何 `UIView`。一个明显的例子是创建带有圆角甚至玻璃光泽的 `UIImageView` 对象。然而，你可能会发现它对于许多 `UIView` 对象都很有用：文本视图、网页视图、滚动视图、地图视图或你可能会构建的任何自定义视图。

虽然这种方法很方便，但它可能变得计算开销很大。执行这类核心动画操作需要我们的视图在绘制到主视图之前先绘制到一个离屏缓冲区。这在我们修改过的视图及其所有子视图的每一帧上都会发生。

这对于任何期望流畅动画的视图（例如滚动视图或表格视图）尤其重要。大量对象执行离屏渲染会很快将流畅滚动的界面变成卡顿、断续的混乱场面。

我们可以使用 Instruments 来检测使用离屏渲染的视图（更多关于 Instruments 的信息，请参阅附录 B）。连接你的测试 iOS 设备，并将 scheme 设置为在其上运行。然后从主菜单中选择 Product > Profile。这将启动 Instruments。当提示时，启动 Core Animation 模板。选择 Core Animation 轨道，并确保选中 “Color Offscreen-Rendered Yellow” 选项（图 4.19）。这将把任何在离屏渲染的视图高亮为黄色，使其易于发现。

正如你所看到的，当你触摸单位按钮时，整个屏幕在翻转过程中被离屏渲染。然而，一旦过渡动画完成，其余部分就可以直接渲染。只有我们的自定义按钮继续在离屏渲染（图 4.20）。

如果核心动画成为性能问题，最简单的修复方法是将 `CALayer` 的 `shouldRasterize` 属性设置为 `YES`。这告诉核心动画该图层需要离屏渲染，并强制它尽可能缓存离屏图像并重复使用。在某些情况下，这可以显著提高核心动画的性能。

然而，`shouldRasterize` 并不是神奇的“运行更快”标志。它只应在非常特定的情况下使用。显然，如果我们的视图外观在变化，那么缓存就没有意义。核心动画将需要丢弃缓存并为每一帧重新渲染视图。更糟糕的是，如果视图本来不需要离屏渲染，设置 `shouldRasterize` 会强制它进行离屏渲染。这实际上会降低应用程序的性能。

在 Health Beat 中，`shouldRasterize` 对我们毫无帮助。我们的按钮的最终图像只渲染一次，所以我们永远不会重用缓存。创建它只会浪费内存。然而，如果我们将按钮放入滚动视图中，设置 `shouldRasterize` 可能会产生很大的不同。

![](img/fe9fea534a8e7868f811f7cd33da015f_216_0.png)

**图 4.19** 使用 Instruments 高亮离屏渲染的视图

![](img/fe9fea534a8e7868f811f7cd33da015f_216_1.png)

**图 4.20** 所有离屏渲染的视图都被高亮为黄色

如果我们不能使用 `shouldRasterize` 来解决性能问题，我们可能不得不回到自定义绘制。在我们的例子中，我们可以创建一个 `UIView` 的子类并重写 `drawRect:` 方法，手动绘制我们的圆角矩形和渐变填充。通常，绘制代码在对象首次放置到屏幕上时只调用一次。然后它被缓存在视图的 `CALayer` 中，并且可以在不进行额外绘制的情况下进行滚动、调整大小或动画化。当然，初始绘制可能比核心动画方法调用稍微慢一些，但我们是将每帧的成本转换为一次性成本。在许多情况下，这会产生显著的性能提升。

我们将在第 5 章“绘制自定义视图”中更深入地介绍自定义绘制。

## 显示体重历史

现在让我们转到历史视图。这里，我们显示 `WeightHistory` 中所有条目的列表。我们将使用 `UITableView` 来呈现这些条目，每行显示一个条目。让我们从设计这些行的自定义单元格开始。

右键单击 Views 组，选择 New File > Objective-C Class。确保它是 `UITableViewCell` 的子类，并将其命名为 HistoryCell。现在打开 HistoryCell.h。按如下所示修改头文件：

```objective-c
#import <UIKit/UIKit.h>
#import "WeightEntry.h"

@interface HistoryCell : UITableViewCell

@property (nonatomic, strong) IBOutlet UILabel* weightLabel;
@property (nonatomic, strong) IBOutlet UILabel* dateLabel;
- (void)configureWithWeightEntry:(WeightEntry*)entry
                     defaultUnits:(WeightUnit)unit;

@end
```

与视图控制器不同，无法从故事板 Control-拖动到视图的头文件来创建 outlet。相反，我们需要先手动声明它们。我们还声明了一个配置单元格的方法——根据 `WeightEntry` 和 `WeightUnit` 参数更改其标签的内容。

切换到实现文件。我们将从合成我们的属性开始。

```objective-c
@synthesize weightLabel=_weightLabel;
@synthesize dateLabel=_dateLabel;
```

然后实现 `configureWithWeightEntry:defaultUnits:`。

```objective-c
- (void)configureWithWeightEntry:(WeightEntry*)entry
                     defaultUnits:(WeightUnit)unit {
    self.weightLabel.text = [entry stringForWeightInUnit:unit];
    self.dateLabel.text =
        [NSDateFormatter
            localizedStringFromDate:entry.date
                         dateStyle:NSDateFormatterShortStyle
                         timeStyle:NSDateFormatterShortStyle];
}
```

在这里，我们使用 `WeightEntry` 的 `stringForWeightInUnit:` 方法，用格式正确的权重字符串设置 `weightLabel` outlet。接下来，我们使用 `NSDateFormatter` 使用短日期和短时间格式创建正确的本地化日期字符串。然后将其分配给 `dateLabel` outlet。

现在，让我们打开故事板并放大历史视图。选择原型单元格并切换到身份检查器。将单元格的类设置为 HistoryCell。然后切换回属性检查器。确保 Accessory 属性设置为 Disclosure Indicator。这将在单元格右侧添加一个灰色 chevron。

Xcode 提供了两个内置的 accessory，功能非常相似。Disclosure Indicator 和 Detail Disclosure 都表示应用程序有与这一行相关的附加信息。然而，它们之间在操作方式和预期用途上略有不同。

Detail Disclosure 创建一个带有白色 chevron 的圆角蓝色按钮。当用户点击该按钮时，它应导航到所选项的详细信息视图。另一方面，Disclosure Indicator 只提供灰色 chevron 图像。在这种情况下，用户必须选择行本身，然后导航到子列表（通常包含其他选项）。

可以说，Health Beat 应该使用 Detail Disclosure accessories——但我觉得让用户选择行而不是 disclosure 按钮效果更好。此外，我们的详细信息视图是一个（某种）列表，所以这并非完全不合适，即使是 Apple 也并非 100% 一致地使用它们的 accessories。

现在，拖出两个标签。将第一个标签的标题设置为 Weight。使其宽度为 100 磅，并将字体设置为 18 磅系统粗体。然后拖动它，使其沿单元格的左边距垂直居中。在尺寸检查器中，将其自动调整大小位置锁定在顶部和左侧。

