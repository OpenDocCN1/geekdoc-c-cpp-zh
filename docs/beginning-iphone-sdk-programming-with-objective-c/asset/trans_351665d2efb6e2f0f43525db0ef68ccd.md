
## 15

## 简单动画

## 本章你将学习的内容

- 如何使用 `NSTimer` 类创建定时器，使其在固定的时间间隔内调用方法
- 如何使用 `NSTimer` 类执行一些简单的动画
- 如何对 `ImageView` 执行仿射变换
- 如何使用 `ImageView` 动画化一系列图像

到目前为止，你所编写的应用程序都使用了 iPhone SDK 提供的标准视图。正如苹果所重申的那样，iPhone 和 iPod Touch 不仅仅是手机。iPhone 也是一个音乐播放器，而且对本章而言更重要的是，iPhone 也是一个游戏平台。

在本章中，你可以尽情发挥并创建一些视觉效果。你将学习如何使用定时器对象执行一些简单动画，然后对视图执行一些变换。虽然本书的范围超出了使用 OpenGL 创建动画的范畴，但本章确实展示了一些有趣的技术，可用于让你的应用程序栩栩如生！

## 使用 NSTIMER 类

开始动画的最简单方法之一是使用 NSTimer 类。NSTimer 类创建定时器对象，可让你在固定的时间间隔内调用方法。使用 NSTimer 对象，你可以定期更新图像，从而营造出图像正在动画的效果。

5. 选择 View（ImageView 外部）并将背景颜色更改为黑色（见图 15-2）。

![](img/aab2d775c46f70cd606f2e58e2521324_370_0.png)

图 15-2

6. 从库中向 View 窗口添加一个 Label 和一个 Slider 视图（见图 15-3）。将 Slider 视图的 Initial 属性设置为 0.01。

![](img/aab2d775c46f70cd606f2e58e2521324_370_1.png)

图 15-3

7. 在 AnimationViewController.h 文件中，声明以下 outlets、actions 和字段：

```
#import <UIKit/UIKit.h>

@interface AnimationViewController : UIViewController {
IBOutlet UIImageView *imageView;
IBOutlet UISlider *slider;

CGPoint position;
NSTimer *timer;

float ballRadius;
}
@property (nonatomic, retain) UIImageView *imageView;
@property (nonatomic, retain) UISlider *slider;

-(IBAction) sliderMoved:(id) sender;

@end
```

8. 返回 Interface Builder，按图 15-4 所示连接 outlets 和 actions。

![](img/aab2d775c46f70cd606f2e58e2521324_371_0.png)

图 15-4

9. 在 AnimationViewController.m 文件中，添加以下以粗体显示的语句：

```
#import "AnimationViewController.h"
@implementation AnimationViewController

@synthesize imageView;
@synthesize slider;

-(void) onTimer {
    imageView.center = CGPointMake(
        imageView.center.x + position.x,
        imageView.center.y + position.y);
    if (imageView.center.x > 320 - ballRadius || imageView.center.x < ballRadius)
        position.x = -position.x;
    if (imageView.center.y > 460 - ballRadius || imageView.center.y < ballRadius)
        position.y = -position.y;
}

-(void)viewDidLoad {
    ballRadius = imageView.frame.size.width/2;
    [slider setShowValue:YES];
    position = CGPointMake(12.0,4.0);
    timer = [NSTimer scheduledTimerWithTimeInterval:slider.value
                                              target:self
                                            selector:@selector(onTimer)
                                            userInfo:nil
                                             repeats:YES];
    [super viewDidLoad];
}

-(IBAction) sliderMoved:(id) sender {
    [timer invalidate];
    timer = [NSTimer scheduledTimerWithTimeInterval:slider.value
                                              target:self
                                            selector:@selector(onTimer)
                                            userInfo:nil
                                             repeats:YES];
}

-(void)didReceiveMemoryWarning {
    [super didReceiveMemoryWarning];
}

-(void)dealloc {
    [timer invalidate];
}
```

为了使动画更流畅，你可以在动画块内对设置视图的 center 属性所引起的视觉变化进行动画处理。动画块的开始由 UIView 类的 beginAnimations:context: 类方法定义：

```
[UIView beginAnimations:@"my_own_animation" context:nil];
imageView.center = CGPointMake(
    imageView.center.x + position.x,
    imageView.center.y + position.y);
[UIView commitAnimations];
```

要结束动画块，你调用 UIView 类的 commitAnimations 类方法。上述代码尝试在 ImageView 从一个位置移动到另一个位置时对其进行动画处理（见图 15-6）。这比之前的结果要流畅得多。

![](img/aab2d775c46f70cd606f2e58e2521324_375_0.png)

## 变换视图

前一节展示了如何使用 NSTimer 类通过不断改变 ImageView 的位置来模拟一些简单动画。除了重新定位视图之外，你还可以使用 iPhone SDK 支持的变换技术来实现相同的效果。

变换在 Core Graphics 中定义，iPhone SDK 支持标准的仿射 2D 变换。你可以使用 iPhone SDK 执行以下仿射 2D 变换：

> 注 仿射变换是一种线性变换，它保持共线性和距离比例不变。这意味着最初位于一条直线上的所有点在变换后仍保持在一条直线上，且彼此之间的距离比例保持不变。

- 平移 — 使用 x 和 y 轴指定的量移动视图的原点
- 旋转 — 按指定的角度移动视图
- 缩放 — 按指定的 x 和 y 因子更改视图的比例

图 15-7 显示了刚才描述的各种变换的效果。

![](img/aab2d775c46f70cd606f2e58e2521324_376_0.png)

![](img/aab2d775c46f70cd606f2e58e2521324_376_1.png)

![](img/aab2d775c46f70cd606f2e58e2521324_376_2.png)

图 15-7

## 平移

要对视图执行仿射变换，只需使用其 transform 属性即可。回想一下，在前面的示例中，你通过其 center 属性设置视图的新位置：

```
imageView.center = CGPointMake(
    imageView.center.x + position.x,
    imageView.center.y + position.y);
```

使用 2D 变换，你可以使用其 transform 属性并将其设置为 CGAffineTransformMakeTranslation() 函数返回的 CGAffineTransform 数据结构，如下所示：

```
//---in the AnimationViewController.h file---
CGPoint position;
CGPoint translation;

//---in the viewDidLoad method---
position = CGPointMake(12.0,4.0);
```

```
translation = CGPointMake(0.0,0.0);

-(void) onTimer {
    imageView.transform = CGAffineTransformMakeTranslation(
        translation.x, translation.y);

    translation.x = translation.x + position.x;
    translation.y = translation.y + position.y;

    if (imageView.center.x + translation.x > 320 - ballRadius ||
        imageView.center.x + translation.x < ballRadius)
        position.x = -position.x;

    if (imageView.center.y + translation.y > 460 - ballRadius ||
        imageView.center.y + translation.y < ballRadius)
        position.y = -position.y;
}
```

CGAffineTransformMakeTranslation() 函数接受两个参数——x 轴的移动值和 y 轴的移动值。

上述代码实现了与设置 ImageView 的 center 属性相同的效果。

## 旋转

旋转变换允许你使用指定的角度旋转视图。在下面的“试一试”中，你修改前一个示例中的代码，以便网球在屏幕上弹跳时可以旋转。

## 试一试 旋转网球

- 1. 在 AnimationViewController.h 文件中，添加 angle 变量的声明：

```
#import <UIKit/UIKit.h>

@interface AnimationViewController : UIViewController {
    IBOutlet UIImageView *imageView;
    IBOutlet UISlider *slider;

    CGPoint position;
    NSTimer *timer;

    float ballRadius;
    float angle;
}

@property (nonatomic, retain) UIImageView *imageView;
```
