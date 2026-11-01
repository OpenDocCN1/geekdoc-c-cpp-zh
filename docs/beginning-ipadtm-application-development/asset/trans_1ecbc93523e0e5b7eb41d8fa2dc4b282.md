
![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_489_0.png)

图 18-8

- **2.** 添加以下粗体语句到 LBSViewController.h 文件中：

```objc
#import <UIKit/UIKit.h>
#import <CoreLocation/CoreLocation.h>

#import <MapKit/MapKit.h>

@interface LBSViewController : UIViewController <CLLocationManagerDelegate, MKMapViewDelegate> {
    IBOutlet UITextField *accuracyTextField;
    IBOutlet UITextField *latitudeTextField;
    IBOutlet UITextField *longitudeTextField;
    CLLocationManager *lm;
    MKMapView *mapView;
}

@property (retain, nonatomic) CLLocationManager *lm;
@property (retain, nonatomic) UITextField *accuracyTextField;
@property (retain, nonatomic) UITextField *latitudeTextField;
@property (retain, nonatomic) UITextField *longitudeTextField;

@end
```

- **3.** 在 LBSViewController.m 文件中，添加以下粗体语句：

```objc
- (void) viewDidLoad {
    self.lm = [[CLLocationManager alloc] init];
    lm.delegate = self;
    lm.desiredAccuracy = kCLLocationAccuracyBest;
    lm.distanceFilter = kCLDistanceFilterNone;
    [lm startUpdatingLocation];

    //---display the map in a region---
    mapView = [[MKMapView alloc]
        initWithFrame:CGRectMake(10, 60, 1004, 678)];

    mapView.delegate = self;
    mapView.mapType = MKMapTypeHybrid;

    [self.view addSubview:mapView];

    [super viewDidLoad];
}

- (void) locationManager:(CLLocationManager *) manager
    didUpdateToLocation:(CLLocation *) newLocation
    fromLocation:(CLLocation *) oldLocation {

    NSString *lat = [[NSString alloc] initWithFormat:@"%f",
        newLocation.coordinate.latitude];
    latitudeTextField.text = lat;

    NSString *lng = [[NSString alloc] initWithFormat:@"%f",
        newLocation.coordinate.longitude];
    longitudeTextField.text = lng;

    NSString *acc = [[NSString alloc] initWithFormat:@"%f",
        newLocation.horizontalAccuracy];
    accuracyTextField.text = acc;

    [acc release];
    [lat release];
    [lng release];

    //---update the map---
    MKCoordinateSpan span;
    span.latitudeDelta=.001;
    span.longitudeDelta=.001;

    MKCoordinateRegion region;
    region.center = newLocation.coordinate;
    region.span = span;

    [mapView setRegion:region animated:TRUE];

}

- (void) dealloc{
    [mapView release];
    [lm release];
    [latitudeTextField release];
    [longitudeTextField release];
    [accuracyTextField release];
    [super dealloc];
}
```

- **4.** 按 Command-R 在 iPhone 模拟器上测试应用程序。观察地图显示位置管理器报告的位置（见图 18-9）。地图的中心是报告的位置。

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_491_0.png)

图 18-9

> **注意** 如果你在 iPad 上测试应用程序，你会看到地图在你移动时动态更新自身。

## 工作原理

要在你的应用程序中使用 Map Kit，你首先需要将 MapKit.framework 添加到你的项目中。

然后，你在视图控制器中实现 MKMapViewDelegate 协议以处理与 MapView 关联的各种方法：

```objc
@interface LBSViewController : UIViewController
<CLLocationManagerDelegate,
MKMapViewDelegate> {
```

当视图加载后，你创建 MKMapView 类的实例并设置地图类型（混合 — 地图和卫星）以显示：

```objc
//---display the map in a region---
mapView = [[MKMapView alloc]
    initWithFrame:CGRectMake(10, 60, 1004, 678)];

mapView.delegate = self;
mapView.mapType = MKMapTypeHybrid;

[self.view addSubview:mapView];
```

在这种情况下，你指定要显示的地图大小。你将 delegate 属性设置为 self，以便视图控制器可以实现 MKMapViewDelegate 协议中声明的所有方法。

要使用地图填满整个视图窗口，你将使用以下语句：

```objc
//---fill up entire screen---
mapView = [[MKMapView alloc] initWithFrame:self.view.bounds];
```

当位置信息更新时，你使用 mapView 对象的 setRegion: 方法放大到该位置：

```objc
//---update the map---
MKCoordinateSpan span;
span.latitudeDelta=.001;
span.longitudeDelta=.001;

MKCoordinateRegion region;
region.center = newLocation.coordinate;
region.span = span;

[mapView setRegion:region animated:TRUE];
```

> **注意** 有关 MKMapView 类的更多信息，请参阅 Apple 的文档 http://developer.apple.com/iphone/library/navigation/Frameworks/CocoaTouch/MapKit/index.html。

## 获取方向信息

iPad 配备了内置指南针。本 Try It Out 向你展示如何使用此新功能以编程方式获取方向信息。

### 试一试 集成指南针

你需要一台真实设备（iPad）来测试此应用程序。

- **1.** 使用 LBS 项目，将名为 Compass.gif 的图像添加到项目的 Resources 文件夹中（见图 18-10）。
- **2.** 在 Interface Builder 中，将 ImageView 拖放到视图窗口中，并在属性检查器窗口中按如下方式设置其属性（另见图 18-11）：
  - Image — Compass.gif
  - Mode — Aspect Fit
- **3.** 向视图窗口添加一个标签视图（见图 18-12）。
- **4.** 在 LBSViewController.h 文件中，添加以下粗体语句：

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_493_0.png)

```objc
#import <UIKit/UIKit.h>
#import <CoreLocation/CoreLocation.h>
#import <MapKit/MapKit.h>

@interface LBSViewController : UIViewController
<CLLocationManagerDelegate,
MKMapViewDelegate> {
    IBOutlet UITextField *accuracyTextField;
    IBOutlet UITextField *latitudeTextField;
    IBOutlet UITextField *longitudeTextField;
    CLLocationManager *lm;
    MKMapView *mapView;
    IBOutlet UIImageView *compass;
    IBOutlet UILabel *heading;
}

@property (retain, nonatomic) CLLocationManager *lm;
@property (retain, nonatomic) UITextField *accuracyTextField;
@property (retain, nonatomic) UITextField *latitudeTextField;
@property (retain, nonatomic) UITextField *longitudeTextField;

@property (nonatomic, retain) UIImageView *compass;
@property (nonatomic, retain) UILabel *heading;

@end
```

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_494_0.png)

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_494_1.png)

图 18-11

图 18-12

- **5.** 在 Interface Builder 中，执行以下操作：
  - Control-click and drag the File's Owner item and drop it over the ImageView. Select compass.
  - Control-click and drag the File's Owner item and drop it over the Label view. Select heading.
- **6.** 在 LBSViewController.m 文件中，添加以下粗体语句：

```objc
#import "LBSViewController.h"

@implementation LBSViewController

@synthesize lm;
@synthesize latitudeTextField;
@synthesize longitudeTextField;
@synthesize accuracyTextField;

@synthesize compass;
@synthesize heading;

- (void)viewDidLoad {
    self.lm = [[CLLocationManager alloc] init];
    lm.delegate = self;
    lm.desiredAccuracy = kCLLocationAccuracyBest;
    lm.distanceFilter = kCLDistanceFilterNone;

    [lm startUpdatingLocation];

    //---get the compass readings---
    [lm startUpdatingHeading];

    //---display the map in a region---
    mapView = [[MKMapView alloc]
        initWithFrame:CGRectMake(10, 60, 720, 678)];
    mapView.delegate = self;
    mapView.mapType = MKMapTypeHybrid;

    [self.view addSubview:mapView];

    [super viewDidLoad];
}

- (void)locationManager:(CLLocationManager *)manager
    didUpdateHeading:(CLHeading *)newHeading {
    heading.text = [NSString stringWithFormat:@"%f degrees",
        newHeading.magneticHeading];

    //---heading is in degrees---
    double d = newHeading.magneticHeading;

    //---convert degrees to radians---
    double radians = d/57.2957795;
    compass.transform = CGAffineTransformMakeRotation(-radians);
}

- (void)dealloc {
    [compass release];
    [heading release];
    [lm release];
    [latitudeTextField release];
    [longitudeTextField release];
    [accuracyTextField release];

    [super dealloc];
}
```

- **7.** 按 Command-R 在 iPad 上测试应用程序。观察你在转动设备时图像的变化（见图 18-13）。

![](img/ab1bbb3d5afcbabb6f4a47f0203b9043_496_0.png)

图 18-13

### 工作原理

获取方向信息与获取位置数据类似。你使用 Core Location 框架。不是调用 CLLocationManager 对象的 startUpdatingLocation 方法，而是调用 startUpdatingHeading 方法：

```objc
//---get the compass readings---
[lm startUpdatingHeading];
```
