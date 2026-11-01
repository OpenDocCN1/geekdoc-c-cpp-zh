

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_342_0.png)

## 图 12-1

7. 回到 Xcode，编辑 GesturesViewController.h 文件，添加以下加粗语句：

```
#import <UIKit/UIKit.h>

@interface GesturesViewController : UIViewController {
    IBOutlet UIImageView *imageView;
}

@property (nonatomic, retain) UIImageView *imageView;

@end
```

8. 在 Interface Builder 中，通过控制点击并拖动 File's Owner 项到 ImageView 上，将 imageView outlet 连接到 ImageView。选择 imageView。

9. 在 Xcode 中，编辑 GesturesViewController.m 文件并添加以下加粗语句：

```
#import "GesturesViewController.h"

@implementation GesturesViewController

@synthesize imageView;

- (void)viewDidLoad {
    //---tap gesture---
    UITapGestureRecognizer *tapGesture =
```
```
[[UITapGestureRecognizer alloc]
    initWithTarget:self
    action:@selector(handleTapGesture:)];

tapGesture.numberOfTapsRequired = 2;
[imageView addGestureRecognizer:tapGesture];
[tapGesture release];

[super viewDidLoad];
}

//---handle tap gesture---
-(IBAction) handleTapGesture:(UIGestureRecognizer *) sender {
    if (sender.view.contentMode == UIViewContentModeScaleAspectFit)
        sender.view.contentMode = UIViewContentModeCenter;
    else
        sender.view.contentMode = UIViewContentModeScaleAspectFit;
}
- (void)dealloc {
    [imageView release];
    [super dealloc];
}
```

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_343_0.png)

## 图 12-2

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_345_0.png)

## 图 12-4

将手势识别器附加到视图上，在本例中为 imageView，将 tapGesture 对象传递给 addGestureRecognizer: 方法：

```
[imageView addGestureRecognizer:tapGesture];
```

最后，释放 tapGesture 识别器对象：

```
[tapGesture release];
```

当应用程序检测到双击时，handleTapGesture: 方法将被调用：

```
//---handle tap gesture---
-(IBAction) handleTapGesture: (UIGestureRecognizer *) sender {
    if (sender.view.contentMode == UIViewContentModeScaleAspectFit)
        sender.view.contentMode = UIViewContentModeCenter;
    else
        sender.view.contentMode = UIViewContentModeScaleAspectFit;
}
```

在 handleTapGesture: 中，你可以通过 sender.view 对象引用识别出该手势的视图，在本例中为 imageView（或者，你也可以通过 self.imageView 直接引用 ImageView）。此方法很有用，因为你可能有多个视图附加到同一个手势处理程序，而 sender.view 会自动引用识别出手势的视图。

在此手势处理程序中，你在 UIViewContentModeScaleAspectFit 和 UIViewContentModeCenter 模式之间切换图像。

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_348_0.png)

## 图 12-5

当识别到捏合手势时，handlePinchGesture: 方法将被调用以处理它。请记住，捏合手势是连续手势，因此只要手指仍在屏幕上，handlePinchGesture: 方法就会被反复调用。

要判断这是否是“放大”或“缩小”手势，你需要检查 UIPinchGestureRecognizer 对象的 scale 属性：

```
```objc
CGFloat factor = [(UIPinchGestureRecognizer *)sender scale];
```
```

如果手指张开，则 scale 的值大于或等于 1。如果手指靠近，则值小于 1。每次执行捏合手势时，你的应用程序都需要记住缩放因子，以便下次执行手势时，可以根据上次绘制的大小调整图像大小。这是在捏合手势结束时完成的（当手指离开屏幕时）。你检查 sender.state 以查看手势是否已结束，然后继续保存上次的缩放因子：

```
```objc
if (sender.state == UIGestureRecognizerStateEnded) {
    if (factor > 1) {
        lastScaleFactor += (factor-1);
    } else {
        lastScaleFactor *= factor;
    }
}
```
```

## 试一试 识别平移

1. 使用上一个试一试中创建的同一项目，编辑 GesturesViewController.m，添加以下加粗语句：

```
```objc
#import "GesturesViewController.h"

@implementation GesturesViewController

@synthesize imageView;

CGFloat lastScaleFactor = 1;

CGFloat netRotation;

CGPoint netTranslation;

- (void)viewDidLoad {
    //---tap gesture---
    UITapGestureRecognizer *tapGesture =
    [[UITapGestureRecognizer alloc]
        initWithTarget:self
            action:@selector(handleTapGesture:)];

    tapGesture.numberOfTapsRequired = 2;
    [self.imageView addGestureRecognizer:tapGesture];
    [tapGesture release];

    //---pinch gesture---
    UIPinchGestureRecognizer *pinchGesture =
    [[UIPinchGestureRecognizer alloc]
        initWithTarget:self
            action:@selector(handlePinchGesture:)];

    [imageView addGestureRecognizer:pinchGesture];
    [pinchGesture release];

    //---rotate gesture---
    UIRotationGestureRecognizer *rotateGesture =
    [[UIRotationGestureRecognizer alloc]
        initWithTarget:self
            action:@selector(handleRotateGesture:)];

    [imageView addGestureRecognizer:rotateGesture];
    [rotateGesture release];

    //---pan gesture---
    UIPanGestureRecognizer *panGesture =
    [[UIPanGestureRecognizer alloc]
        initWithTarget:self
            action:@selector(handlePanGesture:)];

    [imageView addGestureRecognizer:panGesture];
    [panGesture release];
}
```
```

```
[super viewDidLoad];
}

//---handle pan gesture---
-(IBAction) handlePanGesture:(UIGestureRecognizer *) sender {
    CGPoint translation = [(UIPanGestureRecognizer *) sender translationInView:imageView];
    sender.view.transform = CGAffineTransformMakeTranslation(
        netTranslation.x + translation.x,
        netTranslation.y + translation.y);
    if (sender.state == UIGestureRecognizerStateEnded) {
        netTranslation.x += translation.x;
        netTranslation.y += translation.y;
    }
}
```

- 2. 要在 iPhone 模拟器上测试应用程序，请按 Command-R。
- 3. 点击 ImageView 并移动鼠标。观察 ImageView 是否随鼠标移动（见图 12-7）。

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_353_0.png)

## 图 12-7

## 工作原理

你创建一个 UIPanGestureRecognizer 类的实例并将其连接到一个处理方法：

```
UIPanGestureRecognizer *panGesture =
    [[UIPanGestureRecognizer alloc]
        initWithTarget:self
            action:@selector(handlePanGesture:)];

[imageView addGestureRecognizer:panGesture];
[panGesture release];
```

当识别到平移手势时，handlePanGesture: 方法将被调用。平移是连续手势，因此此方法会被反复调用。

要获取平移量，你需要检查 UIPanGestureRecognizer 对象的 translation 属性：

```
CGPoint translation = [(UIPanGestureRecognizer *) sender translationInView:imageView];
```

为了确保 ImageView 可以从上次绘制的位置移动，你在手势结束时保存当前的平移量：

```
if (sender.state == UIGestureRecognizerStateEnded) {
    netTranslation.x += translation.x;
    netTranslation.y += translation.y;
}
```

最后，你使用 CGAffineTransformMakeTranslation() 方法移动 ImageView：

```
sender.view.transform = CGAffineTransformMakeTranslation(
                        netTranslation.x + translation.x,
                        netTranslation.y + translation.y);
```

## 滑动

你会遇到的另一个常见手势是滑动。使用滑动手势，用户用手指触摸屏幕，朝特定方向移动，然后抬起手指。滑动手势通常用于在视图之间切换（例如在照片应用程序中查看一系列照片）。

以下试一试说明如何使用 UISwipeGestureRecognizer 识别滑动手势，然后在 ImageView 中显示不同的图像。

## 试一试 识别滑动

- 1. 使用上一个试一试中创建的同一项目，将名为 Buildings.jpeg 和 Bridge.jpeg 的两张图片拖放到 Xcode 项目的 Resources 文件夹中。当出现 Add 对话框时，勾选 Copy Item into Destination Group's Folder (If Needed) 选项，以便将每张图片复制到项目中（见图 12-8）。

