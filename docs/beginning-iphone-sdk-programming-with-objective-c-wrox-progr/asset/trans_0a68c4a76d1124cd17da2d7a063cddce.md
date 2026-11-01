
2. 按 Command-R 在 iPhone 模拟器上测试应用程序。
3. 在 iPhone 模拟器中，按下 Option 键，应会出现两个圆圈（见图 14-4）。点击屏幕可模拟两个手指触摸设备的屏幕。点击并移动鼠标可模拟捏合屏幕。
4. 打开调试器控制台窗口（按 Command-Shift-R）并在 Option-点击 iPhone 模拟器屏幕时观察输出：

![](img/16991b58db5894715c4a443315e06a22_356_0.png)

图 14-4

```text
2009-08-25 10:01:15.510 MultiTouch[2230:207] Touch1: 107, 201
2009-08-25 10:01:15.511 MultiTouch[2230:207] Touch2: 213, 239
2009-08-25 10:01:15.758 MultiTouch[2230:207] Touch1: 105, 201
2009-08-25 10:01:15.759 MultiTouch[2230:207] Touch2: 215, 239
2009-08-25 10:01:15.918 MultiTouch[2230:207] Touch1: 105, 239
2009-08-25 10:01:15.919 MultiTouch[2230:207] Touch2: 105, 201
2009-08-25 10:01:16.054 MultiTouch[2230:207] Touch1: 105, 201
2009-08-25 10:01:16.055 MultiTouch[2230:207] Touch2: 215, 239
2009-08-25 10:01:16.238 MultiTouch[2230:207] Touch1: 105, 201
2009-08-25 10:01:16.239 MultiTouch[2230:207] Touch2: 215, 239
```

> **NOTE** 使用 iPhone 模拟器时，当你在 iPhone 模拟器屏幕的同一位置进行 Option-点击时，两个触摸的坐标经常会被互换。

## 工作原理

在检测单点触控时所做的那样，你在 touchesBegan:withEvent: 事件中检查多点触控。与仅接收第一个触摸的信息不同，现在你将获得第一个和第二个触摸的信息：

```objc
//---get info of first touch---
UITouch *touch1 = [[allTouches allObjects] objectAtIndex:0];

//---get info of second touch---
UITouch *touch2 = [[allTouches allObjects] objectAtIndex:1];
```

> **NOTE** 基本上，要检测两个以上的触摸，只需通过获取第三个触摸、第四个触摸等的信息来扩展前面的代码即可。

要获取每个触摸的坐标（表示为 CGPoint 结构），你使用 UITouch 类的 locationInView: 方法，并将它当前所在的视图传递给它：

```objc
//---get the points touched---
CGPoint touch1PT = [touch1 locationInView:[self view]];
CGPoint touch2PT = [touch2 locationInView:[self view]];
```

locationInView: 方法返回的坐标相对于指定的视图。在前面的代码片段中，显示的坐标相对于主 View 窗口。

CGPoint 结构的 x 和 y 坐标使用 CGFloat 类型表示，因此在调试器控制台窗口中打印它们时，你需要使用 %f 格式说明符：

```objc
NSLog(@"Touch1: %.0f, %.0f", touch1PT.x, touch1PT.y);
NSLog(@"Touch2: %.0f, %.0f", touch2PT.x, touch2PT.y);
```

需要理解的一点重要事项是，显示的坐标值相对于指定的视图。图 14-5 显示，当相对于主 View 窗口引用时，左上角的坐标为 (0,-20)，右下角的坐标为 (320,460)：

```objc
//---get the points touched---
CGPoint touch1PT = [touch1 locationInView:[self view]];
CGPoint touch2PT = [touch2 locationInView:[self view]];
```

![](img/16991b58db5894715c4a443315e06a22_357_0.png)

图 14-5

假设 image view 的大小缩小到图 14-6 所示的大小（请记住它当前填满整个屏幕）。如果你相对于 imageView 视图引用，(0,0) 位置将从 image view 的左上角开始。所有位于 (0,0) 点左上方的其他点都将具有负的 x 和 y 坐标：

```objc
//---get the points touched---
CGPoint touch1PT = [touch1 locationInView:imageView];
CGPoint touch2PT = [touch2 locationInView:imageView];
```

![](img/16991b58db5894715c4a443315e06a22_358_0.png)

图 14-6

## 实现捏合手势

现在你知道了在应用程序中检测多点触控的技术，你可以编写一些使用多点触控的很酷的应用程序。一个很酷的例子是实现著名的 iPhone 捏合手势，使其区别于竞争对手。

使用捏合手势，你将两个手指放在屏幕上并通过将两个手指相互靠近来捏合。当将此手势应用于正在查看的照片或 Mobile Safari 中的网页等时，这通常会转换为缩放出操作。当你将两个手指分开时，你会放大照片或网页。

要在图像上使用捏合手势，你实际上需要先放大图像。这是因为只有在显示模式设置为 UIViewContentModeScaleAspectFit 时，图像才能被调整大小。因此，在这种情况下，你需要在尝试捏合效果之前先单击图像（这实际上将图像模式设置为 UIViewContentModeScaleAspectFit）。

在下面的“试一试”中，你将学习如何实现捏合手势以在 image view 中放大和缩小图像。

## 试一试 缩放进出

1. 使用之前创建的同一项目，将以下以粗体显示的语句添加到 MultiTouchViewController.h 文件中：

```objc
#import <UIKit/UIKit.h>

@interface MultiTouchViewController : UIViewController {
    IBOutlet UIImageView *imageView;
}

@property (nonatomic, retain) UIImageView *imageView;

-(CGFloat) distanceBetweenTwoPoints: (CGPoint)fromPoint toPoint: (CGPoint)toPoint;

@end
```

2. 在 MultiTouchViewController.m 文件中，实现 distanceBetweenTwoPoints:toPoint: 和 touchesMoved:withEvent: 方法，并将以粗体显示的语句添加到 touchesBegan:withEvent: 方法中：

```objc
#import "MultiTouchViewController.h"

@implementation MultiTouchViewController

@synthesize imageView;

CGFloat originalDistance;

-(CGFloat) distanceBetweenTwoPoints:(CGPoint)fromPoint toPoint:(CGPoint)toPoint {
    float lengthX = fromPoint.x - toPoint.x;
    float lengthY = fromPoint.y - toPoint.y;
    return sqrt((lengthX * lengthX) + (lengthY * lengthY));
}

-(void) touchesBegan: (NSSet *) touches withEvent: (UIEvent *) event {
    //---get all touches on the screen---
    NSSet *allTouches = [event allTouches];

    //---compare the number of touches on the screen---
    switch ([allTouches count])
    {
        //---single touch---
        case 1:
            //---get info of the touch---
            UITouch *touch = [[allTouches allObjects] objectAtIndex:0];

            //---compare the touches---
            switch ([touch tapCount])
            {
                //---single tap---
                case 1: {
                    imageView.contentMode = UIViewContentModeScaleAspectFit;
                } break;

                case 2: {
                    imageView.contentMode = UIViewContentModeCenter;
                } break;
            } break;

        //---double-touch---
        case 2: {
            //---get info of first touch---
            UITouch *touch1 = [[allTouches allObjects] objectAtIndex:0];
            //---get info of second touch---
            UITouch *touch2 = [[allTouches allObjects] objectAtIndex:1];

            //---get the points touched---
            CGPoint touch1PT = [touch1 locationInView:[self view]];
            CGPoint touch2PT = [touch2 locationInView:[self view]];

            NSLog(@"Touch1: %.0f, %.0f", touch1PT.x, touch1PT.y);
            NSLog(@"Touch2: %.0f, %.0f", touch2PT.x, touch2PT.y);

            //---record the distance made by the two touches---
            originalDistance = [self distanceBetweenTwoPoints:touch1PT
                                toPoint: touch2PT];
        } break;
    }
}

//---fired when the user moved his finger(s) on the screen---
-(void) touchesMoved: (NSSet *) touches withEvent: (UIEvent *) event {

    //---get all touches on the screen---
    NSSet *allTouches = [event allTouches];

    //---compare the number of touches on the screen---
    switch ([allTouches count])
    {
        //---single touch---
        case 1: {
        } break;

        //---double-touch---
        case 2: {
            //---get info of first touch---
            UITouch *touch1 = [[allTouches allObjects] objectAtIndex:0];

            //---get info of second touch---
            UITouch *touch2 = [[allTouches allObjects] objectAtIndex:1];

            //---get the points touched---
```
