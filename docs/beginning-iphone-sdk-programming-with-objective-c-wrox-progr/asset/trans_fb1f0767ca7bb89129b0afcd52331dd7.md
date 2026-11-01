

```objc
CGPoint touch1PT = [touch1 locationInView:[self view]];
CGPoint touch2PT = [touch2 locationInView:[self view]];

NSLog(@"Touch1: %.0f, %.0f", touch1PT.x, touch1PT.y);
NSLog(@"Touch2: %.0f, %.0f", touch2PT.x, touch2PT.y);

CGFloat currentDistance = [self distanceBetweenTwoPoints: touch1PT
toPoint: touch2PT];

//---zoom in---
if (currentDistance > originalDistance)
{
    imageView.frame = CGRectMake(imageView.frame.origin.x - 2,
                                 imageView.frame.origin.y - 2,
                                 imageView.frame.size.width + 4,
                                 imageView.frame.size.height + 4);
}
else {
    //---zoom out---
    imageView.frame = CGRectMake(imageView.frame.origin.x + 2,
                                 imageView.frame.origin.y + 2,
                                 imageView.frame.size.width - 4,
                                 imageView.frame.size.height - 4);
}
originalDistance = currentDistance;
} break;
}
```

- 3. 按 Command-R 在 iPhone 模拟器上测试应用程序。
- 4. 单击图像视图可将其放大。若要放大和缩小图像，请按住 Option 键并单击图像（参见图14-7）。

### 工作原理

要检测捏合手势，你需要找出两根手指之间的距离，并不断比较这个距离，以便判断两根手指是在相互靠近还是相互远离。

要找到两根手指之间的距离，你需要定义 `distanceBetweenTwoPoints:toPoint:` 方法：

```objc
-(CGFloat) distanceBetweenTwoPoints:(CGPoint)fromPoint
toPoint:(CGPoint)toPoint {
    float lengthX = fromPoint.x - toPoint.x;
    float lengthY = fromPoint.y - toPoint.y;
    return sqrt((lengthX * lengthX) + (lengthY * lengthY));
}
```

该方法接收两个 `CGPoint` 结构体，然后计算它们之间的距离。这里没有什么高深莫测的数学——只是勾股定理的实际应用。

![](img/16991b58db5894715c4a443315e06a22_361_0.png)

当两根手指第一次触摸屏幕时，你需要在 `touchesBegan:withEvent:` 方法中记录它们的距离（参见以粗体显示的代码）：

```objc
-(void) touchesBegan: (NSSet *) touches withEvent: (UIEvent *) event {
    //...
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
```

![](img/16991b58db5894715c4a443315e06a22_362_0.png)

图14-8

如果当前距离大于原始距离，则这是放大手势；如果不是，则是缩小手势：

``` 
//---fired when the user moved his finger(s) on the screen---
// - (void) touchesMoved: (NSSet *) touches withEvent: (UIEvent *) event {
//
// ...
// //---double-touch---
// case 2: {
// //---get info of first touch---
// UITouch *touch1 = [[allTouches allObjects] objectAtIndex:0];
//
// //---get info of second touch---
// UITouch *touch2 = [[allTouches allObjects] objectAtIndex:1];
//
// //---get the points touched---
// CGPoint touch1PT = [touch1 locationInView:[self view]];
// CGPoint touch2PT = [touch2 locationInView:[self view]];
//
// NSLog(@"Touch1: %.0f, %.0f", touch1PT.x, touch1PT.y);
// NSLog(@"Touch2: %.0f, %.0f", touch2PT.x, touch2PT.y);
//
// CGFloat currentDistance = [self distanceBetweenTwoPoints: touch1PT
// toPoint: touch2PT];
//
// //---zoom in---
// if (currentDistance > originalDistance)
// {
// imageView.frame = CGRectMake(imageView.frame.origin.x - 2,
// imageView.frame.origin.y - 2,
// imageView.frame.size.width + 4,
// imageView.frame.size.height + 4);
// }
// else {
// //---zoom out---
// imageView.frame = CGRectMake(imageView.frame.origin.x + 2,
// imageView.frame.origin.y + 2,
// imageView.frame.size.width - 4,
// imageView.frame.size.height - 4);
// }
// originalDistance = currentDistance;
// } break;
// }
```

### 实现拖拽手势

你可以实现的另一个手势是拖拽手势，即点击屏幕上的某个项目，然后通过移动手指来拖拽该项目。在接下来的动手实验中，你将学习如何通过实现拖拽手势来在屏幕上拖拽图像视图。

### 动手实验：拖拽ImageView

- 1. 使用之前创建的同一个项目，调整 ImageView 视图的大小，使其与图像的尺寸匹配（参见图14-9）。
- 2. 将以下以粗体显示的语句添加到 `touchesMoved:withEvent:` 方法中：

```objc
//---fired when the user moved his finger(s) on the screen---
- (void) touchesMoved: (NSSet *) touches withEvent:
(UIEvent *) event {

//---get all touches on the screen---
NSSet *allTouches = [event allTouches];

//---compare the number of touches on the screen---
switch ([allTouches count])
{
    //---single touch---
    case 1: {
        //---get info of the touch---
        UITouch *touch = [[allTouches allObjects] objectAtIndex:0];

        //---check to see if the image is being touched---
        CGPoint touchPoint = [touch locationInView:[self view]];

        if (touchPoint.x > imageView.frame.origin.x &&
            touchPoint.x < imageView.frame.origin.x +
            imageView.frame.size.width &&
            touchPoint.y > imageView.frame.origin.y &&
            touchPoint.y < imageView.frame.origin.y +
            imageView.frame.size.height) {
            [imageView setCenter:touchPoint];
        }
    } break;

    //---double-touch---
    case 2: {
        //---get info of first touch---
        UITouch *touch1 = [[allTouches allObjects] objectAtIndex:0];
        //---get info of second touch---
        UITouch *touch2 = [[allTouches allObjects] objectAtIndex:1];

        //...
    } break;
}
```

![](img/16991b58db5894715c4a443315e06a22_364_0.png)

图14-9

## 15 简单动画

### 本章学习内容

- 如何使用 `NSTimer` 类创建定时器，以定期调用方法
- 如何使用 `NSTimer` 类执行一些简单动画
- 如何对 `ImageView` 执行仿射变换
- 如何使用 `ImageView` 为一组图像制作动画

到目前为止，你所编写的应用程序都用到了 iPhone SDK 提供的标准视图。正如苹果公司一再强调的那样，iPhone 和 iPod Touch 不仅仅是手机。iPhone 还是一款音乐播放器，而且更重要的是——就本章而言——iPhone 还是一个游戏平台。

在本章中，你可以获得一些乐趣并创建一些可视化内容。你将学习如何使用定时器对象执行一些简单动画，然后对视图执行一些变换。虽然本书不会介绍如何使用 OpenGL 创建动画，但本章会向你展示一些有趣的技术，你可以用它们让你的应用程序变得生动起来！

### 使用 NSTimer 类

开始学习动画最简单的方法之一就是使用 `NSTimer` 类。`NSTimer` 类会创建定时器对象，让你能够按固定的时间间隔调用方法。使用 `NSTimer` 对象，你可以按固定的时间间隔更新图像，从而营造出图像正在动画化的效果。

- 5. 选择 View（ImageView 外部），并将背景颜色更改为黑色（参见图15-2）。

![](img/16991b58db5894715c4a443315e06a22_370_0.png)

图15-2

- 6. 从“资源库”中将一个 Label 视图和一个 Slider 视图添加到 View 窗口（参见图15-3）。将 Slider 视图的 Initial 属性设置为 0.01。

![](img/16991b58db5894715c4a443315e06a22_370_1.png)

图15-3

