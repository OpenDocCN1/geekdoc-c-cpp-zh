
![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_377_0.png)

**图 12-16**

如果当前距离大于原始距离，则为放大手势。否则，为缩小手势：

```objc
//---fired when the user moved his finger(s) on the screen---
-(void) touchesMoved: (NSSet *) touches withEvent: (UIEvent *) event {
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
        CGFloat currentDistance =
            [self distanceBetweenTwoPoints:touch1PT
                                   toPoint:touch2PT];
        //---zoom in---
        if (currentDistance > originalDistance) {
            imageView.frame = CGRectMake(
                imageView.frame.origin.x - 2,
                imageView.frame.origin.y - 2,
                imageView.frame.size.width + 4,
                imageView.frame.size.height + 4);
        }
        else {
            //---zoom out---
            imageView.frame = CGRectMake(
                imageView.frame.origin.x + 2,
                imageView.frame.origin.y + 2,
                imageView.frame.size.width - 4,
                imageView.frame.size.height - 4);
        }
        originalDistance = currentDistance;
    } break;
    ...
}
```

## 实现拖动手势

另一种可以实现的手势是拖动，即在屏幕上触摸一个项目，然后通过移动手指将其拖动。在下面的试一试中，你将学习如何通过实现拖动手势在屏幕上拖动 ImageView。

### 试一试：拖动 ImageView

1. 使用之前创建的 MultiTouch 项目，调整 ImageView 的大小，使其适合图像的大小（见图 12-17）。
2. 将以下以粗体显示的语句添加到 `touchesMoved:withEvent:` 方法中：

```objc
//---fired when the user moved his finger(s) on the screen---
-(void) touchesMoved: (NSSet *) touches withEvent: (UIEvent *) event {

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
            //...
        } break;
    }
}
```

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_379_0.png)

**图 12-17**

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_385_0.png)

**图 13-1**

**表 13-1：X、Y 和 Z 轴的各种读数**

| 位置 | X | Y | Z |
| --- | --- | --- | --- |
| 垂直直立位置 | 0.0 | -1.0 | 0.0 |
| 横向左 | 1.0 | 0.0 | 0.0 |
| 横向右 | -1.0 | 0.0 | 0.0 |
| 倒置 | 0.0 | 1.0 | 0.0 |
| 平放向上 | 0.0 | 0.0 | -1.0 |
| 平放向下 | 0.0 | 0.0 | 1.0 |

如果 iPad 保持直立并快速向右移动，X 轴的值将从 0 增加到正值。如果快速向左移动，X 轴的值将从 0 减小到负值。如果设备快速向上移动，Y 轴的值将从 -1.0 增加到更大的值。如果设备快速向下移动，Y 轴的值将从 -1.0 减小到更小的值。

如果设备处于水平状态然后掉落，Z 轴的值将从 -1.0 减小到更小的数字。如果向上移动，Z 轴的值将从 -1.0 增加到更大的数字。

**注意** iPad 上使用的加速度计的最大读数约为 +/- 2.3 g，分辨率约为 0.018 g。

在下面的试一试中，你将以编程方式访问加速度计返回的数据。获取加速度计数据可以让你构建非常有趣的应用程序，例如水平仪，以及依赖于运动检测的游戏。

### 试一试：访问加速度计数据

代码文件 Accelerometer.zip 可在 Wrox.com 下载

1. 使用 Xcode，创建一个新的基于视图的应用程序项目并将其命名为 Accelerometer。
2. 双击 AccelerometerViewController.xib 文件以在 Interface Builder 中编辑它。
3. 如图 13-2 所示，用六个 Label 视图填充 View 窗口。将左侧的三个标签分别标记为 X-axis、Y-axis 和 Z-axis。

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_386_0.png)

**图 13-2**

4. 在 AccelerometerViewController.h 文件中，添加以下以粗体显示的语句：

```objc
#import <UIKit/UIKit.h>

@interface AccelerometerViewController : UIViewController <UIAccelerometerDelegate> {
    IBOutlet UILabel *labelX;
    IBOutlet UILabel *labelY;
    IBOutlet UILabel *labelZ;
}

@property (nonatomic, retain) UILabel *labelX;
@property (nonatomic, retain) UILabel *labelY;
@property (nonatomic, retain) UILabel *labelZ;

@end
```

5. 在 Interface Builder 中，Control-单击并拖动 File’s Owner 项到右侧的每个三个 Label 视图上，分别选择 labelX、labelY 和 labelZ。

```objc
- (void)accelerometer:(UIAccelerometer *)accelerometer
        didAccelerate:(UIAcceleration *)acceleration {
    if (fabsf(acceleration.x) > kAccelerationThreshold)
    {
        NSLog(@"Shake detected");
    }
}
```

fabsf() 函数返回浮点数的绝对值。在这种情况下，如果 X 轴值记录的绝对值超过 2.2，则认为用户正在摇动设备。

## 使用 Shake API 检测摇动

从 iPhone OS 3.0 开始，Apple 宣布了新的 Shake API 的可用性，该 API 可帮助你检测设备摇动。实际上，此 API 以三种事件的形式出现，你可以在代码中处理这些事件：

- `motionBegan:`
- `motionEnded:`
- `motionCancelled:`

这三个事件在 UIResponder 类中定义，UIResponder 是 UIApplication、UIView 及其子类（包括 UIWindow）的超类。下面的试一试将向你展示如何使用这三个事件检测设备的摇动。

### 试一试：使用 Shake API

代码文件 Shake.zip 可在 Wrox.com 下载

1. 使用 Xcode，创建一个新的基于视图的应用程序项目并将其命名为 Shake。
2. 双击 ShakeViewController.xib 文件以在 Interface Builder 中编辑它。
3. 用以下视图填充 View 窗口，你将看到图 13-4：
   - 文本字段
   - 日期选择器

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_390_0.png)

**图 13-4**

4. 将以下以粗体显示的语句插入到 ShakeViewController.h 文件中：

```objc
#import <UIKit/UIKit.h>

@interface ShakeViewController : UIViewController {
    IBOutlet UITextField *textField;
    IBOutlet UIDatePicker *datePicker;
}

@property (nonatomic, retain) UITextField *textField;
@property (nonatomic, retain) UIDatePicker *datePicker;

-(IBAction) doneEditing: (id) sender;

@end
```

5. 在 Interface Builder 中：
   - Control-单击并拖动 File’s Owner 项到 TextField 视图并选择 `textField`。
   - Control-单击并拖动 File’s Owner 项到 DatePicker 视图并选择 `datePicker`。

6. 右键单击 TextField 视图并将其 Did End on Exit 事件连接到 File’s Owner 项（见图 13-5）。选择 `doneEditing:`。

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_390_1.png)

**图 13-5**
