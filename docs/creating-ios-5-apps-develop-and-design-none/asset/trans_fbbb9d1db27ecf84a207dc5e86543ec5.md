
## 手势识别器

手势识别器是在 iOS 3.2 中引入的。它们极大地简化了常见触摸命令的检测，如点击、轻扫、拖拽、捏合、旋转和长按。在许多方面，手势识别器使我们能够抽象出跟踪和分析单个触摸的繁琐细节，让我们在高层定义交互。假设我们想要检测一个双指三次点击。没问题。我们只需创建一个 `UITapGestureRecognizer` 实例，并设置所需的点击次数和触摸次数。就是这样。我们不需要担心监控单个触摸位置、检测到的触摸次数、每次触摸持续多久，甚至不同触摸组之间的持续时间。手势识别器为我们处理所有这些细节，并且以所有应用程序一致的方式处理。

**注意：** 虽然现有的 `UIGestureRecognizer` 子类覆盖了所有常见的多点触控手势，但我们可以创建自己的子类来识别自定义手势。有关更多信息，请查看 Apple 的 iOS 事件处理指南中的“创建自定义手势识别器”。

![](img/fe9fea534a8e7868f811f7cd33da015f_492_0.png)

手势识别器有两种基本类型：离散型和连续型。这决定了识别器发送的动作消息类型。离散手势识别器在手势完成后发送单个动作消息。它们用于标记单个时间点的快速手势：点击和轻扫。

另一方面，连续手势识别器会随时间跟踪手势。它们会持续发送多个动作消息，直到手势结束。捏合、平移、旋转和长按都使用连续手势识别器建模。

特别要注意轻扫和平移手势之间的区别。从表面上看，它们非常相似。两者都涉及在屏幕上拖动手指。然而，对于轻扫，我们只对触发单个动作感兴趣。一旦检测到轻扫，我们就调用动作并完成。这是一个离散的、单一的事件。对于平移，我们实际上想要跟踪用户手指的移动。手指的位置、移动了多远、移动了哪个方向——所有这些细节可能都很重要。因此，我们可能会使用轻扫手势来触发从一页移动到另一页，而使用平移手势来快进视频或更改应用的音量。

我们在 GravityScribbler 中使用了多种不同的手势。单指平移调整应用的加速度率（基本上是重力光标的响应速度）。双指点击暂停应用。最后，三指水平轻扫将弹出导出菜单。

**注意：** 我们没有将手势识别器附加到单个控件元素（例如暂停按钮），而是直接将它们附加到根视图。这意味着我们可以在屏幕上的任何位置执行手势。实际上，整个视图就是我们的控件，弹出视图只是我们可视化用户交互的方式。

![](img/fe9fea534a8e7868f811f7cd33da015f_493_0.png)

### 创建手势识别器

让我们从最简单的暂停手势开始。我们将首先在 GSRootViewController 的 viewDidLoad 方法中创建手势识别器。

```objective-c
// Add 2-finger tap to pause.
UITapGestureRecognizer* pauseGesture =
    [[UITapGestureRecognizer alloc]
        initWithTarget:self
        action:@selector(pauseGesture:)];
pauseGesture.numberOfTapsRequired = 1;
pauseGesture.numberOfTouchesRequired = 2;
[self.view addGestureRecognizer:pauseGesture];
```

在这里，我们实例化一个 `UITapGestureRecognizer` 对象，设置其目标和选择器。每次此手势识别器识别出点按手势时，它都会调用我们视图控制器的 `pauseGesture:` 方法。接下来，我们设置点按次数和触摸次数。在我们的例子中，我们必须同时用两根手指点按——但只需要单次点按（不是双击或三击）。最后，我们将手势识别器添加到根视图中。它现在就处于活动状态。接下来，我们定义 `pauseGesture:` 方法。

```objective-c
- (void)pauseGesture:(UIGestureRecognizer*)gestureRecognizer {
    if (self.canvasViewController.running) {
        [self showPopupController:self.pauseController
                animationType:GSPopupDropDown
        withCompletionHandler:nil];
    } else {
        [self hidePopupController:self.pauseController
                animationType:GSPopupDropDown];
    }
    self.canvasViewController.running =
    !self.canvasViewController.running;
}
```

`UITapGestureRecognizer` 是一个离散手势识别器。这意味着我们的 `pauseGesture:` 方法对于它检测到的每个点按手势只会被调用一次。如果我们的画布视图当前正在运行，我们显示暂停弹出视图；否则，我们隐藏它。然后我们切换画布视图的 `running` 属性。请注意，我们还接收一个 `UIGestureRecognizer` 参数。虽然我们在该方法中没有使用它，但我们可以利用它来监控手势识别器的状态或确定点按手势的位置。我们将在后面的手势识别器中看到相关示例。

接下来，让我们实现三指轻扫。与我们的点按手势一样，这是一个离散手势。一旦整个手势被识别，动作方法就会被调用。

```objective-c
// Add 3-finger swipe to export--we will add twice
// because we want to distinguish the different directions.
UISwipeGestureRecognizer* swipeToExportDown =
[[UISwipeGestureRecognizer alloc]
    initWithTarget:self
    action:@selector(exportGesture:)];
swipeToExportDown.numberOfTouchesRequired = 3;
swipeToExportDown.direction =
UISwipeGestureRecognizerDirectionDown;
[self.view addGestureRecognizer:swipeToExportDown];
UISwipeGestureRecognizer* swipeToExportUp =
[[UISwipeGestureRecognizer alloc]
    initWithTarget:self
    action:@selector(exportGesture:)];
swipeToExportUp.numberOfTouchesRequired = 3;
swipeToExportUp.direction = UISwipeGestureRecognizerDirectionUp;
[self.view addGestureRecognizer:swipeToExportUp];
```

这表面上看与我们的点按手势识别器类似。我们实例化一个 `UISwipeGestureRecognizer`，为其指定目标/动作对。接下来，我们将所需触摸次数设置为三，并设置所需的轻扫方向。最后，我们将轻扫手势添加到视图中。然而，有几个关键点值得一提。

首先，我们想要检测水平轻扫。请记住，我们保持视图锁定为纵向方向；但是，我们假设用户会以横向左侧或横向右侧的方式握住设备。这意味着水平轻扫实际上将使用 `UISwipeGestureRecognizerDirectionUp` 和 `UISwipeGestureRecognizerDirectionDown` 来检测。

其次，我们实际上创建了两个轻扫识别器——每个方向一个。我们本可以轻松地将两个方向组合成一个位掩码，并用它来检测任意的水平轻扫，但那样我们将无法确定用户向哪个方向轻扫。在动画序列中，我们希望视图的运动与轻扫方向相匹配。通过使用两个独立的手势识别器，我们可以轻松识别轻扫方向。

```objective-c
- (void)exportGesture:(UIGestureRecognizer*)gestureRecognizer {
    self.exportSwipeDirection =
    [(UISwipeGestureRecognizer*)gestureRecognizer direction];
    GSPopupAnimationType animation;
    switch (self.exportSwipeDirection) {
        case UISwipeGestureRecognizerDirectionDown:
            animation = GSPopupSlideTowardsHomeButton;
            break;
        case UISwipeGestureRecognizerDirectionUp:
            animation = GSPopupSlideFromHomeButton;
            break;
        default:
            [NSException
                raise:@"Invalid Swipe Direction"
                format:@"Should only recognize swipes up or "
                    @"down, however this swipe was %d",
                    self.exportSwipeDirection];
            break;
    }
    // Don't process export gestures if paused.
    if (!self.canvasViewController.running) return;
    // Pause the view.
    self.canvasViewController.running = NO;
    // Pass the image snapshot to the export controller.
    self.exportController.imageToExport =
        [self.canvasViewController snapshotOfCanvas];
    self.exportController.deviceOrientation =
        self.bestSubviewOrientation;
    // And show the export options.
    [self showPopupController:self.exportController
            animationType:animation
        withCompletionHandler:nil];
}
```

此方法首先访问手势识别器的 `direction` 属性。请注意，这不是轻扫的方向。它是一个位掩码，指示识别器允许的方向。但是，由于我们创建了两个识别器，每个都有自己的方向值，我们可以使用此属性来区分它们。

