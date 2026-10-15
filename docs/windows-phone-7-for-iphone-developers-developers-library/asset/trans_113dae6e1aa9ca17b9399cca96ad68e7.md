

## 关于 Try/Catch 的说明

如果你查看 FM 收音机代码示例，并且发现 try 和 catch 关键字的用法有点陌生，不用担心。这是 C# 的异常处理系统。try 块中的代码会尝试执行。如果发生了运行时未预期的情况（异常），catch 块中的代码就会执行，让你能够安全地处理错误，而不会导致应用程序崩溃。

需要记住的重要一点是，如果你的代码未能“捕获”发生的异常，应用程序唯一的办法就是崩溃。如果这发生在用户花了好钱购买的生产环境应用程序中，客户是不会满意的。

将代码放在 try/catch 块中会带来轻微的性能开销，以换取对该代码进行意外故障保护。作为一般规则，你应该使用 if 语句和其他测试来检查用户输入错误、边界情况和其他可预测的故障。你应该仅将 try/catch 块用作防止应用程序崩溃的最后手段。

## 使用加速度计

只有少数现代智能手机配备了加速度计。加速度计测量在三个方向上的加速度力：X、Y 和 Z。这些分别对应“法向”，即指向地球中心的向下方向（重力拉力的方向，更常被称为“向下”），左右加速度，以及前后加速度。左右、前后方向都是相对于法向确定的（记住，对我们这些非物理学类型的人来说，那就是“向下”）。

加速度计可用于一些无聊的技巧，例如让你用手机慢慢清空一杯酒；有趣的事情，例如提供“摇晃”动作来洗牌；完全沉浸式的类似操纵杆的控制（例如通过像转动方向盘一样移动手机来驾驶汽车）；甚至高端用途，例如将手机放在汽车里，猛踩油门，并记录你的 0–60 时间。根据个人经验，最后这种用途很可能是迄今为止我最喜欢的加速度计用途。

加速度计通过加速度计监视器上的三个属性报告三个方向的加速度力：X、Y 和 Z。你如何解释这些值超出了本书的范围，因为这些通常需要平滑、聚合和不同的采样率才能产生所需的结果。然而，要获取这些值并激活加速度计，你可以在 Windows Phone 7 应用程序中按如下方式创建一个 XAML 页面。（你可以在第 10.1 节清单中看到，你可以创建一个按钮和几个文本块来存储值。）

### Listing 10.1 MainPage.xaml.cs, Using the Accelerometer Sensor

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Net;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Documents;
using System.Windows.Input;
using System.Windows.Media;
using System.Windows.Media.Animation;
using System.Windows.Shapes;
using Microsoft.Phone.Controls;
using Microsoft.Devices.Sensors;

namespace AccelerometerDemo
{
public partial class MainPage : PhoneApplicationPage
{
    private Accelerometer accel;

    // Constructor
    public MainPage()
    {
        InitializeComponent();
    }

    private void startAccelButton_Click(object sender, RoutedEventArgs e)
    {
        if (accel == null)
        {
            accel = new Accelerometer();
            accel.ReadingChanged +=
                new EventHandler<AccelerometerReadingEventArgs>(
                accel_ReadingChanged);
            try
            {
                accelerometerStatusText.Text = "Accelerometer starting.";
                accel.Start();
            }
            catch (AccelerometerFailedException ex)
            {
                accelerometerStatusText.Text = "Accelerometer error.";
            }
        }
        else
        {
            try
            {
                accel.Stop();
                accel = null;
accelerometerStatusText.Text = "Accelerometer Stopped.";
}
catch (AccelerometerFailedException ex)
{
    accelerometerStatusText.Text =
        "Error stopping Accelerometer.";
}
}
}

void accel_ReadingChanged(object sender,
    AccelerometerReadingEventArgs e)
{
    Deployment.Current.Dispatcher.BeginInvoke(
        () => HandleNewReading(e));
}

void HandleNewReading(AccelerometerReadingEventArgs e)
{
    xText.Text = e.X.ToString();
    yText.Text = e.Y.ToString();
    zText.Text = e.Z.ToString();
}
}
}
```

在讨论代码之前，我应该在这里指出，除非你添加对 Microsoft.Devices.Sensors 程序集的引用，否则此应用程序将无法编译。

如果你没有用 C#、Silverlight 或 WPF 编写过代码，其中一些内容可能会对你来说很新。在 MainPage.xaml 中声明了一个名为 startAccelButton 的按钮。第一次点击此按钮时，它会启动加速度计监控。第二次点击时，它会停止监控。

每次监视器报告变化时（这会根据其采样率发生，即每秒固定的次数），都会调用 accel_ReadingChanged 方法。

这里我们做的事情有点不同。我们正在调用 Deployment.Current.Dispatcher 对象的 BeginInvoke 方法。原因是此事件由后台线程在后台触发。只有主线程上的代码才能更改 UI 对象。换句话说，如果我们尝试直接从后台线程设置三个文本块的 Text 属性，将会抛出异常并且文本永远不会更改。

为了避免这种情况，我们需要让更改文本块的代码在前台线程上执行。iOS 开发者应该对这个概念非常熟悉，事实上，Silverlight 和 WPF 开发者也经常遇到这个问题。

如果我们要在 iOS 应用程序中将此更改转发到前台线程，我们的代码可能如下所示：

```
[self performSelectorOnMainThread:@selector(handleNewReading)
    withObject:e
    waitUntilDone:false];
```

请记住，在你会在 iOS 应用程序中使用 performSelectorOnMainThread:withObject:waitUntilDone: 的情况下，在 Windows Phone 7 上你需要使用 Deployment.Current.Dispatcher.BeginInvoke( ... )。

## 使用 GPS

基于位置的应用程序非常受欢迎。它们可用于从能够在当前位置“签到”、查看朋友在哪里以及查找附近的餐馆或加油站；一直到高级用途，例如地图、逐向导航，以及业余爱好活动如地理藏宝。

GPS 通过使用极其精确的时钟、计时、一组卫星和一些数学来三角测量设备的位置来工作。值得庆幸的是，开发人员不必太担心 GPS 坐标是如何获得的——只需要知道这些坐标是可用的。GPS 坐标使用纬度、经度和海拔来表示设备在地球上的任何位置。

要了解其工作原理，请创建一个具有用于启动和停止 GPS 监控的按钮以及几个文本块来报告纬度、经度和海拔的新应用程序。确保从此项目中添加对 System.Device 程序集的引用。

修改你的 MainPage.xaml.cs，使其看起来像第 10.2 节清单中所示。

### Listing 10.2 MainPage.xaml.cs, Using the Location Monitoring API

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Net;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Documents;
using System.Windows.Input;
using System.Windows.Media;
using System.Windows.Media.Animation;
using System.Windows.Shapes;
using Microsoft.Phone.Controls;
using System.Device.Location;

namespace Location
{
    public partial class MainPage : PhoneApplicationPage
    {
        GeoCoordinateWatcher watcher;

        // Constructor
        public MainPage()
        {
            InitializeComponent();

            stopLocationButton.IsEnabled = false;
        }

        private void startLocationButton_Click(object sender,
            RoutedEventArgs e)
        {
            if (watcher == null)
            {
                watcher =
                    new GeoCoordinateWatcher(GeoPositionAccuracy.High);
                watcher.MovementThreshold = 20; // compensate for noise
                watcher.StatusChanged +=
                    new EventHandler<GeoPositionStatusChangedEventArgs>(
                        watcher_StatusChanged);
                watcher.PositionChanged +=
                    new EventHandler<
                        GeoPositionChangedEventArgs<GeoCoordinate>>(
                            watcher_PositionChanged);
                watcher.Start();
            }
        }

        void watcher_PositionChanged(object sender,
            GeoPositionChangedEventArgs<GeoCoordinate> e)
        {
            latitudeText.Text =
                e.Position.Location.Latitude.ToString("0.000");
            longitudeText.Text =
                e.Position.Location.Longitude.ToString("0.000");
            altitudeText.Text =
                e.Position.Location.Altitude.ToString("00000.00");
        }

        void watcher_StatusChanged(object sender,
            GeoPositionStatusChangedEventArgs e)
        {
            switch (e.Status)
```
