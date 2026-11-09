

![](img/2b293e29fc15b0797f113b85dd429b6e_460_0.png)

## 创建动画和 3D 图形

动画常与游戏联系在一起，但 Cocoa 让用户界面中几乎任何元素都能轻松实现动画。对象可以平滑移动、随颜色或亮度脉动、轻微晃动，或在单击或鼠标悬停时改变大小。Aqua 包含标准动画效果，例如滑出式面板和脉动按钮。其中一部分是自动的。当你创建文件打开/存储面板时，动画已嵌入该类中，无需更多代码即可运行。

你可以添加更多动画来改善应用程序的外观和感觉，使其更专业，并通过巧妙地突出重要功能来增加价值。

在用一个对象替换另一个对象时，也可以创建动画过渡。这种视图交换是 iPhone 应用设计中的一项关键技能，在 iPhone 应用中，交换后的视图会替代桌面应用程序的窗口、面板和窗格。

![](img/2b293e29fc15b0797f113b85dd429b6e_460_1.png)

> **交叉引用**
> 关于视图交换的实际示例，请参见第 19 章。

要有效地使用动画，你必须熟悉 Cocoa 不同的动画类和功能。许多应用程序未能充分利用动画，或以缺乏想象力的方式添加动画。一个关键的设计目标是利用动画创造真正的用户收益。成功的动画不应只是看起来令人印象深刻；它还应该向用户提供视觉提示，帮助用户理解应用程序，并以更直观的方式使用它。

例如，在 iPhone 上，视图通过手指动作进行交换，并伴随相匹配的动画。动画暗示一种隐喻，例如翻页、弹出、滑动或旋转，从而暗示应用的组成结构。如果一个应用以滑动方式进入某个视图，却以翻页方式返回，就会让人觉得不一致。

Cocoa 包含一系列支持动画的类和技术。概括来说，有三种选择：直接访问属性；Core Animation（Cocoa 的主要动画框架）；以及 OpenGL（一种支持 3D 场景渲染的复杂低级语言）。

### 17 本章内容

- 创建直接属性动画
- 使用动画器
- 创建自定义动画对象
- 在 Cocoa 中创建简单的 OpenGL 动画

### 为动画创建定时器

动画定时器就是一个运行专用动画方法的定时器。Cocoa 中没有特殊的动画定时器。要创建定时器，请使用标准的 `NSTimer` 对象。目标通常是 `self`，但也可以是另一个对象。

```objective-c
NSTimer *theTimer = [NSTimer scheduledTimerWithTimeInterval:0.05
                     target: anObject
                     selector: @selector(theAnimationMethod:)
                     userInfo: anOptionalObject
                     repeats: YES];
```

在目标对象中实现动画定时器方法：

```objective-c
- (void) theAnimationMethod: (NSTimer *) theTimer {
    //Do something to a property here
}
```

图 17.1 展示了一个简单示例。该视图包含一个按钮。代码让按钮围绕视图中心做小半径循环移动，并动态修改其大小。按钮始终处于活动状态：如果你能抓住它，就可以点击它。它可以按常规方式连接到某个选择器动作。

**图 17.1**

飞行按钮，这是一种不寻常的 UI 设计，你不太可能在成品应用中看到

![](img/2b293e29fc15b0797f113b85dd429b6e_462_0.png)

### 创建属性动画代码

使用直接属性动画时，你可以完全自由地决定如何实现动画功能。此示例的关键代码段如下：

```objc
@synthesize window, theButton;
float bOffX, bOffY, currX, currY, centerX, centerY, timeCount,
      radius, theta;
CGPoint currPoint;
- (void)applicationDidFinishLaunching:
(NSNotification *)aNotification {
    NSTimer *aTimer =
    [NSTimer scheduledTimerWithTimeInterval:0.017
        target: self selector: @selector(timerMethod)
        userInfo: nil repeats: YES];
}
- (void)timerMethod
{
    timeCount += 0.05;
    theta = timeCount/6.283;
    bOffX = NSMidX(theButton.bounds);
    bOffY = NSMidY(theButton.bounds);
    centerX = window.frame.size.width/2;
    centerY = window.frame.size.height/2;
    radius = centerY*0.6;
    currX = centerX+radius*cos(theta)-bOffX;
    currY = centerY+radius*sin(theta)-bOffY;
    currPoint = NSMakePoint(currX, currY);
    [theButton setFrameOrigin:currPoint];
    [theButton setFrameSize:
    NSMakeSize(50+25*cos(2*theta), 50+25*cos(3*theta))];
}
```

定时器方法更新位置计数器，计算视图中心，然后使用简单的三角函数为按钮创建圆形路径。通过用 `setFrameOrigin:` 更新按钮的 frame 原点来重新定位按钮；并通过用 `setFrameSize:` 更新 frame 大小来调整按钮尺寸。一个偏移项用于校正按钮 frame 的左下角原点，并将绘制点移到按钮中心。

对于简单效果来说，这段代码的复杂度中等。它也非常依赖系统负载。如果你的 Mac 很忙，按钮就会卡顿。这种方法也很难管理多个同时进行的动画。当你需要为少量相关属性制作动画时，这是一个不错的解决方案；但如果同时有多个独立动画在运行，就很难处理。你可以为每个动画创建一个单独的定时器，但这种方法很快就会变得笨拙。

![](img/2b293e29fc15b0797f113b85dd429b6e_463_0.png)

> **提示**
> 为位置和大小制作动画时，请设置对象的 frame 属性，而不是其 bounds。这同样适用于旋转。完整的旋转解决方案需要一个后备层，本章后文将对此进行介绍。

### 使用 drawRect:

你可以使用类似技术，利用上一章介绍的路径和绘图对象来创建自定义的动画 2D 图形。使用定时器方法为每次更新初始化相关的路径和对象值，并在定时器方法末尾调用

```objc
[theView setNeedsDisplay];
```

![](img/2b293e29fc15b0797f113b85dd429b6e_464_0.png)

> **注意**
> 如果视图正在刷新自身，请将 `theView` 替换为 `self`。

这会间接调用视图的 drawRect: 方法并刷新视图。drawRect: 代码可以读取更新后的值，为每次定时器更新创建刷新后的视图。你可以使用此技术创建复杂效果。对于简单游戏来说它足够快，但当绘图代码密集并以典型的游戏刷新率更新时，可能会卡顿。

对于更复杂的效果，可以使用 Cocoa 的其他动画选项之一来获得更平滑的结果。

### 使用动画器

通过添加代理，你可以创建非常简单的动画效果——代理是一种简单的即插即用动画控制器，它会自动添加动画对象，用有用的默认值初始化它，并运行动画。Core Animation 的代理选项让你只需很少的代码就能获得强大的动画能力。你可以用额外的代码自定义动画，但最小实现几乎不需要添加任何代码。

例如，要为按钮的位置更新制作动画，请将

```objc
[theButton setFrameOrigin: newPosition];
```

替换为

```objc
[[theButton animator] setFrameOrigin: newPosition];
```

动画器会创建从当前位置到新位置的平滑变化，默认持续时间为 0.25 秒。

### 创建简单的代理动画

图 17.2 展示了一个非常简单的应用程序的 nib 文件，该程序演示代理动画，并使用一个按钮作为方便的可动画对象。

**图 17.2**

一个简单动画器演示应用程序的 nib 文件，其中包含一个带按钮的子类视图

![](img/2b293e29fc15b0797f113b85dd429b6e_465_0.png)

TheView 是 NSView 的子类，并包含如下所示的代码。当用户点击鼠标时，mouseDown: 处理程序会读取位置并将按钮移动到点击位置。不使用动画器时，按钮的位置会立即改变。使用动画器时，按钮会在旧位置和新位置之间平滑滑动。

代码很直接。与前一个示例一样，一个偏移项用于校正按钮 frame 的左下角原点；除此之外，代码读取鼠标点击的窗口坐标，校正偏移，并使用动画器设置按钮的位置。

```objc
#import "TheView.h"
#import <QuartzCore/QuartzCore.h>

@implementation TheView
@synthesize theButton;
NSPoint oldPosition;
float bOffX, bOffY;
```

