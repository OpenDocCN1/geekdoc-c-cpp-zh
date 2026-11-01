

UIAlertViewDelegate 协议包含与警告视图相关的多个方法。要确定用户点击了哪个按钮，你需要实现 `alertView:clickedButtonAtIndex:` 方法：

```objc
- (void)alertView:(UIAlertView *)alertView clickedButtonAtIndex:
(NSUInteger)buttonIndex {
    NSLog([NSString stringWithFormat:@"%d", buttonIndex]);
}
```

被点击按钮的索引将通过 `clickedButtonAtIndex:` 参数传入。

> 注意：关于 Objective-C 中协议概念的讨论，请参阅附录 D。

## 使用操作表（Action Sheet）

虽然警告视图可以显示多个按钮，但其主要用途仍是在发生某些事件时提醒用户。如果你需要显示一条包含多个选项供用户选择的消息，应使用操作表（Action Sheet）而不是警告视图。操作表显示一组按钮，用户可从中选择一个。

要使用操作表，请参考下面的代码片段：

```objc
UIActionSheet *action = [[UIActionSheet alloc]
    initWithTitle:@"Title of Action Sheet"
    delegate:self
    cancelButtonTitle:@"OK"
    destructiveButtonTitle:@"Delete Message"
    otherButtonTitles:@"Option 1", @"Option 2", nil];
[action showInView:self.view];
[action release];
```

要处理点击操作表中某个按钮时触发的事件，需要在视图控制器中实现 `UIActionSheetDelegate` 协议，如下所示：

```objc
#import <UIKit/UIKit.h>

@interface UsingViewsViewController : UIViewController
<UIActionSheetDelegate> {
}
```

当某个按钮被点击时，会触发 `actionSheet:clickedButtonAtIndex:` 事件：

```objc
- (void)actionSheet:(UIActionSheet *)actionSheet
clickedButtonAtIndex:(NSInteger)buttonIndex{

    NSLog([NSString stringWithFormat:@"%d", buttonIndex]);
}
```

图 3-9 展示了操作表显示时的样子。

请注意，OK 按钮（如方法中 `cancelButtonTitle:` 部分所指定的）并未显示。每个按钮对应的值（`buttonIndex`）如下：

- 删除消息（Delete Message）— 0
- 选项 1（Option 1）— 1
- 选项 2（Option 2）— 2

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_92_0.png)

当用户点击操作表之外的区域时，操作表会被关闭，此时 `buttonIndex` 的值变为 3。有趣的是，如果你在 `cancelButtonTitle:` 部分指定为 `nil`，那么当操作表被关闭时，`buttonIndex` 的值将是 −1。

## 页面控件与图像视图

在 iPad 主屏幕的底部附近有一系列圆点（见图 3-10）。发光的圆点代表当前选中的页面。当你滑动页面到下一页时，下一个圆点会亮起，而第一个圆点会变暗。在图中，这些圆点表示第三个页面是当前活动页。在 iPhone SDK 中，这一系列圆点由 `UIPageControl` 类表示。

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_92_1.png)

在下面的练习中，你将学习如何在自有应用中使用页面控件视图，在图像视图（ImageView）显示的图像之间进行切换。

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_93_0.png)

## 构建高可用的档案系统架构

文件存储是一种比较传统的存储方案，叫做 SAN（Storage Area Network，存储区域网络）和 NAS（Network Attached Storage，网络附加存储）。

在业务比较简单的时代，这个方案基本可以很好的支撑业务，但是随着业务数据量的增长，这种传统存储方案逐渐暴露出很多问题，最核心的问题是成本太高，因为需要通过购买高端服务器和磁盘阵列来提升存储性能，这样的成本往往是普通中小企业无法承受的。

另外，如果 NAS 和 SAN 中的某一台服务器出现故障，会导致整个系统不可用。为了解决这些问题，业界提出了`软件定义存储`的概念，SDS 的核心在于基于通用的硬件，通过软件定义存储的解决方案，降低存储成本，并通过软件层面数据副本机制，保证数据的高可靠。

接下来我们看一下国内的软件定义存储市场的整体情况，这里我列举了部分做存储厂商，其中包含一些老牌存储厂商，也有云厂商，比如华为、阿里云、腾讯云等，还有一些创业公司。

| 厂商 | 产品 | 类型 |
| --- | --- | --- |
| 华为 | OceanStor | 老牌存储厂商 |
| 阿里云 | 云盘 | 云厂商 |
| 腾讯云 | CBS | 云厂商 |
| 七牛云 | Kodo | 云厂商 |
| 杉岩数据 | USP | 创业公司 |
| XSKY | XStor | 创业公司 |

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_95_0.png)

图 3-15

- 8. 在 Interface Builder 中，将三个出口（outlet）连接到 View 窗口上的视图。图 3-16 显示了为 `imageView1`、`imageView2` 和 `pageControl` 出口所做的连接。

- 9. 现在你可以重新排列 View 窗口上的图像视图，使它们彼此重叠。

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_95_1.png)

图 3-16

10. 在 Xcode 中，将以下以粗体显示的语句添加到 `UsingViewsViewController.m` 文件中：

```objc
#import "UsingViewsViewController.h"

@implementation UsingViewsViewController

@synthesize pageControl;
@synthesize imageView1, imageView2;

- (void)viewDidLoad {
    //---initialize the first ImageView to display an image---
    [imageView1 setImage:[UIImage imageNamed:@"iMac_old.jpeg"]];
    tempImageView = imageView2;

    //---make the first ImageView visible and hide the second---
    [imageView1 setHidden:NO];
    [imageView2 setHidden:YES];

    //---add the event handler for the page control---
    [pageControl addTarget:self
                    action:@selector(pageTurning:)
          forControlEvents:UIControlEventValueChanged];

    [super viewDidLoad];
}

//---when the page control's value is changed---
- (void) pageTurning: (UIPageControl *) pageController {

    //---get the page number you can turning to---
    NSInteger nextPage = [pageController currentPage];
    switch (nextPage) {
        case 0:
            [tempImageView setImage:
                [UIImage imageNamed:@"iMac_old.jpeg"]];
            break;
        case 1:
            [tempImageView setImage:
                [UIImage imageNamed:@"iMac.jpeg"]];
            break;
        case 2:
            [tempImageView setImage:
                [UIImage imageNamed:@"Mac8100.jpeg"]];
            break;
        case 3:
            [tempImageView setImage:
                [UIImage imageNamed:@"MacPlus.jpeg"]];
            break;
        case 4:
            [tempImageView setImage:
                [UIImage imageNamed:@"MacSE.jpeg"]];
            break;
    }
}
```

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_98_0.png)

图 3-17

## 工作原理

当视图首次加载时，你先让其中一个图像视图显示图像，然后隐藏另一个：

```objc
//---initialize the first ImageView to display an image---
[imageView1 setImage:[UIImage imageNamed:@"iMac_old.jpeg"]];
tempImageView = imageView2;

//---make the first ImageView visible and hide the second---
[imageView1 setHidden:NO];
[imageView2 setHidden:YES];
```

然后，你将页面控件（Page Control）连接起来，使用户点击它时会触发一个事件并调用一个方法。在本例中，调用的是 `pageTurning:` 方法：

```objc
//---add the event handler for the page control---
[pageControl addTarget:self
    action:@selector(pageTurning:)
    forControlEvents:UIControlEventValueChanged];
```

在 `pageTurning:` 方法中，你根据页面控件的值来确定应加载哪张图像：

```objc
//---when the page control's value is changed---
- (void) pageTurning: (UIPageControl *) pageController {
    //---get the page number you can turning to---
    NSInteger nextPage = [pageController currentPage];
    switch (nextPage) {
        case 0:
            [tempImageView setImage:
                [UIImage imageNamed:@"iMac_old.jpeg"]];
            break;
        case 1:
            [tempImageView setImage:
                [UIImage imageNamed:@"iMac.jpeg"]];
            break;
        case 2:
            [tempImageView setImage:
                [UIImage imageNamed:@"Mac8100.jpeg"]];
            break;
        case 3:
            [tempImageView setImage:
                [UIImage imageNamed:@"MacPlus.jpeg"]];
            break;
        case 4:
            [tempImageView setImage:
                [UIImage imageNamed:@"MacSE.jpeg"]];
            break;
        default:
            break;
    }
    //...
}
```

然后，你通过使用 `UIView` 类中的各种方法来切换两个图像视图并为其添加动画效果：

```objc
//---switch the two ImageView views---
if (tempImageView.tag==0) { //---imageView1---
    tempImageView = imageView1;
    bgImageView = imageView1;
}
else {   //---imageView2---
    tempImageView = imageView1;
    bgImageView = imageView2;
}

//---animate the two views flipping---
```

