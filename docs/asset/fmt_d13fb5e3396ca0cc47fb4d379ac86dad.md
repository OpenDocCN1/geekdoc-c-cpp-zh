
```
private async Task<string> SendMessageAsync(ValueSet message)
{
    using (var connection = new AppServiceConnection())
    {
        connection.AppServiceName = BookServiceName;
        connection.PackageFamilyName = BooksPackageName;

        AppServiceConnectionStatus status = await connection.OpenAsync();
        if (status == AppServiceConnectionStatus.Success)
        {
            AppServiceResponse response =
                await connection.SendMessageAsync(message);
            if (response.Status == AppServiceResponseStatus.Success &&
                response.Message.ContainsKey("result"))
            {
                string result = response.Message["result"].ToString();
                return result;
            }
            else
            {
                await ShowServiceErrorAsync(response.Status);
            }
        }
        else
        {
            await ShowConnectionErrorAsync(status);
        }
        return string.Empty;
    }
}
```

构建解决方案并部署提供者和客户端应用后，你可以启动客户端应用并调用服务。你也可以创建多个调用同一服务的客户端应用。

在应用之间通信之后，让我们利用一些硬件。下一节将使用相机来拍摄照片和视频。

#### 相机

随着应用变得越来越视觉化，并且越来越多的设备内置一个或两个摄像头，使用相机已成为应用中越来越重要的方面——并且使用 Windows Runtime 很容易实现。

> 注意 使用相机需要你在清单编辑器中配置 `Webcam` 功能。对于录制视频，你还需要配置 `Microphone` 功能。

照片和视频可以使用 `CameraCaptureUI` 类捕获（在命名空间 `Windows.Media.Capture` 中）。首先，你需要配置照片和视频设置以使用 `CaptureFileAsync` 方法。第一个代码片段捕获照片。在实例化 `CameraCaptureUI` 类后，应用 `PhotoSettings`。可用的照片格式为 JPG、JPGXR 和 PNG。也可以定义裁剪，其中相机捕获的 UI 直接要求用户根据裁剪大小从完整图片中选择一个剪辑。对于裁剪，你可以使用 `CroppedSizeInPixels` 属性定义像素大小，或使用 `CroppedAspectRatio` 定义比率。用户拍摄照片后，示例代码使用 `CaptureFileAsync` 方法返回的 `StorageFile` 在用户选择的目录中将其存储为文件，并借助 `FolderPicker`（代码文件 `CameraSample/MainPage.xaml.cs`）

```
private async void OnTakePhoto(object sender, RoutedEventArgs e)
{
    var cam = new CameraCaptureUI();
    cam.PhotoSettings.AllowCropping = true;
    cam.PhotoSettings.Format = CameraCaptureUIPhotoFormat.Png;
    cam.PhotoSettings.CroppedSizeInPixels = new Size(300, 300);
    StorageFile file = await cam.CaptureFileAsync(CameraCaptureUIMode.Photo);

    if (file != null)
    {
        var picker = new FileSavePicker();
        picker.SuggestedStartLocation = PickerLocationId.PicturesLibrary;
        picker.FileTypeChoices.Add("Image File", new string[] { ".png" });
        StorageFile fileDestination = await picker.PickSaveFileAsync();
        if (fileDestination != null)
        {
            await file.CopyAndReplaceAsync(fileDestination);
        }
    }
}
```

第二个代码片段用于录制视频。如前所述，首先需要进行配置。除了 `PhotoSettings` 属性外，`CameraCaptureUI` 类型还定义了 `VideoSettings` 属性。你可以根据最大分辨率限制视频录制（使用枚举值 `CameraCaptureUIMaxVideoResolution.HighestAvailable` 允许用户选择任何可用分辨率）以及最大时长。可用的视频格式为 WMV 和 MP4：

```
private async void OnRecordVideo(object sender, RoutedEventArgs e)
{
    var cam = new CameraCaptureUI();
    cam.VideoSettings.AllowTrimming = true;
    cam.VideoSettings.MaxResolution = CameraCaptureUIMaxVideoResolution.StandardDefinition;
    cam.VideoSettings.Format = CameraCaptureUIVideoFormat.Wmv;
    cam.VideoSettings.MaxDurationInSeconds = 5;
    StorageFile file = await cam.CaptureFileAsync(CameraCaptureUIMode.Video);

    if (file != null)
    {
        var picker = new FileSavePicker();
        picker.SuggestedStartLocation = PickerLocationId.VideosLibrary;
        picker.FileTypeChoices.Add("Video File", new string[] { ".wmv" });
        StorageFile fileDestination = await picker.PickSaveFileAsync();
        if (fileDestination != null)
        {
            await file.CopyAndReplaceAsync(fileDestination);
        }
    }
}
```

在需要为用户提供拍摄视频或照片选项的情况下，你可以将参数 `CameraCaptureUIMode.PhotoOrVideo` 传递给 `CaptureFileAsync` 方法。

由于相机还会记录位置信息，用户首次运行应用时，系统会询问是否允许记录位置信息（见图33.9）。

![](img/3d365b72b289213a91ade7eb366b8f35_1271_0.png)

图33.9

运行该应用程序，你可以录制照片和视频。

#### 地理定位与MapControl

了解用户的位置是应用的一个重要方面，无论是显示地图的应用、显示用户所在区域天气的应用，还是需要决定将用户数据保存到最近的哪个云中心的应用。当应用中使用广告时，用户位置对于显示附近区域的广告（如果有的话）也很重要。

使用UWP应用，你还可以显示地图。在Windows 10中，`MapControl`作为Windows API的一部分提供，无需使用额外的库（如Bing SDK）即可实现这一点。

示例应用同时使用`Geolocator`（命名空间`Windows.Devices.Geolocation`）来提供用户地址信息，以及`MapControl`（命名空间`Windows.UI.Xaml.Controls.Maps`）。当然，你可以在应用中独立使用这些类型，而无需相互依赖。

##### 使用MapControl

在示例应用中，`MainPage`中定义了一个`MapControl`，其不同的属性和事件绑定到通过页面的`ViewModel`属性访问的`MapsViewModel`中的值。这样，你可以动态更改应用中的某些设置，并查看`MapControl`可用的不同功能（代码文件`MapSample/MainPage.xaml`）：

```
<maps:MapControl x:Name="map"
    Center="{x:Bind ViewModel.CurrentPosition, Mode=OneWay}"
    MapTapped="{x:Bind ViewModel.OnMapTapped, Mode=OneTime}"
    Style="{x:Bind ViewModel.CurrentMapStyle, Mode=OneWay}"
    ZoomLevel="{x:Bind Path=ViewModel.ZoomLevel, Mode=OneWay}"
    DesiredPitch="{x:Bind Path=ViewModel.DesiredPitch, Mode=OneWay}"
    TrafficFlowVisible="{x:Bind checkTrafficFlow.IsChecked, Mode=OneWay, Converter={StaticResource nbtob}}"
    BusinessLandmarksVisible="{x:Bind checkBusinessLandmarks.IsChecked, Mode=OneWay, Converter={StaticResource nbtob}}"
    LandmarksVisible="{x:Bind checkLandmarks.IsChecked, Mode=OneWay, Converter={StaticResource nbtob}}"
    PedestrianFeaturesVisible="{x:Bind checkPedestrianFeatures.IsChecked, Mode=OneWay, Converter={StaticResource nbtob}}" />
```

示例应用在`SplitView`右侧的`Pane`中定义了用于配置`MapControl`的控件，而`MapControl`定义在`SplitView`的内容区域中。你可以在第32章中了解更多关于`SplitView`控件的信息。

在代码隐藏文件中，定义了`ViewModel`属性，并通过将`MapControl`传递给构造函数来实例化`MapsViewModel`。通常最好避免让视图模型直接访问Windows控件，而应仅使用数据绑定来映射。然而，当你使用一些特殊功能（如街景体验）时，直接在`MapsViewModel`类中使用`MapControl`会更方便。由于该视图模型类型不做其他事情，而且也只能在Windows设备上使用，因此将`MapControl`传递给`MapsViewModel`的构造函数是一种折衷方案（代码文件`MapSample/MainPage.xaml.cs`）：

```
public sealed partial class MainPage: Page
{
    public MainPage()
    {
        this.InitializeComponent();
        ViewModel = new MapsViewModel(map);
    }

    public MapsViewModel ViewModel { get; }
}
```

`MapsViewModel`的构造函数初始化了一些绑定到`MapControl`属性的属性，例如将地图位置设置为维也纳市区内的某个位置、地图样式设置为道路变体、俯仰级别设置为0、缩放级别设置为12（代码文件`MapSample/ViewModels/MapsViewModel.cs`）：

```
public class MapsViewModel: BindableBase
{
	private readonly CoreDispatcher _dispatcher;
	private readonly Geolocator _locator = new Geolocator();
	private readonly MapControl _mapControl;

	public MapsViewModel(MapControl mapControl)
	{
		_mapControl = mapControl;
		StopStreetViewCommand = new DelegateCommand(
			StopStreetView, () => IsStreetView);
		StartStreetViewCommand = new DelegateCommand(
			StartStreetViewAsync, () => !IsStreetView);
		if (!DesignMode.DesignModeEnabled)
		{
			_dispatcher = CoreWindow.GetForCurrentThread().Dispatcher;
		}
		_locator.StatusChanged += async (s, e) =>
		{
			await _dispatcher.RunAsync(CoreDispatcherPriority.Low, () =>
				PositionStatus = e.Status);
		};
		// initialize defaults at startup
		CurrentPosition = new Geopoint(
			new BasicGeoposition { Latitude = 48.2, Longitude = 16.3
			});
		CurrentMapStyle = MapStyle.Road;
		DesiredPitch = 0;
		ZoomLevel = 12;
	}
```

使用初始配置启动应用后，你可以看到地图加载了`BasicGeoposition`定义的维也纳位置，右侧有用于管理`MapControl`的控件，以及有关地图加载状态的文本信息（见图33.10）。

![](img/3d365b72b289213a91ade7eb366b8f35_1274_0.png)

图33.10

当你放大、更改俯仰级别，并选择显示地标和商业地标时，你可以看到著名的建筑，如维也纳的史蒂芬大教堂，如图33.11所示。

![](img/3d365b72b289213a91ade7eb366b8f35_1275_0.png)

图33.11

当你切换到鸟瞰视图时，可以看到真实图像，如图33.12所示。

图33.12

某些位置还能通过`Aerial3D`视图显示精美图像，如图33.13所示。

![](img/3d365b72b289213a91ade7eb366b8f35_1277_0.png)

图33.13

##### 使用Geolocator获取位置信息

接下来，你需要借助`Geolocator`实例`_locator`获取用户的实际位置。`GetPositionAsync`方法通过返回`Geoposition`实例来返回地理位置。结果被应用到视图模型的`CurrentPosition`属性，该属性绑定到`MapControl`的中心（代码文件`MapSample/ViewModels/MapsViewModel.cs`）：

```
public async void GetCurrentPositionAsync()
{
    try
    {
        Geoposition position = await _locator.GetGeopositionAsync(
            TimeSpan.FromMinutes(5), TimeSpan.FromSeconds(5));
        CurrentPosition = new Geopoint(new BasicGeoposition
        {
            Longitude = position.Coordinate.Point.Position.Longitude,
            Latitude = position.Coordinate.Point.Position.Latitude
        });
    }
    catch (UnauthorizedAccessException ex)
    {
        await new MessageDialog(ex.Message).ShowAsync();
    }
}
```
