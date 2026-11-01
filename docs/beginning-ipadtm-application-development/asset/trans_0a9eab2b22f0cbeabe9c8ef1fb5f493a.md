
接下来，从 Library 窗口将一个 Text Field 视图拖放到 View 窗口中，然后再拖放一个 Round Rect Button 视图。通过在 Title 字段中输入 Click Me! 来修改 Round Rect Button 视图的属性（见图 2-9）。

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_64_0.png)

图 2-9

> 注 而不是指定视图的 Text 或 Title 属性来使文本在视图中显示（例如 Label 和 Round Rect Button 视图），你可以直接双击视图本身并直接输入文本。完成此操作后，你可以重新排列视图并按需调整其大小。Interface Builder 会提供对齐指南，帮助你以视觉上美观的布局排列控件。

通过按 Command-S 保存 HelloWorldViewController.xib 文件。然后返回 Xcode，通过按 Command-R 再次运行应用程序。iPhone Simulator 现在显示修改后的 UI（见图 2-10）。

> 注 请务必在 Xcode 中运行应用程序之前保存 Interface Builder 中的所有更改。

点击 Text Field 视图，观看键盘自动出现（见图 2-11）。按下 iPhone Simulator 上的 Home 按钮，你会看到应用程序已安装在模拟器上。要返回应用程序，只需点击 HelloWorld 图标即可（见图 2-12）。

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_65_0.png)

图 2-10

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_65_1.png)

图 2-11

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_67_0.png)

图 2-13

请注意，该方法返回 YES，表示所有方向模式均受支持，并且当方向模式更改时你的应用程序会自动翻转。

第 6 章更详细地讨论了屏幕旋转。

> **注** iPad 应用程序支持所有横向和纵向显示模式非常重要。因此，建议你在 `shouldAutorotateToInterfaceOrientation:` 方法中返回 YES。以上代码片段仅供参考。

## 视图重新定位

在上一节中，你看到随着方向的改变，视图的大小和位置保持不变。在现实世界中，这种情况是不理想的，因为它在使用应用程序时无法为用户提供良好的体验。理想情况下，你应该在屏幕上重新定位视图，使其随视图方向而变化。

要调整视图大小，请进入 Interface Builder，选择 Label 视图，然后选择 Tools ▸ Size Inspector。通过点击两个正方形内部的各种线条来修改视图的 Autosizing 属性，如图 2-15 所示（请仔细观察 Autosizing 部分中设置的各种锚点）。这将导致 Label 视图在视图方向改变时展开/收缩。同时，视图将锚定到屏幕顶部。

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_69_0.png)

图 2-15

同样，通过点击两个正方形内部的各种线条来修改 Text Field 视图的 Autosizing 属性，如图 2-16 所示。

最后，通过点击两个正方形内的线条来修改 Round Rect Button 控件的 Autosizing 属性，如图 2-17 所示。这次，你不是在视图方向改变时调整视图大小。而是仅将其锚定到屏幕顶部。

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_70_0.png)

图 2-16

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_70_1.png)

图 2-17

就这样！在 Interface Builder 中，点击屏幕右上角的箭头（见图 2-18），以旋转屏幕，从而立即查看所做的更改效果。

返回 Xcode 并再次运行应用程序。这次，注意控件在你旋转屏幕时自行重新定位和调整大小。图 2-19 显示了纵向模式下显示的视图。

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_72_0.png)

图 2-19

该粗体语句创建了一个动作（通常称为事件处理程序），名为 btnClicked:。在声明了该动作后，保存文件并返回 Interface Builder。

本章前面你看到一个名为 HelloWorldViewController.xib 的窗口。在此窗口中有三个组件：File's Owner、First Responder 和 View。在 View 窗口中 Control-click Round Rect Button 视图并将其拖到 HelloWorldViewController.xib 窗口中的 File's Owner 项（见图 2-20）。会出现一个包含 btnClicked: 动作的小弹出窗口。选择 btnClicked: 动作。基本上，你在这里做的是将 Round Rect Button 视图与动作（btnClicked:）链接起来，以便用户点击按钮时调用该动作。

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_73_0.png)

图 2-20

在 HelloWorldViewController.m 文件中，添加提供 btnClicked: 动作实现的<|message|>：

```objc
#import "HelloWorldViewController.h"

@implementation HelloWorldViewController

- (IBAction) btnClicked:(id) sender {
    //---display an alert view---
    UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Hello World!"
                                                     message:@"iPad, here I come!"
                                                    delegate:self
                                           cancelButtonTitle:@"OK"
                                           otherButtonTitles:nil];
    [alert show];
    [alert release];
}
```

前述代码显示一个包含句子 “iPad, here I come!” 的警告框。

就这样！返回 Xcode 并再次运行应用程序。这次，当你点击 Button 视图时，会显示一个警告视图（见图 2-21）。

## 自定义应用程序图标

如你之前所见，安装在你的 iPhone Simulator 上的应用程序使用默认的白色图像作为图标。然而，你可以自定义此图标。在为你的 iPad 应用程序设计图标时，请注意以下几点：

- 将你的图标设计为 72 × 72 像素。更大尺寸也可以，因为 iPad 会自动为你调整大小。为了通过 App Store 分发，你需要准备一张 512 × 512 像素的图像。
- 为你的图标图像使用方形角落，因为 iPad 会自动将其圆角并添加光泽表面（你也可以关闭此功能）。

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_74_0.png)

图 2-21

## 摘要

本章是开发你的第一个 iPad 应用程序的惊险之旅。虽然你可能仍有很多疑问，但本章的目的是让你入门。接下来的几章将更深入地探讨 iPad 编程的细节，所有那些神秘的项目协同工作的秘密将逐渐揭示。

## 练习

- 1. 你想在 Xcode 中为你的 iPad 项目添加一个图标。你应该提供什么尺寸的图像？
- 2. 如果你的应用程序想要支持特定的显示方向，你应该怎么做？
- 3. 在 Xcode 项目中将图像添加到 Resources 文件夹时，为什么需要选中“Copy items into destination group's folder (If needed)”选项？

练习的答案可在附录 A 中找到。

## 本章学到的内容

| 主题 | 关键概念 |
|---|---|
| Xcode | 创建你的 iPad 应用程序项目并编写操作应用程序的代码。 |
| Interface Builder | 使用 Library 中位于的各种视图构建你的 iPad UI。 |
| 重新定位视图 | 使用 Interface Builder 中的 Autosizing 功能，确保在方向改变时视图会调整大小。 |
| 添加应用程序图标 | 将图像添加到项目中，然后在 info.plist 文件的 Icon file 属性中指定图像名称。 |
| 为你的 iPad 应用程序创建图标 | 图标尺寸为 72 x 72 像素（主屏幕）和 48 x 48 像素（设置）。对于 AppStore 托管，尺寸为 512 x 512 像素。 |

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_79_0.png)
