
![](img/fe9fea534a8e7868f811f7cd33da015f_237_0.png)

```objc
[WeightEntry stringForWeightInLbs:maxWeight -
    weight inUnit:unit];
self.gainTextField.text =
    [WeightEntry stringForWeightInLbs:weight -
        minWeight inUnit:unit];
}
```

这里我们填充文本字段。同样，我们使用 `stringForWeightInLbs:inUnit:` 类方法来生成格式正确且本地化的重量字符串。这里唯一需要注意的是 `weightTextField`。如果当前 `WeightEntry` 的重量小于月平均值，我们将文本颜色设置为深绿色。如果大于月平均值，则设置为深红色。这里，我们通过指定 RGBA 值来使用自定义颜色（图 4.27）。

还有最后一步。修改 `shouldAutorotateToInterfaceOrientation:` 方法，使其返回 `YES`，允许我们旋转到任意方向。

```objc
- (BOOL)shouldAutorotateToInterfaceOrientation:
    (UIInterfaceOrientation)interfaceOrientation
{
    return YES;
}
```

### 显示文本输出

在 iOS 中，我们可以通过多种不同方式显示文本输出。我们已经看到两种：UILabel 和 UITextField。当你在相对静态的布局中显示较短的文本片段时，这些非常有用。UITextView 则提供了更多的灵活性，允许我们输入多行文本块。与其他控件一样，我们可以设置字体类型、大小和文本颜色。但是，我们必须对整个文本视图使用相同的设置。

如果我们想要更复杂的文本呢？比如带有标题和正文的文本？使用粗体、斜体和不同颜色来吸引注意力的文本？毕竟，Mac 历来拥有强大的文本排版能力。在 90 年代，Mac 处于桌面出版革命的前沿。因此，你会期望 iOS 能继承这一传统的一部分。不幸的是，这里的科技似乎存在一个奇怪的缺口。

有许多不同的技术，各有其优缺点。有些技术，比如 NSString 的 UIStringDrawing 类别，提供了在屏幕上绘制字符串的有用方法——但就像 UILabel 和 UITextField 一样，这些实际上只适用于短标签。Core Animation 的 CATextLayer 和 Core Graphics 的文本支持也属于这一类——在某些边缘情况下有用，但不是通用解决方案。

要实现真正格式化的文本，我们有两个主要选项：使用 UIWebView，或者使用 Core Text 框架自己构建。

UIWebView 代表了高级方法。在这里，我们使用 HTML 和 CSS 来布局文本，然后将其加载到 Web 视图中进行显示。这有很多优点。你可以免费获得完整的复制粘贴支持。你也可以利用已有的任何 Web 开发经验。你可以合并图像和其他媒体。UIWebView 支持广泛的（非 Flash）Web 技术，包括 JavaScript。你甚至可以在原生 Objective-C 代码和 Web 视图中运行的 JavaScript 之间进行通信，从而生成混合应用程序。实际上，在 iOS 5 上，借助 contentEditable 和 execCommand 的一点帮助，你可以轻松构建一个功能齐全的富文本编辑器。

主要缺点是 UIWebView 是出了名的内存大户。确实如此；当你实例化第一个 Web 视图时，系统会执行大量幕后设置。这可能导致首次显示 Web 视图时出现明显的延迟。然而，这种名声可能有点不公平。你通常可以通过预加载 Web 视图来隐藏初始启动成本，一旦初始设置完成，性能其实并没有大多数人想象的那么差。

另一方面，Core Text 提供了一个全速、高性能、马力全开的文本系统。它专为高性能和易用性而设计。它还能提供更高质量的排版控制——尤其是在旧设备上（在 iOS 5 之前，UIWebView 中无法使用字距调整和连字）。

Core Text 特别适合分页应用，而 Web 视图更自然地支持滚动应用。Core Text 还与 Core Graphics 紧密集成，使我们能够执行各种绘图任务。

缺点是，由于它是一个低级库，你必须自己做大部分工作。它不支持其他媒体，也不支持复制粘贴。最后一点尤其重要。iOS 的复制粘贴系统是许多非常有趣控件的门户。作为开发者，我们可以将自己的菜单项添加到复制粘贴菜单中，从而支持从高亮选中文本到在维基百科中查找关键字等各种功能。

我的基本建议是，只要可以，就始终使用 UIWebView。它们有时可能令人沮丧，但物超所值。只有在绝对需要额外功能时，才考虑改用 Core Text。

你可以在 Apple 的文档中找到关于这两种技术的更多信息。请参阅 iOS 的《Text, Web, and Editing Programming Guide》和《Core Text Programming Guide》。你还可以在 https://developer.mozilla.org/en/rich-text_editing_in_mozilla 找到一些 execCommand 文档（用于在 Web 视图中编辑富文本）。

就这样。运行应用程序。尝试添加几个重量条目。转到历史视图，然后从列表中选择几个条目。旋转历史视图和详情视图，确保它们在所有方向下都能正常工作。如果一切正常，提交你的更改。

这样就完成了我们三个视图中的两个。在下一章中，我们将研究为 GraphViewController 创建自定义视图。在第 6 章中，我们将学习如何保存应用程序数据和用户默认设置。

## 5 绘制自定义视图

在本章中，我们将构建一个简单的折线图，显示用户体重随时间的变化。重量轴和时间轴都将缩放以填满所有可用空间。我们还将绘制带标签的参考线，以帮助用户解读图表。

本章大部分内容侧重于在我们的 UIView 中执行自定义绘制。我们将同时研究 UIKit 的绘制方法和底层的 Core Graphics 框架。我们还将探讨 iOS SDK 如何管理普通显示屏和 Retina 显示屏之间的分辨率差异。

![](img/fe9fea534a8e7868f811f7cd33da015f_242_0.png)

让我们从创建 GraphStats 类开始。这个类将处理一个 weightEntries 数组，并计算集合的一些简单统计数据。这些数据包括：开始日期、结束日期、持续时间、最小重量、最大重量和重量跨度。GraphStats 还将提供一个基于块的方法，用于遍历集合中的所有 WeightEntry。

在 Views 组中创建一个新的 NSObject 子类。将其命名为 GraphStats。然后打开 GraphStats.h 并进行以下更改：

```objc
#import <Foundation/Foundation.h>

@class WeightEntry;

@interface GraphStats : NSObject

@property (strong, nonatomic, readonly) NSDate* startingDate;
@property (strong, nonatomic, readonly) NSDate* endingDate;
@property (assign, nonatomic, readonly) NSTimeInterval duration;
@property (assign, nonatomic, readonly) CGFloat minWeight;
@property (assign, nonatomic, readonly) CGFloat maxWeight;
@property (assign, nonatomic, readonly) CGFloat weightSpan;

- (id)initWithWeightEntryArray:(NSArray*)weightEntries;
- (void)processWeightEntryUsingBlock:(void (^)(WeightEntry*)) block;

@end
```

GraphStats 类充当 WeightEntry 对象数组的包装器。我们首先为 WeightEntry 类添加一个前向声明。然后添加六个只读属性。这些属性让我们能够访问计算出的值，比如数组的开始日期或最大重量值。接下来，我们声明指定的初始化方法。毫不奇怪，它接收一个 WeightEntry 对象数组。

我们将 GraphStats 创建为不可变类。在首次实例化对象时传入 WeightEntry 数组，并且权重在对象的生命周期内不能更改。如果你需要添加或删除一个重量，你必须创建一个全新的 GraphStats 对象。这大大简化了我们的代码。例如，我们可以在初始化步骤中批量计算所有属性值，之后永远不需要更改它们。
