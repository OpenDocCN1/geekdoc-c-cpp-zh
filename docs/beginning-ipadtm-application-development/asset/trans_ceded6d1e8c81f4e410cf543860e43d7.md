

```objc
[imageView addGestureRecognizer:swipeLeftGesture];
[swipeLeftGesture release];
}
[super viewDidLoad];

//---handle swipe gesture---
-(IBAction) handleSwipeGesture:(UIGestureRecognizer *) sender {

    UISwipeGestureRecognizerDirection direction =
        [(UISwipeGestureRecognizer *) sender direction];

    switch (direction) {
        case UISwipeGestureRecognizerDirectionUp:
            NSLog(@"up");
            break;
        case UISwipeGestureRecognizerDirectionDown:
            NSLog(@"down");
            break;
        case UISwipeGestureRecognizerDirectionLeft:
            imageIndex++;
            break;
        case UISwipeGestureRecognizerDirectionRight:
            imageIndex--;
            break;
        default:
            break;
    }

    imageIndex = (imageIndex < 0) ? ([images count] - 1) : imageIndex % [images count];
    imageView.image = [UIImage imageNamed:[images objectAtIndex:imageIndex]];
}
-(void)dealloc {
    [images release];
    [imageView release];
    [super dealloc];
}
```

- 3. 按 Command-R 在 iPhone 模拟器上测试应用程序。
- 4. 单击 ImageView，然后从左向右拖动鼠标，再从右向左拖动。当你用鼠标滑动时，ImageView 会改变其显示的图像。

## 工作原理

你首先使用三张图片的名称实例化 images NSArray 对象：

```objc
//---swipe gesture---
images = [[NSArray alloc] initWithObjects:@"architecture.jpg",
    @"Buildings.jpeg",
    @"Bridge.jpeg", nil];
```

> 注意：请记住要注释掉平移手势识别器的相关语句。轻扫手势识别器将无法与平移手势识别器一起工作。

## 长按

使用长按手势识别器来检测用户是否正在触摸视图并持续按住不放。长按手势一个非常常见的用途是在移动 Safari 网页浏览器中保存图片。当你长按一张图片时，会弹出一个操作列表，允许你保存或复制该图片。

下面的“动手实践”向你展示如何使用 UILongPressGestureRecognizer 识别长按操作。

### 动手实践：识别长按操作

- 1. 使用上一个“动手实践”中创建的项目，编辑 GesturesViewController.m，添加以下加粗语句：

```objc
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
    //---comment this out---
    //[imageView addGestureRecognizer:panGesture];
    [panGesture release];

    //---swipe gesture---
    images = [[NSArray alloc] initWithObjects:@"architecture.jpg",
                         @"Buildings.jpeg",
                         @"Bridge.jpeg", nil];

    //---right swipe (default)---
    UISwipeGestureRecognizer *swipeGesture =
        [[UISwipeGestureRecognizer alloc]
            initWithTarget:self
            action:@selector(handleSwipeGesture:)];
    [imageView addGestureRecognizer:swipeGesture];
    [swipeGesture release];

    //---left swipe---
    UISwipeGestureRecognizer *swipeLeftGesture =
        [[UISwipeGestureRecognizer alloc]
            initWithTarget:self
            action:@selector(handleSwipeGesture:)];
    swipeLeftGesture.direction = UISwipeGestureRecognizerDirectionLeft;
    [imageView addGestureRecognizer:swipeLeftGesture];
    [swipeLeftGesture release];

    //---long press gesture---
    UILongPressGestureRecognizer *longpressGesture =
        [[UILongPressGestureRecognizer alloc]
            initWithTarget:self
            action:@selector(handleLongpressGesture:)];
    longpressGesture.minimumPressDuration = 1;
    longpressGesture.allowableMovement = 15;
    longpressGesture.numberOfTouchesRequired = 1;
    [imageView addGestureRecognizer:longpressGesture];
    [longpressGesture release];
}

//---handle long press gesture---
-(IBAction) handleLongpressGesture:(UIGestureRecognizer *) sender {
    UIActionSheet *actionSheet = [[UIActionSheet alloc]
```

要检测 iPad 屏幕上的触摸，你需要熟悉几个处理触摸检测的事件。通过这些事件，你将知道用户是在你的应用程序上单击、双击还是移动手指，并做出相应的响应。这些事件如下：

- touchesBegan:withEvent: — 当一个或多个手指在视图或窗口中按下时触发
- touchesMoved:withEvent: — 当一个或多个手指在视图或窗口中移动时触发
- touchesEnded:withEvent: — 当一个或多个手指从视图或窗口中抬起时触发
- touchesCancelled:withEvent: — 当系统事件（如内存不足警告）取消触摸事件时触发

这些事件定义在 UIResponder 类中，UIResponder 是 UIApplication、UIView 及其子类的父类。因此，你可以在视图控制器中为这些事件实现事件处理程序。

> 注意：这四个触摸事件是本章前面你看到的各种手势识别器所使用的底层事件。要创建你自己的自定义手势识别器来识别你自己的手势（例如“8”字形手势），你需要为这四个事件实现你自己的事件处理程序。创建你自己的自定义手势识别器超出了本书的讨论范围。

## 检测单次触摸

是时候让引擎运转起来了！请确保下载此处指示的代码，以便你能够完成下面的“动手实践”活动，在其中你将看到如何检测用户何时点击屏幕。

### 动手实践：检测点击

MultiTouch.zip 代码文件可在 Wrox.com 下载。

- 1. 使用 Xcode 创建一个新的基于视图的应用程序项目，并将其命名为 MultiTouch。
- 2. 将一张图片拖放到 Resources 文件夹中。图 12-10 显示了一个位于 Resources 文件夹中名为 apple.jpeg 的图片。
- 3. 双击 MultiTouchViewController.xib 文件，在 Interface Builder 中进行编辑。
- 4. 在 View 窗口中放置一个 ImageView。确保 ImageView 覆盖整个 View 窗口。

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_364_0.png)

- 5. 选择 ImageView，查看其“属性检查器”窗口（参见图 12-11）。将其 Image 属性设置为 `apple.jpeg`。
- 6. 在 `MultiTouchViewController.h` 文件中，添加以下加粗语句：

```objc
#import <UIKit/UIKit.h>

@interface MultiTouchViewController : UIViewController {
    IBOutlet UIImageView *imageView;
}

@property (nonatomic, retain) UIImageView *imageView;

@end
```

- 7. 回到 Interface Builder 中，按住 Control 键单击并将 File’s Owner 项拖到 ImageView 上。选择 `ImageView`。
- 8. 在 `MultiTouchViewController.m` 文件中，添加以下加粗语句：

```objc
#import "MultiTouchViewController.h"

@implementation MultiTouchViewController

@synthesize imageView;

//---fired when the user finger(s) touches the screen---
-(void)touchesBegan: (NSSet *) touches withEvent: (UIEvent *) event {

    //---get all touches on the screen---
    NSSet *allTouches = [event allTouches];

    //---compare the number of touches on the screen---
```

