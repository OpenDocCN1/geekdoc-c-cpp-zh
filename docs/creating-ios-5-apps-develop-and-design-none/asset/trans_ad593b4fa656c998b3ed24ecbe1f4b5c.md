

![](img/fe9fea534a8e7868f811f7cd33da015f_488_0.png)

**图 8.11** 可调整大小图像的实际运行效果

平铺图像和可调整大小图像都能让我们创建视觉上有趣的背景，同时最大限度地减少最终应用程序的内存需求和体积。当然，您必须精心设计图像，以便它们能够很好地作为平铺或拉伸图像使用。你不能简单地拉伸任意图像并期望它看起来不错。

**注意：** 在本例中，我们可调整大小图像的内部填充的是纯色，因为我们是在平铺单个像素（在 Retina 显示屏的情况下，则是两个颜色相同的像素）。然而，通过增大内嵌区域之间区域的大小，我们可以创建图案，然后通过平铺来填充图像覆盖的整个区域。确保平铺区域与内嵌设计良好匹配需要额外的精力，但如果处理得当，就可以生成基于镶嵌图案的可调整大小图像。

![](img/fe9fea534a8e7868f811f7cd33da015f_488_1.png)

## 响应用户输入

自定义外观固然很好，但如果我们无法响应用户输入，那也算不上什么控件。同样，UIKit 的控件涵盖了大多数常见的交互，但有时我们需要以内置控件无法实现的方式来响应轻点、轻扫、捏合、倾斜或摇动。

请注意，当我说“控件”时，并不一定指字面上的 UIControl 子类。而是指任何响应用户输入的对象。其中许多是 UIView 的简单子类，或者在更复杂的情况下，是 UIView 和委托（delegate）对。

这常常成为许多新 iOS 开发者的真正绊脚石。当我们开始考虑创建自定义控件时，通常认为必须将我们的想法硬塞进更常见的 UIKit 控件所使用的 target/action 模式中。不幸的是，当我们尝试自行子类化 UIControl 时，很快就会发现文档中缺乏指导。很容易感到不知所措和沮丧。幸运的是，这也并不是必需的。

残酷的事实是，UIControlEvents 的范围狭窄，严重限制了 target/action 模式的实用性。当 UIControl 子类与这些事件紧密匹配时，它们工作得很好——这基本上将我们限制在监视触摸和拖拽上。一些更通用的事件（例如值已更改和编辑事件）可用于模拟更广泛的交互，但它们在控件与其视图控制器之间提供的接口相对较弱。对于更复杂的控件，我们通常需要创建一个委托。这个委托可能与 UIControlEvents 协同工作（例如 UITextField），也可能独立存在（例如 UITextView）。

归根结底，我们不应该觉得必须使用 UIControl。即使在 UIKit 本身中，大多数更复杂的控件也不会费心去子类化 UIControl。相反，像 UITextView、UITableView 和 UIPickerView 这样的类更倾向于使用委托和数据源，而不是 target/action 对。这使它们能够在控件与其视图控制器之间定义更丰富的接口。

因此，我们不会在子类化 UIControl 这个相对狭窄的主题上花太多时间。相反，我们将专注于响应用户输入这个更广泛的任务。特别是，我们将研究使用手势识别器（gesture recognizers）来轻松检测各种多点触控命令。我们还将研究使用 Core Motion 框架来监控设备方向的变化——在我们的示例中，让用户通过倾斜手机来控制光标。

### 子类化 UIControl

在我看来，在考虑子类化 UIControl 时，我们必须回答两个关键问题。首先，我们是否计划在当前项目或其他项目中重用这个控件？如果这仅仅是一次性的自定义控件，那么可能不值得费这个力气。只需为你的控件创建一个可靠的委托协议并使用它即可。

其次，我们是否希望在 Interface Builder 中将控件的事件连接到操作？同样，如果答案是否定的，那么真的没有理由考虑 UIControl。委托在实现和使用上仍然会更简单。

然而，如果我们已经仔细考虑了设计，并且对这两个问题都回答了“是”，那么我们该如何构建 UIControl 子类呢？所有控件都有两个部分。第一部分是它们的外观。就像任何自定义视图一样，我们必须提供自定义绘制代码。但与静态图像不同，我们可能希望控件在视觉上响应用户输入。我们在本章前面使用的 Core Animation 技术通常是实现这一点的关键。此外，就像任何自定义视图一样，我们的控件不需要绘制为单个视图。我们可以将视图分解为多层的视图层次结构。这在处理图像时尤其有用。UIImageView 类是高度优化的，我们通常应该尝试将其添加到视图层次结构中，而不是使用 UIKit 自己绘制图像。

第二部分是实际的用户交互。UIControl 已经响应了许多基于触摸的命令，并且会自动为触摸事件（任何以 UIControlEventTouch... 开头的事件）触发分配的操作。

我们可以通过两种方式修改这种行为。首先，我们可以重写 sendAction:to:forEvent: 来监视和改变事件的调度方式。注意，sendAction:to:forEvent: 只有在给定事件分配了目标和操作时才会被调用。因此，我们必须先分配一个默认的 target/action 对。然后，我们可以使用这个方法来根据控件的状态取消或更改目标或操作。接下来，我们可以通过重写 beginTrackingWithTouch:withEvent:、continueTrackingWithTouch:withEvent: 和 endTrackingWithTouch:withEvent: 来跟踪触摸事件，尽管——正如我们很快就会看到的——使用手势识别器管理复杂的触摸事件通常要容易得多。事实上，我们完全可以把手势识别器直接添加到我们的 UIControl 子类中。

最后，我们可以调用 `sendActionsForControlEvents:` 以编程方式触发我们自己的事件。通常，我们会用它来触发 `UIControlEventValueChanged` 或某个 `UIControlEventEditing...` 事件。只需调用 `sendActionsForControlEvents:` 并传入一个位掩码，其中为每个我们希望触发的事件都设置了一个标志。然后，我们的 UIControl 子类将会为这些事件分配的每个 target/action 对自动调用一次 `sendAction:to:forEvent:`。

举个简单的例子，假设我们想创建一个 2D 滑块。我们基本上需要一个简单的网格，以及一个可以在水平和垂直方向上移动的光标。我们的设计可能如下所示：

首先，我们将视图分解为两层：网格层和光标层。这使我们能够在不影响底层网格的情况下移动光标。

其次，我们添加三个状态变量。一个包含光标的相对 x 坐标（左边缘为 0.0，右边缘为 1.0）。另一个包含相对 y 坐标（同样，顶部为 0.0，底部为 1.0）。最后，第三个变量包含一个 BOOL，用于监控我们的编辑状态（如果我们正在修改控件的值，则为 YES，否则为 NO）。

接下来，这里我们并没有做非常复杂的事情，所以现有的触摸方法可能就足够了。只需重写 `beginTrackingWithTouch:withEvent:`、`continueTrackingWithTouch:withEvent:` 和 `endTrackingWithTouch:withEvent:`。

在 `beginTracking...` 中，我们检查触摸是否离光标足够近。如果是，我们就开始编辑控件。这至少涉及设置 `self.editing = YES` 并调用 `[self sendActionsForControlEvents:UIControlEventEditingDidBegin]` 来触发“编辑开始”事件。我们可能还想改变光标的样式（例如，通过高亮显示它）。

在 `continueTracking...` 中，如果 `self.editing == YES`，我们会根据触摸在视图中的位置更新 x 和 y 坐标。然后更新光标的位置。最后，我们调用 `[self sendActionsForControlEvents:UIControlEventEditingChanged | UIControlEventValueChanged]` 来同时触发“编辑已更改”和“值已更改”事件的操作。

然后，在 `endTracking...` 中，如果 `self.editing == YES`，我们设置 `self.editing = NO` 并调用 `[self sendActionsForControlEvents:UIControlEventEditingDidEnd]`。

就是这样。我们也许可以进一步优化和改进它，但这些就是我们的控件真正需要的全部内容。下次我们在 Interface Builder 中时，可以从库中拖出一个 UIView，将其放置到任何我们想要的位置，并将其类更改为我们自定义的 UIControl 子类。然后，我们就能够像使用 UIKit 的任何控件一样，连接它的事件。

