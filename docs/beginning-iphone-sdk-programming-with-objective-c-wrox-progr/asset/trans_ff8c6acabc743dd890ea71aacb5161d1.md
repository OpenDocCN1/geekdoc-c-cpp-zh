
## 协议

在 Objective-C 中，*协议* 声明了一个可编程接口，任何类都可以选择实现它。协议声明了一组方法，采用该协议的类可以选择实现其中一个或多个声明的方法。定义协议的类预计会调用由采用类实现的协议中的方法。

理解协议最简单的方法是检查 *UIAlertView* 类。正如你在本书各章节中所经历的，你只需创建 *UIAlertView* 类的一个实例，然后调用其 *show* 方法即可简单使用它：

```
UIAlertView *alert = [[UIAlertView alloc]
    initWithTitle:@"Hello"
    message:@"This is an alert view"
    delegate:self
    cancelButtonTitle:@"OK"
    otherButtonTitles:nil];
[alert show];
```

前面的代码显示了一个带有单个按钮 — OK — 的警告视图。点击 OK 按钮会自动关闭警告视图。如果你想显示额外的按钮，可以像这样设置 *otherButtonTitles:* 参数：

```
UIAlertView *alert = [[UIAlertView alloc]
    initWithTitle:@"Hello"
    message:@"This is an alert view"
    delegate:self
    cancelButtonTitle:@"OK"
    otherButtonTitles:@"Option 1", @"Option 2", nil];
```

警告视图现在显示三个按钮 — OK、Option 1 和 Option 2。但是你如何知道用户点击了哪个按钮？你可以通过处理警告视图在按钮被点击时触发的相关方法(s)来确定这一点。这组方法由 *UIAlertViewDelegate* 协议定义。该协议定义了以下方法：

- alertView:clickedButtonAtIndex:
- willPresentAlertView:
- didPresentAlertView:
- alertView:willDismissWithButtonIndex:
- alertView:didDismissWithButtonIndex:
- alertViewCancel:

action: 参数接收类型为 SEL（选择器）的参数。在前面的代码中，你传入了你定义的方法的名称 — buttonClicked: — 该方法在类中定义：

```objc
- (IBAction) buttonClicked: (id) sender{
    //...
}
```

或者，你可以创建一个类型为 SEL 的对象，然后使用 NSSelectorFromString 函数实例化它（该函数接收包含方法名称的字符串）：

```objc
NSString *nameOfMethod = @"buttonClicked:";
SEL methodName = NSSelectorFromString(nameOfMethod);
```

对 addTarget:action:forControlEvents: 方法的调用现在看起来像这样：

```objc
[button addTarget:self action:methodName
forControlEvents:UIControlEventTouchUpInside];
```

> **注意** 为选择器命名时，请务必指定方法的全名。例如，如果方法名有一个或多个参数，你需要在选择器中添加 ":"，例如：
>
> ```objc
> NSString *nameOfMethod = @"someMethod:withPara1:andPara2:";
> ```

> **注意** 由于 Objective-C 是 C 的扩展，在你的 Objective-C 应用程序中常见到 C 函数穿插其中。C 函数使用圆括号 () 来传递参数的参数。

## 类别

Objective-C 中的类别允许你在无需子类化的情况下向现有类添加方法。你也可以使用类别来覆盖现有类的实现。

> **注意** 在某些语言（如 C#）中，类别被称为扩展方法。

例如，假设你想测试一个字符串是否包含有效的电子邮件地址。你可以将 isEmail 方法添加到 NSString 类，以便你可以像这样在任何 NSString 实例上调用 isEmail 方法：

```
NSString *email = @"weimenglee@gmail.com";
if ([email isEmail])
{
    //...
}
```

为此，你只需创建一个新的类文件并按如下方式编码：

```
//---utils.h---
#import <Foundation/Foundation.h>
//---NSString is the class you are extending---
@interface NSString (stringUtils)
//---the method you are adding to the NSString class---
- (BOOL) isEmail;
@end
```

基本上，它看起来与声明一个新类相同，只是它不继承自任何其他类。stringUtils 是标识你要添加的类别的名称，你可以使用任何你想要的名称。

接下来，你需要实现你要添加的方法：

```
//---utils.m---
#import "Utils.h"
@implementation NSString (Utilities)
- (BOOL) isEmail
{
    NSString *emailRegEx = @"^([a-z0-9!#$%&'*+/=?^_`{|}~-]+(?:\.[a-z0-9!#$%&'*+/=?^_`{|}~-]+)*|\"(?:[\x01-\x08\x0b\x0c\x0e-\x1f\x21\x23-\x5b\x5d-\x7f]|\\[\x01-\x09\x0b\x0c\x0e-\x7f])*\")@(?:(?:[a-z0-9](?:[a-z0-9-]*[a-z0-9])?\.)+[a-z0-9](?:[a-z0-9-]*[a-z0-9])?|\[(?:(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.){3}(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?|[a-z0-9-]*[a-z0-9](?:\:[a-z0-9-]*[a-z0-9])?:\d{1,5}\])";
    NSPredicate *regExPredicate = [NSPredicate predicateWithFormat:@"SELF MATCHES %@", emailRegEx];
    return [regExPredicate evaluateWithObject:self];
}
@end
```

> **注意** 使用正则表达式验证电子邮件地址的代码改编自 http://cocoawithlove.com/2009/06/verifying-that-string-is-email-address.html。

然后你可以使用新添加的方法来测试电子邮件地址的有效性：

```
NSString *email = @"weimenglee@gmail.com";
if ([email isEmail])
    NSLog(@"Valid email");
else
    NSLog(@"Invalid email");
```

## 摘要

在本附录中，你对 Objective-C 语言有了一个概述。虽然它没有全面涵盖该语言，但它提供了足够的信息供你开始 iPhone 编程。

## 论文排版格式说明

本文档用于说明本课程论文的排版格式要求，包括字体、字号、行距、页边距以及各级标题的样式规范。请各位同学严格按照以下要求进行排版。

### 一、总体要求

- 正文字数要求：不少于 5000 字。
- 论文须包含题目、摘要、关键词、正文、参考文献等部分。
- 全文需保持格式统一，行文流畅，逻辑清晰。

### 二、字体与字号

| 项目 | 字体 | 字号 | 行距 |
| --- | --- | --- | --- |
| 正文 | 宋体 | 小四 | 1.5 倍 |
| 一级标题 | 黑体 | 四号 | 1.5 倍 |
| 二级标题 | 黑体 | 小四 | 1.5 倍 |
| 图表标题 | 宋体 | 五号 | 单倍 |

注：表格内容一律使用五号宋体，表头使用黑体五号。

![](img/16991b58db5894715c4a443315e06a22_514_0.png)

**图 E-2**

在钥匙串访问应用程序中，选择钥匙串访问 ⌘ 证书助理并选择从证书颁发机构请求证书（参见图 E-3）。

![](img/16991b58db5894715c4a443315e06a22_514_1.png)

**图 E-3**

在证书助理窗口中（参见图 E-4），输入你的电子邮件地址，选择保存到磁盘单选按钮，并选择让我指定密钥对信息复选框。点击继续。

![](img/16991b58db5894715c4a443315e06a22_515_0.png)

**图 E-4**

选择 2048 位的密钥大小并选择 RSA 算法（参见图 E-5）。点击继续。

![](img/16991b58db5894715c4a443315e06a22_515_1.png)

**图 E-5**

系统会要求你将请求保存到文件。使用建议的默认名称并点击保存（参见图 E-6）。

![](img/16991b58db5894715c4a443315e06a22_516_0.png)

**图 E-6**

## 登录 iPhone 开发者计划门户

生成证书签名请求后，你需要登录苹果的 iPhone Dev Center（参见图 E-7）。点击页面右侧的 iPhone 开发者计划门户链接。记住，你需要支付 $99 才能访问此页面。

> **警告** 请务必尽早注册，因为审批过程需要一段时间 — 从几个小时到几天不等。

![](img/16991b58db5894715c4a443315e06a22_516_1.png)

**图 E-7**

在 iPhone 开发者计划门户页面上，点击启动助手按钮（参见图 E-8），以引导你完成为 iPhone 配置描述文件并生成开发证书的过程。

![](img/16991b58db5894715c4a443315e06a22_517_0.png)

**图 E-8**

你应该会看到欢迎页面。点击继续。

首先，你需要创建一个 App ID（参见图 E-9）。App ID 是一串字符，用于唯一标识 iPhone 上的应用程序（或应用程序）。输入一个友好的名称来描述此 App ID（由 Apple 生成）。点击继续。

