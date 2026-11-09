
```objc
Download Persistence/HelloApplication4D/PreferencesController.h
#import <Cocoa/Cocoa.h>

@interface PreferencesController : NSWindowController {
    NSButton *loadSavedRemovedAppsCheckbox;
}
@property IBOutlet NSButton *loadSavedRemovedAppsCheckbox;
-(IBAction) toggleLoadSavedRemovedApps: (id)sender;

@end
```

PreferencesController 不需要做太多事情。当偏好设置窗口出现时，我们希望将复选框设置为用户偏好设置中存储的状态：

```objc
Download Persistence/HelloApplication4D/PreferencesController.m
-(void) awakeFromNib {
    [self.loadSavedRemovedAppsCheckbox
        setState:[[NSUserDefaults standardUserDefaults]
            boolForKey:@"LoadSavedRemovedApps"]];
}
```

当用户选中或取消选中复选框时，我们需要将新值存储到用户偏好设置中：

```objc
Download Persistence/HelloApplication4D/PreferencesController.m
-(IBAction) toggleLoadSavedRemovedApps: (id) sender {
    [[NSUserDefaults standardUserDefaults]
        setBool:[self.loadSavedRemovedAppsCheckbox state]
            forKey:@"LoadSavedRemovedApps"];
}
```

让我们将 PreferencesController 连接到它所管理的 nib。双击 Preferences.xib。将 File's Owner 的类设置为 PreferencesController。将其 window 出口连接到 Window。将其 loadSavedRemovedAppsCheckbox 出口和 toggleLoadSavedRemovedApps 动作连接到 Checkbox。选择 Window，并将其委托连接到 File's Owner。

保存你的工作。我们已经创建了偏好设置窗口及其控制器。我们已经实现了该控制器，并在新的 nib 中连接好了所有内容。同时，我们还设置了 ActivityController 来使用这些偏好设置。剩下的全部工作就是：当用户选择 HelloApplication > 偏好设置时，弹出偏好设置窗口。

使用连接检查器将 HelloApplicationDelegate 的 openPreference: 动作连接到“偏好设置...”菜单项。

因此，现在当用户选择“偏好设置...”时，我们会初始化 PreferencesController 并加载 Preferences nib 文件。当用户关闭偏好设置窗口时，我们还需要清理这些资源。窗口不可见时没有必要继续存在，因此我们会销毁它，并在用户之后决定修改偏好设置时创建一个新窗口。

PreferencesController 是其窗口的委托，因此我们可以实现这个委托方法：

```objc
// Persistence/HelloApplication4D/PreferencesController.m
- (void)windowWillClose:(NSNotification *)notification {
    [self autorelease];
}
```

这又是使用许多小而专注的 nib 的另一个优势。我们可以在需要时加载资源，并在之后清理它们。

此时，如果你单击“构建并运行”，就可以使用菜单项或 ⌘, 键盘快捷键调出偏好设置窗口。所有内容都已就位，可供你设置和读取设置。你可以随意更改偏好设置，并退出、重新启动来试试。

你甚至可以打开你的偏好设置文件（是 plist 文件，而不是窗口），查看你设置的值。

| 键 | 类型 | 值 |
| --- | --- | --- |
| Root | 字典 | （1 项） |
| LoadSavedRemovedApps | 布尔值 | ☑ |

在本章中，你学习了保存少量数据的技术。你已经了解了如何从 NSArrays 等基本类型创建 plist，以及如何归档更复杂的数据。你还了解了如何使用用户偏好设置。当我们需要存储更大量的数据或组织更复杂的数据时，我们将转向 Core Data。在下一章中，我们将切换不同的视图，然后开始理解 Core Data 的旅程。

## 第 18 章

## 更改视图

回到第 16 章 *在表格中显示数据*（第 256 页），我们当时让窗口控制器可以轻松切换所使用的视图控制器和视图。好消息是，你可以通过更改视图控制器类的名称和 nib 名称并重新编译来来回切换。坏消息是，你的用户无法在运行时做出同样的更改。

在本章中，我们将创建一个新的偏好设置，用户可以通过它指定应用程序启动时应显示哪个视图。然后，我们将使用该偏好设置在启动时显示用户选择的视图。接着，我们将扩展这个示例，让用户在应用程序运行期间可以随意来回切换。

我们通过重新创建简单的 iPhone 网页浏览器，结束了故事的第一幕。那并没有太多新内容，但目的是在一个新的情境中快速回顾你到目前为止学到的知识。

随着第二幕落幕，让我们回顾一下你在处理这个示例时学到的一些技术。尽管你会时不时学到新东西，但主要目标是让你看到使用多个 nib 以及小而定义良好的类和方法的优势。

### 18.1 使用单选按钮

让我们向偏好设置面板添加一组单选按钮。双击 Preferences.xib，并在库中搜索 *单选按钮*（Radio）。

你应该会找到这个控件：

![](img/9355405953264484a02198b0e3d25b7e_285_0.png)

将它拖到偏好设置窗口上。调整控件和窗口的大小，并在两个单选按钮右侧添加文本，使其看起来大致如下：

![](img/9355405953264484a02198b0e3d25b7e_285_1.png)

看一下 Preferences.xib 文档窗口中 GUI 元素的层级结构：

![](img/9355405953264484a02198b0e3d25b7e_285_2.png)

我们本可以分别连接单选按钮组中的每个 NSButtonCell 对象并与之交互。相反，我们将通过 NSMatrix 对象把整个组作为一个整体来处理。

为了从 PreferencesController 对象中设置选中哪个单选按钮，请向 PreferencesController 类添加一个名为 group、类型为 NSMatrix 的属性。你还需要向 PreferencesController 添加一个动作，每当选中某个单选按钮时都会调用它。将你的动作命名为 chooseView:，并保存 PreferencesController.h。在 IB 中，使用连接检查器将这个出口和动作连接到 NSMatrix。

如果我们要将控制器连接到 NSMatrix，而不是连接到各个按钮，就需要一种区分这两个按钮的方法，以便判断哪一个被选中。在处理表格时，我们使用了列的标识符。NSButtonCell 没有标识符，但它们有标签。

在 Interface Builder 中，选择你标记为“启动时显示图标视图”的按钮。查看属性检查器的底部，你应该会看到 Tag 属性的值为 1。同样，另一个按钮单元格的 Tag 属性值为 0。¹

### 18.2 为启动时使用的视图添加偏好设置

要让偏好设置正常工作，我们需要做四件事：

- 1. 为偏好设置选择一个名称和一种格式。
- 2. 创建一个默认值，在用户设置自己的偏好设置之前使用。
- 3. 当我们的 PreferencesController 从 nib 唤醒时读取该偏好设置。
- 4. 当用户选择某个单选按钮时写入该偏好设置。

我们可以像处理复选框那样，将偏好设置存储为布尔值。目前这样做没问题，因为我们要么使用图标视图，要么不使用。我们已经这样做过了。让我们做点不同的。

让我们将当前选中按钮的标签存储为偏好设置的值。标签是一个 int。在写入或读取偏好设置时，我们需要在 int 与 NSNumber 之间进行转换。我们使用类方法 numberWithInt: 从 int 创建 NSNumber。反过来，我们使用方法 intValue 从 NSNumber 中取出 int。

现在我们已经有了偏好设置的格式，可以给它起一个能说明其含义的名称。我们把它叫作 TagForView。我们可以在 HelloApplicationAppDelegate.m 中注册默认值，位置就在我们为 LoadSavedRemovedApps 注册默认值的下方。

```objective-c
+(void)initialize {
    NSDictionary *defaults =
        [NSDictionary dictionaryWithObjectsAndKeys:
            @"NO", @"LoadSavedRemovedApps",
            [NSNumber numberWithInt:1], @"TagForView",
            nil];
    [[NSUserDefaults standardUserDefaults] registerDefaults:defaults];
}
```

¹ 如果这些标签的值不同，请将它们改为 1 和 0。
