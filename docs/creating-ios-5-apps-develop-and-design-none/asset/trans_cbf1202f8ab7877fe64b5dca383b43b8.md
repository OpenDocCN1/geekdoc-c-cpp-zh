
## 实现动作与回调方法

现在切换到 EnterWeightViewController.m。在我们开始处理动作方法和委托方法之前，先添加一个带有几个私有属性的扩展。

```objc
@interface EnterWeightViewController()
@property (nonatomic, strong) NSDate* currentDate;
@property (nonatomic, strong) NSNumberFormatter* numberFormatter;
@end
```

我们添加了两个属性：currentDate 将保存当前日期（基于视图出现时的日期和时间），numberFormatter 将用于处理用户的输入。

接下来，合成这些属性。

```objc
@synthesize currentDate = _currentDate;
@synthesize numberFormatter = _numberFormatter;
```

然后，转到 viewDidLoad 方法，添加以下代码来实例化并配置我们的数字格式化器：

```objc
- (void)viewDidLoad
{
    [super viewDidLoad];
    self.numberFormatter = [[NSNumberFormatter alloc] init];
    [self.numberFormatter
        setNumberStyle:NSNumberFormatterDecimalStyle];
    [self.numberFormatter
        setMinimum:[NSNumber numberWithFloat:0.0f]];
    self.unitsButton = [UIButton buttonWithType:UIButtonTypeCustom];
    self.unitsButton.frame = CGRectMake(0.0f, 0.0f, 25.0f, 17.0f);
    self.unitsButton.backgroundColor = [UIColor lightGrayColor];
    ...
}
```

setTitle:forState: 和 setTitleColor:forState: 都涉及按钮的状态。每个控件都有一种状态：正常、高亮、选中或禁用。不同的动作可以改变控件的状态（参见表 4.2）。我们的按钮只用到两种状态：被触摸时高亮，其他时候为正常状态。

在按状态设置属性时，如果没有为某个状态显式指定值，该状态将默认回退到 UIControlStateNormal 的设置。例如，在我们的代码中只需要设置一次标题。除非另有说明，其他所有状态也同样会使用这个值。

这里引出了一个常被混淆的问题。如果你在开发者文档中查阅 UIControlState，就会发现该枚举被设计成位掩码。这意味着我们应该能够使用按位或运算符（|）组合多种状态。因此，你可能会忍不住想用类似下面的代码为所有状态显式设置标题：

```objc
UIControlState all = UIControlStateNormal |
                     UIControlStateSelected |
                     UIControlStateHighlighted |
                     UIControlStateDisabled;
[self.button setTitle:@"default text" forState:all];
```

遗憾的是，这么做行不通。你实际上并不是在为所有状态设置标题，而是在为单个状态设置标题：具体来说，你实际上是在为控件同时处于选中、高亮和禁用状态时的那个状态设置标题（这种情况下 UIControlStateNormal 被忽略）。

在创建自定义双状态按钮之类的控件时，这会很方便。这类按钮有 ON 和 OFF 两种状态，而每种状态又可以显示为正常或高亮。这意味着我们需要为这四种不同的状态定义四种不同的外观。

我们可以使用按钮的 selected 属性来表示其 ON/OFF 状态。于是，我们的外观定义如下：UIControlStateNormal 表示按钮处于 OFF；UIControlStateHighlighted 表示按钮处于 OFF 且被触摸；UIControlStateSelected 表示按钮处于 ON；UIControlStateHighlighted | UIControlStateSelected 表示按钮处于 ON 且被触摸（图 4.11）。请注意，这里没有使用 UIControlStateDisabled。

## UIControl 与状态（续）

![](img/fe9fea534a8e7868f811f7cd33da015f_190_0.png)

不过，如果你只是想在所有状态中设置一个默认外观，只需使用 UIControlStateNormal，并让其他状态默认回退到它即可。

表 4.2 控件状态

| 状态 | 触发条件 |
| --- | --- |
| UIControlStateNormal | 默认控件状态。 |
| UIControlStateHighlighted | 高亮状态通常用于在控件被触摸时改变其外观。当触摸进入和离开控件时，该状态会自动设置和清除。我们的应用也可以通过 highlighted 属性访问该状态。 |
| UIControlStateSelected | 通常，此状态对控件的外观没有影响；不过，像 UISwitch 这样的控件会在 ON 与 OFF 状态之间切换时使用它。该状态也可以通过控件的 selected 属性访问。 |
| UIControlStateDisabled | 该状态通常通过控件的 enabled 属性设置。禁用时，控件不会响应触摸事件。许多控件在被禁用时也会改变外观。 |

在上一章中，我们使用数字格式化器生成数字字符串，无论设备的语言和国家/地区设置如何，这些字符串都能正确格式化。在本章中，我们将看到另一面。我们将使用 NSNumberFormatter 来验证和过滤用户的输入。在这里，我们将其设置为只接受正十进制数。我们还将使用该格式化器解析用户输入，将其从字符串转换为浮点值。

同样，我们在 viewDidLoad 中设置的内容需要在 viewDidUnload 中清理。添加以下代码：

```objective-c
- (void)viewDidUnload
{
    [self setWeightTextField:nil];
    [self setDateLabel:nil];
    self.unitsButton = nil;
    self.numberFormatter = nil;
    [super viewDidUnload];
}
```

每次视图出现时，我们仍然需要重置视图。请记住，一个视图可能只创建一次，但会多次出现。实际上，情况比这还要复杂。一个视图可能会被多次加载和卸载（通常是由于内存不足）。每次加载后，它可能会不止一次地出现在屏幕上。因此，把这些问题想清楚很重要。哪些配置项需要且仅需要执行一次？这些通常在应用委托的 application:didFinishLaunchingWithOptions: 方法中执行。哪些配置项应该在每次视图加载时执行？这些应该在视图控制器的 viewDidLoad 方法中执行。最后，哪些配置项应该在每次视图出现在屏幕上时执行？这些在 viewWillAppear: 或 viewDidAppear: 方法中完成。

### viewWillAppear: 与 viewDidAppear:

viewWillAppear: 和 viewDidAppear: 方法可能会让人有些困惑。在大多数情况下，只要使用一个视图控制器来显示另一个视图控制器，系统就会调用这些方法。这包括显示模态视图、向导航控制器添加新视图，或在标签栏上切换视图。当视图重新出现时，系统甚至也会调用这些通知方法。例如，从模态视图返回，或当覆盖视图从导航栈中弹出时。

然而，使用 addSubview: 方法手动添加视图并不会触发这些通知。修改视图的 hidden 或 alpha 属性来隐藏或显示视图，也不会触发。而且，更令人困惑的是，使用 addSubview: 将视图添加到应用的窗口时，却会触发这些通知（尽管在 iOS 4.0 及更高版本中，你应该将视图控制器赋值给窗口的 rootViewController 属性，而不是使用 addSubview:）。

虽然这些规则和例外情况看起来可能令人困惑，但它们确实指向了一个常见的设计问题。如果你的视图出现在屏幕上，但你的视图控制器的 viewWillAppear: 和 viewDidAppear: 方法没有被调用，那么你的视图层级可能是不一致的。这种情况发生在你向视图层级添加视图时，却没有将其视图控制器正确添加到视图控制器层级中。

有几种方法可以解决这个问题。最简单的是，你可以去掉视图控制器，直接把视图添加到其父视图的控制器上。毕竟，视图控制器通常一次管理多个视图。每当我们为某个控件创建 outlet 时，我们都在这样做。

另外，在 iOS 5.0 中，我们可以创建一个自定义容器视图控制器，并用它来呈现子视图的控制器。顾名思义，容器视图控制器管理一个或多个其他视图控制器。UIKit 中的示例包括 UINavigationController、UITabBarController 和 UIPageViewController。iOS 5 扩展了 UIViewController 类，为我们提供了向控制器层级添加控制器（addChildViewController:）或从控制器层级移除控制器（removeFromParentViewController）的方法。这让我们能够创建与视图层级相对应的控制器层级。因此，系统可以正确地将重要消息沿着这两个层级进行转发。

更多信息请查阅 UIViewController 文档，特别是查看 automaticallyForwardAppearanceAndRotationMethodsToChildViewControllers 属性。其中包含需要沿着视图控制器层级转发的所有消息的列表。我们还会在第 8 章的“创建 UIViewController 容器”一节中创建我们自己的自定义容器视图控制器。
