
8. 回到 Interface Builder 中，按如下方式连接输出口和动作（图11-5显示了所有输出口和动作连接完成后的连接情况）：

-   按住Control键并点击，将File's Owner项拖拽到ImageView上，然后选择`imageView`。
-   按住Control键并点击，将File's Owner项拖拽到Slider视图上，然后选择`slider`。
-   将Slider视图拖拽到File's Owner项上，然后选择`sliderMoved:`。

![](img/744c5ec15e15ca7891c98be71dc25d13_326_0.png)

图11-5

9. 在AnimationViewController.m文件中添加以下粗体语句：

```objc
#import "AnimationViewController.h"

@implementation AnimationViewController

@synthesize imageView;
@synthesize slider;

- (void) onTimer {
    imageView.center = CGPointMake(imageView.center.x + delta.x,
                                   imageView.center.y + delta.y);
    if (imageView.center.x > self.view.bounds.size.width - ballRadius ||
        imageView.center.x < ballRadius)
        delta.x = -delta.x;

    if (imageView.center.y > self.view.bounds.size.height - ballRadius ||
        imageView.center.y < ballRadius)
        delta.y = -delta.y;
}

- (void)viewDidLoad {
    ballRadius = imageView.frame.size.width / 2;
    [slider setShowValue:YES];
    delta = CGPointMake(12.0,4.0);

    timer = [NSTimer scheduledTimerWithTimeInterval:slider.value
                                              target:self
                                            selector:@selector(onTimer)
                                            userInfo:nil
                                             repeats:YES];

    [super viewDidLoad];
}

- (IBAction) sliderMoved:(id) sender {
    [timer invalidate];
    timer = [NSTimer scheduledTimerWithTimeInterval:slider.value
                                              target:self
                                            selector:@selector(onTimer)
                                            userInfo:nil
                                             repeats:YES];
}

- (void)didReceiveMemoryWarning {
    [super didReceiveMemoryWarning];
}

- (void)dealloc {
    [timer invalidate];
    [imageView release];
    [slider release];
    [super dealloc];
}

@end
```

10. 按Command-R在iPhone模拟器上测试应用程序。现在网球应该在屏幕上进行动画显示（见图11-6）。通过向右移动滑块来减慢动画速度，向左移动滑块来加快动画速度。

> **注**：`NSTimer`对象启动后，无法更改其触发间隔。因此，更改间隔的唯一方法是使当前定时器失效，然后创建一个新的`NSTimer`对象。

## 动画化视觉变化

你可能已经注意到，当将滑块向右移动时，动画会变慢并且变得不连贯。

为了让动画更平滑，你可以使用动画块对视觉变化进行动画处理。动画块的起点由`UIView`类的`beginAnimations:context:`类方法定义：

```objc
[UIView beginAnimations:@"my_own_animation" context:nil];

//---animate for the duration of the slider value (time interval)---
[UIView setAnimationDuration:slider.value];

//---set the animation curve type---
[UIView setAnimationCurve:UIViewAnimationCurveLinear];

imageView.center = CGPointMake(imageView.center.x + delta.x,
    imageView.center.y + delta.y);

[UIView commitAnimations];
```

要结束动画块，你需要调用`UIView`类的`commitAnimations`类方法。前面的代码在ImageView从一个位置移动到另一个位置时对其进行了动画处理（见图11-7）。这使动画比以前平滑得多。

![](img/744c5ec15e15ca7891c98be71dc25d13_330_0.png)

## 视图变换

你可以使用`NSTimer`类，通过不断更改ImageView的位置来模拟一些简单的动画，但也可以使用iPhone SDK支持的变换技术来实现相同的效果。

变换在Core Graphics中定义，iPhone SDK支持标准仿射2D变换。你可以使用iPhone SDK执行以下仿射2D变换：

-   平移（Translation）——使用x轴和y轴指定的量移动视图的原点
-   旋转（Rotation）——按指定的角度旋转视图
-   缩放（Scaling）——按指定的x和y因子更改视图的缩放比例

### 旋转

```objc
NSTimer *timer;

float ballRadius;
float angle;
}

@property (nonatomic, retain) UIImageView *imageView;
@property (nonatomic, retain) UISlider *slider;
- (IBAction) sliderMoved:(id) sender;

@end
```

2. 在AnimationViewController.m文件中，添加以下粗体语句：

> **注**：如果你已在“平移”部分添加了执行平移的代码，请务必在添加onTimer方法中列出的代码之前移除该代码。

```objc
- (void)onTimer {
    //---rotation---
    imageView.transform = CGAffineTransformMakeRotation(angle);
    angle += 0.02;
    if (angle >= 6.285) angle = 0;

    imageView.center = CGPointMake(imageView.center.x + delta.x,
                                   imageView.center.y + delta.y);

    if (imageView.center.x > self.view.bounds.size.width - ballRadius ||
        imageView.center.x < ballRadius)
        delta.x = -delta.x;

    if (imageView.center.y > self.view.bounds.size.height - ballRadius ||
        imageView.center.y < ballRadius)
        delta.y = -delta.y;
}

- (void)viewDidLoad {
    //---set the angle to 0---
    angle = 0;
    ballRadius = imageView.frame.size.width / 2;
    [slider setShowValue:YES];
    delta = CGPointMake(12.0, 4.0);

    timer = [NSTimer scheduledTimerWithTimeInterval:slider.value
                                             target:self
                                           selector:@selector(onTimer)
                                           userInfo:nil
                                            repeats:YES];

    [super viewDidLoad];
}
```

3. 按Command-R测试应用程序。现在网球在屏幕上弹跳时会旋转。

### 工作原理

要旋转视图，请使用`CGAffineTransformMakeRotation()`函数返回的`CGAffineTransform`数据结构设置其`transform`属性。`CGAffineTransformMakeRotation()`函数接受一个参数，该参数包含要旋转的角度（以弧度为单位）。每次旋转后，你将角度递增0.02：

```objc
//---rotation---
imageView.transform = CGAffineTransformMakeRotation(angle);
angle += 0.02;
```

完整旋转需要360度，也就是2π弧度。如果角度超过6.2857（=2*3.142857），则将角度重置为0：

```objc
if (angle > 6.2857) angle = 0;
```

### 缩放

对于视图的缩放，你可以使用`CGAffineTransformMakeScale()`函数返回`CGAffineTransform`数据结构，并将其设置到视图的`transform`属性：

```objc
imageView.transform = CGAffineTransformMakeScale(angle, angle);
```

`CGAffineTransformMakeScale()`接受两个参数：x轴的缩放因子和y轴的缩放因子。

如果你用前面的语句修改之前的“动手试一试”中的代码，网球在屏幕上弹跳时会变大（见图11-9）。然后它会重置回原始大小，并再次变大。

## 动画化一系列图像

如果需要，选择“文件夹”选项，以便将每个图像复制到项目中。图11-10显示了已添加的图像。

![](img/744c5ec15e15ca7891c98be71dc25d13_336_0.png)

3. 在Animations2ViewController.m文件中，添加以下粗体语句：

```objc
- (void)viewDidLoad {

    NSArray *images = [NSArray arrayWithObjects:
        [UIImage imageNamed:@"MacSE.jpeg"],
        [UIImage imageNamed:@"imac.jpeg"],
        [UIImage imageNamed:@"MacPlus.jpeg"],
        [UIImage imageNamed:@"imac_old.jpeg"],
        [UIImage imageNamed:@"Mac8100.jpeg"],
        nil];

    CGRect frame = CGRectMake(0,0,320,460);

    UIImageView *imageView = [[UIImageView alloc] initWithFrame:frame];
    imageView.animationImages = images;
    imageView.contentMode = UIViewContentModeScaleAspectFit;
    imageView.animationDuration = 3; //---seconds to complete one set
    // of animation---
    imageView.animationRepeatCount = 0; //---continuous---
    [imageView startAnimating];
    [self.view addSubview:imageView];
    [imageView release];
    [super viewDidLoad];
}
```

4. 按Command-R在iPhone模拟器上测试图像序列。这些图像会一张一张地显示在ImageView中（见图11-11）。
