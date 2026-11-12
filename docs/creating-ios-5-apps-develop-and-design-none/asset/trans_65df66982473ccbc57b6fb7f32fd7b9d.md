最后，我们检查文档的 `UIDocumentStateEditingDisabled` 标志。只要文档处于不再适合安全编辑的状态，该标志就会被设置。通常，这发生在文档正在加载远程更新时，但其他事件也可能触发它。

如果标志已打开，我们让文本字段放弃第一响应者状态，从而隐藏键盘。同时我们也会禁用文本字段，防止用户进行任何修改。如果标志已关闭，我们则启用文本字段，并将其设为第一响应者。这会使键盘重新出现。我们还会更新 `currentDate` 属性和用户界面的日期标签。这有助于确保我们的体重记录保持顺序排列。

至此，我们对文档的处理就完成了；不过，我们仍然需要保存用户默认设置。幸运的是，你将看到，这要简单得多。不过，这里是一个休息的好地方。稍微伸展一下，（像往常一样）提交你的更改。

## 保存用户默认设置

我们首先使用 `NSUserDefaults` 存储默认重量单位。让我们先定义几个函数来简化代码。

我们将直接编写 C 函数，但仍希望它们能够完全访问我们的 Objective-C 类。因此，我们需要让该文件像 Objective-C 一样被编译。最简单的做法是新建一个 NSObject 类，然后删除该类接口及其实现。

右键点击 Model 分组，新建一个名为 WeightUnits 的 NSObject。然后打开头文件和实现文件，删除除 `#import` 指令之外的所有内容。我们甚至可以将 Foundation 导入指令从头文件移动到实现文件中。

现在，在 WeightUnits.h 中添加以下代码：

```objc
typedef enum {

    LBS,

    KG

} WeightUnit;

WeightUnit getDefaultUnits(void);

void setDefaultUnits(WeightUnit value);
```

这里我们只是定义了 `WeightUnit` 枚举，并为默认重量声明了两个访问器函数。

接下来，切换到实现文件。

```objc
#import "WeightUnits.h"

#import <Foundation/Foundation.h>

static NSString* const WeightUnitKey = @"weight_unit";

WeightUnit getDefaultUnits(void) {
    return [[NSUserDefaults standardUserDefaults]
        integerForKey:WeightUnitKey];
}

void setDefaultUnits(WeightUnit value) {
    [[NSUserDefaults standardUserDefaults]
        setInteger:value forKey:WeightUnitKey];
}
```

`NSUserDefaults` 使用键来存储值，因此我们首先定义一个静态字符串作为键。`getDefaultUnits()` 函数只是访问标准用户默认设置，并返回与我们的键关联的值。`setDefaultUnits()` 也使用我们的键，将新值保存到标准用户默认设置中。

我们将在应用程序的多个地方使用这些函数。因此，让我们向预编译前缀头文件中添加一条 `#import` 指令。打开 Health Beat-Prefix.pch 并按如下所示修改。

![](img/fe9fea534a8e7868f811f7cd33da015f_360_0.png)

```objc
#import <Availability.h>

#ifndef __IPHONE_5_0

#warning "This project uses features only available in iOS SDK 5.0
        and later."

#endif

#ifdef __OBJC__

    #import <UIKit/UIKit.h>

    #import <Foundation/Foundation.h>

    #import "WeightUnits.h"

#endif
```

这会自动将 `WeightUnits.h` 导入到项目中的每个类中，使我们的访问器函数随处可见。

现在，我们需要在项目中逐个检查，将每一处 `self.weightHistory.defaultUnits` 替换为我们两个访问器函数之一。首先，切换到搜索导航器（导航器选择栏中看起来像放大镜的图标），并搜索 `self.weightHistory.defaultUnits`（图 6.6）。

我们的搜索找到了七个匹配项。依次选中每一个。如果代码是在获取默认单位值，则将其替换为对 `getDefaultUnits()` 的调用。

```objc
WeightUnit unit = getDefaultUnits();
```

如果匹配的代码是在设置新的默认单位值，则将其替换为对 `setDefaultUnits()` 的调用。

```objc
setDefaultUnits(unit);
```

我们还需要从 WeightEntry.h 顶部删除 `WeightUnit` 的 typedef。我们已经将它复制到 WeightUnits.h 中，重复定义只会导致编译错误。

最后，当默认单位改变时，我们需要更新 UI。幸运的是，只要 `NSUserDefaults` 的值发生变化，它就会发布 `NSUserDefaultsDidChangeNotification` 通知。我们只需要监听这个通知即可。

在 EnterWeightViewController.m 中，导航到 `viewDidLoad` 方法，并在方法底部添加以下代码。

```objc
    [[NSNotificationCenter defaultCenter]
    addObserverForName:NSUserDefaultsDidChangeNotification
    object:[NSUserDefaults standardUserDefaults]
    queue:nil
    usingBlock:^(NSNotification *note) {
        NSString* title = [WeightEntry stringForUnit:
            getDefaultUnits()];
        [self.unitsButton setTitle:title
            forState:UIControlStateNormal];
    }];
```

然后，在 `viewDidUnload` 方法中，我们需要注销自己。

```objc
    [[NSNotificationCenter defaultCenter]
    removeObserver:self];
```

在 GraphViewController 的 `viewDidLoad` 方法中，注册类似的通知。别忘了在 `viewDidUnload` 方法中也要注销。

```objc
    // Register to receive notifications when the default unit changes.
    [[NSNotificationCenter defaultCenter]
    addObserverForName:NSUserDefaultsDidChangeNotification
    object:[NSUserDefaults standardUserDefaults]
    queue:nil
    usingBlock:^(NSNotification *note) {
        [graphView
            setWeightEntries:self.weightHistory.weights
            andUnits:getDefaultUnits()];
    }];
```

我们还希望 HistoryViewController 也注册通知。同样，将以下代码添加到它的 `viewDidLoad` 方法中。和往常一样，记得在 `viewDidUnload` 方法中注销。

```objc
// Register to receive notifications when the user
// defaults change.
    [[NSNotificationCenter defaultCenter]
      addObserver:self
      selector:@selector(reloadTableData)
      name:NSUserDefaultsDidChangeNotification
      object:[NSUserDefaults standardUserDefaults]];
```

最后，我们要确保 EnterWeightController 视图以正确的单位启动。打开 EnterWeightViewController.m，导航到 `viewWillAppear:` 方法。添加以下代码。

```objc
- (void)viewWillAppear:(BOOL)animated {
    // Sets the current time and date.
    self.currentDate = [NSDate date];
    self.dateLabel.text =
      [NSDateFormatter
        localizedStringFromDate:self.currentDate
        dateStyle:NSDateFormatterLongStyle
        timeStyle:NSDateFormatterShortStyle];
    // Clear the text field.
    self.weightTextField.text = @"";
    [self.weightTextField becomeFirstResponder];
    [self.unitsButton
      setTitle:[WeightEntry stringForUnit:getDefaultUnits()]
      forState:UIControlStateNormal];
    [super viewWillAppear:animated];
}
```

项目现在应该可以无错误构建。尝试运行它。添加几条体重记录。更改默认单位。然后将应用发送到后台，再停止它。重新运行。它应该会同时记住体重记录和更改后的单位。

> **注意：** 将应用发送到后台会强制应用保存所有待处理的更改。另一方面，在 Xcode 中按下停止按钮会立即终止应用，使其没有机会保存状态。在测试任何基于文档的项目时，最好先让应用进入后台，然后再停止它。

![](img/fe9fea534a8e7868f811f7cd33da015f_363_0.png)

尝试在两台设备上运行该应用。在一台设备上添加一条新体重记录，然后将应用发送到后台。大约 30 秒内，你应该会看到新记录出现在第二台设备上。

尝试同时向两台设备添加新体重记录。将两个应用都发送到后台，然后再将它们带回前台。两个应用最初都应该显示各自独有的体重记录集。然后，一个应用将解决冲突，改为显示合并后的体重记录集。大约一分钟后，另一个应用也会随之更新。冲突就此解决。

请注意，应用的两个副本都在成功同步它们的体重历史记录，但它们并没有同步默认单位。我们来修复这个问题。

## 实现 iCloud 键值存储

我们希望继续使用 `NSUserDefaults` 在本地存储偏好设置；但是，我们可以使用 iCloud 键值存储来在这些机器之间同步这些默认设置。过程很简单。我们注册有关 iCloud 键值存储更改的通知。如果发生变化，我们就修改用户默认设置以保持同步。同样，我们监视用户默认设置。如果它们发生变化，我们就更新 iCloud 键值存储。此外，我们可以在我们的应用委托中完成所有这些工作。我们的视图控制器已经会对用户默认设置的任何更改做出响应。
