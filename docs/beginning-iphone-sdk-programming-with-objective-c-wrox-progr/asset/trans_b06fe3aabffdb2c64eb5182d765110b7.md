
## 17

## 访问硬件

### 本章你将学到什么

- 如何从你的 iPhone 或 iPod Touch 获取加速度计数据
- 如何检测设备的摇动
- 如何使用 iPhone 和 iPod Touch 中的 Core Location 服务获取地理位置数据
- 如何在你的应用程序中显示地图

在上一章中，你看到了如何通过各种方式访问 iPhone 和 iPod Touch 上的内置应用程序——URL 字符串以及使用 iPhone SDK 提供的专用类。在本章中，你将学习如何访问设备的硬件，例如加速度计，并通过 GPS、蜂窝基站和无线热点获取位置信息。

### 使用加速度计

iPhone 和 iPod Touch 最具创新性的功能之一是内置加速度计。加速度计允许设备检测设备的方向并调整内容以适应新的方向。例如，当你将设备横向旋转时，Safari 网页浏览器会自动将屏幕切换到横向模式，以便你现在拥有更宽的观看空间。同样，相机也依赖加速度计来判断你是在竖屏还是横屏模式下拍照。

如果设备直立并快速向右移动，X 轴的值将从 0 增加到正值。如果快速向左移动，X 轴的值将从 0 减少到负值。如果设备快速向上移动，Y 轴的值将从 -1.0 增加到更大的值。如果设备快速向下移动，Y 轴的值将从 -1.0 减少到更小的值。

如果设备平放在桌子上然后掉落，Z 轴的值将从 -1.0 减少到更小的数字。如果向上移动，Z 轴的值将从 -1.0 增加到更大的数字。

> 注意 iPhone 和 iPod Touch 上使用的加速度计的最大读数为约 +/- 2.3G，分辨率约为 0.018 g。

在下面的“动手试一试”中，你将学习如何以编程方式访问加速度计返回的数据。获取加速度计数据可以让你构建非常有趣的应用程序，例如水平仪，以及依赖运动检测的游戏。

### 动手试一试 访问加速度计数据

代码文件 [Accelerometer.zip] 可在 Wrox.com 下载

- 1. 使用 Xcode，创建一个新的基于视图的应用程序项目并将其命名为 Accelerometer。
- 2. 双击 AccelerometerViewController.xib 文件在 Interface Builder 中编辑它。
- 3. 在 View 窗口中填充六个 Label 视图，如图 17-2 所示。
- 4. 在 AccelerometerViewController.h 文件中，添加以下以粗体显示的语句：

```
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

![](img/16991b58db5894715c4a443315e06a22_410_0.png)

- 5. 返回 Interface Builder，Control-点击并拖动 File's Owner 项到每个三个 Label 视图并分别选择 labelX、labelY 和 labelZ。
- 6. 在 AccelerometerViewController.m 文件中，添加以下以粗体显示的语句：

```
#import "AccelerometerViewController.h"

@implementation AccelerometerViewController

@synthesize labelX, labelY, labelZ;

- (void)viewDidLoad {
    UIAccelerometer *acc = [UIAccelerometer sharedAccelerometer];
    acc.delegate = self;
    acc.updateInterval = 1.0f/60.0f;
    [super viewDidLoad];
}

- (void)accelerometer:(UIAccelerometer *)acc didAccelerate:(UIAcceleration *)acceleration {
    NSString *str = [[NSString alloc] initWithFormat:@"%sg", acceleration.x];
    labelX.text = str;
    str = [[NSString alloc] initWithFormat:@"%sg", acceleration.y];
    labelY.text = str;
    str = [[NSString alloc] initWithFormat:@"%sg", acceleration.z];
    labelZ.text = str;
    [str release];
}

- (void)dealloc {
    [labelX release];
    [labelY release];
    [labelZ release];
    [super dealloc];
}
```

- 7. 按 Command-R 在 iPhone 设备上测试应用程序。图 17-3 显示了当我的 iPhone 放置在 iPhone 底座上时应用程序上显示的数据。

> 注意 对于加速度计数据，你需要一个真实设备——iPhone 或 iPod Touch。

![](img/16991b58db5894715c4a443315e06a22_412_0.png)

图 17-3

### 工作原理

要在你的 iPhone 或 iPod Touch 中使用加速度计，你需要在你的代理（例如视图控制器）中实现 UIAccelerometerDelegate 协议：

```
@interface AccelerometerViewController : UIViewController
<UIAccelerometerDelegate> {
```

当视图加载时，你首先使用 sharedAccelerometer 方法获取 UIAccelerometer 类的单个实例。然后你指定实例的代理和你想要获取加速度计数据的更新间隔：

```
- (void)viewDidLoad {
    UIAccelerometer *acc = [UIAccelerometer sharedAccelerometer];
    acc.delegate = self;
    acc.updateInterval = 1.0f/60.0f;
    [super viewDidLoad];
}
```

updateInterval 属性指定以秒为单位的间隔——即两次更新之间的秒数。在前一种情况下，你表示希望加速度计数据每秒更新 60 次。

UIAccelerometerDelegate 协议定义了你需要实现以获取加速度计数据的单个方法：`accelerometer:didAccelerate:`。在你的情况下，你提取三个轴的值并将其显示在三个 Label 视图上：

```
- (void)accelerometer:(UIAccelerometer *) acc
didAccelerate:(UIAcceleration *)acceleration {
    NSString *str = [[NSString alloc] initWithFormat:@"%g", acceleration.x];
    labelX.text = str;
    str = [[NSString alloc] initWithFormat:@"%g", acceleration.y];
    labelY.text = str;
    str = [[NSString alloc] initWithFormat:@"%g", acceleration.z];
    labelZ.text = str;
    [str release];
}
```

### 在 iPhone OS 2 及更早版本中检测摇动

在 iPhone OS 3.0 中，Apple 提供了 Shake API（在下一节中讨论），它是一组允许你检测设备摇动的方法。然而，如何在 iPhone OS 2.0 及更早版本中检测摇动？

答案其实非常简单。你可以在 `accelerometer:didAccelerate:` 事件中添加一些代码，如下所示：

```
#import "AccelerometerViewController.h"
#define kAccelerationThreshold 2.2
//...
//...

- (void)accelerometer:(UIAccelerometer *) acc
    didAccelerate:(UIAcceleration *)acceleration {
    if (fabsf(acceleration.x) > kAccelerationThreshold)
    {
        NSLog(@"Shake detected");
    }
}
```

`fabsf()` 函数返回浮点数的绝对值。在这种情况下，如果 X 轴值记录的绝对值超过 2.2，则认为用户正在摇动设备。

- 6. Control-点击并拖动 File's Owner 项到 DatePicker 视图并选择 datePicker。
- 7. 右键点击 TextField 视图并将其 Did End on Exit 事件连接到 File's Owner 项（参见图 17-5）。选择 doneEditing:。

![](img/16991b58db5894715c4a443315e06a22_415_0.png)

图 17-5

- 8. 向 ShakeViewController.m 文件插入以下以粗体显示的语句：

```
#import "ShakeViewController.h"

@implementation ShakeViewController

@synthesize textField, datePicker;

- (void) viewDidAppear:(BOOL)animated
{
    [self.view becomeFirstResponder];
    [super viewDidAppear:animated];
}

- (IBAction) doneEditing: (id) sender {
    //---when keyboard is hidden, make the view the first responder
    // or else the Shake API will not work---
    [self.view becomeFirstResponder];
}

- (void)motionBegan:(UIEventSubtype)motion withEvent: UIEvent *)event (
```
