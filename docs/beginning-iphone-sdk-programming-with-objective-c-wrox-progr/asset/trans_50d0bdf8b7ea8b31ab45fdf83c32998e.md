
**注意** 启动 Xcode 最简单的方法是在 Spotlight 中输入 *Xcode*，然后按 Enter 键启动它。

![](img/16991b58db5894715c4a443315e06a22_53_0.png)

图 2-1

要创建新的 iPhone 项目，请选择 File ▸ New Project。图 2-2 显示了使用 Xcode 可以创建的不同类型的项目。有两个主要类别：iPhone OS 应用程序和 Mac OS X 应用程序。本书显然主要讲解 iPhone 应用程序。因此，单击 iPhone OS 下列出的 Application 项目以查看用于开发 iPhone 应用程序的各种模板。

![](img/16991b58db5894715c4a443315e06a22_55_0.png)

图 2-3

Xcode 的左侧面板显示项目中的分组。你可以展开每个分组以显示每个分组（和文件夹）中包含的文件。Xcode 的右侧面板显示你在左侧面板中选择的分组（或文件夹）中包含的文件。要编辑特定文件，请选择该文件，然后右侧面板底部的编辑器会打开该文件以供编辑。如果你想要单独的编辑窗口，只需双击文件即可在新窗口中编辑它。

在下面的 Try It Out 中，你将学习如何自定义 Xcode 工具栏区域以添加常用项目。

## 试用 自定义 Xcode 工具栏区域

*代码文件 [HelloWorld.zip] 可从 Wrox.com 下载*

Xcode 的顶部是工具栏区域。该区域包含开发过程中常用的所有工具栏菜单项。你可以自定义工具栏区域以添加此类项目。

- 1. 通过选择 View ⌘ Customize Toolbar 来试试。会出现一个下拉窗口（见图 2-4）。

- 3. Active SDK 项目允许你选择将应用程序部署到真实设备还是 iPhone 模拟器（见图 2-6）。

![](img/16991b58db5894715c4a443315e06a22_57_0.png)

### 工作原理

通过将常用项目添加到 Xcode 工具栏区域，你可以提高开发过程的效率。在这种情况下，你已将 Active SDK 工具栏项目添加到工具栏区域，以便你只需在工具栏上选择活动 SDK，即可快速在 iPhone 模拟器和真实设备上测试应用程序之间切换。

## 使用 Interface Builder

到目前为止，该项目还没有 UI。为了证明这一点，只需按 Command-R（或选择 Run ↻ Run），你的应用程序就会部署到包含的 iPhone 模拟器中。图 2-7 显示了 iPhone 模拟器上显示的空白屏幕。现在看到这一点很好，因为在你阅读本章的过程中，你会看到基于你的操作发生了哪些变化。

显然，空白屏幕并不是很有用。所以，是时候尝试向应用程序的 UI 添加一些控件了。如果你检查项目中的文件列表，你会注意到有两个以 .xib 为扩展名的文件——MainWindow.xib 和 HelloWorldViewController.xib。以 .xib 为扩展名的文件基本上是包含应用程序 UI 定义的 XML 文件。你可以通过修改其 XML 内容来编辑 .xib 文件，或者更简单（更理智）地使用 Interface Builder 编辑它们。

Interface Builder 是 iPhone SDK 的一部分，允许你使用拖放来构建 iPhone（和 Mac）应用程序的 UI。

双击 HelloWorldViewController.xib 文件以启动 Interface Builder。图 2-8 显示了 Interface Builder 显示 HelloWorldViewController.xib 的内容（目前实际上是空的）。正如你所见，Library 窗口显示了你可以添加到 iPhone 应用程序 UI 的各种控件。View 窗口显示了你的 UI 的图形布局。你很快就会看到其他窗口的使用。

![](img/16991b58db5894715c4a443315e06a22_57_1.png)

图 2-8

现在，滚动到 Library 面板中的 Label 控件并将 Label 视图拖放到 View 窗口上。添加 Label 视图后，选择 Label 视图并选择 Tools ▸ Attributes Inspector。在 Text 字段中输入 Hello World！此外，在 Layout 旁边，单击居中对齐类型（见图 2-9）。

![](img/16991b58db5894715c4a443315e06a22_58_0.png)

图 2-9

![](img/16991b58db5894715c4a443315e06a22_58_1.png)

## 视图重新定位

在上一节中，你看到随着方向的变化，视图的大小和位置保持不变。在现实世界中，这种情况是不理想的，因为它在使用应用程序时不会给用户带来良好的体验。理想情况下，你应该在屏幕上重新定位视图，使其随视图方向而变化。

要重新定位视图，请转到 Interface Builder，选择 Label 视图，然后选择 Tools ⇧ Size Inspector。修改视图的 autosizing 属性，如图 2-16 所示（仔细观察 Autosizing 部分中设置的各种锚点）。这将导致 Label 视图在视图方向变化时展开/收缩。同时，视图将锚定到屏幕的左侧、顶部和右侧。

![](img/16991b58db5894715c4a443315e06a22_62_0.png)

图 2-16

同样，修改 Text Field 视图的 Autosizing 属性，如图 2-17 所示。注意不同的像素大小。

在 HelloWorldViewController.h 文件中，为 btnClicked: 操作添加头声明：

```
//
// HelloWorldViewController.h
// HelloWorld
//
// Created by Wei-Meng Lee on 3/30/09.
// Copyright __MyCompanyName__ 2009. All rights reserved.
//

#import <UIKit/UIKit.h>

@interface HelloWorldViewController : UIViewController {
}

//---declaration for the btnClicked: action---
-(IBAction) btnClicked:(id)sender;

@end
```

在 HelloWorldViewController.m 文件中，添加提供 btnClicked: 操作实现的：

```
-(void)dealloc {
    [super dealloc];
}

//---implementation for the btnClicked: action---
-(IBAction) btnClicked:(id)sender {
    //---display an alert view---
    UIAlertView *alert = [[UIAlertView alloc]
        initWithTitle:@"Hello World!"
        message:@"iPhone, here I come!"
        delegate:self
        cancelButtonTitle:@"OK"
        otherButtonTitles:nil, nil];

    [alert show];
    [alert release];
}

@end
```

前面的代码显示一个包含句子 "iPhone, here I come!" 的警告框！

就这样！返回 Xcode 并再次运行应用程序。这次，当你点击按钮视图时，会显示一个警告视图（见图 2-23）。

![](img/16991b58db5894715c4a443315e06a22_66_0.png)

- 2. 要向应用程序添加图标，请将图像拖放到项目的 Resources 文件夹中（见图 2-25）。系统会询问你是否要复制正在拖放的图像。选中此选项，以便图像的副本现在存储在你的项目文件夹中。

![](img/16991b58db5894715c4a443315e06a22_68_0.png)

图 2-25

- 3. 选择 Info.plist 项目（也位于 Resources 文件夹下）。选择 Icon file 项目并将其值设置为图标的名称（app-icon.png；见图 2-26）。这指定了用作应用程序图标的图像的名称。

## 练习

- 1. 你在 Xcode 中尝试向 iPhone 项目添加图标。你应该提供什么尺寸的图像？
- 2. 如果你的应用程序需要支持不同的显示方向，你应该怎么做？

## 本章学到的内容

| 主题 | 关键概念 |
|---|---|
| Xcode | 创建你的 iPhone 应用程序项目并编写操作应用程序的代码。 |
| Interface Builder | 使用 Library 中位于的各种视图构建你的 iPhone UI。 |
| 视图重新定位 | 使用 Interface Builder 中的 Autosizing 功能确保视图即使在方向更改时也能调整大小。 |
| 添加应用程序图标 | 将图像添加到项目中，然后在 `info.plist` 文件的 Icon file 属性中指定图像名称。 |
| 为你的 iPhone 应用程序创建图标 | 图标大小为 57 x 57 像素（主屏幕）和 29 x 29 像素（设置）。对于 AppStore 托管，大小为 512 x 512 像素。 |
