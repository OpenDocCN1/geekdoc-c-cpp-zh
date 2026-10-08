

3. **向项目中添加一个控制器。**

将 `NSObject` 从库窗口拖到 `XIB` 项目窗口中。按 `⌘ + 6`，然后在身份检查器窗口中将类名更改为 `InternetController`。

4. **向该类添加一个输出接口（outlet）和两个动作（action）。**

在检查器窗口中，添加一个 `emailField` 输出接口，以便你可以检索用户输入的电子邮件地址。然后向该类添加两个新动作，分别命名为 `sendEmailManually` 和 `sendEmailWithClient`。图 15-9 显示了身份检查器窗口，其中展示了 `InternetController` 类的动作。

5. **将界面连接到 `InternetController` 类：**

- a. *按住 Control 键并拖动 `Send Email with Client` 按钮，将其拖到 `XIB` 项目窗口中的 `InternetController` 类上。在弹出小的黑色连接列表覆盖层中，将按钮连接到 `sendEmailWithClient` 动作。*
- b. *按住 Control 键并拖动 `Send Email Manually` 按钮，将其拖到 `InternetController` 类上。将按钮连接到 `sendEmailManually` 动作。*
- c. 按住 Control 键并拖动，将 `emailField` 输出接口连接到界面上：从 `InternetController` 拖到界面主窗口中的 `NSTextField`。
- d. 点击 `Identity Inspector` 窗口中的 `Connect` 以建立连接。

6. 点击 `InternetController` 类，然后选择 `File ⇄ Write Class Files`，以便在 Xcode 中创建并添加类文件。

7. 返回 Xcode 并更改 `InternetController.h` 中的这一行：

```objectivec
@interface InternetController : /* Specify a superclass (eg: NSObject or NSView) */ {
```

改为这一行：

```objectivec
@interface InternetController : NSObject {
```

![](img/ea40cad434a338535474e82c1a6ace20_312_0.png)

**图 15-9：** 为电子邮件功能向 Internet Controller 类添加两个动作和一个输出接口。

8. 将以下代码添加到 `InternetController.m` 中：

注意代码开头处增加了 `#import <Message/MessageKit.h>` 语句（原文此处似有误，实际下文代码为 Message/NSMailDelivery.h，但根据上下文“permits use of the Message Framework”对应导入 MessageKit 或特定框架，此处严格翻译原意，即允许使用 Message 框架）：
*注：原文文本中提到 `#import <Message/NSMailDelivery.h>`，但前一句描述为“Message Framework”。此处忠实于原文代码块和说明。*
注意代码开头增加了 `#import <Message/NSMailDelivery.h>` 语句；该语句允许使用 Message 框架：

```objectivec
#import "InternetController.h"
#import <Message/NSMailDelivery.h>

@implementation InternetController
- (IBAction)sendEmailWithClient:(id)sender
{
    NSString *theURLString = @"mailto:";
    theURLString =
        [theURLString stringByAppendingString: [emailField stringValue]];
    NSURL *theURL = [NSURL URLWithString:theURLString];
    if ( [[NSWorkspace sharedWorkspace] openURL:theURL] )
        NSLog(@"Email Loaded");
}

- (IBAction)sendEmailManually:(id) sender
{
    NSString *theEmailDest = [emailField stringValue];
    NSString *theSubject = @"Important Message";
    NSString *theBody = @"Hello there!";

    if ( [NSMailDelivery deliverMessage:theBody
          subject:theSubject to:theEmailDest] )
        NSLog(@"Email Sent");
    else
        NSLog(@"Email Not Sent");
}
@end
```

9. 要查看你辛勤工作的成果，请选择 **Build ⌘B** 并选择 **Go**。

如果你的项目成功发送了电子邮件，你会在控制台窗口中看到 *Email Sent* 消息。你可以通过选择 **Run ⌘C Console** 在 Xcode 中查看控制台。

## 第 16 章

## 多媒体

### 本章内容

- 播放系统声音和音频文件
- 构建音频播放器项目
- 使用 Cocoa 播放电影
- 加载并使用数十种其他媒体格式

处理文本和创建文件对于你的应用程序来说是很有用的功能，但它们并不总是最让人兴奋的功能。另一方面，多媒体*确实*令人兴奋。Cocoa 延续了 Macintosh 提供高质量多媒体功能供你在项目中使用这一悠久传统。

在本章中，你将发现为你的应用程序添加复杂的多媒体功能有多容易。首先，你通过创建一个简单应用程序来探索音频，该应用程序可以从多个来源播放音频文件。然后，你深入真正的乐趣所在——电影！通过构建一个电影播放器应用程序，你将看到向你的 Cocoa 项目添加动态 QuickTime 内容有多容易。只需更改一行代码，你还将看到如何显示（或隐藏）QuickTime 电影之外的许多其他媒体类型。

## 聆听音频

Macintosh 长期以来一直是音频爱好者喜爱的机器。Cocoa 延续了这一传统，提供了一套完整的工具，让你可以用自己的应用程序制作音频。Cocoa 提供的一些可能性包括

- 播放位于你的应用程序包内的声音
- 播放位于 Mac OS X 系统文件夹中的声音
- 播放来自你硬盘任意位置的声音

除了播放位于多种位置的各种音频文件外，Cocoa 还可以播放许多不同的音频文件格式。在过去，你必须了解各种文件格式才能使用它们。Cocoa 免除了这种必要性，让你可以在不了解相关知识的情况下播放常见的音频文件格式，如 AIFF、MP3 和 WAVE。

## 播放系统声音

Cocoa 在 **NSSound** 类中提供了一种方便的方法来播放声音。

要使用 **NSSound** 类播放音频，通常遵循一个简单的三步过程：

1. 基于 **NSSound** 类创建一个对象。
2. 将音频文件加载到 **NSSound** 对象中。
3. 播放音频。

你通常将前两步甚至全部三步合并为一行代码。加载音频文件最简单的方法是使用其文件名。例如，将一个 AIFF 文件（在此示例中为 `banjo.aiff`）拖入你的 Cocoa 项目。然后使用 **soundNamed** 类方法将其作为 **NSSound** 对象加载：

```objectivec
NSSound *theSound = [NSSound soundNamed:@"banjo"];
```

> **提示** 你可以省略文件扩展名。

除了加载你拖入项目的音频文件外，你还可以加载位于 Mac OS X 三个声音目录之一的声音，位置如下：

```
/System/Library/Sounds
/Library/Sounds
~/Library/Sounds
```

例如，假设你想播放 Mac OS X 附带的著名 Sosumi 警报声。代码与前面的示例相同，只是名称发生了变化：

```objectivec
NSSound *theSound = [NSSound soundNamed:@"Sosumi"];
```

加载声音后，播放它就是一件微不足道的事：

```objectivec
[theSound play];
```

为了进一步简化，你可以将所有内容合并为一行播放声音的代码：

```objectivec
[[NSSound soundNamed:@"Sosumi"] play];
```

## 加载和播放声音文件

对于某些应用程序，播放位于你的项目中或库声音文件夹中的声音是不够的。假设你希望你的应用程序播放用户选择的任何声音。要完成此任务，请遵循以下步骤：

1. 使用 soundUnfilteredFileTypes 类方法创建一个数组，并用 Cocoa 识别的所有声音文件类型填充它：

    ```objectivec
    NSArray *audioFileTypes = [NSSound soundUnfilteredFileTypes];
    ```

    如果你好奇 Cocoa 识别（并且可以播放）哪些类型的声音，你可以通过循环遍历 *audioFileTypes* 数组中的元素并在控制台通过 NSLog 显示每个元素来在控制台中显示它们。以下代码片段列出了 NSSound 支持的文件扩展名。注意，该列表对大小写敏感，因此你可能会看到同一文件类型的多个实例（例如，mp3, MP3, Mp3）：

    ```objectivec
    int i;
    for (i=0; i<[theFileType object count]; i++)
        NSLog([theFileTypes objectAtIndex:i]);
    ```

    图 16-1 显示了用户可以打开的声音文件类型的可用列表。

    ![](img/ea40cad434a338535474e82c1a6ace20_316_0.png)

2. 显示 NSOpenPanel，并将该面板中用户的选项限制为你的数组中的文件类型。

    在这种情况下，因为你使用了第 1 步中的 soundUnfilteredFileTypes，它用所有可能的声音文件类型填充了数组，所以你并没有限制声音文件类型。将用户在 NSOpenPanel 中可以打开的文件数量限制为一个文件：

    ```objectivec
    NSOpenPanel *theOpenPanel = [NSOpenPanel openPanel];
    [theOpenPanel setAllowsMultipleSelection:NO];
    result = [theOpenPanel runModalForTypes:theFileTypes];
    ```

3. 使用 NSSound 的 initWithContentsOfFile 方法加载用户在 NSOpenPanel 中选择的声音（由 theFileName 表示）。

    因为你将用户限制为只能打开一个音频文件，所以它的路径位于 NSOpenPanel 返回的数组的第一个元素中。

    ```objectivec
    theFiles = [theOpenPanel filenames];
    theFileName = [theFiles objectAtIndex:0];
    NSSound *theSound = [[NSSound alloc] initWithContentsOfFile:theFileName byReference:YES];
    ```

4. 照常播放声音：

    ```objectivec
    [theSound play];
    ```

前面的示例将用户在 NSOpenPanel 中的选择限制为仅一个音频文件。根据你的应用程序的需求，你可能允许用户在 NSOpenPanel 中选择多个音频文件。要做到这一点，你需要首先允许在 theOpenPanel 中进行多重选择：

```objectivec
[theOpenPanel setAllowsMultipleSelection:YES];
```

当用户在 NSOpenPanel 中点击确定按钮后，循环遍历结果 theFiles 数组中的所有选定音频文件：

```objectivec
theFiles = [theOpenPanel filenames];
int i;
for (i=0; i<[theFiles count]; i++) {
    theFileName = [theFiles objectAtIndex:i];
    //do something with the file located at this path:
    theFileName
}
```

![](img/ea40cad434a338535474e82c1a6ace20_317_0.png)

