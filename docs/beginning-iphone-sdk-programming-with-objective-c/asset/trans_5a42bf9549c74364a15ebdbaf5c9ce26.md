
要处理操作表触发的事件，需要让视图控制器遵循 UIActionSheetDelegate 协议：

```objective-c
@interface UsingViewsViewController : UIViewController
    <UIActionSheetDelegate> {
    //...
}
```

要知道按下了哪个按钮，需要实现 actionSheet:clickedButtonAtIndex: 方法：

```objective-c
- (void)actionSheet:(UIActionSheet *)actionSheet
clickedButtonAtIndex:(NSInteger)buttonIndex {
    NSLog([NSString stringWithFormat:@"%@", buttonIndex]);
}
```

点击按钮的索引将通过 clickedButtonAtIndex: 参数传入。

## 页面控件与图像视图

在 iPhone 主屏幕上，你会在屏幕底部看到一系列点。点亮的点代表当前选中的页面。当你滑动到下一页时，下一个点会被点亮。在 iPhone SDK 中，这一串点由 UIPageControl 类表示。图 4-5 显示了页面控件在 iPhone 主屏幕上的作用。

在下面的练习中，你将学习如何在自己的应用程序中使用页面控件视图在 ImageView 视图中显示的图像之间切换。

![](img/aab2d775c46f70cd606f2e58e2521324_113_0.png)

- 4. 选择其中一个 ImageView 视图后，打开属性检查器窗口并将 Tag 属性设置为 0。选择第二个 ImageView 并将 Tag 属性设置为 1（见图 4-8）。

![](img/aab2d775c46f70cd606f2e58e2521324_115_0.png)

图 4-8

- 5. 将 Page Control 视图拖放到 View 窗口中，并将其页面数设置为五（见图 4-9）。

> **注意** 确保增加 Page Control 视图的宽度，以便五个点现在都可见。

![](img/aab2d775c46f70cd606f2e58e2521324_116_0.png)

图 4-9

- 6. 回到 Xcode，在 UsingViewsViewController.h 文件中，定义三个 outlet 和两个 UIImageView 对象：

```objective-c
#import <UIKit/UIKit.h>

@interface UsingViewsViewController : UIViewController {
    IBOutlet UIPageControl *pageControl;
    IBOutlet UIImageView *imageView1;
    IBOutlet UIImageView *imageView2;

    UIImageView *tempImageView, *bgImageView;
}

@property (nonatomic, retain) UIPageControl *pageControl;
@property (nonatomic, retain) UIImageView *imageView1;
@property (nonatomic, retain) UIImageView *imageView2;

@end
```

- 7. 在 Interface Builder 中，将三个 outlet 连接到 View 窗口上的视图。图 4-10 显示了为 imageView1、imageView2 和 pageControl outlet 建立的连接。

```objective-c
[super viewDidLoad];
}

//---when the page control's value is changed---
-(void) pageTurning: (UIPageControl *) pageController
{
    //---get the page number you can turning to---
    NSInteger nextPage = [pageController currentPage];
    switch (nextPage) {
        case 0:
            [tempImageView setImage:[UIImage imageNamed:@"iMac_old.jpeg"]];
            break;
        case 1:
            [tempImageView setImage:[UIImage imageNamed:@"iMac.jpeg"]];
            break;
        case 2:
            [tempImageView setImage:[UIImage imageNamed:@"Mac8100.jpeg"]];
            break;
        case 3:
            [tempImageView setImage:[UIImage imageNamed:@"MacPlus.jpeg"]];
            break;
        case 4:
            [tempImageView setImage:[UIImage imageNamed:@"MacSE.jpeg"]];
            break;
        default:
            break;
    }

    //---switch the two imageview views---
    if (tempImageView.tag==0) { //---imageView1---
        tempImageView = imageView2;
        bgImageView = imageView1;
    }
    else {  //---imageView2---
        tempImageView = imageView1;
        bgImageView = imageView2;
    }

    //---animate the two views flipping---
    [UIView beginAnimations:@"flipping view" context:nil];
    [UIView setAnimationDuration:0.5];
    [UIView setAnimationCurve:UIViewAnimationCurveEaseInOut];
    [UIView setAnimationTransition:UIViewAnimationTransitionFlipFromLeft
         forView:tempImageView cache:YES];
    [tempImageView setHidden:YES];
    [UIView commitAnimations];

    [UIView beginAnimations:@"flipping view" context:nil];
    [UIView setAnimationDuration:0.5];
    [UIView setAnimationCurve:UIViewAnimationCurveEaseInOut];
    [UIView setAnimationTransition:UIViewAnimationTransitionFlipFromRight
         forView:bgImageView cache:YES];
    [bgImageView setHidden:NO];
}
```

```objective-c
[UIView commitAnimations];
}

- (void)dealloc {
    [pageControl release];
    [imageView1 release];
    [imageView2 release];
    [super dealloc];
}

- (void)didReceiveMemoryWarning {
    // Releases the view if it doesn't have a superview.
    [super didReceiveMemoryWarning];
}

- (void)viewDidUnload {
}
@end
```

![](img/aab2d775c46f70cd606f2e58e2521324_119_0.png)

- 10. 按 Command-R 在 iPhone 模拟器上测试应用程序。当你点击屏幕底部的 Page Control 时，图像视图会翻转以显示下一个（见图 4-11）。

## 其工作原理

当 View 第一次加载时，你让其中一个 ImageView 视图显示图像，然后隐藏另一个：

```objective-c
//--initialize the first imageview to display an image--
[imageView1 setImage:[UIImage imageNamed:@"Mac_01d.jpeg"]];
tempImageView = imageView2;
```

```objective-c
//--make the first imageview visible and hide the second---
[imageView1 setHidden:NO];
[imageView2 setHidden:YES];
```

然后你将 Page Control 接线，以便当用户点击它时，会触发一个事件并触发一个方法。在这种情况下，会调用 pageTurning: 方法：

```objective-c
//--add the event handler for the page control---
[pageControl addTarget:self action:@selector(pageTurning:)
       forControlEvents:UIControlEventValueChanged];
[super viewDidLoad];
```

在 pageTurning: 方法中，你根据 Page Control 的值确定应加载哪个图像：

```objective-c
//--when the page control's value is changed--
- (void) pageTurning: (UIPageControl *) pageController
{
    //--get the page number you can turning to---
    NSInteger nextPage = [pageController currentPage];
```

## 使用分段控件对视图进行分组

分段控件是一个包含一系列按钮的水平视图。使用分段控件，用户可以点击其中任意一个按钮。这样做会取消先前选中的按钮的选中状态。

下面的“试一试”展示了如何使用分段控件将多个视图组合在一起。它还展示了如何使用此控件选择特定的一组视图。

## 试一试 使用分段控件

*代码文件 (UsingViews2.zip) 可在 Wrox.com 下载*

- 1. 使用 Xcode 创建一个新的基于视图的应用程序项目，并将其命名为 UsingViews2。
- 2. 双击 UsingViews2ViewController.xib 文件以使用 Interface Builder 编辑它。
- 3. 向 View 窗口添加以下视图（见图 4-12）：
  - 分段控件
  - 视图
  - 标签（确保它嵌入在视图内）
- 4. 在 View 窗口上再添加一个 View（来自库），然后向其添加一个 Label 视图（见图 4-13）。放置第二个视图时要小心——确保第二个视图不包含在第一个视图内。这是因为当你使用鼠标将第二个 View 拖到第一个 View 上时，Interface Builder 会认为你正试图将第二个 View 设为第一个 View 的子视图。为防止这种情况发生，使用光标移动

![](img/aab2d775c46f70cd606f2e58e2521324_121_0.png)

图 4-12

第二个视图覆盖在第一个视图上。View 窗口现在应如下图 4-13 所示。

- 5. 你可以通过以列表模式查看 UsingViews2ViewController.xib 窗口来验证两个 View 是否处于同一级别（见图 4-14）。

![](img/aab2d775c46f70cd606f2e58e2521324_122_0.png)

图 4-13

![](img/aab2d775c46f70cd606f2e58e2521324_122_1.png)

图 4-14

- 6. 在 UsingViews2ViewController.h 文件中，声明以下 outlet：

```objective-c
#import <UIKit/UIKit.h>

@interface UsingViews2ViewController : UIViewController {
IBOutlet UIView *view1;
IBOutlet UIView *view2;
IBOutlet UISegmentedControl *segmentedControl;
}

@property (nonatomic, retain) UIView *view1;
@property (nonatomic, retain) UIView *view2;
@property (nonatomic, retain) UISegmentedControl *segmentedControl;

@end
```

- 7. 回到 Interface Builder，将 outlet 连接到 View 窗口中的相应视图。（你可能需要移动两个 View，以便将两个 UIView outlet 连接到它们。）
