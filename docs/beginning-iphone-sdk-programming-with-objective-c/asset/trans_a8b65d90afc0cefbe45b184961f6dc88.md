

由于属性的值会被保留，因此在退出应用程序之前释放它非常重要。一个合适的释放位置是类的 `dealloc` 方法（例如视图控制器）：

```
-(void) dealloc {
    [self.name release];    //---释放name属性---
    [super dealloc];
}
```

当对象的引用计数达到 0 时，类的 `dealloc` 方法就会被触发。
考虑下面的示例：

```
SomeClass *sc1 = [[SomeClass alloc] initWithName:@"Wei-Meng Lee" andRate:35];
//...在这里做一些操作...
[sc1 release];  //---引用计数变为0；dealloc将被调用---
```

前面的示例显示，当 `sc1` 的引用计数变为 0（即调用 `release` 语句）时，类中定义的 `dealloc` 方法将被调用。如果你没有在类中定义这个方法，则会调用基类中的实现。

## 内存管理提示

内存管理是 iPhone 编程中的一个棘手问题。虽然有一些工具可以用来测试内存泄漏，但本节将介绍一些简单的方法，帮助你检测可能影响应用程序的内存问题。

首先，确保你在视图控制器中实现了 `didReceiveMemoryWarning` 方法：

```
- (void)didReceiveMemoryWarning {
    //---在此处插入代码以释放未使用的对象---
    [super didReceiveMemoryWarning];
}
```

当你的 iPhone 内存不足时，`didReceiveMemoryWarning` 方法将被调用。你应该在此方法中插入代码，以便释放不需要的资源/对象。

此外，你还应该在应用程序委托中处理 `applicationDidReceiveMemoryWarning:` 方法：

```
- (void)applicationDidReceiveMemoryWarning:(UIApplication *)application
{
    //---在此处插入代码以释放未使用的对象---
    [[ImageCache sharedImageCache] removeAllImagesInMemory];
}
```

在此方法中，你应该停止所有内存密集型活动，例如音频和视频播放。你还应该移除所有缓存到内存中的图片。

如果你想实现 `UIAlertViewDelegate` 协议中的任何方法，你需要确保你的类（在这里是视图控制器）遵循该协议。类使用尖括号（<>）来遵循协议，如下所示：

```objc
@interface UsingViewsViewController : UIViewController
<UIAlertViewDelegate> { //----这个类遵循UIAlertViewDelegate
//协议---
}
```

> 注意 要遵循多个委托，请用逗号分隔各个协议，例如 `<UIAlertViewDelegate, UITableViewDataSource>`。

类遵循协议后，你就可以在类中实现该方法：

```objc
- (void)alertView:(UIAlertView *)alertView
clickedButtonAtIndex:(NSInteger)buttonIndex {
    NSLog([[NSString stringWithFormat:@"%d", buttonIndex]]);
}
```

## 委托

在 Objective-C 中，委托只是一个对象，由另一个对象指定为负责处理事件的对象。考虑你之前见过的 `UIAlertView` 示例：

```objc
UIAlertView *alert = [[UIAlertView alloc]
    initWithTitle:@"Hello"
    message:@"This is an alert view"
    delegate:self
    cancelButtonTitle:@"OK"
    otherButtonTitles:nil];
```

`UIAlertView` 类的初始化方法包含一个名为 `delegate` 的参数。将此参数设置为 `self` 意味着当前对象负责处理由这个 `UIAlertView` 类实例触发的所有事件。如果你不需要处理此实例触发的事件，只需将其设置为 `nil`：

```objc
UIAlertView *alert = [[UIAlertView alloc]
    initWithTitle:@"Hello"
    message:@"This is an alert view"
    delegate:nil
    cancelButtonTitle:@"OK"
    otherButtonTitles:nil];
```

`action:` 参数接收一个类型为 `SEL`（选择器）的参数。在前面的代码中，你传入的是你定义的方法名——`buttonClicked:`——该方法定义在类中：

```
- (IBAction) buttonClicked: (id) sender{
    //...
}
```

或者，你可以创建一个 `SEL` 类型的对象，然后使用 `NSSelectorFromString` 函数（该函数接受一个包含方法名的字符串）来实例化它：

```
NSString *nameOfMethod = @"buttonClicked:";
SEL methodName = NSSelectorFromString(nameOfMethod);
```

现在，对 `addTarget:action:forControlEvents:` 方法的调用如下所示：

```
[button addTarget:self action:methodName
forControlEvents:UIControlEventTouchUpInside];
```

> 注意 命名选择器时，请务必指定方法的完整名称。例如，如果方法名包含一个或多个参数，你需要在选择器中添加“:”，例如：
> 
> NSString *nameOfMethod = @"someMethod:withPara1:andPara2:";

> 注意 由于 Objective-C 是 C 语言的扩展，在 Objective-C 应用程序中经常可以看到 C 函数穿插其中。C 函数使用圆括号 () 来传递参数。

## 类别

Objective-C 中的类别允许你向现有类添加方法，而无需创建其子类。你也可以使用类别来覆盖现有类的实现。

> 注意 在某些语言（如 C#）中，类别被称为扩展方法。

例如，假设你想测试一个字符串是否包含有效的电子邮件地址。你可以向 `NSString` 类添加一个 `isEmail` 方法，以便在任何 `NSString` 实例上调用 `isEmail` 方法，如下所示：

```objc
NSString *email = @"weiminglee@gmail.com";
if ([email isEmail])
{
    //...
}
```

要做到这一点，你只需创建一个新的类文件，并按如下方式编写代码：

```objc
//---utils.h---
#import <Foundation/Foundation.h>
//---NSString是你要扩展的类---
@interface NSString (stringUtils)
//---你要添加到NSString类的方法---
- (BOOL) isEmail;
@end
```

基本上，这看起来与声明一个新类相同，只是它不继承自任何其他类。`stringUtils` 是一个名称，用于标识你要添加的类别，你可以使用任何你想要的名称。

接下来，你需要实现你要添加的方法：

```objc
//---utils.m---
#import "Utils.h"
@implementation NSString (Utilities)
- (BOOL) isEmail
{
NSString *emailRegEx = @"...";
NSPredicate *regExPredicate = [NSPredicate predicateWithFormat:@"SELF MATCHES %@", emailRegEx];
return [regExPredicate evaluateWithObject:self];
}
@end
```

> 注意 使用正则表达式验证电子邮件地址的代码改编自 http://cocoawithlove.com/2009/06/verifying-that-string-is-email-address.html。

然后，你可以使用新添加的方法来测试电子邮件地址的有效性：

```objc
NSString *email = @"weimenglee@gmail.com";
if ([email isEmail])
    NSLog(@"Valid email");
else
    NSLog(@"Invalid email");
```

## 总结

在本附录中，你了解了 Objective-C 语言的概貌。虽然它并未全面涵盖该语言，但提供了足够的信息，帮助你开始 iPhone 编程。

## 在真实的 iPhone 或 iPod Touch 上进行测试

虽然 iPhone 模拟器是一个非常方便的工具，可以让你无需真实设备即可测试 iPhone 应用程序，但在真实设备上进行测试是无可替代的。当你准备将应用程序推向世界时尤其如此——你必须确保它在真实设备上能正确运行。此外，如果你的应用程序需要访问 iPhone/iPod Touch 的硬件功能，例如加速度计和 GPS，你需要在真实设备上进行测试——仅靠 iPhone 模拟器是不够的。

本附录将引导你完成在真实设备（无论是 iPhone 还是 iPod Touch）上测试 iPhone 应用程序所需的步骤。

## 注册 iPhone 开发者计划

在真实设备上测试应用程序的第一步是注册 iPhone 开发者计划，网址为 http://developer.apple.com/iphone/program/。有两种计划可供选择：标准版和企业版。对于大多数想在 App Store 上发布应用程序的开发者来说，费用为 99 美元的标准版计划就足够了。请访问 http://developer.apple.com/iphone/program/apply.html 了解标准版和企业版计划之间的更多差异。

如果你只想在你自己的 iPhone/iPod Touch 上测试应用程序，请注册标准版计划。

