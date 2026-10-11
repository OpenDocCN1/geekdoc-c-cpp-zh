
```objectivec
int operation;
```

5. 通过向弹出按钮发送 `selectedTag` 消息来确定用户选择了哪一项。

执行此操作时，弹出按钮会返回其当前选中项的标签，将其存储在 `operation` 变量中。弹出按钮中的第一个菜单项的标签为 0（零），因此 `operationPopup` 控件中的所有项目都由索引 0 到 3 覆盖：

```objectivec
operation = [operationPopup selectedTag];
```

6. 在知道用户从 `operationPopup` 中选择了哪一项后，根据该索引执行相应的数学运算：

```objectivec
switch (operation) {
    case 0://加法
        answer = num1 + num2;
        break;
    case 1://减法
        answer = num1 - num2;
        break;
    case 2://乘法
        answer = num1 * num2;
        break;
    case 3://除法
        answer = num1 / num2;
        break;
}
```

完整的 `calculateAnswer` 动作代码如下。

```objectivec
- (IBAction)calculateAnswer:(id)sender {
    float num1,num2,answer;
    int operation;
    num1 = [numberField1 floatValue];
    num2 = [numberField2 floatValue];
    operation = [operationPopup selectedTag];
    switch (operation) {
        case 0://加法
            answer = num1 + num2;
            break;
        case 1://减法
            answer = num1 - num2;
            break;
        case 2://乘法
            answer = num1 * num2;
            break;
        case 3://除法
            answer = num1 / num2;
            break;
    }

    NSNumberFormatter *answerFormatter = [
        [[NSNumberFormatter alloc] init]
        autorelease];

    [answerFormatter setFormat:@"#,##.00;##.00; (#,##.00)"];
    [answerField cell setFormatter:answerFormatter];
    [answerField setFloat:answer];
}
```

7. 为了计算出现在菜单栏中的菜单，向 Fusebox 添加一个新动作：`changeOperation`。

当用户选择特定的菜单项时，代码会将 `operationPopup` 控件更改为与该菜单项中的运算相匹配。例如，如果用户选择“Add”（加法）菜单项，代码会将 `operationPopup` 控件的索引设置为 0（零）。“Subtract”（减法）菜单项会将 `operationPopup` 控件的索引设置为 1，以此类推。代码如下所示：

```objectivec
(IBAction)changeOperation:(id)sender {
    [operationPopup selectItemAtIndex:[sender tag]];
}
```

完整的 `Fusebox.m` 源文件将 `calculateAnswer` 动作和新的菜单项动作合并到一个文件中。为了保持条理清晰，以下是完整的 `Fusebox.m` 文件：

```objectivec
#import "Fusebox.h"

@implementation Fusebox
-(IBAction)calculateAnswer:(id)sender {
    float num1,num2,answer;
    int operation;
    num1 = [numberField1 floatValue];
    num2 = [numberField2 floatValue];

    operation = [operationPopup selectedTag];
    switch (operation) {
        case 0://加法
            answer = num1 + num2;
            break;
        case 1://减法
            answer = num1 - num2;
            break;
        case 2://乘法
            answer = num1 * num2;
            break;
        case 3://除法
            answer = num1 / num2;
            break;
    }

    NSNumberFormatter *answerFormatter = [
        [[NSNumberFormatter alloc] init]
        autorelease];

    [answerFormatter setFormat:@"#,##.00;##.00; (#,##.00)"];
    [answerField setFormatter:answerFormatter];
    [answerField setFloat:answer];
}

-(IBAction)changeOperation:(id)sender {
    [operationPopup selectItemAtIndex:[sender tag]];
}
@end
```

8. 选择“文件：保存” (`File: Save`) 以保存 `Fusebox.m` 文件。

9. 选择“构建：构建并运行” (`Build: Build and Go`) 以查看您的工作成果。

其结果是一个执行加法、减法、乘法和除法的应用程序。您可以通过从界面的弹出按钮中选择、从菜单栏的“Calculate”（计算）菜单中选择，或使用“Calculate”菜单中列出的键盘快捷键来选择数学运算。图 4-22 显示了完成的计算器应用程序。

![](img/ea40cad434a338535474e82c1a6ace20_106_0.png)

如果在界面构建过程或代码添加过程中迷失了方向，您可以从 `www.dummies.com/go/cocoafd` 获取完整的项目。完成的项目位于以下目录中：

```text
Chapter 4/End Code/Calculator
```

### 第 5 章

#### 为应用添加润色细节

**本章内容**

- 实现“关于”页面
- 重命名应用程序
- 设置应用程序版本
- 创建和设置应用程序图标
- 分发应用程序

在完成界面构建、代码编写和应用调试后，您将需要对其进行准备并构建为可独立执行的文件以便分发。您可能会认为，在设计和编写应用程序后，它已准备好向世界展示，但在通过 Mac 用户的考验（他们可能要求很高！）并真正准备好公开发布之前，您仍需完成几个步骤。

Mac 用户期望“良好”的 Mac 应用程序具备某些特定元素。在本章中，我将向您展示您可以添加到应用程序的一些最常见功能，以及在将其发布给朋友、家人、同事或公众之前需要调整的设置。

您的大部分开发任务都在 Xcode 和 Interface Builder 中进行。本章中的一些项目可以在 Xcode 和 Interface Builder 中完成。然而，这些并不是苹果为创建 Cocoa 应用程序提供的所有工具。在您的开发者文件夹的“应用程序” (`Applications`) 文件夹中，您可以找到十多种额外的工具和实用程序，它们有助于您创建出色的 Cocoa 软件。本章将展示如何使用其中两个：Icon Composer 用于创建图标，icns Browser 用于管理项目中的图标。随所有 Mac 附带的磁盘工具（Disk Utility）也将在本章中亮相。

#### 添加“关于”面板

每个应用程序菜单中都有一个标题为“关于 My Application”（About My Application）的菜单项，其中 My Application 是您的应用程序的名称。这通常被称为“关于”菜单，点击它会打开“关于”面板。“关于”面板传达关于应用程序的重要信息（想象一下！）。多年来，开发人员自己创建“关于”面板（有时称为“关于”框或“关于”窗口），但苹果已将其使用标准化。根据苹果的指导原则，“关于”面板可以显示应用程序的以下信息：

- **名称或标题**：应用程序的名称
- **图标**：应用程序的图标
- **版本号**：一个数字，如 1.0，表示这是哪个版本
- **版权日期**：声明应用程序受版权保护的年份的版权声明
- **鸣谢**：关于应用程序的其他相关信息，通常包括构建该应用的团队姓名和其他致谢

应用程序默认在“关于”面板中并不包含所有这些元素。您必须将它们添加到“关于”面板中，或者修改项目设置以使其出现在“关于”面板中。图 5-1 显示了默认的“关于”面板，其中包含应用程序名称和版本号，当您创建一个 Cocoa 应用程序时（在本例中，应用程序名为 Utility）。

![](img/ea40cad434a338535474e82c1a6ace20_109_0.png)

在修改了适当的设置并向项目中添加了一些项目后，生成的“关于”面板看起来更有趣，对用户也更有用。图 5-2 显示了一个包含“关于”面板基本元素的“关于”面板。

### 第一部分：开发人员工具

这么大的项目肯定需要编写一些代码，对吧？并非如此！只需设置几个参数并添加必要的文件，Cocoa 就会帮你处理剩下的工作！

图 5-2：增强后的“关于”面板外观更加美观，且对用户更有帮助。

![](img/ea40cad434a338535474e82c1a6ace20_110_0.png)

自定义“关于”面板所需的大部分设置都在项目的 `Info.plist` 文件中。该文件位于项目的资源（Resource）文件夹内。图 5-3 展示了其在项目窗口中的位置。

`Info.plist` 文件略有特殊。从本质上讲，它只是一个文本文件，但它包含 XML（可扩展标记语言），可以被专用应用程序解析，例如属性列表编辑器（Property List Editor）。该工具位于开发工具文件夹（Developer folder）内的应用程序文件夹（Applications folder）中（属性列表编辑器位于其中的实用工具文件夹（Utilities folder）内）。

图 5-3：`plist` 文件包含应用程序的重要设置。

![](img/ea40cad434a338535474e82c1a6ace20_110_1.png)

不过，你不必大费周章，因为 Xcode 也能解析 `Info.plist` 中的数据。Xcode 不会将文件显示为普通的纯文本，而是解析数据并将其显示为层次树（即 XML 的结构形式）。层次中的每个元素由一个键值对组成。你可以双击任何值，并在 Xcode 内部进行修改。

#### 设置图标

“关于”面板顶部显示应用程序的图标，该图标能让你一眼识别出应用程序，但主要起美观作用。为应用程序设置图标后，“关于”面板中的图标也会随之更改。要设置图标，你需要做两件事：

- 1. 通过拖放操作，将图标（扩展名为 `.icns` 的文件）添加到项目窗口中。

通常，图标文件放置在项目的资源（Resources）文件夹中。在本章中，我将向你展示如何使用图标编辑器（Icon Composer）制作图标。

- 2. 在 `Info.plist` 中，在“图标文件”（Icon File）字段中输入图标的名称。

请按照在 Finder 中看到的那样准确输入图标文件的名称。但是，文件扩展名（`.icns`）是可选的。

图 5-4 显示图标文件 `Utility.icns` 已被添加到项目中。

![](img/ea40cad434a338535474e82c1a6ace20_111_0.png)

#### 设置名称或标题

接下来，你可能需要更改“捆绑包名称”（Bundle Name），以影响显示在“关于”面板中的应用名称。这通常是“关于”面板中最重要的元素，因为该面板会在你点击“关于本应用程序”（About This Application）菜单项时出现。标题仅用于标识该应用程序。

你可能会被 `Info.plist` 中紧邻“捆绑包名称”的下一个项所吸引，但不要修改它。相反，请在项目目标（target）的信息窗口（Info window）中设置应用程序的名称。默认情况下，项目会将 `Info.plist` 中的“捆绑包名称”赋值为 `${PRODUCT_NAME}`。这意味着名称来自项目的其他位置，因为 `${PRODUCT_NAME}` 是一个变量。当你更改项目目标信息窗口中的值时，`Info.plist` 会在运行时自动反映这些更改。

产品默认名称通常与项目名称相匹配，但不一定如此。要更改产品名称，进而更改显示在“关于”面板中的应用名称，请遵循以下步骤：

- 1. 在项目中找到并展开“目标”（Targets）文件夹。

“目标”文件夹有一个红色的靶心图标，很容易找到。

- 2. 在“目标”文件夹中选择应用程序目标。

该目标将拥有一个你能识别的名称；很可能与项目目标本身的名称相同。图 5-5 显示了所选的目标。

![](img/ea40cad434a338535474e82c1a6ace20_112_0.png)

![](img/ea40cad434a338535474e82c1a6ace20_112_1.png)

- 3. 点击项目工具栏中的“信息”（Info）按钮，打开信息窗口。
- 4. 在信息窗口中，点击“构建”（Build）选项卡。
- 5. 找到并更改“产品名称”（Product Name）的键值。

“产品名称”位于信息窗口的“打包”（Packaging）部分，如图 5-6 所示。更改“产品名称”将使你的构建应用程序拥有新的名称，且该新名称将反映在“关于”面板中。

![](img/ea40cad434a338535474e82c1a6ace20_113_0.png)

#### 显示版本号、版权日期和致谢

除了使用标题来标识应用程序外，在“关于”面板中提供版本号、版权声明和致谢也是一个好主意：

- 版本号帮助用户一眼就知道他们正在使用应用程序的哪个版本，以防他们想知道何时下载新版本。
- 版权日期有助于提醒你作品已受版权保护，同时也提供了一个方便的时间戳。
- “关于”面板中的致谢允许你感谢协助创建应用程序的各个成员。此元素并非严格必需，但有时炫耀一下你的应用程序感觉也不错。

要在“关于”面板中显示应用程序的版本号，请更改 `Info.plist` 中的“捆绑包版本”（Bundle version）键。图 5-7 显示了版本 1.5。

![](img/ea40cad434a338535474e82c1a6ace20_114_0.png)

图 5-7：更改“捆绑包版本”键，以影响显示在“关于”面板中的版本号。

你可以使用 `Info.plist` 中的“版权”（Copyright）键在“关于”面板底部显示版权日期。默认情况下，“版权”键不存在，因此你必须添加它。请遵循以下步骤：

- 1. 在 `Info.plist` 中，选择层次结构中的“信息属性列表”（Information Property List）项，如图 5-8 所示。
- 2. 点击“值”（Value）列右侧的按钮，向 `Info.plist` 添加新键。从可能的键列表中选择“版权（可读形式）”（Copyright (Human-Readable)）。
- 3. 将“版权（可读形式）”键的值更改为你希望显示在“关于”面板底部的任何内容。

图 5-9 展示了一个完整的“版权（可读形式）”键。

![](img/ea40cad434a338535474e82c1a6ace20_115_0.png)

图 5-8：在 `Info.plist` 中选择“信息属性列表”。

![](img/ea40cad434a338535474e82c1a6ace20_115_1.png)

图 5-9：向 `Info.plist` 添加“版权（可读形式）”键，以在“关于”面板底部显示版权信息。

你可以在“关于”面板的模式文本（mode of the About Panel）滚动文本字段中显示各种有趣且有用的致谢内容。你只需向资源文件夹添加一个“致谢”（Credits）文件即可。“致谢”文件可以是富文本文件（`.rtf` 或 `.rtfd`）或 HTML（超文本标记语言）文件。两者都可以显示样式化文本和图像；HTML 可以显示可点击的链接，这对于添加公司网址或支持邮箱很有用。请预先了解，HTML 文件本身不包含图像；相反，它们引用单独的图像文件。因此，如果你计划使用 HTML 来显示图形，请仅使用 HTML 来显示图形。图 5-10 显示了项目中的富文本“致谢”文件。

![](img/ea40cad434a338535474e82c1a6ace20_116_0.png)

图 5-10：向项目添加一个文件，以在“关于”面板中显示样式化文本和图形。

## 为你的项目分配图标

用户注意到的你的应用程序的第一个特征之一就是它的图标。当你首次使用 Xcode 构建应用程序时，它会分配一个通用应用程序图标，如图 5-11 所示。

![](img/ea40cad434a338535474e82c1a6ace20_116_1.png)

图 5-11：Xcode 为它构建的所有应用程序分配通用图标。
