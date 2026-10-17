
## 过渡样式 (Transition Styles)

`modalStyle` 属性决定视图出现的方式。有四种过渡选项：

- **Cover（覆盖）：** 模态视图从底部向上滑动。
- **Flip（翻转）：** 模态视图水平翻转。
- **Cross-dissolve（交叉溶解）：** 模态视图淡入。
- **Page Curl（翻页）：** 模态视图像书页一样翻转。

# 第三部分：多视图应用

为了检查是否运行正常，请保存你的项目并在模拟器中启动它。尝试点击 `Settings`（设置）按钮，然后点击 `Done`（完成）按钮。你的视图应该像接豆豆一样来回切换。如果没有切换，最可能的原因是你的 `Done` 按钮没有连接到 Interface Builder 中的 `doneButtonPressed` 方法。

## 模型

到目前为止，你已经构建了应用程序的视图并成功地将它们连接到了控制器。你还完成了对用户如何在应用中导航的定义。现在连接工作已经完成，让我们开始在应用中实现 Twitter 集成。在这一阶段，你将创建一个 `TwitterUser` 类来跟踪用户及其最新的推文。

正如你将看到的，`TwitterUser` 模型类非常简单。它只包含两个属性：一个用于用户名，一个用于推文，仅此。模型类通常像这样简单。它们的主要作用是跟踪应用程序数据，因此它们不需要做太多。

要添加 `TwitterUser` 模型类，右键点击 `Classes` 组，并执行以下步骤：

- 1. 在 Xcode 中，右键点击 `Classes` 组，选择 `Add > New File`（添加 > 新文件）。
- 2. 在 `iPhone OS > Cocoa Touch Class` 类别下，选择 `Objective-C class`，并确保 "`Subclass of`" 子类）设置为 `NSObject`。
- 3. 点击 `Next`（下一步）。将文件命名为 "`TwitterUser.m`" ，并点击 `Finish`（完成）。
- 4. 编辑 `TwitterUser.h`，使其与以下代码匹配：

```
// TwitterUser.h

#import <Foundation/Foundation.h>

@interface TwitterUser : NSObject
    NSString *username;
    NSString *tweet;
}

@property (nonatomic, copy) NSString *username;
@property (nonatomic, copy) NSString *tweet;

@end
```

- 5. 编辑 `TwitterUser.m`，使其与以下代码匹配：

```
// TwitterUser.m

#import "TwitterUser.h"

@implementation TwitterUser

@synthesize username;
@synthesize tweet;

-(void)dealloc {
  [username release];
  [tweet release];
  [super dealloc];
}

@end
```

保存并构建你的项目，以确保没有任何拼写错误。此时它应该可以顺利构建。

关于 `TwitterUser.h` 文件有一点需要注意：注意属性是如何使用 `copy` 属性的？根据经验，当对象类型为 `NSString` 时，你应该使用 `copy` 属性。对于其他对象类型，你通常使用 `retain`。

## 控制模型

现在你已经定义了模型类，应该使用它了。模型类的目标是在 `Tweet` 和 `Settings` 视图之间跟踪数据。当 `Tweet` 视图显示时，它将使用默认用户名初始化 `TwitterUser` 对象。当用户切换到 `Settings` 视图更改用户名时，`TwitterUser` 对象也会反映这一变化。然后，当用户切换回 `Tweet` 视图时，它将根据存储在 `TwitterUser` 对象中的用户名刷新最新的推文。如果这听起来没什么逻辑，在你编写代码时它会变得更加清晰。

你需要做的第一件事是为 `TweetViewController` 添加对 `TwitterUser` 模型类的支持。首先，将 `TwitterUser` 添加你的 `ViewController.h` 文件，如下：

```
// ViewController.h

#import "TwitterUser.h"

@interface ViewController : UIViewController
{
  TwitterUser *twitterUser;
}
@end
```

现在，你将在 nib 文件首次加载时初始化 `twitterUser` 变量。你还将添加代码来根据模型对象更新界面。将以下代码添加到 `ViewController.m` 中以进行这些更改：

```
// ViewController.m

#define kDefaultUsername "@ActuallyNPH"

// 使用最新的用户数据更新界面
(void)updateInterface {
  // 使用模型数据更新界面
  usernameLabel.text = [NSString stringWithFormat:@"%@", twitterUser.username];
  textView.text = twitterUser.tweet;
}

// 在 nib 加载时初始化用户
(void)awakeFromNib {
  twitterUser = [[TwitterUser alloc] init];
  twitterUser.username = kDefaultUsername;
  twitterUser.tweet = @"";
}

(void)dealloc {
  [usernameLabel release];
  [textView release];
  [twitterUser release];
  [super dealloc];
}
```

对于前面的代码，如果你熟悉 C 语言，你可能会疑惑 `kDefaultUsername` 是什么。这个术语本身是一个常量。特别注意 `#define` 行末尾没有分号。

保存你的项目，并确保它仍然可以顺利构建。此时，`TweetViewController` 在启动时创建模型，但它需要与 `SettingsViewController` 共享此模型类。为了方便共享模型，你将在 `SettingsViewController` 上添加一个 `twitterUser` 属性，以便 `TweetViewController` 可以传递指向其 Twitter 实例的指针。

首先，确保你在 `TweetViewController.m` 的正确位置调用此属性。在 `settingsButtonTapped` 动作中初始化 `SettingsViewController` 对象后，添加此行：

```
// TweetViewController.m

-(IBAction)settingsButtonTapped {
    SettingsViewController *settingsViewController = [[SettingsViewController alloc] init];
    settingsViewController.modalTransitionStyle = UIModalTransitionStyleFlipHorizontal;
    settingsViewController.twitterUser = twitterUser;

    [self presentViewController:settingsViewController animated:YES];
}
```

现在，你必须向 `SettingsViewController` 添加该属性。将以下代码添加到 `SettingsViewController.h` 中：

```
// SettingsViewController.h

#import "TwitterUser.h"

@interface SettingsViewController : UIViewController<UITextFieldDelegate>
{
    TwitterUser *twitterUser;
}

@property (nonatomic, retain) TwitterUser *twitterUser;

@end
```

然后，将此代码添加到 `SettingsViewController.m` 中：

```
// SettingsViewController.m

#import "SettingsViewController.h"

@implementation SettingsViewController

-(void)awakeFromNib {
    [super awakeFromNib];
}

-(void)dealloc {
    [twitterUser release];
    [super dealloc];
}

@end
```

# 视图生命周期方法

控制器有很多在控制器生命周期内自动调用的方法。有时，你会在视图控制器初始化时进行一些设置。或者你可能想在视图显示之前通过编程对其进行自定义。你可以在视图控制器子类中覆盖这些生命周期方法。

以下是每个视图生命周期方法的简单描述：

- `awakeFromNib`：如果你在 Interface Builder 中为控制器构建了视图，那么 `awakeFromNib` 在从 nib 文件初始化视图之前调用。
- `loadView`：在 `awakeFromNib` 之后，会调用 `loadView`。`loadView` 是你可以通过编程方式向界面添加视图的地方。

## 注意事项

这里有一个你应该知道的小秘密：你不需要 Interface Builder 来构建界面。你完全可以在 `loadView` 中通过编程创建整个界面。手动编写代码并没有固有的优势，在书中你将继续使用 Interface Builder 来视觉化地布局每个应用的界面。

- `viewDidLoad`：无论视图是通过编程创建还是加载的，`viewDidLoad` 在视图完全加载到内存后调用。
- `viewWillAppear`：`viewWillAppear:` 方法在视图控制器出现在屏幕之前立即调用。然而，`viewWillAppear:` 在视图器的生命周期内可以被多次调用。在 Tweet 中，每当你在 Tweet 和 Settings 视图之间切换时，它们的 `viewWillAppear:` 方法都会被调用。
- `viewDidAppear`：`viewDidAppear:` 方法在到视图器的过渡动画完成后调用。
- `viewWillDisappear`：`viewWillDisappear:` 方法正如你猜的那样——在视图消失之前调用。具体来说，这是用户离开当前视图但在任何动画开始之前。
- `viewDidDisappear`：`viewDidDisappear:` 方法在离开当前控制器的过渡动画完成后调用。
- `viewDidUnload`：`viewDidUnload` 方法在内存不足的情况下被调用。具体来说，当视图控制器不可见并接收到一个低内存警告，随后 `viewDidLoad` 方法会被调用。你应该在该方法中释放所有被保留的视图，以释放尽可能多的内存。当你的视图控制器下次显示时，你的视图将重新构建。

## 崩溃与学习（CRASH AND LEARN）

永远不要直接调用上述任何生命周期方法。系统会在适当的时间自动调用每个生命周期方法。直接调用这些方法可能会导致灾难性的结果。

如果现在听起来这还不完全合逻辑，请不要担心。你需要花费时间和实践，才能准确理解如何在应用中具体使用这些生命周期方法。只需关注书中示例应用程序是如何使用这些方法的，从 Tweet 应用开始即可。

## 为 TweetViewController 添加 viewWillAppear:

在 `SettingsViewController` 中，你使用 `viewWillAppear:` 方法将用户名字段的字符串设为模型类中的值。通过使用 `viewWillAppear:`，你能够确保在 `SettingsViewController` 变得可见之前设置好文本字段的值。

在 `TweetViewController` 中，你将使用 `viewWillAppear:` 获取用户的最新推文，并使用来自模型对象的数据进行更新。`viewWillAppear:` 是执行此操作的完美位置，原因有两个：

- 当应用首次启动时，`viewWillAppear:` 方法在界面变得可见之前被调用，这意味着文本视图中的拉丁文将被替换为真实的推文。
- 当用户在设置屏幕上更新 Twitter 用户名后，`viewWillAppear:` 在其切换回 Tweet 视图之前被调用。你可以用新用户名更新 `usernameLabel` 属性，并在用户再次看到 Tweet 视图之前获取该用户的最新推文。

然而，在重写 `viewWillAppear;` 之前，你需要下载 `TwitterHelper` 文件，你可以用它与 Twitter API 交互。按照以下步骤在项目中获取并使用 `TwitterHelper` 文件：

- 1. 下载并解压 `http://trybryant.net/iphonebook/chapter11/TwitterHelper.zip` 中的文件。
- 2. 将 `TwitterHelper` 目录拖入 Xcode 中的 `Classes` 组。确保勾选了“Copy items into destination group's folder”（如果需要）。
- 3. 保存并构建项目。它应该能够无问题地构建。
- 4. 在 `TweetViewController.m` 中添加以下方法：

```objc
// TweetViewController.m

#import "TwitterHelper.h"
// 在视图出现之前，用真实的推文更新界面
- (void)viewWillAppear:(BOOL)animated {

    [super viewWillAppear:animated];

    NSString *latestTweet = [TwitterHelper fetchLatestTweetForUsername:twitterUser.username];
    twitterUser.tweet = latestTweet;

    [self updateInterface];
}
```

注意，当你获取推文时，你的第一件事是用信息更新模型。然后，在 `updateInterface` 中，你使用模型中的数据来更新视图。始终按照此顺序更新应用程序：先模型，后视图。

见证时刻到了。保存项目，构建它，并在 iPhone 模拟器中运行它。你应该拥有一个功能完全的多视图 Twitter 应用。尝试更改用户名看看推文是否更新。如果更新了，你就成功完成了你的第一个多视图应用。

## 这有妙门

注意看获取推文时界面卡顿了一片刻了吗？

与其挂起界面，你应该立即切换到另一个视图，并在应用检索推文时显示一个旋转器（spinner）。要正确实现这一点，你需要在后台线程中获取推文。如果你现在感兴趣，可以查看 `http://troybrant.net/iphonebook/chapter11/Tweet-spinner.zip` 在线使用的后台线程的 Tweet 版本源码。

完成后的 Tweet 应用的完整源码可以在线 `http://troybrant.net/iphonebook/chapter11/Tweet-done.zip` 获取。

## Tweedle Dee, Tweedle Done（搞定！）

呼！花了一段时间，但你终于完成了应用。你终于可以休息一下，看会儿电视，处理邮件，然后……检查你的 Twitter 馈？当然，你没有多少闲时间——你只需要用你新手手的 iPhone 应用一次次读一条推文即可。

这一章涵盖了很多内容。在接触了 MVC 理论后，你通过构建 Tweet 应用看到了它的实际应用。你还读了关于模态视图的内容，并发现切换到新的视图控制器是多么简单。提到新的视图控制器，发现这是在视图控制器之间传递数据的一种非常有用的方法。最后，你回顾了如 `viewDidLoad` 和 `viewWillAppear:` 等控制器生命周期方法。

要吸收的内容很多，但下面的图显示了你如何根据 MVC 结构构建 Tweet 应用：

在下一章中，你将深入学习使用导航控制器（navigation controllers）在视图控制器之间进行水平切换。`Push`（推送）和 `pop`（弹出）听起来将不再像异域舞蹈动作，而更像是在读完本章后管理视图控制器的方法。导航控制器专门为组织层级数据而构建，你将构建另一个 Twitter 应用来确切这一切是如何运作的。

## 第11 章：视图控制器 193

![](img/5eb8ee1dd8eb3ab735869e75af92d0ef_210_0.png)

MVC 对 iPhone 开发至关重要，这正是它应用到 Tweet 应用上的样子。

# 你需要知道的最少知识

- 在 MVC 应用中，模型类管理数据，视图处理应用外观，而控制器类将所有部分胶在一起。
- 要启动模态视图，请使用 `UIViewController` 的 `presentViewController:animated:`。
- 使用模型类在视图控制器之间传递数据。
- 永远不要直接调用 `viewWillAppear:` 等视图控制器方法。

## 定义

**栈**（stack）是一个特殊的元素集合，其中最后添加的元素最先被移除——也称为后入先出（LIFO）。向栈中添加元素是把该元素**推**（push）到栈的顶部。从栈中移除元素是通过**弹出**（popping）最近添加到栈中的元素来实现的。

通常在你的应用中设置导航控制器（navigation controller）时，你会提供一个视图控制器用于初始显示。这个视图控制器被称为*根视图控制器*（root view controller）。让我们看看在应用程序启动时如何设置导航控制器。

## 定义
