

## 罗盘

罗盘的使用方式非常相似。GetDefault 方法返回 Compass 对象，而 GetCurrentReading 则检索表示罗盘当前值的 CompassReading。CompassReading 定义了 HeadingAccuracy、HeadingMagneticNorth 和 HeadingTrueNorth 属性。

在 HeadingAccuracy 返回 MagnetometerAccuracy、Unknown 或 Unreliable 的情况下，需要对罗盘进行校准（代码文件 SensorSampleApp/ViewModels/CompassViewModel.cs）：

```
public class CompassViewModel: BindableBase
{
    public void OnGetCompass()
    {
        Compass sensor = Compass.GetDefault();
        if (sensor != null)
        {
            CompassReading reading = sensor.GetCurrentReading();
            CompassInfo = $"magnetic north: {reading.HeadingMagneticNorth}" +
                          $"real north: {reading.HeadingTrueNorth}" +
                          $"accuracy: {reading.HeadingAccuracy}";
        }
        else
        {
            CompassInfo = "Compass not found";
        }
    }

    private string _compassInfo;
    public string CompassInfo
    {
        get { return _compassInfo; }
        set { SetProperty(ref _compassInfo, value); }
    }

    // etc.
}
```

### 罗盘同样提供连续更新：

```
public class CompassViewModel: BindableBase
{
    // etc.

    public void OnGetCompassReport()
    {
        Compass sensor = Compass.GetDefault();
        if (sensor != null)
        {
            sensor.ReportInterval =
            Math.Max(sensor.MinimumReportInterval, 1000);
            sensor.ReadingChanged += async (s, e) =>
            {
                CompassReading reading = e.Reading;
                await CoreApplication.MainView.Dispatcher.RunAsync(
                    CoreDispatcherPriority.Low, () =>
                    {
                        CompassInfoReport =
                        $"magnetic north: {reading.HeadingMagneticNorth}" +
                        $"real north: {reading.HeadingTrueNorth}";
                    });
            };
        }
    }

    // etc.
}
```

```
$"real north: {reading.HeadingTrueNorth}" +
$"accuracy: {reading.HeadingAccuracy}
{reading.Timestamp:T}";
    });
    }
}
private string _compassInfoReport;
public string CompassInfoReport
{
    get { return _compassInfoReport; }
    set { SetProperty(ref _compassInfoReport, value); }
}
}
```

## 加速度计

加速度计提供设备 x、y、z 轴上的 g 力值。对于横向放置的设备，x 轴为水平，y 轴为垂直，z 轴指向用户方向。例如，如果设备直立在桌子上呈直角且 Windows 按钮在底部，则 x 的值为 −1。当你将设备翻转使 Windows 按钮在顶部时，x 的值为 +1。

与迄今为止看到的其他传感器类似，静态方法 GetDefault 返回 Accelerometer，而 GetCurrentReading 则通过 AccelerometerReading 对象提供实际的加速度计值。AccelerationX、AccelerationY 和 AccelerationZ 是可读取的值（代码文件 SensorSampleApp/ViewModels/AccelerometerViewModel.cs）：

```
public class AccelerometerViewModel: BindableBase
{
    public void OnGetAccelerometer()
    {
        Accelerometer sensor = Accelerometer.GetDefault();
        if (sensor != null)
        {
            AccelerometerReading reading = sensor.GetCurrentReading();
            AccelerometerInfo = $"X: {reading.AccelerationX}" +
                $"Y: {reading.AccelerationY} Z:
{reading.AccelerationZ}";
        }
        else
        {
            AccelerometerInfo ="Accelerometer not found";
        }
    }

    private string _accelerometerInfo;
    public string AccelerometerInfo
    {
        get { return _accelerometerInfo; }
        set { SetProperty(ref _accelerometerInfo, value); }
    }
    // etc.
}
```

你可以通过为 `ReadingChanged` 事件分配事件处理程序来获取加速度计的连续值。正如迄今为止介绍的其他传感器一样，代码片段未在书中显示。但是，你可以通过本章的代码下载获得此功能。你可以测试你的设备并在读取加速度计值时连续移动它。

## 倾斜仪

倾斜仪用于高级方向检测；它相对于重力给出以度为单位的偏航、俯仰和横滚值。所得值由属性 `PitchDegrees`、`RollDegrees` 和 `YawDegrees` 指定（代码文件 `SensorSampleApp/ViewModels/InclinometerViewModel.cs`）：

```
public class InclinometerViewModel: BindableBase
{
    public void OnGetInclinometer()
    {
        Inclinometer sensor = Inclinometer.GetDefault();
        if (sensor != null)
        {
            InclinometerReading reading = sensor.GetCurrentReading();
            InclinometerInfo = $"pitch degrees: {reading.PitchDegrees}" +
                $"roll degrees: {reading.RollDegrees}" +
                $"yaw accuracy: {reading.YawAccuracy}" +
                $"yaw degrees: {reading.YawDegrees}";
        }
        else
        {
            InclinometerInfo = "Inclinometer not found";
        }
    }

    private string _inclinometerInfo;
    public string InclinometerInfo
    {
        get { return _inclinometerInfo; }
        set { SetProperty(ref _inclinometerInfo, value); }
    }
    // etc.
}
```

## 陀螺仪

`Gyrometer` 提供 x、y、z 设备轴的角速度值（代码文件 `SensorSampleApp/ViewModels/GyrometerViewModel.cs`）：

```
public class GyrometerViewModel: BindableBase
{
    public void OnGetGyrometer()
    {
        Gyrometer sensor = Gyrometer.GetDefault();
        if (sensor != null)
        {
            GyrometerReading reading = sensor.GetCurrentReading();
            GyrometerInfo = $"X: {reading.AngularVelocityX}" +
                $"Y: {reading.AngularVelocityY} Z: {reading.AngularVelocityZ}";
        }
```

```
else
{
    GyrometerInfo ="Gyrometer not found";
}
}

private string _gyrometerInfo;
public string GyrometerInfo
{
    get { return _gyrometerInfo; }
    set { SetProperty(ref _gyrometerInfo, value); }
}
// etc.
}
```

## 方向

OrientationSensor 是最复杂的传感器，因为它取自加速度计、陀螺仪和磁力计的值。你可以以四元数形式通过 Quaternion 属性或旋转矩阵（RotationMatrix 属性）获取所有值。

尝试示例应用以查看值以及移动设备时的情况（代码文件 SensorSampleApp/ViewModels/OrientationViewModel.cs）：

```
public static class OrientationSensorExtensions
{
    public static string Output(this SensorQuaternion q) =>
        $"x {q.X} y {q.Y} z {q.Z} w {q.W}";

    public static string Output(this SensorRotationMatrix m) =>
        $"m11 {m.M11} m12 {m.M12} m13 {m.M13}" +
        $"m21 {m.M21} m22 {m.M22} m23 {m.M23}" +
        $"m31 {m.M31} m32 {m.M32} m33 {m.M33}";
}
```

```
public class OrientationViewModel: BindableBase
{
    public void OnGetOrientation()
    {
        OrientationSensor sensor = OrientationSensor.GetDefault();
        if (sensor != null)
        {
            OrientationSensorReading reading =
            sensor.GetCurrentReading();
            OrientationInfo = $"Quaternion:
{reading.Quaternion.Output()}" +
                $"Rotation: {reading.RotationMatrix.Output()}" +
                $"Yaw accuracy: {reading.YawAccuracy}";
        }
        else
        {
            OrientationInfo ="OrientationSensor not found";
        }
    }

    private string _orientationInfo;
    public string OrientationInfo
    {
        get { return _orientationInfo; }
        set { SetProperty(ref _orientationInfo, value); }
    }
    // etc.
```

运行应用时，你可以看到如图 33.16 所示的传感器数据。

![](img/3d365b72b289213a91ade7eb366b8f35_1289_0.png)

图 33.16

## 滚动弹珠示例

为了不只在 TextBlock 元素中以结果值查看传感器值，还可以制作一个简单的示例应用，利用 Accelerometer 使弹珠在屏幕上滚动。

弹珠由一个红色椭圆表示。将 Ellipse 元素放置在 Canvas 元素内可以借助附加属性移动 Ellipse（代码文件 RollingMarble/MainPage.xaml）：

```
<Canvas Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
    <Ellipse Fill="Red" Width="100" Height="100" Canvas.Left="550" Canvas.Top="400" x:Name="ell1" />
</Canvas>
```

